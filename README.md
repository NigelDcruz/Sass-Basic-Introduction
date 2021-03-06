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

## Partials

So, when we run the compilation command in our scss folder, all our files that end with a **.scss** extension are compiled to a simple **CSS** files. 

- Imagine if we have 3 different scss files-variables.scss, mixins.scss, extends.scss.
- When we run the compilation command, each of these files will be compiled to variables.css, mixin.css, extend.css. If we have 10 such files, we'll have 10 css files for the same. This is why we have **Partials**.

A partial is simply a **Sass file that has a name starting with an underscore** eg: _variables.scss

- The underscore tells Sass that the file is a partial and that it should not be compiled to CSS.
- This partial file can then be imported into another file.

So, instead of variables.scss, mixins.scss, and extend.scss we should name them as _variables.scss, _mixins.scss, _extend.scss.

The next section will tell you how to import partials in a single file.

## @import

- Using **@import**, we can import other SASS files in our main .scss file. Using @import combined with partial files, we can avoid generating multiple css files during compilation.

In the above section, we have created _variables.scss, _mixins.scss, _extend.scss. _ _ _
To Import these files in our main.scss, we simply do the following:
``` 
@import './path/FileName'
```

**Note** that we the .scss extension was not added. This is because SASS is smart enough to figure it out. So we can omit it if we want to.

Since my files are in the same directory, I don't need to specify a path and can directly do the following: 
```
@import 'variables'
@import 'mixins'
@import 'extend'
```

That's It. The next step is to have an architecture for your project using partials and @import. There is no fixed structure that works for everyone. We must set up the architecture based on the project requirement.


## @mixin

As you advance in your career, you eventually realize that writing :
```
.box{
  transform: translateX(50%);
}
```
is **not enough**. We need to take care of cross browser compatibility. I.e, we must use vender prefixes like:
```
.box {
-webkit-transform: translateX(50%);
    -ms-transform: translateX(50%);
        transform: translateX(50%)
}
```
but prefixing everything over and over again makes the code long and repetitive.

To Solve this issue, we can use **@mixin**.

- To simplest way to understand Mixins is by thinking them as functions, just like in JavaScript.
- Basically, you create a function (@mixin), pass a **Parameter** inside that function. That's all you need to know about @mixins to get started.

**Here's how it works:**

1. Lets Create a Mixin:
```
@mixin fruit($apple) {
   -webkit-transform: $apple;
       -ms-transform: $apple;
           transform: $apple;
	}
```
2. Here fruit in the **name of the mixin** and $apple is the **parameter** that will be passed inside the function.
   Note: I'm using silly names so that you don't get confused and understand that these names can be anything.
   
```
// This is how we call the @mixin
.box {
	@include fruit(translateX(50%)); 
}

//Compiled code
.box {
-webkit-transform: translateX(50%);
    -ms-transform: translateX(50%);
        transform: translateX(50%)
}
```
3. We call the function (@mixin) by using **@include** like in the above example.
   
4. Here's a better example
  ```
  @mixin transform($property) {
  -webkit-transform: $property;
      -ms-transform: $property;
          transform: $property;
}

.box {
   @include transform(rotate(30deg)); 
  }
  
  //Compiled code
  .box {
-webkit-transform: rotate(30deg);
    -ms-transform: rotate(30deg);
        transform: rotate(30deg);
}
  ```

That's it. There are Endless possibilities of what you can do with mixins and all the basic sections mentioned above.



