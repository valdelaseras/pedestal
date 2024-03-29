# Pedestal 

An SCSS/SMACCS 'pedestal' to accelerate your workflow. 

Pedestal provides a solid foundation, with an automatically responsive, flexible and consistent layout and 
clean overall look. Quickly configure some variables to adjust the base styles, then you can focus on the fun stuff 
and easily add your own unique flair by sprinkling your custom styles on top °˖✧◝(⁰▿⁰)◜✧˖°

## Installation

[pedestal](https://www.npmjs.com/package/@valdelaseras/pedestal) | [sass](https://www.npmjs.com/package/sass)

Install Sass in your project if you haven't already:

```
npm i sass
```

Add the following script to your package.json:

```
"scripts": {
    "sass": "sass --watch path/to/index.scss path/to/index.css"
},
```

Install Pedestal:

```
npm i @valdelaseras/pedestal
```

## Guide

1. [Overriding variables](#overriding-variables)
    - [Colours](#colours)
    - [Typography](#typography)
2. [Templating](#templating)
    - [Main structure](#main-structure)
    - [Column system](#column-system)
    - [Grid system](#grid-system)
    - [Paddings](#paddings)

### Overriding variables

Copy and paste the codeblock below to your __index.scss__ and overwrite Pedestal variable values as desired. 
The values below are Pedestals defaults. Those you do not intend to override, can simply be removed.

```scss
@use '../../node_modules/@valdelaseras/pedestal/scss/index.scss' with (
    ///* variables *///

    //* base *//
    /* layout */
    $breakpoint: 1440px,
    $padding: 20px,
    $grid: 80vw, /* for min-width $breakpoint screens */
    $max-grid: 80vw,  /* optional fixed maximum grid width ( for really large screens for example ) */
    
    /* borders */
    $border-width: 1px,
    $border-radius: 0,
   
    //* colors (rgba) *//
    /* base */
    $color-primary: rgb(0,0,0),
    $color-secondary: rgb(255,255,255),
    
    /* accent */
    $accent-color-primary: rgb(69,180,134),
    $accent-color-secondary: rgb(180,69,115),
    
    /* utility */
    $color-success: rgb(19,190,108),
    $color-warning: rgb(224,107,27),
    $color-error: rgb(196,78,78),
    $color-disabled: rgb(125,125,125),
    
     /* lighten value for utility element background-color, derived from the utility base colours */
    $lighten: 32,
    
    //* typography *//
    /* stack */
    $font-stack-primary: #{Barlow, Helvetica-Neue, Arial, sans-serif},
    $font-stack-secondary: #{Garamond, serif},
    
    /* colors */
    $font-color-primary: rgb(0,0,0),
    $font-color-secondary:rgb(255,255,255),
    $accent-font-color-primary: rgb(69,180,134),
    $accent-font-color-secondary: rgb(180,69,115),
    
    /* size */
    $font-size-mobile: 16px,
    $font-size-desktop: 18px,
    $heading-base-font-size-mobile: 1, /* assuming 'rem' as suffix */
    $heading-base-font-size-desktop: 2, /* in 'rem' */
    
    //* scrollbar *//
    $scrollbar-width: 4px,
    $background-color-scrollbar-thumb: rgb(255,255,255),
    $background-color-scrollbar-thumb-hover: rgb(180,69,115),
);
```

To use the variables directly in your custom SCSS, import the package at the top of your stylesheet and
use it like so:

```scss 
@use '../../node_modules/@valdelaseras/pedestal/scss/index.scss' as pedestal;

#some-section {
    h1 {
        -webkit-text-stroke: 4px pedestal.$accent-font-color-secondary;
    }
}
```

### Colors

I advise, for an average UI, to pick 2 contrasting, "muted" colors for `$color-primary` and `$color-secondary` ( e.g.
black and white ), and then two contrasting, "fun" colors for `$accent-color-primary` and `$accent-color-secondary`. 

The colors in these two sets are used in combination with one other, so it works best following this pattern. Of course,
you can add as many colors as you like on top of these. 


### Typography

Heading sizes are automatically calculated by the configurable `$heading-base-font-size`. The value for this variable is 
applied to `<h5>` elements, and subsequently multiplied by 1.618, the `$golden-ratio`, the further we go 'up' like so:

```scss
$h5-size: $heading-base-font-size-mobile;
$h4-size: calc( $h5-size * $golden-ratio );
$h3-size: calc( $h4-size * $golden-ratio );
$h2-size: calc( $h3-size * $golden-ratio );
$h1-size: calc( $h2-size * $golden-ratio );

h1 { font-size: #{$h1-size}rem; }
h2 { font-size: #{$h2-size}rem; }
h3 { font-size: #{$h3-size}rem; }
h4 { font-size: #{$h4-size}rem; }
h5 { font-size: #{$h5-size}rem; }
```

You can set different base values for `mobile` and `desktop` font sizes and heading base sizes.

### Templating

There are a few recommended template structures to follow in order for Pedestal to work nicely. It's not difficult and
the templating is clean. If you stick to this structure, your layout will always be nice and responsive. 

#### Main structure

A general page outline, divided into sections, may follow a basic structure as below: 

```html
   <!-- section A -->
   <section>
      <div class="grid">
          <div class="column">
              <div class="content">
                  <!-- section A content goes here -->
              </div>
          </div>
      </div>
   </section>
   
   <!-- section B -->
   <section>
      <div class="grid">
          <div class="column">
              <div class="content">
                  <!-- section B content goes here -->
              </div>
          </div>
      </div>
   </section>
   
   <!-- section C ...etc-->
```

#### Column system

In Pedestal, everything is ordered into columns. Note that whatever column combination you use, on screen widths
below your configured `$breakpoint` value, the columns will stack vertically by default. 

If you do wish to also have multiple columns on mobile or tablet devices, you can simply add additional scss like:

```scss
.column.two.mobile {
    width: 50%;
}
```

You can write intuitive column structures in any combination like so:

```html
<!-- a 2 column layout -->
<div class="column"> <!-- 100% -->
    <div class="column two"> <!-- 50% -->
        <div class="content">
            <!-- content goes here -->
        </div>
    </div>
    <div class="column two"> <!-- 50% -->
        <div class="content">
            <!-- content goes here -->
        </div>
    </div>
</div>

<!-- a 3 column layout -->
<div class="column"> <!-- 100% -->
    <div class="column three"> <!-- 33% -->
        <div class="content">
            <!-- content goes here -->
        </div>
    </div>
    <div class="column three"> <!-- 33% -->
        <div class="content">
            <!-- content goes here -->
        </div>
    </div>
    <div class="column three"> <!-- 33% -->
        <div class="content">
            <!-- content goes here -->
        </div>
    </div>
</div>

<!-- nest columns -->
<div class="column"> <!-- 100% -->
    <div class="column three a"> <!-- 33% -->
        <div class="content">
            <!-- content goes here -->
        </div>
    </div>
    <div class="column three b"> <!-- 66% -->
        <div class="column two"> <!-- 50% of parent column -->
            <div class="content">
                <!-- content goes here -->
            </div>
        </div>
        <div class="column two"> <!-- 50% of parent column -->
            <div class="column four"> <!-- 25% of parent column -->
                <div class="content">
                    <!-- content goes here -->
                </div>
            </div>
            <div class="column four"> <!-- 25% of parent column -->
                <div class="content">
                    <!-- content goes here -->
                </div>
            </div>
            <div class="column four"> <!-- 25% of parent column -->
                <div class="content">
                    <!-- content goes here -->
                </div>
            </div>
            <div class="column four"> <!-- 25% of parent column -->
                <div class="content">
                    <!-- content goes here -->
                </div>
            </div>
        </div>
    </div>
</div>
```

The following column classes are available by default:

| column | column two | column three (a) | column four (a) | column phi a | column phi b | column three b | column four b |
|--------|------------|------------------|-----------------|--------------|--------------|----------------|---------------|
| 100%   | 50%        | 33.33%           | 25%             | 38%          | 62%          | 66.66%         | 75%           |


Columns stack vertically by default on screens below `$breakpoint`, but will align to the left as a row from that 
breakpoint without any additional SCSS.

When you have the desired column structure, wrap your content in `<div class="content"></div>` as in the sample above. This 
is going to ensure you will always have consistent padding between content vertically and horizontally, on small or 
large devices.

#### Responsive content reversal
Sometimes you need to reverse the position of adjacent columns. Consider the scenario where you might have a paragraph of
text and a graph you want to show after the paragraph. On devices with a large screen, for whatever
reason, you want to show the graph to the left and the text on the right: the reverse of the normal flow of a template 
with two nested sibling columns. Not a problem!

Of course we are going to build for mobile first ;) so all you really have to do is add the `reverse-on-desktop` class
to the parent column, which will reverse your columns at your `$breakpoint` and above.

```html
<div class="column reverse-on-desktop">
   <div class="column two">A</div>
   <div class="column two">B</div>
</div>
```

`A` and `B` will be vertically stacked on mobile in that order, while `B` will be positioned left and `A` to the right
from the `$breakpoint`.

#### Grid system

The `$grid` value you configure will set the default width of your content, center aligned, on screen widths with a 
minimum of your `$breakpoint` value. Nest it within `<section>` elements, or leave it out of a section to break out of
the grid if desired.

```html
<section class="theme-primary">
    <div class="grid">
        <!-- columns go here -->
    </div>
</section>
```

You can optionally set a `$max-grid` as well. You might want to set a maximum fixed width for really large screens, for example:
`80vw` on a screen width over `2560px` can really mess up the look of your UI. 


