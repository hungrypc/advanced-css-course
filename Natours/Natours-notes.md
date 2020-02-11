# SECTION 3

three pillars to write good html and css
1. responsive design
2. maintainable and scalable code
3. web performance

## CSS specificity:
1. importance
    - user !important declarations
    - author !important declarations
    - author declarations
    - user declarations
    - default browser declarations

2. specificity
    - inline styles
    - ids
    - classes, pseudo-classes, attribute
    - elements, pseudo-elements

3. source code 
    - the last declaration in the code overrides other declarations

## box types:
1. block-level
    - elements formatted visually as blocks
    - 100% of parent's width
    - vertically, one after another
    - box-model applies as showed

2. inline
    - content distributed inlines
    - occupies content's space
    - no line breaks
    - no height and widths
    - padding and margins only horizontal

3. inline-block
    - a mix of block and inline
    - occupies only content's space
    - no line breaks
    - box-model applies as showed

## positioning schemes:
1. normal flow
    - dfault positioning scheme
    - NOT floated
    - NOT absolutely positioned
    - elements laid out according to their source order

2. floats
    - element is removed from the normal flow
    - text and inline elements will wrap around the floated element
    - the container will not adjust height to the element

3. absolute
    - element is removed from the normal flow
    - no impact on surrounding content or elements
    - we use top, bottom, left, right to offset the element from its relatively positioned container

## css architecture:
think-build-architect mindset

1. THINK:  component driven design:
    - modular building blocks that make up interfaces
    - held together by the layout of the page
    - reusable across project
    - independent, allowing us to use them anywhere on the page
    
2. BUILD:  BEM (Block Element Modifier):
    - BLOCK: standalone component that is meaningful on its own (.block{})    
    - ELEMENT: part of a block that has no standalone meaning (.block__element{})
    - MODIFIER: a different version of a block or an element (.block__element--modifier{})

3. ARCHITECTURE:   the 7-1 pattern:
    - 7 different folders for partial Sass files
    - 1 main Sass file to import all other files into a ocompiled CSS stylesheet


# SECTION 4
we can have variables in scss
```scss 
$color-primary: #fff;
$color-secondary: #eee;
nav {
    background-color: $color-primary;
    color: $color-secondary;
}
```
we use & to attach psuedo-elements to the element it is nested within
```scss
nav {
    margin: 30px; 
    &::after {
        content: '';
        clear: both;
        display: table;
    }
}
```

this is an example of a clearfix, which may be reusable. lets put it in a mixin and include it in nav
```scss
@mixin clearfix {
    &::after {
        content: '';
        clear: both;
        display: table;
    }
}
nav {
    margin: 30px;
    @include clearfix;
}
```

we can go further with mixins
```scss
@mixin style-link-text($col) {
    text-decoration: none;
    text-transform: uppercase;
    color: $col
}
.btn-main {
    padding: 10px;
    text-align: center;
    a:link{
        @include style-link-text($primary-color);
    }
}
.btn-secondary {
    a:link {
        @include style-link-text($secondary-color);
    }
}
```

we're even able to bring in functions
```scss
@function divide($x, $y) {
    @return $x / $y;
}
.test {
    margin: divide(60, 2) * 1px // ... * 1px so that it becomes pixels
}
```

placeholders
```scss
%btn-placeholder {
    padding: 10px;
    display: inline-block;
    text-align: center;
    border-radius: 100px
}
.btn-main {
    &:link {
        @extend %btn-placeholder
    }
}
.btn-secondary {
    &:link {
        @extend %btn-placeholder
    }
}
```

# SECTION 5 
 
## responsive design principles:
1. fluid grids and layouts
    - to allow content to easily adapt to current viewport
    - uses % rather than px for all layout related lengths

2. flexible/responsive images
    - images behave differently than text content, so we need to ensure that they also adapt nicely to the current viewport

3. media queries
    - to change styles on certain viewport widths (breakpoints), allowing us to create different version of site for diff widths

## grid 
select elements that start with "col-"
```scss
[class^="col-"] {
    color: #fff;
}
```
select elements that includes "col"
```scss
[class*="col"] {
    color: #fff;
}
```
select elements that ends with "-col"
```scss
[class$="-col"] {
    color: #fff;
}
```

## sibling selectors
+ to select the direct next sibling
~ to select any sibling that isn't directly next 

# SECTION 6

## media query
order of queries important (depending on mobile first vs desktop first)

classic order:
base + typography > general layout + grid > page layout > comonents

## responsive images
density switching:
instead of src, we use srcset
```html
<img srcset="img/logo-1x.png 1x, img/logo-2x.png 2x" alt="logo" >
```

art direction (using different images depending on screen width):
use html element < picture >
```html
<picture class="footer__logo">
    <source srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x" media="(max-width: 600px)"> 
    <img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x" alt="logo" >
</picture>
```

resolution switching:
we allow broswer to choose best image for current viewport and piel density situation
```html
<img 
srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w" 
sizes="(max-width: 900x) 20vw, (max-width: 600px) 30vw, 300px" 
alt="Photo 1" class="composition__photo composition__photo--p1"
src="img-nat-1-large.jpg"
>
```

responsive in css:
can have multiple conditions:
and = and
, = or
```css
    @media (min-resolution: 192dpi) and (min-width: 600px),
        (min-width: 2000px) {
        background-image: linear-gradient(to right bottom, 
        rgba($color-primary-light, 0.8), 
        rgba($color-primary-dark, 0.8)),
        url(../img/hero.jpg);
    }
```

note: safari doesn't support (min-resolution), need to add (-webkit-min-device-pixel-ratio: 2) with what we already have

## feature queries
if browser supports what's in the (), code applies
```scss
@supports(-webkit-backdrop-filter: blur(10px)) or (backdrop-filter: blur(10px)) {
    -webkit-backdrop-filter: blur(10px);
    backdrop-filter: blur(10px);
}
```
use http://www.caniuse.com to check if certain attributes apply 

## build process
in package.json:
```json
"scripts": {
    "watch:sass": "node-sass sass/main.scss css/style.css -w",
    "compile:sass": "node-sass sass/main.scss css/style.comp.css -w",
    "concat:css": "concat -o css/style.concat.css css/icon-font.css css/style.comp.css",
    "prefix:css": "postcss --use autoprefixer -b 'last 10 versions' css/style.concat.css -o css/style.prefix.css",
    "compress:css": "node-sass css/style.prefix.css css/style.css --output-style compressed",
    "build:css": "npm-run-all compile:sass concat:css prefix:css compress:css"
}
```
watch for change > compile > concat existing css files (need npm i concat) > prefix (npm i autoprefixer postcss-cli) > compress

the last task (build) does all the above (npm i npm-run-all)

## identifying touch devices in css
```scss
@media only screen and (max-width: 900px), only screen and (hover: none) {
    // content
}
```
