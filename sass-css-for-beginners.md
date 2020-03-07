## What is Sass?
Sass stands for Syntactically Awesome Style Sheets. From the name alone, we can infer SASS is an awesome way of writing css. 
In more technical terms, it's a preprocessor scripting language that is compiled into CSS (wiki). Basically, an extension to css.

### Why the need?

SASS was created to bring the basic programming concepts like separation of concerns, the use of variables, nesting, functions etc into CSS, what then happen is that after the css is written in sass format, a sass live compiler is then used to compile the sass code into plain css which the browser then understands.

## SASS Syntax
**SASS has two syntaxes**
* .scss
* .sass

The major difference between the `.scss` and `.sass` is that when nesting, `.scss` uses the curly brackets and semicolon, meanwhile the `.sass` uses indentation to specify blocks of codes.

**For example**
```CSS 
/* .scss */
.main {
   font-size: 2rem;
   text-align: center;

   &_content {
       font-size: 1rem;
       text-align: right;
   }
}
```

```CSS
/* .sass */
.main 
   font-size: 2rem
   text-align: center

   &_content
       font-size: 1rem
       text-align: right
```   

_At this point, i know you be like hollop hollop, what's going on here..What's with the ampersand sign and the nesting of selectors? We'll get right to it in the next few lines. :)_ 
_**Also note, for the purpose of this tutorial we'll be using the .scss syntax.**_


## Installation/Requirements

To get started using sass, for node.js, you can install using `npm install -g sass`.

For vs code, you can install the Sass live compiler extension, 
![live sass compiler extension] (https://drive.google.com/open?id=12guWXeQwcnWebYaYocDY2gKsH9rz70JR)

then, click "watch sass" to compile sass code to watch and compile code to css.

![watch css] (https://drive.google.com/open?id=1Vt6hjfaLpmKhxxRs0hQD1PdjyAAp3k8M)

![watching css] (https://drive.google.com/open?id=1Km0NRfkxwrWDSskhf9WpFssOvrxbrOFJ)


## SASS Simple Basic Concepts
### Variables
Variables are used to store information you would like to use throughout the stylesheets. for example, font primary color, text secondary color, background color, header font size etc. 

**For example**
```CSS
/* SASS */
$primary-font: 'Segoe UI', Tahoma, 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
$primary-color: #272727;
$secondary-color: #ff642f;

body {
  font:  $primary-font;
  color: $primary-color;
  h1: $secondary-color;
}
```

```CSS
/* css */
body {
  font: 'Segoe UI', Tahoma, 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #272727;
  h1: #ff642f;
}
```

_When the sass file is saved and compiled, the values of the variables are placed in the CSS property._


### Nesting
Sass provides a means for our css to follow an orderly visual hierarchy. It allows selectors to be nested within eachother to provide a flow when writing css.
**For example**

```HTML
/* HTML */
<section class="main-section"> 
    <div class="social-icons">
        <a href="#!">
            <i class="fab fa-twitter fa-2x"></i>
        </a>
        <a href="#!">
            <i class="fab fa-facebook fa-2x"></i>
        </a>
    </div>
</section>
```

```CSS
/* sass */
.main-section{
    height: 100%;
    width: 100%;

    .social-icons {
        position: fixed;
        bottom: 1rem;
        left: 1rem;

        a {
            padding: 0.4rem;

            &:hover {
                color:$secondary-color;
            }
        }
    }
}
```
```CSS
/* css */
.main-section {
    height: 100%;
    width: 100%;
}
.main-section .social-icons {
    position: fixed;
    bottom: 1rem;
    left: 1rem;
}
.main-section .social-icons a {
    padding: 0.4rem
}
.main-section .social-icons a:hover {
    color:$secondary-color;
}
```
_You'll notice sass helps to keep the selectors organized and to avoid repetition. Also, the ampersand (*&*) was introduced. It is used to represent the parent selector._

**For example**
```CSS
/* sass */
.social-icons a { 
/* some anchor code css*/ 

    &:hover {
        /*hover property*/
    }  
}
```
```CSS
/* css */
.social-icons a:hover {
     /* hover property */ 
}
```

## Partials
Partial is a sass file named with a leading underscore. The underscore lets the compiler know it's only a partial. This helps to maintain separation of concerns in the css code.

**For example**
```CSS
/* sass _variables.scss file*/
$primary-font: 'Segoe UI', Tahoma, 'Segoe UI', Tahoma, 

Geneva, Verdana, sans-serif;
$primary-color: #272727;
$secondary-color: #ff642f;
```
```CSS
/* sass _resets.scss file */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0; 
}
```
```Scss
/* sass main.scss file */
@import './resets'
@import './variables'

body {
  font:  $font-stack;
  color: $primary-color;
  h1: $secondary-color;
}
```

_In main.css, the _resets.scss and _variables.scss sass files were imported inorder for it to be accessible._

```CSS
/* CSS main.css file */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0; 
}

body {
  font:  'Segoe UI', Tahoma, 'Segoe UI', Tahoma, Geneva, 

Verdana, sans-serif;
  color:  #272727;
  h1: #ff642f;
}
```

_In the equivalent main.css, the partial files are compiled into it. Partials helps to maintain separation of concerns and reduce the bulky main.css file when working on large projects._

### Functions
In programming generally, Function basically is a block of code that does something specific. It can accept an arguement, and do something specific with it. Functions in sass are blocks of code that return a single value of any sass data type. There are two essential directives for creating sass functions; @function for creating the function, and @return for signalling value to be returned when function is called. There are other function derivative in sass eg @percentage, @lightness etc.. you can look up the doc at ![sass-lang](sass-lang.com) for more.

**For example**
```CSS
/* sass */
@function set-col-width($col, $totalColSize){
    @return percentage($col/$totalColSize);
}

.box1 {
    width: set-col-width(2, 5);
}
.box2 {
    width: set-col-width(4, 5);
}
```
```CSS
/* css */
.box1 {
    width: 40;
}
.box2 {
    width: 80;
}
```

### Mixins
Mixins are function like declaration used to group css code that'll be used throughout the site. It also allow the passing of values.

**For example**
```CSS
/* sass file */
@mixin transition-ease {
    transition: all 0.5s ease-in-out;
}

@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box { 
   @include transform(rotate(30deg)); 
   @include transition-ease;
   width: 50px;
   height: 100px;
}
.box2 {
   @include transform(rotate(60deg)); 
   @include transition-ease;
   width: 50px;
   height: 100px;
}
```
_The @include is used to import the mixin css properties into the .box code block._

```css
/* css file */
.box {
    -webkit-transform: 30;
    -ms-transform: 30;
    transform: 30;
    transition: all 0.5s ease-in-out;
}

.box2 {
    -webkit-transform: 60;
    -ms-transform: 60;
    transform: 60;
    transition: all 0.5s ease-in-out;
}
```

### Operators
Sometimes, we can't help but have the need to calculate some values in css. Sass helps take away the stress of having to use calculator while coding as it has the capability to do basic mathematical operations on values.

**For example**
```css
/* sass */
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```
```css
/* css */
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 62.5%;
}

aside[role="complementary"] {
  float: right;
  width: 31.25%;
}
```

## Final Notes
To know more about the sass concept, you can study bootstrap file. Sass styling was used for the project.
 

This is my first article on dev.to, I hope it's helpful to you. 
Don't forget to Like, and drop comments too.

_Next up - Setting up Redux for React app. Watch this space. :)_