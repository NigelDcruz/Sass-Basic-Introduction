#Introduction to SASS basics
Sass lets you use features that don't exist in CSS. Example- variables, nesting, mixins, inheritance etc. CSS on its own can be fun, but stylesheets are getting larger, more complex, and harder to maintain. This is where a preprocessor like SASS can help.

## Variables
 - Variables as a way to store information that you can reuse over and over throughout the stylesheet.
 - You can store things like colors, font stacks, or any CSS value you think you'll want to reuse.
 - The way we create a variable in SASS is by prefixing the name with **$**. Example- **$NameOfTheVariable**:**value**;
 
 Here's an SCSS example:
 ```
 
$font-variable: arial, sans-serif;
$primary-color: #333;

body {
  font: $font-variable;
  color: $primary-color;
}
 
 ```
This is what the compiled version looks like in plain CSS:
```
body {
  font: arial, sans-serif;
  color: #333;
}
```

