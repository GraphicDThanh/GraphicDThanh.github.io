---
title: "Relation fields in Django Rest Framework Serializer"
categories:
  - Django
  - Django Rest Framework (DRF)
tags:
  - django
  - drf
  - serializer
  - fields
  - english
---


![](/assets/images/2023/10/2023-10-relation-fields-in-drf-serializer-cover.png)
The Django model offers various types of relationships such as OneToOneField, ForeignKey, ManyToManyField, and GenericForeignKey.

To present or write data of relationship in a serializer, you can utilize DRF Relation fields.

In this post, I will summarize the key points of relational fields and then delve into customizing a relation field to facilitate reading and writing relationship data.

Although the [official document](https://www.django-rest-framework.org/api-guide/relations/#serializer-relations) mentions this custom relational topic, it lacks examples and use cases. Therefore, I aim to make it more practical by providing relevant illustrations.

Before we delve into the content, let’s take a look at the relevant models:

```python
class Album(models.Model):
    album_name = models.CharField(max_length=100)

class Track(models.Model):
    album = models.ForeignKey(
        Album,
        related_name='tracks',
        on_delete=models.CASCADE
    )
    title = models.CharField(max_length=100)
    duration = models.IntegerField()
```

## Performance concerns related to relation fields and the responsibility of developers

When using Django REST Framework (DRF), it is important to note that DRF **does not automatically optimize the queryset that is passed to the serializer**.

It is the responsibility of the developer to optimize the performance of relation fields in DRF. By using methods like prefetch_related and select_related, developers can improve the efficiency of their queries and enhance the overall performance of their applications.

With above models, if we have *AlbumSerializer*:

```python
class AlbumSerializer(serializers.ModelSerializer):
    tracks = serializers.StringRelatedField(many=True)


    class Meta:
        model = Album
        fields = ['album_name', 'tracks']

data = AlbumSerializer(Album.objects.all(), many=True).data
```

then serializer all albums as above.

This cause **serious performance issues** since it will hit database N times with N is total number of albums.

It is important to address the issue of hitting the database multiple times, which can cause **serious performance issues**.

By using `Album.objects.prefetch_related('tracks')` , developers can optimize the performance by fetching the related tracks in a single database query. This reduces the number of round trips to the database and improves the overall performance of the serializer.

## Relation fields readonly built-in

DRF provides relation fields readonly includes:

– **StringRelatedField**

– **HyperlinkedIdentityField**

## Relation fields read-write built-in

DRF provides relation fields read-write includes:

– PrimaryKeyRelatedField

– HyperlinkedRelatedField

– SlugRelatedField

If you want these readonly, add param read_only=True in the field.

For mor detail about these built-in fields, please read the [official document](https://www.django-rest-framework.org/api-guide/relations/).

## Nested serializer

For nested relationship, you could use its own serializer. By default, nested serializer is readonly.

For example, Track has serializer TrackSerializer then could use:

```python
tracks = TrackSerializer(many=True, read_only=True)
```

Above is how to present data. If you want to write into nested relationship, you could use method create() or update() to write.

For example, when create an album, you also want to write tracks, then:

```python
def create(self, validated_data):
    tracks_data = validated_data.pop('tracks')
    album = Album.objects.create(**validated_data)
    for track_data in tracks_data:
        Track.objects.create(album=album, **track_data)

    return album
```

## Custom relation fields
In some case, all above options not fit your needs. You could write a custom relation fields to handle.

### Example 1: Custom presentation
For this example, take a look on [document](https://www.django-rest-framework.org/api-guide/relations/#example_1) where create a custom relation field named **“TrackListingField”** extends from **“serializers.RelatedField”** then override method **“to_representation“**

### Example 2: Read-write relation fields with nested serializer
For this example, let’s start with this context:

I have class **TrackSerializer** as above on nested serializer, but I don’t want it just use for readonly by default, I want a **read-write** relation fields which could help me read and write in clean way.

From the guide, I will implement **“.to_internal_value()”** method to help it could be writable. And implement **“.to_representation()”** method to present the data.

So, it could look like this:

```python
class CustomRelatedField(serializers.RelatedField):
    """Custom Related Field for Read and Write"""

    def to_representation(self, value):
        pass

    def to_internal_value(self, data):
        pass
```

#### **Implement to_presentation method**

As I want to use serializer class to present the data, then will need a way to get the serializer class from input of the field, then I decided to put it as a part of keyword arguments kwargs.

Above class could be like this:

```python
class CustomRelatedField(serializers.RelatedField):
    """Related Field with Serializer Class for presentation"""

    def __init__(self, **kwargs):
        self.serializer_class = kwargs.pop("serializer_class")
        if not self.serializer_class:
            raise ValueError("serializer_class is required")

        super().__init__(**kwargs)

    def to_representation(self, value):
        return self.serializer_class(value).data
```

As above, we able to present object with nested serializer class.

#### **Implement to_internal_value method**

To help the relation field writable, to_internal_value must be implement. Because this method help decide the data to write to relation models.

There are 2 case of relationships here should be concern:

– ForeignKey in model stands for 1 to many relation

– ManyToManyField in model stands for many to many relation

As example of this post, the tracks belong to 1 to many relations.

One album able to have multiple tracks and 1 track belong to 1 album.

**1 to many relation**

As 1-n relation, I could get the album by id and set it as value to the write.

The to_internal_value could looks like:

```python
def to_internal_value(self, data):
    return self.get_queryset().get(uuid=data)
```
Then we have full custom relation fields for a ForeignKey field as FKRelationField below:

```python
class ForeignKeyRelationField(serializers.RelatedField):
    """Related Field with Serializer Class for presentation"""

    def __init__(self, **kwargs):
        self.serializer_class = kwargs.pop("serializer_class")
        super().__init__(**kwargs)

    def to_representation(self, value):
        return self.serializer_class(value).data

    def to_internal_value(self, data):
        return self.get_queryset().get(uuid=data)
```

I changed the name class from “CustomRelatedField” to “ForeignKeyRelationField” in this case.

**many to many relation**

Many to many relation will similar to FK with minor change of internal value will be a list of ids instead of single object then each object will return an id instead.

```python
def to_internal_value(self, data):
    return self.get_queryset().get(uuid=data).id
```

You could named this field ManyToManyRelationField.

## Using custom relation field

As above example, I could use my ForeignKeyRelationField on TrackSerializer to read and write the album

```python
class TrackSerializer(serializers.ModelSerializer):
    class Meta:
        model = Track
        fields = ['title', 'album']

    album = ForeignKeyRelatedField(
        many=False,
        queryset=Album.objects.all(),
        serializer_class=AlbumSerializer,
    )
```

Above serializer could help represent album with nested serializer AlbumSerializer as well as write the album of a track.

And for “tracks” in AlbumSerializer, could use ManyToManyFieldRelationField to read and write for relation many to many.

```python
class AlbumSerializer(serializers.ModelSerializer):

    class Meta:
        model = Album
        fields = ['album_name', 'tracks']

    tracks = ManyManyKeyRelatedField(
        many=True,
        required=False,
        queryset=Track.objects.all(),
        serializer_class=TrackSerializer,
    )
```

In this post, I have give you more detail of relational fields and how to custom a relation fields.
