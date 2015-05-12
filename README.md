# GSTV FE Coding Exercise

1. [System Requirements](#system-requirements)
1. [Getting Started](#getting-started)
1. [Build System](#build-system)
1. [Application Architecture](#application-architecture)
1. [Jade](#jade)
1. [Sass](#sass)
1. [Version Control](#version-control)
1. [Exercise Overview](#exercise-overview)

## System Requirements

* Node.js or IO.js
* Bower

## Getting Started

To get up and running, all you need to do is install the project dependencies with npm and bower. You can either run our `npm run setup` wrapper or do this manually with:

```
npm install
bower install
```

With this done, you should have everything you need to run the application; you can now run `npm run dev` to spin up the webpack development server at `http://localhost:3000`. We recommend that you check out the documentation below to learn more about the build system, application structure, styles, and more.

## Build System

We use [Webpack](http://webpack.github.io/) for our build system, as it provides a lot of built-in functionality that would require more boilerplate with something like [Browserify](http://browserify.org/). Some key features that we use:

* Bundle splitting (vendor dependencies are compiled to a separate file).
* Non-JS imports. Now you can directly require `.jade` or `.scss`!
* Live reloading (with hot module replacement). Webpack enables watchers for all file types so you don't have to go through the extra effort yourself.
* Convenient development server, with an iframe option (known as "inlining") that displays the status of your bundle directly in the browser.
* Angular Annotate ([ng-annotate](https://github.com/olov/ng-annotate)). Use `/* @ngInject */` to enable automatic injection annotations.
* ES6 support thanks to Babel.

So how do you use it? While you can directly run it from the CLI via `webpack`, it's recommended to use one of our npm scripts:

#### `npm run build`
Runs the webpack build system with your current node environment. This will compile your application and write it to disk (into `~/dist`).

#### `npm run build:prod`
Runs the production webpack build with `NODE_ENV=production`. This will enable functionality such as minification and dead/unused code removal.

#### `npm run dev`
Runs the webpack development server at `http://localhost:3000` (inlined at `http://localhost:3000/webpack-dev-server/`). The application is served from memory and file watchers are automatically enabled for livereload.

Note: if you have trouble viewing the inlined version, make sure you include the trailing slash after /webpack-dev-server/.

#### `npm run dev:quiet`
Same as `npm run dev`, but hides verbose debugging information.

## Application Structure
Our goal with this project is to give you a working application out of the box without restricting you to a specific architecture. There are some key design decisions to note, however:

The Webpack development server will point to `~/app/index.html`, which will be compiled on the fly (or to disk if you use the non-development build script). This is important because bundled files append a dynamic query string hash for cache busting.

The application entry point is in `~/app/index.js`, and contains all core vendor dependencies. Please reference that file for additional documentation.

## Jade
Our templates are all written in [Jade](http://jade-lang.com/) - the [syntax](http://naltatis.github.io/jade-syntax-docs/#basics) is easier to read - especially with Angular templates - and it reduces the likelihood of destroying a layout by simply not including a closing tag.

While Jade does not require a div tag prior to a class or ID declaration we add the div tag for the sake of clarity.

**Original Jade Template**
``` jade
doctype html
html
  head
    title my jade template
  body
    h1 Hello #{name}
    div#content
      div.block
        input#bar.foo1.foo2
```

**Compiled HTML**
``` html
<!DOCTYPE html>
<html>
  <head>
    <title>my jade template</title>
  </head>
  <body>
    <h1>Hello Bob</h1>
    <div id="content">
      <div class="block">
        <input id="bar" class="foo1 foo2">
      </div>
    </div>
  </body>
</html>
```

## Sass
### On Node Sass
We rely on Node Sass to compile our stylesheets because of its speed. However, because there is not currently feature parity between Ruby Sass and LibSass so not all documented features are supported. Hugo Giraudel's [Sass Compatibility](http://sass-compatibility.github.io/) project is the best way to identify these differences.

### Sass Standards
We loosely follow Hugo Giraudel's [Sass Guidelines](http://sass-guidelin.es/) - particularly his thoughts on code clarity and avoiding [nesting selectors](http://sass-guidelin.es/#selector-nesting) unless absolutely necessary.

### Class Naming Conventions
Our styles are written using [OOCSS](http://appendto.com/2014/04/oocss/) principles specifically using  [BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) methodology. This promotes a separation of content from context leading to highly reusable styles.

**BEM naming conventions**
``` sass
.block {}
.block__element {}
.block__element--modifier {}
.block--modifier {}

.media {}
.media__img {}
.media__img--rev {}
.media__body {}
```

**BEM naming conventions used in markup**
``` jade
div.media
  img.media__img--rev(src='logo.png" alt='Foo Corp logo')
    div.media__body
      h3.alpha Welcome to Foo Corp
      p.lede Foo Corp is the best, seriously!
```

## Version Control
### GitFlow and GithubFlow
We use [GitFlow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow/) as a way to build quality control in to our development, QA and deployment process.

For this exercise we are asking that you use a modified [Github Flow](https://guides.github.com/introduction/flow/) or sometimes referred to as a [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) methodology instead of GitFlow - conceptually GitFlow and Github flow are similar.

Please fork our angular-coding-exercise and use a feature branch workflow while developing your functionality. When you are ready to submit your work make a pull request against our angular-coding-exercise repository.

## Exercise Overview
