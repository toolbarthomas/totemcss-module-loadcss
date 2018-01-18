# Totem module: loadCSS
Twig partial for outputting your stylesheets in the loadCSS pattern to load your css asynchronous.

This module is created for [Totem](https://www.github.com/toolbarthomas/totem) projects but can also be used in any other Twig related project.

## Installation

Install totemcss-module-loadcss with [npm](https://www.npmjs.com/) (we assume you have pre-installed [node.js](https://nodejs.org/)).

```bash
$ npm install totemcss-module-loadcss --save
```

## How to include loadcss.twig
In the following example we will include loadcss.twig from our default page.
You can define multiple stylesheets at the include. You this by defining the **stylesheets** parameter.

### Source

```twig
<head>
    ...
    <link rel="stylesheet" href="main.css">
    {% include 'node_modules/totemcss-module-loadcss/partials/loadcss.twig' with {
        stylesheets: [
            'foo.css',
            'bar.css'
        ]
    } %}
    ...
</head>
```


### Result:

```html
<link rel="preload" href="foo.css" as="style" onload="this.rel='stylesheet'">
<link rel="preload" href="bar.css" as="style" onload="this.rel='stylesheet'">

<noscript>
    <link rel="stylesheet" href="foo.css">
    <link rel="stylesheet" href="bar.css">
</noscript>
<script>
    /*! loadCSS. [c]2017 Filament Group, Inc. MIT License */
    (function(){ ... }()); /* loadCSS.min.js */
    (function(){ ... }()); /* cssrelpreload.min.js */
</script>

```

## Include onloadCSS.js
This module will output the Javascript functions for browser that support the onload event.
You can extend the ouput by setting the **include_onload_fallback** parameter to *true*

## Base parameter
loadcss.twig will include the loadCSS Javascript Functions from itself.
You can include the loadCSS Javascript files from another location by defining the **base** parameter.

Using the *base* parameter is optional since we asum you can use the totem_submodules:: namespace.
The loadCSS javascript file will also be synced to your **dist**
When using this module within the Totem project structure.

```twig
<head>
    ...
    <link rel="stylesheet" href="main.css">
    {% include 'node_modules/totemcss-module-loadcss/partials/loadcss.twig' with {
        stylesheets: [
            'foo.css',
            'bar.css'
        ],
        base: 'dist/resources/' {# Lookup into: `dist/resources/totemcss-module-loadcss/` #}
    } %}
    ...
</head>
```

## loadCSS
This module uses the original loadCSS package created by [Filament group](https://www.filamentgroup.com/).
Any bugs related to the actual loadCSS functions should be reported at it's [Github Repository](https://github.com/filamentgroup/loadCSS/issues)
