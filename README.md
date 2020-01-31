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

### stacking context:

not just z-index

### css architecture:

think-build-architect mindset:

THINK:
    component driven design:
        - modular building blocks that make up interfaces
        - held together by the layout of the page
        - reusable across project
        - independent, allowing us to use them anywhere on the page
    
BUILD:
    BEM (Block Element Modifier):
        - BLOCK: standalone component that is meaningful on its own (.block{})    
        - ELEMENT: part of a block that has no standalone meaning (.block__element{})
        - MODIFIER: a different version of a block or an element (.block__element--modifier{})

ARCHITECTURE:
    the 7-1 pattern:
        - 7 different folders for partial Sass files
        - 1 main Sass file to import all other files into a ocompiled CSS stylesheet


## SECTION 4
