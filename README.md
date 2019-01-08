# Introduction to SASS basics
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

## Nesting
Suppose you have a **div** tag which has a class "main-container" and it contains an **h1** tag and a **p** tag, Example :
```
<div class="main-container">
    <h1>I'm Learning Sass</h1>
    <p>SASS is AWESOME</p>
</div>
```
If we want to target **only** the **h1** and **p** tag that has a parent class named "**main-container**" using only plain CSS, we'd have to do something like this:
```
.main-container{
	background-color: #000;
 padding: 50px 20px;
}

.main-container h1{
  color: #fff;
  font-size: 32px
 }
 
 .main-container p{
  color: #fff;
  font-size: 28px
 }
 
```
- Notice that we're repeating the "**.main-container**" class over and over again. In SASS, we can use **Nesting** to avoid repeating it over and over again.
- The SCSS version of the following is:
```
.main-container {

  background-color: #000;
  padding: 50px 20px;
  
  h1 {
   color: #fff;
   font-size: 32px
  }
  
  p {
   color: #fff;
   font-size: 28px
  }
  
}
```
- We just wrap every child element inside the parent class and SCSS takes care of the rest.
