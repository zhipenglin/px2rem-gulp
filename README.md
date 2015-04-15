# gulp-px3rem

This is a gulp plugin for [px2rem](https://www.npmjs.com/package/px2rem)

CLI tool provided in [px2rem](https://www.npmjs.com/package/px2rem)

## Usage

The raw stylesheet only contains @2x style, and if you

* don't intend to transform the original value, eg: 1px border, add `/*no*/` after the declaration
* intend to use px by force，eg: font-size, add `/*px*/` after the declaration

**Attention: Dealing with SASS or LESS, only `/*...*/` comment can be used, in order to have the comments persisted**

Gulpfile.js：

```
var gulp = require('gulp');
var px2rem = require('gulp-px3rem');

gulp.task('px2rem', function() {
    gulp.src('./*.css')
        .pipe(px2rem())
        .pipe(gulp.dest('./dest'))
});
```

### Options

```
px2rem({
    baseDpr: 2,             // base device pixel ratio (default: 2)
    threeVersion: true,     // whether to generate 3x version (default: true)
    remVersion: true,       // whether to generate rem version (default: true)
    remUnit: 64,            // rem unit value (default: 64)
    remPrecision: 6,        // rem precision (default: 6)
    forcePxComment: 'px',   // force px comment (default: `px`)
    keepComment: 'no'       // no transform value comment (default: `no`)
})
```

### Example

#### Pre processing:

One raw stylesheet: `test.css`

```
.selector {
    width: 128px;
    height: 64px; /*px*/
    font-size: 28px; /*px*/
    border: 1px solid #ddd; /*no*/
}
```

#### After processing:

Rem version: `test.debug.css`

```
.selector {
    width: 2rem;
    border: 1px solid #ddd;
}
[data-dpr="1"] .selector {
    height: 32px;
    font-size: 14px;
}
[data-dpr="2"] .selector {
    height: 64px;
    font-size: 28px;
}
[data-dpr="3"] .selector {
    height: 96px;
    font-size: 42px;
}
```

@1x version: `test1x.debug.css`

```
.selector {
    width: 64px;
    height: 32px;
    font-size: 14px;
    border: 1px solid #ddd;
}
```

@2x version: `test2x.debug.css`

```
.selector {
    width: 128px;
    height: 64px;
    font-size: 28px;
    border: 1px solid #ddd;
}
```

@3x version: `test3x.debug.css`

```
.selector {
    width: 192px;
    height: 96px;
    font-size: 42px;
    border: 1px solid #ddd;
}
```

## Change Log

### 0.1.8

* Deps: px2rem@~0.1.8
    * Fix regular expression bug and common comments bug which affects rem transformation.

## License

MIT
