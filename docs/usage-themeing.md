# Themeing

Bük packs an easy to customize themeing experience. 

The main color can be changed in `src/sass/_variables.scss` with the variable `$buk-color`.

## Stylesheets

There are two stylesheets included by default:

* `src/sass/app.scss` holds styling rules applicable to the entire application. 
* `src/sass/theme.scss` holds styling rules applicable to the markdown wrapper (`#wrapper`). The wrapper is compatbile with [Marked 2](http://marked2app.com/help/Writing_Custom_CSS.html) theme. 

> CHANGED in 3.1: there are no more bootstrappers and "theme" key in `manifest.json`. Swapping theme is as simple as changing the content of `src/sass/theme.scss` now! 