# pedestal

A very simple, basic SCSS 'pedestal' to accelerate new project setups. 

Pedestal provides a solid base to work from, creating a super easy-to-implement responsive, flexible and 
consistent layout. Some basic variables are provided that can be easily overridden and to quick start a new 
project hassle-free.    


## installation

```
npm i @valdelaseras/pedestal
```

find it on [npm](https://www.npmjs.com/package/@valdelaseras/pedestal)

---

## variables

In your project, install sass:

```
npm i sass --save-dev
```

Create an index.scss file as normal and add the code below to overwrite Pedestal variables as desired. 
The values in this example below are Pedestals defaults. Those you do not intend to override, can be removed.

```scss
@use '../../node_modules/@valdelaseras/pedestal/scss/index.scss' with (
    /* base */
    $breakpoint: 1440px,
    $padding: 20px,
    $grid: 80vw,              
    $border-width: 2px,
    $scrollbar-width: 4px,
    $border-radius: 0,
    
    /* typography */
    $font-size: 16,
    $heading-base-font-size: 1.5, /* assuming 'rem' as suffix */
    $primary-font-stack: "'Helvetica-Neue', sans-serif",
    $secondary-font-stack: "'Helvetica', sans-serif",
    
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
    
    /* utility */
    $success-color: rgb(19,190,108),
    $warning-color: rgb(224,107,27),
    $error-color: rgb(196,78,78),
    $disabled-color: rgb(125,125,125),
    
    /* alpha value for utility element backgrounds derived from the utility base colours */
    $background-alpha: .25
);
```

