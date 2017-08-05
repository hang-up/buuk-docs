# Extending renderer

Bük uses [markdown-it](https://github.com/markdown-it/markdown-it) as its underlying parser so any non conventional markdown features will require the use of a `markdown-it-plugin`.  
-> A list of plugin is available **[here](https://www.npmjs.com/browse/keyword/markdown-it-plugin)**. <-
 
--- 

## Default plugins

### [Subscript](https://github.com/markdown-it/markdown-it-sub) / [Superscript](https://github.com/markdown-it/markdown-it-sup)

- 19^th^
- H~2~O

### [\<center>](https://github.com/jay-hodgson/markdown-it-center-text)

-> Centered text <-

### [\<underline>](https://www.npmjs.com/package/markdown-it-underline)

_underlined text_

### [Emojies](https://github.com/markdown-it/markdown-it-emoji)

> Classic markup: :wink: :cry: :laughing: :yum:
>
> Shortcuts (emoticons): :-) :-( 8-) ;)

see [how to change output](https://github.com/markdown-it/markdown-it-emoji#change-output) with twemoji.

### [\<mark>](https://github.com/markdown-it/markdown-it-mark)

==Marked text==

--- 

## How to?

Integrating a plugin into Bük can be achieved in (usually) a few steps:
1) Install plugin
2) Reference plugin
3) Configure webpack for caveats

---

> **1) Install plugin**

`npm install #name-of-plugin# --save-dev` 

---

> **2) Reference plugin**

In `src/js/bootstrap/renderer.js` is where we attach plugins to the renderer.

```javascript
md
    /*
        Base plugins.
     */
    .use(require('#name-of-plugin-1'))
    .use(require('#name-of-plugin-2'))
    /*
        Conditional plugins.
    */
    //.use(require('#name-of-plugins-3'))
```

Of course, you can chain-load as many plugins as you need but keep in mind plugins come at a cost: in order to minimize script output size, only essential plugins are being loaded by default.
It is therefore highly recommended to conditionally import feature specific plugin.

##### Conditional import

The easiest way to conditionally import a plugin is to set up an option key in the `manifest.json`. Then, import the plugin in `src/js/bootstrap/renderer.js@renderer()` under `Conditional plugins`.
 
--- 

> **3) Webpack caveats** (Optional)

Some plugins will be written using ES6. Although it is possible for webpack to minify ES6 code through [uglify-js-harmony](https://www.npmjs.com/package/uglify-js-harmony), it is not the default setup at the current time.
Therefore if the plugin you are intending to import does make use of ES6 features, you will need to exclude it from being minified by webpack.

To do so, add your plugin name in `/build/webpack.base.conf.js`, under the `/\.js$/` test:
 
```javascript
{
    test: /\.js$/,
    exclude: /node_modules\/(?!(markdown-it-highlightjs|markdown-it-mermaid)\/).*/
}
```

## Example

Let's go through an example by extending the renderer with the [markdown-it-sup ](https://www.npmjs.com/package/markdown-it-sup) plugin, enabling Superscript (<sup>) tags support.

> 1) **Install plugin**

`npm install markdown-it-sup --save-dev `

> 2) **Reference plugin**

* If we consider this plugin as a base plugin. 
In `src/js/bootstrap/renderer.js`, simply add:

```javascript
md
     /*
       Base plugins.
     */
    .use(require('markdown-it-sup'))
```

* If we consider this as an conditional plugin. 
Create a new options key in `manifest.json`

```json
{
  "options": {
    "sup": true
  }
}
```

Then in `src/js/bootstrap/renderer.js`, add:

```javascript
md
     /*
       Conditional plugins.
     */
    .use(require('markdown-it-sup'))
```

For the sake of simplicty, we will consider this plugin as a base plugin.

> 3) **Webpack caveats**

[This plugin](https://github.com/markdown-it/markdown-it-sup/blob/master/index.js) does not seem to make use of ES6 features, therefore, no need to exclude it from being uglified by webpack!
