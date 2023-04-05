# Pedestal [WIP] 

An SCSS/SMACCS 'pedestal' to accelerate your workflow. 

Pedestal provides a solid UI foundation, with an automatically responsive, flexible and consistent layout and 
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
3. [Theming](#theming)
    - [Base](#base)
    - [Accent](#accent)
    - [Font base](#font-base)
    - [Font accent](#font-accent)
    - [Utility](#utility)

### Overriding variables

Copy and paste the codeblock below to your __index.scss__ and overwrite Pedestal variable values as desired. 
The values below are Pedestals defaults. Those you do not intend to override, can simply be removed.

```scss
@use '../../node_modules/@valdelaseras/pedestal/scss/index.scss' with (
    ///* variables *///

    //* base *//
    $breakpoint: 1440px,
    $padding: 20px,
    $grid: 80vw, /* for min-width $breakpoint screens */
    $border-width: 1px,
    $border-radius: 0,
    $scrollbar-width: 4px,
   
    //* colours (rgba) *//
    /* base */
    $color-primary: rgb(0,0,0),
    $color-secondary: rgb(255,255,255),
    $color-tertiary: rgb(128,128,128),
    $color-quaternary: rgb(66,66,66),
    
    /* accent */
    $accent-color-primary: rgb(37, 127, 210),
    $accent-color-secondary: rgb(199, 50, 137),
    
    //* typography *//
    $font-stack-primary: #{Helvetica-Neue, Arial, sans-serif},
    $font-stack-secondary: #{Helvetica, Arial, sans-serif},
    
    $accent-font-color-primary: rgb(37, 127, 210),
    $accent-font-color-secondary: rgb(199, 50, 137),
    
    $font-size: 16px,
    $heading-base-font-size: 1, /* assuming 'rem' as suffix */
  
    //* utility *//
    $color-success: rgb(19,190,108),
    $color-warning: rgb(224,107,27),
    $color-error: rgb(196,78,78),
    $color-disabled: rgb(125,125,125),
    
    /* lighten value for utility element background-color, derived from the utility base colours */
    $lighten: 32,
);
```

To use the variables directly in your custom SCSS, import the package at the top of your stylesheet and
use it like so:

```scss 
@use '../../../node_modules/@valdelaseras/pedestal/scss/index.scss' as pedestal;

#some-section {
    h1 {
        -webkit-text-stroke: 4px pedestal.$accent-font-color-secondary;
    }
}
```

### Colours
It is strongly advised to pick 2 highly contrasting, "muted" colours for `$color-primary` and `$color-secondary` ( e.g.
black and white ), and then two contrasting, "fun" colours for `$accent-color-primary` and `$accent-color-secondary`. 
The colours in these two sets are used in combination with one other in [themes](#theming), so it works best following
this pattern.

### Typography

Heading sizes are automatically calculated by the configurable `$heading-base-font-size`. The value for this variable is 
applied to `<h5>` elements, and subsequently multiplied by 1.618, the `$golden-ratio`, the further we go 'up' like so:

```scss
$h5-size: $heading-base-font-size;
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

### Templating

Pedestal is designed to minimally 'pollute' your templates with classes, so sprinkling your own styles on top will be 
easier to do and maintain. However, there are a few recommended template structures to follow in order for Pedestal to
work nicely. I promise it will be good, as it will make Pedestal work optimally but also nudges you to stick to semantic 
template structures.

#### Main structure

A general main element outline should follow the basic structure below: 

```html
<main>
    <article>
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
    </article>
</main>
```

#### Column system

In Pedestal, everything is ordered into columns. Note that whatever column combination you use, on screen widths
below your configured `$breakpoint` value, the columns will stack vertically by default. This means you never have to worry
about responsiveness and don't need to do any extra work for small or larger devices. 

If you do wish to also have multiple columns on mobile devices or tablet devices, you can simply add additional scss like:

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


Columns stack vertically by default on screens below `$breakpoint`, but will align to the left in a row from that 
breakpoint without any additional, custom SCSS.

When you have the desired column structure, wrap your content in `<div class="content"></div>` as in the sample above. This 
is going to ensure you will always have consistent padding between content vertically and horizontally, on small or 
large devices.

#### Grid system

The `$grid` value you configer will set the default width of your content, center aligned, on screen widths with a 
minimum of your `$breakpoint` value. Nest it within `<section>` elements, or leave it out of a section to break out of
the grid if desired.

```html
<section class="primary-theme">
    <div class="grid">
        <!-- columns go here -->
    </div>
</section>
```

#### Paddings

Paddings are calculated across all the stylesheets based on the provided `$padding` value. Most of the time
the `$golden-ratio` variable ( 1.618 ) is used to automatically create consistent and visually pleasing whitespace and 
paddings within elements, by either multiplying or dividing the configurable `$padding` value.

### Theming

The following theme classes are available by default to apply to elements like `section`, `form` and
`card`, setting you up with a variety of themes and options while using just a few colours.
Too many colours in a palette can be problematic, so you might consider not to add too many on top, although that
is complete up to you.

The primary- and corresponding secondary themes are generally the inverse of one another, hence it is advised to
pick contrasting sets of [colours](#colours). 

#### Base

```scss
.theme-primary {
   background-color: $background-color-primary;
   color: $font-color-primary;

   &.bordered {
      border-color: $color-secondary;
   }
}

.theme-secondary {
   background-color: $background-color-secondary;
   color: $font-color-secondary;

   &.bordered {
      border-color: $color-primary;
   }
}
```

#### Accent

```scss
.accent-theme-primary {
   background-color: $accent-background-color-primary;
   color: $font-color-primary;

   &.bordered {
      border-color: $color-secondary;
   }
}

.accent-theme-secondary {
   background-color: $accent-background-color-secondary;
   color: $font-color-primary;

   &.bordered {
      border-color: $color-secondary;
   }
}
```

#### Font base

```scss
.font-color-primary {
   color: $font-color-primary;
}

.font-color-secondary {
   color: $font-color-secondary;
}
```

#### Font accent

```scss
.accent-font-color-primary {
   color: $accent-font-color-primary;
}

.accent-font-color-secondary {
   color: $accent-font-color-secondary;
}
```

#### Utility

```scss
.theme-success {
   background-color: $background-color-success;
   color: $font-color-success;

   &.bordered {
      border-color: $color-success;
   }
}

.theme-warning {
   background-color: $background-color-warning;
   color: $font-color-warning;

   &.bordered {
      border-color: $color-warning;
   }
}

.theme-error {
   background-color: $background-color-error;
   color: $font-color-error;

   &.bordered {
      border-color: $color-error;
   }
}
```


