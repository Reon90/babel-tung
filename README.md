# babel-tung

Babel plugin for [tung](https://github.com/Reon90/tung).

## Install
```
npm install babel-tung
```

## Usage

### Webpack 2

```js
module.exports = {
  entry: './app/app.js',
  output: {
    filename: 'bundle.js',
    path: './dist'
  },
  module: {
    loaders: [{
        test: /.tpl?$/,
        loader: 'babel-loader?filename=[name]',
        options: {
            babelrc: false, plugins: "babel-tung"
        }
    }]
  },
};
```

### Gulp

```js
const gulp = require('gulp');
const babel = require("babel-core");
const transform = require('gulp-transform');
const rename = require('gulp-rename');

gulp.task('tpl', () => {
  return gulp.src('assets/html/**/*.tpl')
    .pipe(transform((content, file) => {
        return babel.transform(content, { babelrc: false, filename: file.basename.replace('.tpl', ''), plugins: "babel-tung" }).code;
    }))
    .pipe(rename({
        extname: ".js"
    }))
    .pipe(gulp.dest('dist/html'));
});
```
