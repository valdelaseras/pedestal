# pedestal

A basic SCSS 'pedestal' to accelerate new project setups. 

Pedestal provides a style foundation to work from, with an easy-to-implement responsive, flexible, 
consistent layout and clean overall look. Some variables are provided that can be overridden, 
then just sprinkle your awesome custom styles on top :)     

---

## installation

[pedestal](https://www.npmjs.com/package/@valdelaseras/pedestal) | [sass](https://www.npmjs.com/package/sass)

Install __sass__ if you haven't already:

```
npm i sass
```

Add the following script to your package.json:

```
"scripts": {
    "sass": "sass --watch path/to/index.scss path/to/index.css"
},
```

Install __@valdelaseras/pedestal__:

```
npm i @valdelaseras/pedestal
```

---

## guide

1. [overriding variables](#overriding-variables)
2. [templating](#templating)
    - [page structure](#page-structure)
    - [column system](#column-system)
    - [grid system](#grid-system)
    - [components](#components)
        - [button](#button)
        - [card](#card)
        - [form](#form)
        - [input](#input)
        - [select](#select)
        - [textarea](#textarea)

### overriding variables

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

---

### templating

Pedestal is designed to minimally 'pollute' your templates with classes ( kind of like the opposite of Tailwind ),
but there are a few recommended template structures to follow in order for Pedestal to work nicely. I promise it 
will be a good as it will make Pedestal work optimally, but also nudges you to stick to semantically correct HTML.

#### page structure

A general page outline should follow the structure below: 

```html
<header>
    <nav role="navigation">
        <!-- navigation goes here -->
    </nav>
</header>
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
        
        <!-- ...etc-->
    </article>
</main>
<footer>
    <!-- footer content goes here -->
</footer>
```

#### column system

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

When you have the desired column structure, wrap your content in `<div class="content">` as in the sample above. This 
is going to ensure you will always have consistent padding between content vertically and horizontally, on small or 
large devices.

#### grid system

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

#### components

##### button
##### card
##### form
##### input
##### select
##### textarea



