# Agave.JS

A lightweight library for cleaner, simpler Javascript.

For modern browsers (Chrome, Firefox, IE9 and newer) and for node.js

 - Only adds things you use every day. See 'What does Agave provide?' below
 - Is tiny. Around 2K unminified.
 - Built for ES5:
   - Leverages ES5’s native methods
   - Doesn’t try and re-implement anything already in ES5. 
 - Is an AMD module, easily loadable by requirejs in both the browser and node.

## What does Agave provide?

### Object

#### .getKeys() 
Returns an array of the object’s keys.

#### .getSize() 
Returns the number of properties in the object.

#### .getPath([_array_,_of_,_keys_]) 
Provided an array of keys, get the value of the nested keys in the object. 
If any of the keys are missing, return undefined. This is very useful for useful for checking JSON API responses where something useful is buried deep inside an object. Eg, given:

    var mockObject = {
      foo: 'bar',
      baz: {
        bam:'boo',
        zar:{
          zog:'something useful'
        }
      }
    }

The following code:
    
    mockObject.getPath(['baz','zar','zog']    

will return:

    'something useful'
    
Keys, of course, could be strings, array indices, or anything else.

### Array

#### .hasItem(_item_) 
returns true if the array has the item.

#### .findItem(_testfunction_) 
When provided with a function to test each item against, returns the first item that where testfunction returns true.

### String

#### .hasSubstring(_substring_) 
returns true if a string contains a substring

#### .forEach(_iterationfunction_)
Runs _iterationfunction_ over each character in the String. Just like ES5’s inbuilt Array.forEach().

### NodeList

#### .forEach(_iterationfunction_)
Runs _iterationfunction_ over each node in the NodeList. Just like ES5’s inbuilt Array.forEach().

Here’s an example of changing every paragraph in a document to say ‘Hello’ (look ma, No JQuery!).

    var paragraphs = document.getElementsByTagName('p');
    paragraphs.forEach(function(paragraph){
      paragraph.innerHTML = 'Hello.';
    })

## Why would I want to use Agave?

Agave will make your code shorter and more readable.

## How Does Agave Compare to Sugar.js?

Sugar.js is an excellent project and was the inspiration for Agave. Like Sugar, Agave provides useful additional methods on native objects.
 - Agave focuses only on things JS programmers do every day, and is much smaller than Sugar.js. Sugar.js has String.prototype.humanize() and .hankaku(). Agave won’t ever have those. 
 - Agave has a more explicit method naming style that’s consistent with the ES5 specification.
 - Agave does not attempt to support IE8 and other ES3 browsers, resulting in a much smaller code base that is free of ES3 shims.

## How Does Agave Compare to Underscore.js and Lodash?

 - Agave.js provides additional methods to complement those provided by ES5, rather than functions attached to punctuation. 
 - Agave doesn’t require a separate string library.

## But Adding Methods to Inbuilt Objects is Bad!

Adding methods to inbuilt objects _was_ bad, back in ES3 days, on browsers like IE8 and Firefox 3. There wasn’t a way for developers to add their own non-enumerable properties to inbuilt objects. I.e., if a developer you wanted objects to have .myMethod(), and thus created Object.prototype.myMethod(), things like ‘for (var key in someobject)’ would include ‘myMethod’ as one of the keys.

**ES5 - the current version of Javascript created in 2009 that Chrome, Firefox, and IE9/10 use - specifically allows for the creation of non-enumerable properties via Object.defineProperty()**

So if you’re OK with not supporting IE8, you can use Agave.

Another concern may be naming or implementation conflicts - ie, some other code that uses the same method name but does something different. Agave, like ES5 itself, uses very clear method naming. 

 - If your project already has a String.prototype.hasSubstring(), and it does something other than tell you whether a string has a substring, you should consider many things, the least of which is whether you should use this library.
 - If however, like most people, your code is filled with things like: 

    if ( mystring.indexof(substring) !== −1 ) { ... }

Then your code will be improved by using Agave.

    if ( mystring.hasSubstring(substring) ) { ... }  

## Using Agave

Agave is currently provided as an AMD module. You’d normally load it (either in the browser or on node.js) using [RequireJS](http://requirejs.org/)

    requirejs(['agave'], function () {  
      // Your code here
    })

## Tests

Install [node.js](http://nodejs.org/), and run:

    npm install mocha requirejs
    mocha

Inside the folder you downloaded Agave to.

## License

[MIT license](MIT_LICENSE.md).

## Author

Mike MacCana (mike.maccana@gmail.com)