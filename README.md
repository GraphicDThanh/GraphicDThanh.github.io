# GraphicDThanh Blog

> This github pages use jekyll

## [prerequisites](https://jekyllrb.com/docs/installation/): 
  - `>` Ruby v2.5.0: check by `ruby -v`
  - RubyGems: check by `gem -v`
  - GCC and Make: check by `gcc -v`, `g++ -v`, `make -v`

    If have error on gem not found, add config PATH to shell `~/.zshrc`
    ```bash
    export GEM_PATH="$HOME/.gem/ruby/2.6.0/bin"
    export PATH="$GEM_PATH:$PATH"
    ```

### Run app
- Go to app directory
```bash
cd docs
```

- build the site on local
```bash
bundle exec jekyll serve
```

- Go `http://127.0.0.1:4000/` to see the site


### Init app:
> Do follow guide on jekyll ([here](https://jekyllrb.com/docs/))

- install jekyll and bundler gems

  ```bash
  gem -user-install install jekyll bundler
  which jekyll
  ```

- create new Jekyll site
  ```bash
  jekyll new graphicdthanh
  ```

- change into new directory
  ```bash
  cd graphicdthanh
  ```

- build the site on local
  ```bash
  bundle exec jekyll serve
  ```

- go `http://127.0.0.1:4000/` to see the site