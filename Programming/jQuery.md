# jQuery

Query is a JavaScript Library.

jQuery greatly simplifies JavaScript programming.

jQuery takes a lot of common tasks that require many lines of JavaScript code to accomplish, and wraps them into methods that you can call with a single line of code.

### Getting Started

There are two versions of jQuery available for downloading: 

- Production version - this is for your live website because it has been minified and compressed
- Development version - this is for testing and development (uncompressed and readable code)

Both versions can be downloaded from [jQuery.com](http://jquery.com/download/).

### Syntax

```javascript
$(selector).action()
```

### The Document Ready Event

It is good practice to wait for the document to be fully loaded and ready before working with it. This also allows you to have your JavaScript code before the body of your document, in the head section.

```javascript
//This is to prevent any jQuery code from running before the document is finished loading (is ready). 
$(document).ready(function(){

  // jQuery methods go here...

}); 

//The jQuery team has also created an even shorter method for the document ready event
$(function(){

  // jQuery methods go here...

}); 
```

| Syntax                   | Descriptions                                                 |      |
| ------------------------ | ------------------------------------------------------------ | ---- |
| $("*")                   | Selects all elements                                         |      |
| $(this)                  | Selects the current HTML element                             |      |
| $("p.intro")             | Selects all <p> elements with class="intro"                  |      |
| $("p:first")             | Selects the first <p> element                                |      |
| $("ul li:first")         | Selects the first <li> element of the first <ul>             |      |
| $("ul li:first-child")   | Selects the first <li> element of every <ul>                 |      |
| $("[href]")              | Selects all elements with an href attribute                  |      |
| $("a[target='_blank']")  | Selects all <a> elements with a target attribute value equal to "_blank" |      |
| $("a[target!='_blank']") | Selects all <a> elements with a target attribute value NOT equal to "_blank" |      |
| $(":button")             | Selects all <button> elements and <input> elements of type="button" |      |
| $("tr:even")             | Selects all even <tr> elements                               |      |
| $("tr:odd")              | Selects all odd <tr> elements                                |      |

### jQuery Syntax For Event Methods

```javascript
//To assign a click event to all paragraphs on a page, you can do this
$("p").click(); 

//The next step is to define what should happen when the event fires. You must pass a function to the event:
$("p").click(function(){
  // action goes here!!
}); 

```

### Reference

[w3school](https://www.w3schools.com/jquery/default.asp)

