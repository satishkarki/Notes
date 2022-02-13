# Notebook

Here I wrote about the things that I learned during the web development boot camp

 [Web Archive](https://web.archive.org/). This site stores all the web pages over time.

## HTML

* VS Code Extension for HTML Boilerplate 
  * Launch VS Code Quick Open (Ctrl+P)
  * Type ``` ext install sidthesloth.html5-boilerplate```
  * Type 'html5-boilerplate' in an HTML file and select the snippet from the auto suggestion drop down to get the HTML boilerplate.

* DOCTYPE html : This tag tells the browser to render the file as a HTML5 document

* Emmet: With Emmet we can rapidly create our markup. It expands the simple abbreviations into complex HTML and CSS code snippets.
* Meta Tag: Description about the website used by the search engine
* <em> vs <i>, Bold vs Strong, Emphasis Vs. Strong
*  Anchor Element <a>
* Table Element <table>
* HTML Form <form>

## CSS 

- Beautiful color to choose from [colorhunt.co](https://colorhunt.co/)

- style

- [Browser Default CSS](https://www.w3schools.com/cssref/css_default_values.asp)

- CSS Rule hierarchy: Inline>Internal>External

- CSS Syntax

- ``` css
  selector {property:value}
  who {what:How}
  ```

- Comment in CSS: 

  ```css
  /* Your Comment */
  ```

- Use the browser's developer tool to debug CSS errors.

- CSS Selectors: Selecting class(it is an attribute) or tag according to your need or a unique ID

  ```css
  .class{
  property: value
  }
  
  tag{
  property:value
  }
  #ID{
  property:value
  }
  Example: You want to have a particular background of an image but not all images, in this case you choose class attribute, instead of "img" tag
  ```

- Difference between Id and Class

  - We cannot have same ID for different tags, it must be unique where as class can be used with different tags (it can be used to group different tags)
  - Same HTML element can have multiple class but only one ID
  - Pseudo Classes....example : hover

  

## Building a Website

- Color Picker: https://colorhunt.co/

- favicon generator: https://www.favicon.cc/
- free vector images: https://www.flaticon.com/
- giphy animations: https://giphy.com/search/computer

- [Pesticide](https://addons.mozilla.org/en-CA/firefox/addon/pesticide-css-for-firefox/): This extension inserts the Pesticide CSS into the current page, outlining each element to better see placement on the page. 

- HTML div: A block to put different things together to customise

- HTML Box Model: Try using the box model of web developer tool. It will save a lot of time debugging.

- CSS Display Property 

  - span: <span> inline display element

  - Images: <img> inline-block element

  - anchors: <a> inline

  - When to use block element and span element 

    ```css
    p{
    	display:inline;
    }
    span{
    	display:block;
    }
    p{
    	display:inline-block;
    }
    p{
    	display:none
    	visibility:none;
    }
    
    ```

- CSS Positioning

  - Content is everything

  - Order comes from code

  - Children Sit On top of Parents: Introduces the Z-indexes

  - Position

    - Static
    - Relative: relative in the sense that where the natural flow of static HTML would be
      - Coordinates: top, right, bottom, left

    - Absolute: Relative position compared to the parent  element
    - Fixed 

- The Dark art of centring the element

  ```css
  body{
  	text-align:center;
  }
  h1{
  	width: 10px;
  	margin: auto;
  }
  ```

  

- [CSS Web Safe Fonts](https://www.w3schools.com/css/css_font_websafe.asp)

  - Font Fallback

  - [Google Fonts](https://fonts.google.com/)

    ```html
     <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Comic+Neue&family=Montserrat&family=Sacramento&display=swap" rel="stylesheet"> 
    ```

    CSS Rule to specific family

    ```css
        font-family: 'Comic Neue', cursive;
    
            font-family: 'Montserrat', sans-serif;
    
        font-family: 'Sacramento', cursive;
    ```

    https://media.giphy.com/media/077i6AULCXc0FKTj9s/giphy.gif

    https://media.giphy.com/media/3oKIPEqDGUULpEU0aQ/giphy.gif

- Font Size
  - 1em=16px=100%
  - 1 em is the width of letter "M"
  - One thing to note is that, if we are using px or em in the parent block and we specify the em in the child block then, the value will be added to the child block. Example: If I set body text size to be 200 % i.e. 2 em and then I specify 2,5 em for h1 tag, the actual size of h1 will be 4.5 em.
  - So it is better to use rem instead of em, it ignores the root em value
  - Line height
  - Font weight
  - Margin
  - Clear
  - height: 5px;
    border: 0;
    box-shadow: 0 10px 10px -10px #8c8b8b inset;
- [CSS Button Creator](https://cssbuttoncreator.com/)
- Z-Index [1,0,-1]
- Media Query Break Point
- Combining CSS Selectors
  - Hierarchical Selector
  - Multiple Selector

- Advanced CSS Selector
- Code Refactor DRY: Don't Repeat Your Self, WET: We Love Typing
  - Readability
  - Modularity
  - Efficiency
  - Length
  - Challenge: Code Gulf

# Bootstrap 4

- Bootstrap is used to create mobile first responsive web page

- We can use bootstrap either from the CDN  or we can download it from [getbootstarp](https://getbootstrap.com/)

- Using bootstrap from CDN would have faster loading time compared to downloading it and hosting it yourself

  

  ```html
   <!-- Latest compiled and minified CSS -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
  
  <!-- jQuery library -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  
  <!-- Popper JS -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
  
  <!-- Latest compiled JavaScript -->
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script> 
  
  ```

- Easiest way to start working with the bootstrap is with the starter template. I am using  v4.6, right now we have a new version v5.0 which has a different starter template.

  ```html
  <!doctype html>
  <html lang="en">
    <head>
      <!-- Required meta tags -->
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  
      <!-- Bootstrap CSS -->
      <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">
  
      <title>Hello, world!</title>
    </head>
    <body>
      <h1>Hello, world!</h1>
  
      <!-- Optional JavaScript; choose one of the two! -->
  
      <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
      <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
      <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-Piv4xVNRyMGpqkS2by6br4gNJ7DXjqk09RmUpJ8jgGtD7zP9yug3goQfGII0yAns" crossorigin="anonymous"></script>
  
      <!-- Option 2: Separate Popper and Bootstrap JS -->
      <!--
      <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
      <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
      <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.min.js" integrity="sha384-+YQ4JLhjyBLPDQt//I+STsc9iw4uQqACwlvpslubQzn4u2UU2UFM80nGisd026JF" crossorigin="anonymous"></script>
      -->
    </body>
  </html>
  
  
  ```

  

- This tags should be included in the header section of html file, if you plan to use it from CDN

- **Containers**: 

  - .container : fixed width container
  - .container-fluid: full width container

- Wireframing: low fidelity, mock up, looking at other peoples design pattern, prototype 

  - For my website, I love this awesome website https://chirpy.cotes.info/, I will try to clone it.

- Bootstrap Navigation Bar

- Grid Layout

-  bootsnip

- Mobile friendly test

  

# Building a Good Website

- Understanding the Colour Theory
  - Mood
  - Combining Colour
    - Analogous Colour
  - Adobe Color Pallet
- Understanding Typography and Font
  - Fonts Matter
  - Learn more about the Serif, San-serif, 
  - Be ware of the similarity and the contrast between type form
- User Interface
  - Hierarchy
  - Layout
  - Characters per line
  - Alignment
  - White space
  - Audience
- UX Design [user experience]
  - Simplicity
  - Consistency
  - Reading Pattern
    - F layout
    - Z pattern
  - All Platform Design
  - Don't use your power to do evil