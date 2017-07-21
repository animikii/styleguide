# Animikii Style Guide

Welcome to the Animikii style guide where we layout our code conventions, patterns and solutions to problems we encounter.

# Javascript/React/Babel
Please refer to airbnb's style guide on javascript https://github.com/airbnb/javascript

Rules to live by
- pure functions - *no side effects!*
- use classes for reusable objects
- maintain immutable data

# Css/Sass

Our conventions for css and scss is comprised of variations of [BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/), [OOCSS](https://github.com/stubbornella/oocss/wiki), [SUIT](http://suitcss.github.io/)
and [airbnb](https://github.com/airbnb/css).

We try to use an approach that combines both OOCSS and BEM for these reasons:

- It helps create clear, strict relationships between CSS and HTML
- It helps us create reusable, compossible components
- It allows for less nesting and lower specificity
- It helps in building scalable stylesheets

Under no circumstance should you use `!important`, if you are, then your doing something wrong.

## Bootstrap

Most of our projects use bootstrap as a our starting point. When you need to change something, try to change the source first.
This means going into the un minified version of bootstrap and changing the styles you want.

## Ruby/Rails

...
