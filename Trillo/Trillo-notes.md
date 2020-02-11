#SECTION 7

The element with display: flex = flex container. Elements within flex container = flex items.
2 axis to remember:
- main axis (horizontal)
- cross axis (vertical)

container:
1. flex-direction: row | row-reverse | column | column-reverse
2. flex-wrap: nowrap | wrap | wrap-reverse
3. justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly
    (affects main axis
4. align-items: stretch | flex-start | flex-end | center | baseline
    (affects cross axis)
5. align-content: stretch | flex-start | flex-end | center | space-between | space-around

items:
1. align-self: auto | stretch | flex-start | flex-end | center | baseline
2. order: 0 | < integer >
3. flex-grow: 0 | < integer >
4. flex-shrink: 1 | < integer >
5. flex-basis: auto | < length >

3, 4, 5 can be defined within one attribute (flex: 0 1 auto)

