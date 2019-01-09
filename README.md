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

## @extend

This is one of my favorite and one of the most useful features of Sass. It helps you to not repeat your code over and over again.

Now, suppose we have 3 **li** tags. All 3 **li** tags contain a social media background image. 
Here's how the code looks

```
li.facebook{
	background-image: url('../images/facebook.jpg');
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
	height: 50px;
	width: 50px;
}
li.instagram{
	background-image: url('../images/instagram.jpg');
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
	height: 50px;
	width: 50px;
}
li.twitter{
	background-image: url('../images/twitter.jpg');
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
	height: 50px;
	width: 50px;
}

```
- If you notice above, we're basically repeating code over and over again. 

Now lets use @extend to avoid code reuse:
```
.common-styles{
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
	height: 50px;
	width: 50px;
}

li.facebook{
	background-image: url('../images/facebook.jpg');
	@extend .common-styles
}
li.instagram{
	background-image: url('../images/instagram.jpg');
	@extend .common-styles
}
li.twitter{
	background-image: url('../images/twitter.jpg');
	@extend .common-styles
}
```
- As you can see, we don't need to repeat the code over and over again.
- Wherever we need common styles, we can just create and extend a class.

**NOTE: DON'T USE @extend AS SHOWN ABOVE** 
Why? 
- Because using @extend duplicates every instance of that selector. 
- It introduces specificity and inheritance problems and increases your file size.

**Instead, use placeholder selectors/silent classes** because they don't become part of your generated CSS until you extend them.

Placeholder selectors (also called silent classes) begin with a percent symbol **%**

Instead of the above example, you should use @extend the same it's used in the below example:
```
%common-styles{
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
	height: 50px;
	width: 50px;
}

li.facebook{
	background-image: url('../images/facebook.jpg');
	@extend %common-styles
}
li.instagram{
	background-image: url('../images/instagram.jpg');
	@extend %common-styles
}
li.twitter{
	background-image: url('../images/twitter.jpg');
	@extend %common-styles
}
```
- The only difference is using **%** instead of a **.** before the class name.



