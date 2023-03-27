# pedestal

A simple, basic SCSS 'pedestal' to accelerate new ( private ) project setups in our companies 
'house style' structure.

## installation

```
npm i @valdelaseras/pedestal
```

[npm](https://www.npmjs.com/package/@valdelaseras/pedestal)

---

## variables

Overwrite the following variables and default values for quick and simple customisation:

```scss
/* variables */
$breakpoint: 1440px!default;
$padding: 20px!default;
$grid: 80vw!default;
$font-size: 16px!default;
$border-width: 2px!default;

/* colours */
/* base */
$primary-color: rgb(0,0,0)!default;
$secondary-color: rgb(255,255,255)!default;

$success-color: rgb(19,190,108)!default;
$warning-color: rgb(224,107,27)!default;
$error-color: rgb(196,78,78)!default;

/* fonts */
$primary-font-color: $primary-color;
$secondary-font-color: $secondary-color;

$success-font-color: $success-color;
$warning-font-color: $warning-color;
$error-font-color: $error-color;

/* background */
$primary-background-color: $primary-color;
$secondary-background-color: $secondary-color;

$success-background-color: rgba($success-color, .25);
$warning-background-color: rgba($warning-color, .25);
$error-background-color: rgba($error-color, .25);

/* typography */
$primary-font-stack: 'Helvetica-Neue', sans-serif!default;
$secondary-font-stack: 'Helvetica', sans-serif!default;
```

