# Advanced CSS Notes - Udemy course by Jonas Schmedtmann

# The Three Pillars of writing GOOD HTML and CSS

1. Responsive Design
2. Maintainable and scalable code
3. Web Performance

## Responsive Design

- Your app should work across ALL devices
  Fluid Layouts, Media Queries, Responsive Images, Correct Units and Desktop first or Mobile first

## Maintainable Code

- To write code that is clean, easy to understand, supports future growth and is reusable.
- File organization
- Class names
- HTML structure

## Web Performance

- Less HTTP Requests
- Less code
- Compress code
- Use a CSS preprocessor (Like SaSS)
- Less images
- Compress images

# How does CSS work behind the scenes?

## What happens to CSS when we load up a webpage?

1. Load HTML
2. Parse HTML (Decodes the code line by line)
3. Creates Document Object Model (DOM)
   <br />
   <br />
   3.5 Loads CSS and Pareses CSS.
   <br />

   3.5.1 Resolve conflicting CSS
   <br />

   3.5.2 Process final CSS values.

4. CSS object model (CSSOM)
5. Render Tree
6. Website rendering (The visual formatting model)
7. Final website is rendered

# How CSS is parsed (Part 1)

.myClass = selector <br />
{} = declaration block <br />
font-size = property <br />
20px = declaration value <br />
font-size: 20px; = declaration

```
.my-class {
  color: blue;
  text-align: center;
  font-size: 20px
}
```

## The cascade (The "C" in CSS)

- Process of combining different stylesheets and resolving conflicts between CSS rules and declarations, when more than one rule applies to a certain element.

- Default browser declarations (Example default anchor tags been styled with blue text and underlines). This is called the `User agent css/stylesheet`

importance > specificity > source order

### Importance

1. User !important declarations
2. Author !import declarations
3. Author declarations
4. User declarations
5. Default browser declarations

### Specificity

1. Inline styles
2. ID's
3. Classes, pseudo-classes, attributes
4. Elements, pseudo-elements

### Source order

If everything from importance, and specificity is still a tie at this point the last declaration written in the code will override all other declarations and will be applied.

## Recap

- CSS Declarations marked with !important have the highest priority
- You should only use !important as a last resort, it's better to use correct specificities - this will make your code more maintainable
- inline styles will always have priortiy over styles in external stylesheets however this is not good practice
- A selector contains 1 ID more specific than one with 1000 classes
- A selector that contains 1 class is more specific than one with a 1000 elements

- The universal selector `*` has no specificity value (0,0,0,0)

- Rely more on specificity than on the order of your selectors

- But, rely on order when using 3rd party style sheets - always put your author (your own) stylesheet last

[CodePen Example!](https://codepen.io/christopherdalziel/pen/qBbppwj)

# How CSS is parsed (Part 2)

### How CSS values are processed

```
You must understand EVERYTHING is converted to pixels in the end
```

1. Declared value (author declarations)

2. Cascaded value (after the cascade (Example of `font-size`: if there is absolutely no value the browser default value of `16px` will still be specified here))

3. Specified value (default, there is no cascaded value?, (Example of `padding`: if there is absolutely no value the initial value of `0` will still be specified here))

4. Computed value (converting relative values from absolute)

5. Used value (final calculations based on layout)

6. Actual value (browser and device restrictions)

`This information was explained clearly with tables on the udemy tut, would check again later.`

### How units are converted from relative to absolute (px)

#### em (font)

3em converted to pixels = <br />
em * parent computed font size = 72px (3*24)

#### em (lengths)

2em <br />
`Exmaple in tut` <br/>
em \* current element computed font-size = 48px

#### rem

em \* root =

## Recap

- Each CSS property has an initial value which is used if nothing is declared
- Browers specify a `root font-size` for each page (Usually 16px)
- Percentages and relative values are always converted to pixels
- Percentages are measured relative to their parents font-size, if used to specify font size
- Percentages are measured relative to their parents with, if used to specify lengths
  -em are measured relative to their parent font-size, if used to specify font-size
  -em are measured relative to the current font-size, if used to specify lengths
- rem are always measured relative to the documents root font-size

# Inheritance in CSS

Example:
Lets analyse the line-height of the child

```
.parent {
  font-size: 20px;
  line-height: 150%;
}

.child {
  font-size: 25px;
}
```

Every CSS property must have a value even if it is not specified.

Is there a cascaded value? <br />
Yes: Specified value = cascaded value <br />
No: Is the property inherited? (Specific to each property) <br/>
Yes the property is inherited: specified value = computed value of the parent element.

The value isn't simply 150% it's the computed value, in this case it's 150% of 20px which is 30px so the line height in the child element will be 30px not 150% of the 25px font size.

No the property is not inherited: specified value = initial value

## Recap

- Inheritance passes the values of some specific properties from parents to children - more maintainable code
- Properties related to text are inherited: font-family, font-size, color etc
- The computed value of a property is what gets inherited not the declared value
- Inheritance of a property only works if nobody declares a value for that property
- The inherit keyword forces inheritance on a certain property
- The initial keyword resets a property to it's initial value

# Converting px to rem, why?

- How and why to use rem units in our projects
- A workflow to convert px to rem

Using rem always the developer to easily create responsive websites because the sizings will be automatically adjusted to the font size

# How CSS renders a website

"Algorithm that calculates boxes and determines the layout of these boxes, for each element in the render tree, to determine the final layout of the page"

- Dimensions of the boxes: the box model
- Box type: inline, block and inline-block
- Position scheme: floats and positioning
- Stacking contexts
- Other elements in the render tree
- Viewport size, dimensions of images etc

## The box model

- Each and every element on the webpage can be seen as a box, each box can have a width, height, padding, border etc

### Normal CSS box

total width = right border + right padding, specified width + left padding + left border

total height = top border + top padding + specified height + bottom padding + bottom border

### Box Sizing: border-box

Using border-box allows us to only get the width/height of our box by the specified dimensions, the padding/borders will take away from the inner sizing of the box

total width = specified width
total height = specified height

## Box types

### Block-level-boxes

- Elements formatted visually as blocks
- 100% of parents width
- Vertically, one after another

```
display: block
(display: flex)
(display: list-item)
(display: table)
```

### Inline-block boxes

- A mix of block and inline
- Occupies only contents space
- No line-breaks
- Box-model applies as showed

```
display: inline-block
```

### Inline boxes

Essentially the opposite of a block-level-box

- Content is distributed in lines
- Occupies only contents space
- No line-breaks
- No heights / widths
- Padding and margins only horizontal (left and right)

```
display: inline
```

## Positioning Schemes

### Normal flow

- Default positioning scheme
- Not floated
- Not absolutely positioned
- Elements laid out according to their source order

```
Default
position: relative
```

### Floats

- Element is removed from the normal flow
- Text and inline elements will wrap around the floated element
- The container will not adjust its height to the element

```
float: left
float: right
```

### Absolute positioning

- Element is removed from the normal flow
- No impact on surrounding content or elements
- We use top, bottom, left and right to offset the element from it's relative positioned container

```
position: absolute
position: fixed
```

# Components and BEM

We want code that is

- Clean, Modular, Reusable, and Ready for growth

Think => Build => Architect

### Think

Component-driven-design

- modular components that make up interfaces
- held together by the layout of the page
- reusable across a project and different projects
- independent allowing us to use them anywhere on the page

### Build

BEM

- Block element modifier

```
.block {}
.block__element {}
.block__element--modifier {}
```

- BLOCK: standalone component that is meaningful on it's own
- ELEMENT: part of a block that has no standalone meaning
- MODIFIER: a different version of a block or element

[Example code block on udemy tut]

### Architect

The 7-1 pattern

- 7 different folders for partial SaSS files
- 1 main SaSS file to import all other files into a compiled CSS stylesheet

#### The 7 folders

1. base/
2. components/
3. layout/
4. pages/
5. themes/
6. abstracts/
7. vendors/

# What is SaSS ?

SaSS is a CSS preprocessor an extension of CSS - we use it to fix the problems that CSS creates

SaSS needs to be compiled

SaSS Source Code => SaSS Compiler => Compiled SaSS Code (Regular CSS Code)

## What does SaSS give us?

- Variables: for reusable values such a colours, font sizes, spacing etc
- Nesting: to nest selectors inside of another, allowing us to write less code
- Operators: for mathematical operations right inside of CSS
- Partials and imports: to write CSS in different files and importing them all into a single file
- Mixins: to write reusable pieces of CSS code
- Functions: similar to mixins, with the difference that they produce a value that can be used
- Extends: to make different selectors inherit declarations that are common to all of them
- Control directives: for writing complex code using conditionals and loops (Not covered in this course, often used for writing CSS frameworks)

## Syntax

#### SaSS

```
.navigation {
  list-style: none
  float: left

  & li
  display: inline-block
  margin-left: 30px
}
```

#### SCSS syntax

```
.navigation {
  list-style: none;
  float: left;

  & li {
    display: inline-block;
    margin-left: 30px;
  }
}
```

# Responsive design

1. Fluid grids and layouts

- Allows content to easily adapt to the current viewport width to browse the website uses % rather than px for all layout related lengths.

2. Flexible and responsive images

- Images behave differently to text content so we need to ensure they adapt nicely to the current viewport.

3. Media Queries

- To change styles on certain viewport widths (Known as breakpoints), allowing us to create a different version of the website for different widths.

## Fluid grids and layouts

There are 3 major ways to layout our application

1. Float layouts
2. Flexbox
3. CSS Grid

# Responsive Design

## Desktop v Mobile

### Desktop

Traditionally design for desktop first, and then write media queries of max width for mobile

```
@media (max-width: 600px)
```

### Mobile

Start writing CSS for small screens, and then the media queries expand to a large desktop screen, this is becoming the new norm.

```
@media (min-width: 600px)
```

When designing for mobile we really need to keep in mind what we NEED to display to create an efficient and fast design

### Desktop

- 0px
- 600px ( - Example: max-width 600px all the css that was written would be applied to ALL screens from 0-600px)
- 900px
- 1200px

When using max-width media queries, if the screen was 500px, and we had a max-with of 600px and 900px both would apply, conflicting css rules will often occur the the one that appears LAST in the code takes precedence, this is because media queries do not add any importance of specificity to selectors so only the order of the code matters. (This is why media queries ALWAYS come last).

In this example anything above 1200px would be 'desktop first' / our initial css design

### Mobile

- 0px
- 600px ( - Example: min-width 600px, if the current viewport with is more than 600px then the css applies)
- 900px
- 1200px

We use min-width approach when designing for mobile first because we want the media queries to stay away from our small screen styles. This is why the max-width media queries would not work.
As we go up to 900px and 1200px view port sizes, the same logic applies designing for each view port.

## Pro's Con's of Mobile First

No matter what you decided always keep desktop and mobile in mind

### Pro's

- 100% optimized for the mobile experience
- Reducers websites and apps to the essentials
- Results in smaller, faster and more efficient products
- Prioritizes content over aesthetic design which may be desirable.

### Con's

- The desktop version might feel overly empty and simplistic
- More difficult and counterintuitive to develop
- Less creative freedom making it more difficult to create distinctive products
- Clients are used to seeing a desktop version of the site as a prototype
- Do your users even use the mobile internet.. consider the purpose of your website

## Breakpoints

### Bad

- Using the width of popular products <br/>
  This is not good because you're designing for specific products, what if apple decides to change their screen size or resolution? - Your app won't function as intended

### Good

- Get all the most used device widths, group them together and create breakpoints around these. <br/>
  This is much better than the first one because you aren't designing with a single device in mind but many.

### Perfect

Begin at a size desktop or mobile, then start increasing/decreasing your view port size, each time the app breaks, add a media q. This is the most difficult, but the most ideal.

## Chosing your breakpoints: "Good" design method

`www.gs.statcounter.com` - Use this site to find the average of most used screen resolutions to make some up to date decisiomns about where your break points might be.

Usually we will need the following <br/>

1. Phone (0-600) [iPhone 8]
2. Tablet portrait (600-900) [iPad portrait]
3. Tablet landscape (900-1200) [iPad landscape]
4. Desktop (1200-1800) [MacBook pro 15"]
5. Big desktop (1800+) []
