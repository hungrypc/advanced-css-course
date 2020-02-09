# advanced css notes

## SECTION 3

three pillars to write good html and css
1. responsive design
2. maintainable and scalable code
3. web performance

### CSS specificity:
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

### box types:
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

### positioning schemes:
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

### css architecture:
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


## SECTION 4
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

## SECTION 5 
 
### responsive design principles:
1. fluid grids and layouts
    - to allow content to easily adapt to current viewport
    - uses % rather than px for all layout related lengths

2. flexible/responsive images
    - images behave differently than text content, so we need to ensure that they also adapt nicely to the current viewport

3. media queries
    - to change styles on certain viewport widths (breakpoints), allowing us to create different version of site for diff widths

### grid 
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

### sibling selectors
+ to select the direct next sibling
~ to select any sibling that isn't directly next 

## SECTION 6

### media query
order of queries important (depending on mobile first vs desktop first)

classic order:
base + typography > general layout + grid > page layout > comonents



