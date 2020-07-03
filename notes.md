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
