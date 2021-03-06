# Animikii Style Guide
Welcome to the Animikii style guide where we layout our code conventions, patterns and solutions to problems we encounter.

Please keep in mind that **master** is the production branch. If you merge anything to the **master** branch it will be pushed.

**Note: if you need review, make a pull request and assign to the person(s) you would like to review.**

## Local Jekyll Development
Everything is compiled using [Jekyll](https://jekyllrb.com/docs/) please read if you need a refresher.

    // load dependencies for local build
    bundle install

    // serve
    bundle exec jekyll serve

    // watch and serve
    bundle exec jekyll serve -w

Go to http://localhost:4000

> Note: When adding Liquid snippets wrap the code in `{%- raw -%}{% endraw %}` tag
