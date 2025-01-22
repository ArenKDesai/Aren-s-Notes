
## JavaScript Basics
- variables declared with ```var``` are old with scoping issues. ```var``` should simply not be used. Instead, use ```let```, or ```const``` for constants. 
- Arrays in javascript can hold multiple different types. 
- A "real test" is ```===```, not ```==```. 
- Undefined is false. Something existing is true. 
- Checking for a key in a dict that doesn't exist provides undefined, not an exception. 
- The keyword ```this``` is complicated, and can have multiple meanings. 
- Checking for an indexed position beyond the length of an array returns undefined, not an exception. 
- the ```for i in nums``` of javascript is ```for i of nums```. ```is``` is something else (deprecated, don't use). 
- You can use functions as in-code variables. 
- Referring to a variable in a different scope is called a closure. 
- Functional programming is very helpful for event-driven programming. 
- Its usually best to check if an element exists before running a script. 

## Web Basics
Webpages are made of elements, where scripts can be ran on objects indexed by IDs. 
Javascript code can be written either in-page or in a separate file, with the ```defer``` tag to execute the script after the elements have been rendered. 
Browsers are historically non-parallel. Commonly, we add events to a queue to be processed later. 

Common loop structure:
```javascript
function drawLoop() {
	// change things
	// draw something
	wind
}
```