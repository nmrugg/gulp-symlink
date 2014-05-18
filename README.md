This is a fork of ben-eb's gulp-symlink that does not show annoying debug output. Later I might update it more to make it behave the way I want it and even add it to npm too.

## Installation

Install via npm:

```
npm install nmrugg/gulp-symlink --save-dev
```

## Example

```js
var gulp = require('gulp');
var symlink = require('gulp-symlink');

gulp.task('default', function() {
    return gulp.src('assets/some-large-video.mp4')
        .pipe(symlink('build/videos')) // Write to the destination folder
        .pipe(symlink('build/videos/renamed-video.mp4')) // Write a renamed symlink to the destination folder
});
```

## API

### symlink(symlinkpath) or symlink.relative(symlinkpath)

Pass a `string` or a `function` to create the symlink. The function is passed the [vinyl](https://github.com/wearefractal/vinyl) object, so you can use `file.base`, `file.path` etc. Just make sure you return a string that is the location and or filename of the new symlink. For example:

```js
var path = require('path');

gulp.task('symlink', function() {
    return gulp.src('assets/some-large-video.mp4')
        .pipe(symlink(function(file) {
            return path.join(file.base, 'build', file.relative.replace('some-large', ''));
        }));
});
```

The string options work in the same way. If you pass a string like 'build/videos', the symlink will be created in that directory. If you pass 'build/videos/video.mp4', the symlink will also be renamed.

### symlink.absolute(symlinkpath)

The exact same as `symlink.relative` except this will create an *absolute symlink* instead.
