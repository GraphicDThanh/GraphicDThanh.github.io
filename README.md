# GraphicDThanh Blog
> This github pages use [jekyll](https://jekyllrb.com/docs/installation/)

## Run App
### Install gem 
```bash
$ cd docs
$ bundle install
```
### Run app
```
$ bundle exec jekyll serve 
```

```
$ bundle exec jekyll serve --livereload
```

Access blog by http://127.0.0.1:4000/

## Set Up Your New App
> Note: this app use approach create separate env of ruby instead of use global. (
> [ref](https://collectionbuilder.github.io/cb-docs/docs/software/ruby_mac/)
> [ref](https://jekyllrb.com/docs/installation/)
> )

### Set up a separate Ruby development environment with `rbenv`

```bash
$ brew update
$ brew install rbenv
$ rbenv init
$ eval "$(rbenv init - zsh)" > ~/.zshrc
$ rbenv install 3.1.4
$ rbenv local 3.1.4
rbenv rehash
```

### Install gem
```bash
$ bundle install
```

## Naming convention
- Image name: `YYYY-MM-post-slug-img##.jpg`
- Example: 2020-07-dai-ban-doanh-python-series-overview-cover.jpg
- Folder: `assets/images/2020/07`

## Theme
- https://mmistakes.github.io/minimal-mistakes/docs/structure/
- 