---
layout: post
title: "Export Multiple CSVs file into a ZIP in Django Application"
date:   2023-04-01 10:00:00 +0700
categories: django, export
---

![](/assets/img/export-django/export-zip-multiple-csv-files.png)

In this next installment of the Django export series, I will be demonstrating how to create a `zip` file containing multiple CSV files. Throughout the post, we will explore various methods, providing you with a range of options to consider for your own project.

## Models example
Let's consider a basic library system in which a book can be associated with multiple libraries.

The corresponding models are structured as follows:

```python
class Library(models.Model):
    name = models.TextField()


class Book(models.Model):
    title = models.TextField()
    libraries = models.ManyToManyField(
        null=True,
        blank=True,
        to='Library',
        related_name='books'
    )
```

Our objective is to export a zip file that contains several CSV files, each one representing a library and displaying a list of books available in that library.

### Export view

As is typical when creating a download API, we will create a view that only allows the GET method.

```python
import csv, io, zipfile 
from wsgiref.util import FileWrapper
from django.http import StreamingHttpResponse
from rest_framework.views import APIView

class ExportZip(APIView):
    def get(self):
        csv_datas = self.build_multiple_csv_files()
        
        temp_file = io.BytesIO()
        with zipfile.ZipFile(
             temp_file, "w", zipfile.ZIP_DEFLATED
        ) as temp_file_opened:
            # add csv files each library
            for data in csv_datas:
                data["csv_file"].seek(0)
                temp_file_opened.writestr(
                    f"library_{data['library_name']}.csv",
                    data["csv_file"].getvalue()
                )

        temp_file.seek(0)
        
        # put them to streaming content response 
        # within zip content_type
        response = StreamingHttpResponse(
            FileWrapper(temp_file),
            content_type="application/zip",
        )

        response['Content-Disposition'] = 'attachment;filename=Libraries.zip'
        return response

    def build_multiple_csv_files(self):
        csv_files = []
        return csv_files
```

In the aforementioned view, we utilize the Python Standard Library's [`zipfile` module](https://docs.python.org/3/library/zipfile.html) for compressing and archiving data.

The [`zipfile.ZipFile`](https://docs.python.org/3/library/zipfile.html#zipfile.ZipFile) method enables us to open a zip file for writing. In this instance, the file is a binary I/O object, specified as `temp_file_opened`, with the `temp_file` object being its [file-like](https://docs.python.org/3/library/io.html#module-io) equivalent.

```python
class zipfile.ZipFile(
    file, mode='r', compression=ZIP_STORED, 
    allowZip64=True, compresslevel=None, 
    *, strict_timestamps=True
)
```

We utilize a context manager via the `"with"` statement to guarantee the closure of our zip file after the suite within the "with" block has been executed, even if an exception is raised.

```python
temp_file = io.BytesIO()
with zipfile.ZipFile(
    temp_file, "w", zipfile.ZIP_DEFLATED
) as temp_file_opened:
    # write to zip file
```

Within the context manager, we write the CSV content file to the zip `temp_file_opened` using the `writestr` method.

```python
ZipFile.writestr(
    zinfo_or_arcname, data, 
    compress_type=None, compresslevel=None
)
```

Here, we specify two mandatory parameters - `zinfo_or_arcname` and `data`.

```python
temp_file_opened.writestr(
    f"File_library_{file['lib']}.csv",
    file["csv_file"].getvalue()
)
```

Once we have completed writing multiple CSV files, we locate the zip file by using [seek](https://docs.python.org/3/library/io.html#io.IOBase.seek). We then convert the file-like objects to an iterator using [FileWrapper](http://filewrapper/) before returning them in the StreamingHttpResponse.

At this stage, we can download an empty file named "Libraries.zip".


## Build CSV files

As shown, we have defined a method named `"build_multiple_csv_files"` that currently returns an empty list. In the following step, we will add the code to this function to generate a list of CSV files.

```python
class ExportLibraries(APIView):
    header_data = {
        "name": "Name",
        "library": "Library Name"
    }
    
    def get(self):
        ...
        return response

    def build_multiple_csv_files(self, libraries, books):
        csv_files = []
        
        for library in libraries.iterator():
            mem_file = io.StringIO()
            writer = csv.DictWriter(
                mem_file, fieldnames=self.header_data.keys()
            )
            writer.writerow(self.header_data)
            
            books_in_library = books.filter(libraries__in=[library.id])
            for book in books_in_library:
                book_row = self.build_book_row(book, library)
                writer.writerow(book_row)
            
            mem_file.seek(0)
            
            csv_files.append({
                "library_name": library.name,
                "csv_file": mem_file
            })
            
        return csv_files
    
    def build_book_row(self, book, library):
        row = self.header_data.copy()
        
        row["name"] = book.name
        row["library"] = library.name
        
        return row
```

Reviewing the code above, we iterate over all libraries and construct a CSV file for each one. This is achieved by initializing a writer object using `csv.DictWriter()` and the keys from `header_data`. 

Here is an example of what `header_data` might look like:

```python
header_data = {
    "name": "Book Name",
    "library": "Library Name"
}
```

Next, we add the header to the writer and utilize a loop to add each book row by row to the writer using the .`write_row()` method.

Once the writing is complete, we append an object for each library, with the library's name included in the object's name, to help establish the CSV filename along with the file's contents.

To enable export functionality, you may add this view to the URLs file.

```python
urlpatterns = [
    path(
        'export_libraries/',
        ExportLibraries.as_view(),
        name="export_libraries"
    )
]
```

## Unit Test

The following question is how to verify the output?

It is recommended to carry out this step before implementing the logic, as per the `TDD` (Test Driven Development) approach. However, I will demonstrate how the logic works first, as it may help you better understand which components require testing.

I intend to create two unit tests for this:

One for the API: Upon calling the API, a zip file should be exported.
One for the CSV files and their contents: Calling `build_multiple_csv_files()` on the view should return a list containing data for each library. At this stage, the content of each CSV file can also be verified row by row.

**NOTE**: Please keep in mind that the sample unit tests provided below are solely intended to provide an idea of what they may look like, and you should adapt them according to your specific feature.


### Test content response

This unit test is straightforward; we only need to verify that the API call returns a `200` status code and that the exported file is a zip file with the expected name.

```python
def test_export_libraries(self):
    response = self.client.get(reverse('export_libraries'))
    assert response.status_code is status.HTTP_200_OK
    assert response.get('Content-Disposition') == "Libraries.zip"
```


### Test view function to get multiple CSV files

```python
def test_build_csvs_files(self):
    # assume we mock 2 libraries
    # library_1, library_2
    # queryset is books and libraries
    view = ExportRecipesCost()
    view.request = drf_request_for_context(self.user)
    csv_files = view.build_multiple_csv_files(
        libraries, books
    )
    # check number of csv files
    assert len(csv_files) == 2
    # first csv file
    assert csv_files[0]["library_name"] == library_1.name
    assert csv_files[0]["csv_file"]
    # go check csv content in first file here

    # second csv file
    assert csv_files[0]["library_name"] == library_2.name
    assert csv_files[0]["csv_file"]
    # go check csv content in first file here
```

I have added some comments in the code to indicate the data we will use for testing. Our approach is to call the view function using a mock DRF request, created using the `drf_request_for_context` utility function.

In addition to checking the number of CSV files returned, we can also verify the content of each CSV file based on its header.


## Optimizing performance

To improve performance, we can optimize the current solution by using a single loop to prepare all the books data, regardless of the library it belongs to, and then loop through the libraries using this set of data. This approach can significantly reduce processing time.

Instead of solely relying on Django queries, one could use Pandas to flatten the data and make the export process even easier by working with dataframes.

Another improvement could be to handle the export process as a background task, such as a Celery task. Instead of using StreamingHttpResponse to download the file from the browser, we can upload the zip file to a service like S3 and provide the user with a URL or other means of accessing the file. This approach can improve user experience and prevent timeout errors when handling large amounts of data.

(If you have any other ideas for improving performance, please share them with me.)

## Final word

To summarize, we have explored a method (referred to as "use Django queries") for exporting a zip file containing multiple CSV files within a Django application. While there is an alternative approach using pandas to export data from a Django app, we may discuss it in the future.
