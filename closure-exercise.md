
# Closures, Scope, and Execution Context
[View it on CSbin](http://csbin.io/closures)

## Challenge 1
Create a function createFunction that creates and returns a function. When that created function is called, it should print "hello".

```javascript
function createFunction() {
  return function() {
    console.log("Hello");
  }
}

// UNCOMMENT THESE TO TEST YOUR WORK!
var function1 = createFunction();
function1();
```

## Challenge 2
Create a function createFunctionPrinter that accepts one input and returns a function. When that created function is called, it should print out the input that was used when the function was created.

```javascript

function createFunctionPrinter(input) {
  return function() {
    console.log(input);
  }
}

// UNCOMMENT THESE TO TEST YOUR WORK!
var printSample = createFunctionPrinter('sample'); //should console.log('sample');
printSample();
var printHello = createFunctionPrinter('hello'); //should console.log('hello');
printHello();
```

## Challenge 3
Examine the code for the outer function. Notice that we are returning a function and that function is using variables that are outside of its scope.
Uncomment those lines of code. Try to deduce the output before executing.

```javascript
function outer() {
  var counter = 0; // this variable is outside incrementCounter's scope
  function incrementCounter () {
    counter ++;
    console.log('counter', counter);
  }
  return incrementCounter;
}

var willCounter = outer();
var jasCounter = outer();

// Uncomment each of these lines one by one.
// Before your do, guess what will be logged from each function call.

willCounter();
willCounter();
willCounter();

jasCounter();
willCounter();
```


## Challenge 4
Now we are going to create a function addByX that returns a function that will add an input by x.

```javascript
function addByX(x) {
  var result = x;
  
  return function(input) {
    console.log(result + input);
    return result + input;
  }
}

var addByTwo = addByX(2);

// now call addByTwo with an input of 1
addByTwo(1); //should return 3
addByTwo(2); //should return 4
addByTwo(3); //should return 5


// now call addByTwo with an input of 2
var addByThree = addByX(3);
addByThree(1); //should return 4
addByThree(2); //should return 5

var addByFour = addByX(4);
addByFour(4); //should return 8
addByFour(10); //should return 14
```

## Extension: Challenge 5
Write a function once that accepts a callback as input and returns a function. When the returned function is called the first time, it should call the callback and return that output. If it is called any additional times, instead of calling the callback again it will simply return the output value from the first time it was called.

```
function once(func) {
  var called = 0;
  var counter;
  
  return function(input) {
    
    if(called === 0) {
      counter  = input
      func(input);
    } else {
      func(counter);
    }
  
    called++;
  }
} 

var onceFunc = once(addByTwo);

// UNCOMMENT THESE TO TEST YOUR WORK!
console.log(onceFunc(4));  //should log 6
console.log(onceFunc(10));  //should log 6
console.log(onceFunc(9001));  //should log 6
```

## Extension: Challenge 6
Write a function after that takes the number of times the callback needs to be called before being executed as the first parameter and the callback as the second parameter.

```
function after(count, func) {
  var called = 0;
  
  return function() {
    called++;
    if (called >= count) {
      func();      
    }
  }
}

var called = function() { console.log('hello') };
var afterCalled = after(3, called);

afterCalled(); // -> nothing is printed
afterCalled(); // -> nothing is printed
afterCalled(); // -> 'hello' is printed
```
