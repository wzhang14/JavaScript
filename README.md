JavaScript
1. check if a number is an integer.
2. write a function to do this: multiply(5)(6)
3. when to use bind function
when to use bind function 2
4. when to use “use strict”
5. different between == and ===
6. callback function
7. 0.1 + 0.2 === 0.3
8. access private variable
9. empty an array
10. self invoking function
11. hide JavaScript code from older browser
12. hoisting
11. check if bar is an object
12. check if a string is a palindrome
13. a method works with both sum(2,3) and sum(2)(3)
14. correct the code (use of closure in loop)
correct the code 2
15. a recursive code without the stack overflow problem
16. calculate 10!
17. visit all elements in a tree(DOM)
18. clone an object
19. add an element at the beginning / end of an array
19. calculate the length of an associative array (object)

jQuery
1. query
2. define a click handler for all buttons, including those added later dynamically
3. $ an alias for the jQuery object and jQuery() function
4. animate the div over 3 seconds
5. method chaining
6. event.preventDefault() & event.stopPropagation()
7. .promise()

HTML
Inline level elements / block level elements:
entity: 

CSS
position: 
display: 
@media
flexbox 
justify-content
variables:
@keyframes
transition
grid

SASS
$primary-color: #fff;
& parent 
inheritance:
%
@extend %btn-shared;
_variables.scss: partial
@import ‘variables’;
@import ‘fuctions’;
_functions.scss:   
@function 
@mixin
@include 

PHP
1. upload file
2. multiple inheritance: interface

=================


JavaScript

1. check if a number is an integer.

ES6: Number.isInteger()

ES5:
function isInt(num) {
    return num % 1 === 0;  //   return Math.round(num) === x;  
}

console.log(isInt(4));
console.log(isInt(12.3));


2. write a function to do this: multiply(5)(6)

function multiply(a) {
    return function(b) {   // a closure, can access variables in the outer function
        return a * b;
    }
}

multiply(5)(6);


3. when to use bind function

when you pass a specific object to a function that uses a this reference.

function myName() {
    return “My name is “ + this.name;
}
var person = { name: “Wei” };
console.log( myName.bind(person)() );

when to use bind function 2

var hero = {
    name: ‘Wei Zhang’,
    getId: function () {
        return this.name;
    }
};

var stoleId = hero.getId;   // should change to = hero.getId.bind(hero);

console.log(stoleId());
console.log(hero.getId());


4. when to use “use strict”

throw an error if global variable is created by mistake.

function addTen(val) {
    “use strict”
    x = val + 10;
}  // will throw an error because x was not defined and it’s being set to some value in the global scope. Should change to var x = val + 10.


5. different between == and ===

== performs implicit type conversion to check if values are equal. 
“1” == 1 // true
true == 1 // true
[] == false // true
“” == false // true
undefined == null // true

=== check both type and values.


6. callback function

a function that is passed to another function as an argument, and is executed after some operation has been completed.

function updateArray( arr, callback ) {
    arr.push(100);
    callback();
}

var arr = [1, 2, 3, 4, 5];

updateArray( arr, function() {
    console.log(“Array updated“, arr );
});


7. 0.1 + 0.2 === 0.3

output false.  Floating point errors in internally representing certain numbers. 


8. access private variable

by a helper function

function func() {
    var priv = “private variable”;
}

console.log(priv); // throws error

function func() {
    var priv = “private variable”;
    return function() {
        return priv;
    }
}

var getPriv = func();
console.log(getPrive());  // private variable


9. empty an array

clear the array and update all reference variables that point to this array

arr.length = 0;


10. self invoking function

( function () {
    return ();
} () );


11. hide JavaScript code from older browser

<script>
<!--
 …
// -- >
</script>


12. hoisting

num = 100;
elem=document.getElementById(“xxx”);
elem.innerHTML = “num= “ + num;
var num;


11. check if bar is an object

console.log( ( bar !== null ) && ( typeof bar === “object” ) );  // null is an object



12. check if a string is a palindrome

function isPalindrome(str) {
    str = str.replace( / \W /g, ‘ ’ ).toLowerCase();
    return ( str == str.split( ‘ ’ ).reverse().join( ‘ ’ ) );
}

console.log( isPalindrom(“ A car, a man, a maraca” ));


13. a method works with both sum(2,3) and sum(2)(3)

function sum(x, y) {
    if (y !== undefined ) {
        return x + y;
    } else {
        return function(y) {
            return x + y;
        }
    }
}


14. correct the code (use of closure in loop)

for ( var i = 0; i < 5; i ++ ) {
    var btn = document.createElement(‘button’);
    btn.appendChild( document.createTextNode(‘Button ‘ + i ) );
    btn.addEventListener( ‘click’, function() { console.log(i); });
    document.body.appendChild(btn);
}

ES6:
for ( let i = 0; i < 5; i ++ ) {
    var btn = document.createElement(‘button’);
    btn.appendChild( document.createTextNode(‘Button ‘ + i ) );
    btn.addEventListener( ‘click’, function() { console.log(i); });
    document.body.appendChild(btn);
}

ES5:
for ( var i = 0; i < 5; i ++ ) {
    var btn = document.createElement(‘button’);
    btn.appendChild( document.createTextNode(‘Button ‘ + i ) );
    btn.addEventListener( ‘click’, function(i) { 
         return function() { console.log(i); };
    })(i) );
    document.body.appendChild(btn);
}

correct the code 2

for ( var i = 0; i < 5; i ++ ) {
    setTimeout( function() { console.log(i); } , i*1000 );
}

ES5
for ( var i = 0; i < 5; i ++ ) {
    ( function(x) {
        setTimeout( function() { console.log(x); } , x*1000 );
     })(i);
}


15. a recursive code without the stack overflow problem

var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();
    if(item) {
        setTimeout( nextListItem, 0 );  // the event loop handles the recursion, not the call stack.
   }
};


16. calculate 10!

console.log( (function f(n) { return ( (n>1) ? n*f(n-1) : n ) } ) (10) );


17. visit all elements in a tree(DOM)

function Traverse( p_element, p_callback ) {
    p_callback( p_element );
    var list = p_element.children;
    for ( var i =0; i < list.length; i ++ ) {
        Traverse( list[ i ], p_callback );
    }
}


18. clone an object

var obj = { a: 1, b: 2 }
var objClone = Object.assign( {}, obj );

Object.clone(): shallow copy, not deep copy, nested objects aren’t copied. 
  

19. add an element at the beginning / end of an array

ES5
var myArray = [ ‘a’, ‘b’, ‘c’ ];
myArray.push(‘end’);
myArray.uhshift(‘start’);

ES6: spread operator
myArray = [ ‘start, ...myArray, ‘end’ ];


19. calculate the length of an associative array (object)

var myArray = { 
   A : 3;
   B : 4;
};
myArray[ “C” ] = 1;

Object.keys(myArray).length;
=========================
function getLength(object) {
    var count = 0;
    for ( key in object ) {
        if ( object.hasOwnProperty(key) ) count++;
    }
    return count;
}



jQuery

1. query
$( “ div#first, div.first, ol#items > [ name$=’first’ ] ” )   // name ends with first
$( “ [ id$=’txt’ ] ” )   // query all elements with an id ends with ‘txt’
$( “ div [ id$=’txt’ ] ” )  // query div elements with an id ends with ‘txt


2. define a click handler for all buttons, including those added later dynamically

// define the click handler for all buttons
$( document ).on( “click”, “button”, function() {
    alert( “Button Clicked” )
});

// dynamically add another button to the page
$( “html” ).append( “<button>Click Here</button>” );


3. $ an alias for the jQuery object and jQuery() function.


4. animate the div over 3 seconds

html
<div id=”expander”></div>

css
div#expander {
    width: 100px;
    height: 100px;
    background-color: blue;
}

jquery
$( “#expander” ).animate(
    { 
      width: “200px”,
      height: “200px”,
    },
    3000 );


5. method chaining

$( “button#play-movie” ).on( “click”, playMovie )
                                     .css( “background-color”, “orange” )
                                     .show();

$( “div” ).css( “width”, “300px” ).add( “p” ).css( “background-color”, “blue” );


6. event.preventDefault() & event.stopPropagation()

event.preventDefault(): prevent the browser’s default action
event.stopPropagation(): stop an event from bubbling up the event chaining

$( “#foo” ).click( function() {
    …
});

$( “#bar” ).click( function(e) {
    …
    e.stopPropagation();
});


7. .promise()

function getMinsSecs() {
    var dt = new Date();
    return dt.getMinutes() + “:” + dt.getSeconds();
}

$( “ input ” ).on( “click”, function() {
    $( “p” ).append( “Start time: “ + getMinsSecs() + “<br/>” );
    $( “div” ).each( function( i ) {
       $( this ).fadeOut( 1000*( i*2 ) );
    });
    $( “div” ).promise().done( function() {
        $( “p” ).append( “End time: “ + getMinsSecs() + “<br/>” );
    });
});


HTML

Hypertext Markup Language, for creating webpages, display content (text, image.. )

<form>
action=”where the form will be submitted to, like a PHP file, process.php”

<select> <option>
<input type=”radio”> <input type=”checkbox”>
<input type=”submit” value=”Submit”>
<button type=”submit”>Submit</button>

Inline level elements / block level elements:

block: span 100% width of the page

inline:  a, button, span...

entity: 
non breaking space &nbsp; 
copyright &copy;

CSS

cascading style sheets, styling language.

background:  url(‘’) no-repeat center center/cover;
height: 100vh;
background-attachment: fixed;

.container {
    max-width: 960px; //responsive
    margin: 30px auto;
}

.navbar li {
    display: inline;  
}

.navbar li a {
    padding: 10px;
}

img {
    display: block;
    margin: auto;  // only works with block elements
}

position: 
static: not effected by tblr.
relative: effected by tblr.
absolute: relative to its parent element(relative)
fixed: relative to the viewport
sticky: based on scroll position  // for navbar, position: sticky; top: 0;

display: none;
visibility: hidden;

@media(max-width: 500px) {   // for smart phones
@media(min-witdh: 501px) and (max-width: 768px) {   // for tablet
@media(min-witdh: 769px) and (max-width: 1200px) {   // for normal screen
@media(min-witdh: 1201px) {   // for wide screen

<link rel=”stylesheet” media=”screen and (max-width: 768px)” href=”mobile.css”>

flexbox (CSS3): align things easily without using float

parent {
    display: flex;
    flex-direction: row / column;
}

child {
    flex: 1;  // all child equal width
}

child1 {
    flex: 2;
}
child2 {
    flex:1;
}

justify-content: center / around;   // horizontal
height: 600px;    align-items: center / flex-start / flex-end;   // vertical
align-content: center / flex-start;  // vertical when have extra space

#navbar {
    display: flex;
    position: sticky;
    top: 0;
    justify-content: space-between;
    z-index: 1;
}
#navbar ul {
    display: flex;
    align-items: center;
}

variables:
:root {
    --primary-color: #fff;
}

color: var(--primary-color);

@keyframes animate1 {
    to {
        color: red;

transition: background 2s ease-in-out;

transform: rotate(25deg);
transition: all 1s ease-in-out;




grid:
parent {
    display: grid;
    grid-template-columns / rows: 1fr 2fr 1fr;
    grid-gap: 1rem;
}
child:nth-child(9) {
    grid-column: 2 / span 3;
    grid-row: 4 / span 2;
}

grid-template-areas:
grid-area:


SASS (Syntactically Awesome StyleSheets)

CSS precompiler.     .scss
Variables, nesting, imports, funcitons/ mixins, conditionals, inheritance, operators, color functions…

npm install node-sass
scripts:
    sass: node-sass -w scss/ -o dist/css/ --recursive
npm run sass

$primary-color: #fff;

& parent 

inheritance:
%btn-shared { … }
.btn-light {
    @extend %btn-shared;
}

_variables.scss: partial
@import ‘variables’;
@import ‘fuctions’;

_functions.scss:   
@function set-text-color($color) {
    @if ( lightness($color) > 50 ) {
        @return #000;
    } @else {
        @return #fff;
    }
}

color: set-text-color($dark-color);

@mixin transform($property) {
    transform: $property;
}

@include transform( rotate(20deg) );


PHP

1. upload file

1) php.ini:
    file_uploads = On

2)html:
    <form action=”upload.php” method=”post” enctype=”multipart/form-data”>
    <input type=”file” name=”upd” id=”upd”>
    <input type=”submit” value=”Upload” name=”upload”>
    </form>

3)upload.php:
    if ( move_uploaded_file ( $_FILES[“upd”][“tmp_name”], “Uploads/” ) ) {
        echo “The file “. basename( $_FILES[“upd”][“name’] ). “ is uploaded.”;
    } else {
        echo “ There is an error in uploading.”;
    }


