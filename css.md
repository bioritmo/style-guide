CSS/SCSS Styleguide
==============

Coding Style
============

* Keep a whitespace after property names (like ```color: #000```) and before the opening bracket (as in  ```.selector {```);
* Write hexadecimal colors using downcase letters;
* Write new selectors using ```-``` as a word separator rather than ```_``` (```section-title``` instead of ```section_title```);


Property organization
=====================

Do your best to organize properties in related groups of functionality (such as the following), and sort them in this given order:

+ Preprocessor specific directives, like ```@extends``` or ```@include```;
+ ```position``` and related properties like ```top```, ```right```, ```z-index``` and such;
+ ```display``` and box-model related properties: ```height```, ```width```, ```padding```, ```margin```, ```box-sizing```, ```visibility```, etc;
+ Font/text definitions (```font-family``` and friends, ```line-height```, ```text-decoration```) and ```color```;
+ ```background``` and ```border``` related properties;
+ Additional CSS3 properties like ```box-shadow```, ```transform``` and such. Such grouping rules might be enough to most of the daily CSS you should face.

Everything else
---------------

In case of complex definitions and long list of properties, consider splitting up groups of related styles into different selectors and applying multiple classes to the same element. (TODO notes on modularity?)

Format
======

* You may separate each selector by a newline to improve readability of a complex set of selectors;

```
input[type='submit'],
input[type='reset'],
input[type='button'] {
  /* ... */
}
```

* In case of single property declaration you may use a single-line format:

```.selector { font-weight: bold; }```


Documentation
=============

CSS isn't the most expressive language and requires a lot of knowledge of the existing domain and markup to understand the purpose of specific styles, how they should be used and what we can achieve with it. A good way to communicate these details about your code is to explain them with some bits of documentation.

As we have things like [TomDoc](http://tomdoc.org/) to specify how we should document our Ruby code, here is a small specification on how to document stylesheets.

```
/* ==========================================================================
Main comment block

This can be used as a top level description block of your stylesheet,
explaning the purpose of the following styles and the subtle variations
that will be available. If your module/section/component requires a complex
markup structure you can always write down a small markup example below.

<div class='fancy-component'>
  <h2 class='fancy-component-title'>How you doing?</h2>
  <div class='fancy-component-body'>
    ...
  </div>
</div>
========================================================================== */

.fancy-component {
  /* ... */
}

/* Sub section comment block
A sub section can be used to split big chunks of code and describe what
the following styles are about - you can use to document variations of
the core styles (a `much-more-fancy` variation of our `fancy-component`)
or secondary definitions of your code.
========================================================================== */
.fancy-component.much-more-fancy {
  /* ... */
}

/*
  Bullet lists can be useful to enumerate several details of a group
  of properties. Here is an example from https://github.com/necolas/idiomatic-css:

 * Grid container
 *
 * Must only contain `.cell` children.
 *
 * 1. Remove inter-cell whitespace
 * 2. Prevent inline-block cells wrapping
 */

.grid {
  height: 100%;
  font-size: 0; /* 1 */
  white-space: nowrap; /* 2 */
}

/* Or you can add just a simple remark, about an odd line or something very specific */
```

Selector Specificity
====================

TODO: Notes on specificity

Vendor prefixes
===============
In case of using vendor prefixed properties and functions be sure to check browser compatibility at [Can I use…](http://caniuse.com/) to be sure of it and which prefixes you will need. Several CSS3 properties don't require vendor prefixes on several browsers, like ```border-radius``` and ```box-shadow```. If you are not that lucky, place the vendor-prefixed properties before it's own unprefixed version.

```css
 .button:hover {
    -moz-transform: background-position .2s ease;
    -ms-transform: background-position .2s ease;
    -o-transform: background-position .2s ease;
    -webkit-transform: background-position .2s ease;
    transform: background-position .2s ease;
  }
```

Preprocessors
=============

Preprocessors like [Sass](http://sass-lang.com/), [LESS](http://lesscss.org/) or [Stylus](http://learnboost.github.io/stylus/) are useful for handling a large set of stylesheets and we should take note on a few details so we won't do bad use of these tools.

Whenever using variables, define them with Screaming snake case so it's easier to scan the variable usage through your code. It is easier to spot $FONT_SIZE than $font-size;
Use a language specific comment delimiter like // instead of the classic /* */ from CSS. They will work nicer with syntax highlighters and will be always ignored when compiling your stylesheets;
Use the same extensions for all your stylesheets, even vendored files and those that have vanilla CSS code, since @import directives with .css files won't combine both files but emit a traditional CSS @import directive;
Don't get too high on nesting - nested selector is a good way to reduce duplication of parent selectors but it compromises readability of your code. So, keep in mind to use a maximum nest of 3 levels deep and keep nested blocks with at most 40/50 lines, so they can fit in a single editor screen.

Organization
============

TODO: Notes on file organization

References
==========

Parts of this guideline was based on several resources across the Internet, that might provide extra information on specific topics, different approaches for similar scenarios or unanticipated scenarios on this guideline.

* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [GitHub CSS Styleguide](https://github.com/styleguide/css)
* [CSS-Tricks Sass Style Guide](http://css-tricks.com/sass-style-guide/)
* [Mark Otto Code guide](https://github.com/mdo/code-guide)
