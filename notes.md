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
