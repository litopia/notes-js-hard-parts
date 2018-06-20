## Javascript 3 principles
1. Thread
    - As soon as we start running Javascript code, we create a **global execution context**
    - Thread of execution (parsing and executing the code line after line)
2. Execution context
    - When executing a function, it creates a new execution context comprising: **the thread of execution** and **a local memory**
    - A local memory (variable environment) where anything defined in the function is stored
3. Call stack
    - a special data structure to keep track of where is the thread
    - push and pop
    - tracks which execution context we are in - that is, what function is currently being run and where to return to after an execution context is popped off the stack

*Notes:*
*Functions in Javascript = first class objects*

## Closure
When our functions get called, we create a live store of data (local memory/variable environment) for that function's execution context. WHen the function finishes execution, its local memory is deleted (except the returned value).

However, returning a function from another function will give us ability to hold on to state between execution.

### Higher order function
    - A function that can take in a function
    - Functions co-exist and can be treated as object, meaning:
        1. assigned to variables and properties of other objects
        2. passed as arguments into functions
        3. returned as values from functions

### lexical scope
When a function is defined, it gets a `[[scope]]` property that reference the local memory/variable environment in which it can be defined. 

Our lexical scope (the available live data when our functions was defined) is what determines our available variables at function's execution, not where our function is called.

```javascript
function addByX(x) {
  var result = x;
  
  function increment(input) {
    console.log(result + input);
    return result + input;
  }

  return increment;
}

var addByTwo = addByX(2);

// now call addByTwo with an input of 1
addByTwo(1); //should return 3
addByTwo(2); //should return 4
addByTwo(3); //should return 5

```


