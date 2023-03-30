# Pedestal [WIP] 

A basic SCSS 'pedestal' to accelerate new project setups. 

Pedestal provides a style foundation to work from, with an easy-to-implement responsive, flexible, 
consistent layout and clean overall look. Some variables are provided that can be overridden, 
then just sprinkle your own awesome, custom styles on top °˖✧◝(⁰▿⁰)◜✧˖°

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

Copy and paste the codeblock below to your __index.scss__ file and overwrite Pedestal variables 
as desired. The values below are Pedestals defaults. Those you do not intend to override, can simply be removed.

```scss
@use '../../node_modules/@valdelaseras/pedestal/scss/index.scss' with (
    /* base */
    $breakpoint: 1440px,
    $padding: 20px,
    $grid: 80vw, /* for min-width $breakpoint screens */              
    $border-width: 2px,
    $scrollbar-width: 4px,
    $border-radius: 0,
    
    /* typography */
    $font-size: 16px,
    $heading-base-font-size: 1.5, /* assuming 'rem' as suffix */
    $primary-font-stack: #{Helvetica-Neue, Arial, sans-serif},
    $secondary-font-stack: #{Helvetica, Arial, sans-serif},
    
    /* colours */
    /* Please use rgb values */
    /* base */
    $primary-color: rgb(0,0,0),
    $secondary-color: rgb(255,255,255),
    $tertiary-color: rgb(128,128,128),
    $quaternary-color: rgb(66,66,66),
    
    /* accent */
    $primary-accent-color: rgb(37, 127, 210),
    $secondary-accent-color: rgb(199, 50, 137),
    
    $primary-accent-font-color: rgb(37, 127, 210),
    $secondary-accent-font-color: rgb(199, 50, 137),
    
    /* utility */
    $success-color: rgb(19,190,108),
    $warning-color: rgb(224,107,27),
    $error-color: rgb(196,78,78),
    $disabled-color: rgb(125,125,125),
    
    /* alpha value for utility element backgrounds derived from the utility base colours */
    $background-alpha: .25
);
```

### Colours
It is strongly advised to pick 2 highly contrasting, "muted" colours for `$primary-color` and `$secondary-color` ( e.g.
black and white ), and then two contrasting, "fun" colours for `$primary-accent-color` and `$secondary-accent-color`. 
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

Pedestal is designed to minimally 'pollute' your templates with classes ( kind of like the opposite of Tailwind ),
but there are a few recommended template structures to follow in order for Pedestal to work nicely. I promise it 
will be a good as it will make Pedestal work optimally, but also nudges you to stick to semantically correct HTML.

#### Main structure

A general main element outline should follow the structure below: 

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
below your configured `$breakpoint` value, the columns will always stack vertically. This means you never have to worry
about responsiveness and don't need to do any extra work for small or larger devices. 

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
Too many colours in a palette can be problematic, so consider not to add too many on top.

The primary- and corresponding secondary themes are generally the inverse of one another, hence it is advised to
pick contrasting sets of [colours](#colours). 

#### Base
```scss
.primary-theme {
    background-color: $primary-background-color;
    color: $primary-font-color;
    &.bordered {
        border-color: $secondary-color;
    }
}

.secondary-theme {
    background-color: $secondary-background-color;
    color: $secondary-font-color;
    &.bordered {
        border-color: $primary-color;
    }
}
```

#### Accent 
```scss
.primary-accent-theme {
    background-color: $primary-accent-background-color;
    color: $primary-font-color;
    &.bordered {
        border-color: $secondary-color;
    }
}

.secondary-accent-theme {
    background-color: $secondary-accent-background-color;
    color: $primary-font-color;
    &.bordered {
        border-color: $secondary-color;
    }
}
```

#### Font base
```scss
.primary-font-color {
    color: $primary-font-color;
}

.secondary-font-color {
    color: $secondary-font-color;
}
```

#### Font accent
```scss
.primary-accent-font-color {
    color: $primary-accent-font-color;
}

.secondary-accent-font-color {
    color: $secondary-accent-font-color;
}
```

#### Utility 
```scss
.success-theme {
    background-color: $success-background-color;
    color: $success-font-color;
    &.bordered {
        border-color: $success-color;
    }
}

.warning-theme {
    background-color: $warning-background-color;
    color: $warning-font-color;
    &.bordered {
        border-color: $warning-color;
    }
}

.error-theme {
    background-color: $error-background-color;
    color: $error-font-color;
    &.bordered {
        border-color: $error-color;
    }
}
```


