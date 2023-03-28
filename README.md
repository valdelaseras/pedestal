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

Overwrite the following variables for quick and simple customisation:

```scss
/* base */
$breakpoint             /* 1440px!default */
$padding                /* 20px!default */
$grid                   /* 80vw!default */
$border-width           /* 2px!default */
$scrollbar-width        /* 4px!default */
$border-radius          /* 0!default */

/* typography */
$font-size              /* 16px!default */
$heading-base-font-size /* 1.5!default, assuming 'rem' as suffix */
$primary-font-stack     /* 'Helvetica-Neue', sans-serif!default */
$secondary-font-stack   /* 'Helvetica', sans-serif!default */

/* colours */
/* base */
$primary-color          /* rgb(0,0,0)!default */
$secondary-color        /* rgb(255,255,255)!default */
$tertiary-color         /* rgb(128,128,128)!default */
$quaternary-color       /* rgb(66,66,66)!default */

/* accent */
$primary-accent-color   /* rgb(37, 127, 210)!default */
$secondary-accent-color /* rgb(199, 50, 137)!default */

/* utility */
$success-color          /* rgb(19,190,108)!default */
$warning-color          /* rgb(224,107,27)!default */
$error-color            /* rgb(196,78,78)!default */
$disabled-color         /* rgb(125,125,125)!default */

/* alpha value for utility element backgrounds derived from the utility base colours */
$background-alpha       /* .25!default */
```

