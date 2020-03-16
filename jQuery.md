# <center>jQuery Emphasis <font size=3px color="ffeedd">&nbsp; Recorded by Shine.Lee</font> </center>


## jQuery Syntax

` $(selector).action() `
* A `$` sign to define/access jQuery
* A (selector) to "query (or find)" HTML elements
* A jQuery action() to be performed on the element(s)

Examples:

* ` $(this).hide() ` - hides the current element.

* ` $("p").hide() ` - hides all ` <p> ` elements.

* ` $(".test").hide() ` - hides all elements with class="test".

* ` $("#test").hide() ` - hides the element with id="test".

---

## The Document Ready Event
``` JavaScript
$(document).ready(function(){

  // jQuery methods go here...

});
```
> This is to prevent any jQuery code from running before the document is finished loading (is ready).

> <b>Tip:</b> even shorter method for the document ready event:
``` JavaScript
$(function(){

  // jQuery methods go here...

});
```

|Syntax|Description|
|---|---|
|$("*")|Selects all elements|
|$(this)|Selects the current HTML element|
|$("p.intro")|Selects all `<p>` elements with class="intro"|
|$("p:first")|Selects the first ` <p> ` element
|$("ul li:first-child")|Selects the first `<li>` element of the first `<ul>`
|$("[href]")|Selects all elements with an href attribute
|$("a[target='_blank']")|Selects all ` <a>`  elements with a target attribute value equal to "_blank"
|$("a[target!='_blank']")|Selects all ` <a> ` elements with a target attribute value NOT equal to "_blank"
|$(":button")|Selects all ` <button> ` elements and ` <input> ` elements of type="button"
|$("tr:even")|Selects all even ` <tr> ` elements
|$("tr:odd")|Selects all odd ` <tr> ` elements

## jQuery Event Methods

Mouse Events|Keyboard Events|Form Events|Document/Window Events|
|---|---|---|---|
click|keypress|submit|load|
dblclick|keydown|change|resize
mouseenter|keyup|focus|scroll
mouseleave| |blur|unload

## jQuery Effects - Hide and Show

Examples:

``` JavaScript
$("#hide").click(function(){
  $("p").hide();
});

$("#show").click(function(){
  $("p").show();
});
```

Syntax:
``` JavaScript
$(selector).hide(speed,callback);

$(selector).show(speed,callback);
```

## jQuery toggle()

> You can also toggle between hiding and showing an element with the toggle() method.

``` JavaScript
$("button").click(function(){
  $("p").toggle();
});
```

## jQuery Fade

* ` jQuery fadeIn() `

* ` jQuery fadeOut() `

* ` jQuery fadeToggle() `

* ` jQuery fadeTo() `

## jQuery Slide

* ` jQuery slideDown() `

* ` jQuery slideUp() `

* ` jQuery slideToggle() `

## jQuery Animations - The animate() Method

Syntax:
* ` $(selector).animate({params},speed,callback); `

* [Documentation about animate method ](https://www.w3schools.com/jquery/jquery_animate.asp)


## jQuery The stop() Method

> The jQuery ` stop() ` method is used to stop an animation or effect before it is finished.

## jQuery Callback Functions

Syntax:

* ` $(selector).hide(speed,callback); `

<b>Example with Callback:</b>

``` JavaScript
$("button").click(function(){
  $("p").hide("slow", function(){
    alert("The paragraph is now hidden");
  });
});
```
<b>Example without Callback:</b>
``` JavaScript
$("button").click(function(){
  $("p").hide(1000);
  alert("The paragraph is now hidden");
});
```
## jQuery - AJAX Introduction

* [AJAX Tutorial Link](https://www.w3schools.com/xml/ajax_intro.asp)

> AJAX = Asynchronous JavaScript and XML.

> AJAX is the art of exchanging data with a server, and updating parts of a web page - without reloading the whole page.

> With the jQuery AJAX methods, you can request text, HTML, XML, or JSON from a remote server using both HTTP Get and HTTP Post - And you can load the external data directly into the selected HTML elements of your web page!



