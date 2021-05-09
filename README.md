# gulp-html-engine [![NPM version][npm-image]][npm-url]

## Make it easy to extend, include and replace your html files

layout.html

```html
<body>
  @placeholder content
  @placeholder footer
</body>
```

content.html

```html
@extends layout.html

@block content
<main>my content</main>
@close

@block footer
<footer>my footer</footer>
@close
```

output

```html
<body>
  <!-- start content -->
  <main>my content</main>
  <!-- end content -->

  <!-- start footer -->
  <footer>my footer</footer>
  <!-- end footer -->
</body>
```

## Features

- Nested extending
- Nested including

## Install

```sh
$ npm install --save-dev gulp-html-engine
```

## Syntax

**@extends [=] path [jsonString]**

e.g. `@master master.html {"foo":"bar"}`

**@placeholder [=] blockName**

e.g. `@placeholder footer`

**@include [=] path [jsonString]**

e.g. `@include /footer.html {"foo":"bar"}`

**{ variableName }**

e.g. `{ foo }`

**@block [=] blockName**

e.g. `@block footer`

**@close**

You must add `@close` at the end of every block

## Usage

```js
var gulp = require('gulp')
var extender = require('gulp-html-engine')

gulp.task('extend', function () {
    gulp.src('./*.html')
        .pipe(extender({annotations:true,verbose:false})) // default options
        .pipe(gulp.dest('./output'))

})

gulp.task('watch', function () {
    gulp.watch(['./*.html'], ['extend'])
})

...
```

## Options

**annotations** [bool]

Make it `false` if you dont want too see `<!-- start foo.html -->` in output files.

**verbose** [bool]

Show extra info in the console.

**root** [string (dir path)]

To make absolute path which starts with `/` works.

## Changelog

- 1.0.0 Initial release

[npm-url]: https://npmjs.org/package/gulp-html-engine
[npm-image]: https://badge.fury.io/js/%40naourass%2Fgulp-html-engine.svg