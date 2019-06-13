# Implicit Coercion

Operators in JavaScript are designed to never throw errors.  This means that if you try to operate on values of different types, JS needs to do some work behind the scenes to avoid causing any errors.  That work is called __implicit coercion__.  JavaScript perform type conversions on the values before trying to compare, add, divide, whatever. 

To understand implicit coercion, it's helpful to realize that the rules are same as with explicit coercion (Number(x), String(x), Boolean(z), void a) but just happens without you writing it by hand. 

Because emplicit coercion is 'simply' applying explicit coercion in a well-defined way, the best way to understand implicit coercion is to try replicating native operators.

### Index:
* example to study: [+](#plus)
    * [plus replicated](#plus-replicated)
    * [a + b](#a-plus-b)
    * [a + b + c](#a-plus-b-plus-c)
    * [a + (b + c)](#a--b--c)
    * [+a](#plus-a)
* exercise: [replicate ```==```](#replicate-loose-equality)
    * [describing behavior](#describing-behavior)
    * [run\_tests function](#run--tests-function)
    * [test driven development](#test-driven-development)
    * [study ```==```](#study-it)
    * [replicate ```==```](#replicate-it)
* [resources](#resources)

---

## Plus

Explaining and talking about implicit coercion is certainly helpful, but the ultimate test for how well you understand JS is the JS interpreter itself.  Before moving on play around with this [interactive coercion table](https://janke-learning.github.io/arithmetic-coercion/), let JavaScript show you how + and - behave.

### Plus replicated

The function below replicates the behavior of the + operator on primitive types (num, str, bool, null, undefined).  Often the best way to understand a language feature is to replicate it's behavior by hand.  If your replication passes the same test cases as the + operator, you have understood.

Before moving on the + exercises, study this function then copy-paste it into your console.  The exercises will break if it is not declared.

[parsonized plus function](https://janke-learning.github.io/parsonizer/?snippet=function%20plus%28x%2C%20y%29%20%7B%0A%20%20%0A%20%20if%20%28typeof%20x%20%3D%3D%3D%20%22string%22%20%7C%7C%20typeof%20y%20%3D%3D%3D%20%22string%22%29%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20String%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20String%28y%29%3B%0A%20%20%7D%20else%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20Number%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20Number%28y%29%3B%0A%20%20%7D%0A%0A%20%20return%20x_coerced%20%2B%20y_coerced%3B%0A%7D)
```js
function plus(x, y) {
  
  if (typeof x === "string" || typeof y === "string") {
    var x_coerced = String(x);
    var y_coerced = String(y);
  } else {
    var x_coerced = Number(x);
    var y_coerced = Number(y);
  }

  return x_coerced + y_coerced;
}
```


### a plus b

[on pytut](http://www.pythontutor.com/live.html#code=/*%20test%20cases%20%20%20%20%20%20%20%20%20%20%3A%20fill%20in%20the%20correct%20results%0A%20%20%223%22,%203,%203%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%203,%20%223%22,%203%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%203,%203,%20%223%22%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20%22%22,%20true,%20false%20%20%20%20%20-%3E%20%3F%0A%20%20true,%20false,%20%22%22%20%20%20%20%20-%3E%20%3F%0A%20%20null,%200,%20%22%22%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20%22%22,%200,%20null%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20undefined,%200,%20true%20%20-%3E%20%3F%0A*/%0Aconst%20a%20%3D%20,%20b%20%3D%20,%20c%20%3D%20%3B%0Aconst%20typeof_a%20%3D%20typeof%20a%3B%0Aconst%20typeof_b%20%3D%20typeof%20b%3B%0Aconst%20typeof_c%20%3D%20typeof%20c%3B%0A%0Aconst%20native_plus%20%3D%20a%20%2B%20%28b%20%2B%20c%29%3B%20//%20right%20to%20left%0Aconst%20replication%20%3D%20plus%28%20a,%20plus%28b,%20c%29%29%3B%0A%0Aconsole.assert%28native_plus%20%3D%3D%3D%20replication,%20replication%29%3B%0A%0Afunction%20plus%28x,%20y%29%20%7B%0A%20%20%0A%20%20if%20%28typeof%20x%20%3D%3D%3D%20%22string%22%20%7C%7C%20typeof%20y%20%3D%3D%3D%20%22string%22%29%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20String%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20String%28y%29%3B%0A%20%20%7D%20else%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20Number%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20Number%28y%29%3B%0A%20%20%7D%3B%0A%0A%20%20return%20x_coerced%20%2B%20y_coerced%3B%0A%7D&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-live.js&py=js&rawInputLstJSON=%5B%5D&textReferences=false)
```js
{
  /* test cases      : fill in the correct results
    null, undefined -> ?
    "3", 3          -> ?
    3, "3"          -> ?
    "3", "e"        -> ?
    3, "e"          -> ?
    "", 0           -> ?
    undefined, 4    -> ?
    true, false     -> ?
    true, "false"   -> ?
    null, false     -> ?
    1, null         -> ?
    null, ""        -> ?
  */

  const a =  , b = ;
  const typeof_a = typeof a;
  const typeof_b = typeof b;

  const native_plus = a + b;
  const replication = plus(a, b);

  console.assert(native_plus === replication, replication);
}
```

### a plus b plus c

[on pytut](http://www.pythontutor.com/live.html#code=%0A/*%20test%20cases%20%20%20%20%20%20%20%20%20%20%3A%20fill%20in%20the%20correct%20results%0A%20%20%223%22,%203,%203%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%203,%20%223%22,%203%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%203,%203,%20%223%22%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20%22%22,%20true,%20false%20%20%20%20%20-%3E%20%3F%0A%20%20true,%20false,%20%22%22%20%20%20%20%20-%3E%20%3F%0A%20%20null,%200,%20%22%22%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20%22%22,%200,%20null%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20undefined,%200,%20true%20%20-%3E%20%3F%0A*/%0Aconst%20a%20%3D%20,%20b%20%3D%20,%20c%20%3D%20%3B%0Aconst%20typeof_a%20%3D%20typeof%20a%3B%0Aconst%20typeof_b%20%3D%20typeof%20b%3B%0Aconst%20typeof_c%20%3D%20typeof%20c%3B%0A%0Aconst%20native_plus%20%3D%20a%20%2B%20b%20%2B%20c%3B%20//%20left%20to%20right%0Aconst%20replication%20%3D%20plus%28%20plus%28a,%20b%29,%20c%29%3B%0A%0Aconsole.assert%28native_plus%20%3D%3D%3D%20replication,%20replication%29%3B%0A%0Afunction%20plus%28x,%20y%29%20%7B%0A%20%20%0A%20%20if%20%28typeof%20x%20%3D%3D%3D%20%22string%22%20%7C%7C%20typeof%20y%20%3D%3D%3D%20%22string%22%29%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20String%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20String%28y%29%3B%0A%20%20%7D%20else%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20Number%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20Number%28y%29%3B%0A%20%20%7D%3B%0A%0A%20%20return%20x_coerced%20%2B%20y_coerced%3B%0A%7D&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-live.js&py=js&rawInputLstJSON=%5B%5D&textReferences=false)
```js
{ 
  /* test cases          : fill in the correct results
    "3", 3, 3           -> ?
    3, "3", 3           -> ?
    3, 3, "3"           -> ?
    "", true, false     -> ?
    true, false, ""     -> ?
    null, 0, ""         -> ?
    "", 0, null         -> ?
    undefined, 0, true  -> ?
  */
  const a = , b = , c = ;
  const typeof_a = typeof a;
  const typeof_b = typeof b;
  const typeof_c = typeof c;
  
  const native_plus = a + b + c; // left to right
  const replication = plus( plus(a, b), c);

  console.assert(native_plus === replication, replication);
}
```


### a + (b + c)

[on putut](http://www.pythontutor.com/live.html#code=/*%20test%20cases%20%20%20%20%20%20%20%20%20%20%3A%20fill%20in%20the%20correct%20results%0A%20%20%223%22,%203,%203%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%203,%20%223%22,%203%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%203,%203,%20%223%22%20%20%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20%22%22,%20true,%20false%20%20%20%20%20-%3E%20%3F%0A%20%20true,%20false,%20%22%22%20%20%20%20%20-%3E%20%3F%0A%20%20null,%200,%20%22%22%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20%22%22,%200,%20null%20%20%20%20%20%20%20%20%20-%3E%20%3F%0A%20%20undefined,%200,%20true%20%20-%3E%20%3F%0A*/%0Aconst%20a%20%3D%20,%20b%20%3D%20,%20c%20%3D%20%3B%0Aconst%20typeof_a%20%3D%20typeof%20a%3B%0Aconst%20typeof_b%20%3D%20typeof%20b%3B%0Aconst%20typeof_c%20%3D%20typeof%20c%3B%0A%0Aconst%20native_plus%20%3D%20a%20%2B%20%28b%20%2B%20c%29%3B%20//%20right%20to%20left%0Aconst%20replication%20%3D%20plus%28%20a,%20plus%28b,%20c%29%29%3B%0A%0Aconsole.assert%28native_plus%20%3D%3D%3D%20replication,%20replication%29%3B%0A%0Afunction%20plus%28x,%20y%29%20%7B%0A%20%20%0A%20%20if%20%28typeof%20x%20%3D%3D%3D%20%22string%22%20%7C%7C%20typeof%20y%20%3D%3D%3D%20%22string%22%29%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20String%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20String%28y%29%3B%0A%20%20%7D%20else%20%7B%0A%20%20%20%20var%20x_coerced%20%3D%20Number%28x%29%3B%0A%20%20%20%20var%20y_coerced%20%3D%20Number%28y%29%3B%0A%20%20%7D%3B%0A%0A%20%20return%20x_coerced%20%2B%20y_coerced%3B%0A%7D&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-live.js&py=js&rawInputLstJSON=%5B%5D&textReferences=false)
```js
{ 
  /* test cases          : fill in the correct results
    "3", 3, 3           -> ?
    3, "3", 3           -> ?
    3, 3, "3"           -> ?
    "", true, false     -> ?
    true, false, ""     -> ?
    null, 0, ""         -> ?
    "", 0, null         -> ?
    undefined, 0, true  -> ?
  */
  const a = , b = , c = ;
  const typeof_a = typeof a;
  const typeof_b = typeof b;
  const typeof_c = typeof c;
  
  const native_plus = a + (b + c); // right to left
  const replication = plus( a, plus(b, c));

  console.assert(native_plus === replication, replication);
}
```


### plus a

[on pytut](http://www.pythontutor.com/live.html#code=/*%20test%20cases%20%20%20%20%20%20%3A%20fill%20in%20the%20correct%20results%0A%20%20null%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20undefined%20%20%20-%3E%20%20%3F%0A%20%200%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%201%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20-1.5%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20NaN%20%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20Infinity%20%20%20%20-%3E%20%20%3F%0A%20%20%22%22%20%20%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20%22%20%22%20%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20%223%22%20%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20%223.3%22%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20%223%20%2B%203%22%20%20%20%20%20-%3E%20%20%3F%0A%20%20true%20%20%20%20%20%20%20%20-%3E%20%20%3F%0A%20%20false%20%20%20%20%20%20%20-%3E%20%20%3F%0A*/%0A%0Aconst%20a%20%3D%20%20,%20b%20%3D%20%3B%0Aconst%20typeof_a%20%3D%20typeof%20a%3B%0Aconst%20typeof_b%20%3D%20typeof%20b%3B%0A%0Aconst%20native_plus%20%3D%20%2Ba%3B%0Aconst%20replication%20%3D%20Number%28a%29%3B%0A%0Aconsole.assert%28native_plus%20%3D%3D%3D%20replication,%20replication%29%3B&cumulative=false&heapPrimitives=nevernest&mode=display&origin=opt-live.js&py=js&rawInputLstJSON=%5B%5D&textReferences=false)
```js
{
   /* test cases      : fill in the correct results
     null        ->  ?
     undefined   ->  ?
     0           ->  ?
     1           ->  ?
     -1.5        ->  ?
     NaN         ->  ?
     Infinity    ->  ?
     ""          ->  ?
     " "         ->  ?
     "3"         ->  ?
     "3.3"       ->  ?
     "3 + 3"     ->  ?
     true        ->  ?
     false       ->  ?
   */

   const a =  , b = ;
   const typeof_a = typeof a;
   const typeof_b = typeof b;

   const native_plus = +a;
   const replication = Number(a);

   console.assert(native_plus === replication, replication);
}
```

[TOP](#implicit-coercion)

---

## Replicate Loose Equality


## Describing Behavior

Code's behavior is what has changed in your program _after_ the code has executed, implementation is the lines of text that make up the code.  This exercise will introduce how to understand behavior using __test cases__.

Practically speaking you can think of test cases as just inputs and outputs.   What values went into the function, and what values come out of the function?  The test case will contain the input-output pairs that your function _should_ implement, a test case fails if the function returns something else.  

Test cases may be relatively easy to read and use, but writing good ones can be tricky.  You have to think about all possible strange combinations and fringe cases. So don't worry about writing the perfect test cases yet, just do your best and compare with a friend to help each other understand how you thought of your test cases.

For this exercise you will write test cases in this format:
```js
test_cases = [
    {name:'meaningful name', args:['the inputs', 'for this snippet'], expected: 'what it should output'},
    {name:'another test case', args:['different', 'inputs'], expected: 'the expected output'},
  ];
```

[TOP](#implicit-coercion)

---

## run\_tests Function

To check if your function passes all of it's test cases, we'll be using this function.  It takes two arguments (the function to test, and the test cases), and console.log's a message for every test case that fails.

Study it for a minute then paste it in the console, the exercises below won't work otherwise.  If you don't understand entirely how this function works that's okay.  The main objective for this exercise is to write & use test cases, understand JS operators.  

```js
function run_tests(_target, _cases) {
  console.groupCollapsed('<- click this arrow to see the function')
  console.log(_target.toString());
  console.groupEnd();
  for (let t_case of _cases) {
    
    // prep variables for convenience
    const expected = t_case.expected;
    const args = t_case.args;
    
    // run function with test case
    const actual = _target(...args);

    // compare
    let pass;
    if (typeof expected === 'object' && expected !== null) {
      const _actual = JSON.stringify(actual);
      const _expected = JSON.stringify(expected);
      pass = _actual === _expected;
    } else if ( typeof expected === 'number' && isNaN(expected) ) {
      pass = isNaN(actual) && typeof actual === 'number';
    } else {
      pass = actual === expected;
    };

    // communicate result to developer 
    if (!pass) {
      console.groupCollapsed(`%c  ${t_case.name}:`, 'color:red');
      console.log(`%cactual: ${typeof actual},`, 'color:orange', actual);
      console.log(`%cexpected: ${typeof expected},`, 'color:blue', expected);
      console.groupEnd();
    } else {
      console.groupCollapsed(`%cPassed: ${t_case.name}!`, 'color:green');
      console.log(`result: ${typeof actual},`, actual);
      console.groupEnd();
    };
  };
}
```

[TOP](#implicit-coercion)

---

## Test Driven Development

Very briefly this is a development philosophy that says to write all the tests your code should pass, then write the code to pass the tests.  

In the following exercise you will be practicing TDD by starting with the ```test_cases```, and then writing the ```==``` replication to pass the tests.

For more info and TDD exercises [check this out](https://github.com/janke-learning/tdd).

[TOP](#implicit-coercion)

---

### Study It

Study [this comparison table](https://dorey.github.io/JavaScript-Equality-Table/).     
Play around with this [interactive table](https://janke-learning.org/equalities-coercion/).    
Then test yourself with [this quiz](https://eqeq.js.org).  



### Replicate It

It's your turn.  In this exercise you'll write your own replication of the == operator for primitive values 'number', 'string', 'boolean', 'null' and 'undefined'.  We've provided you with a whole bunch of test cases and a commented starter function.  It's up to you to do the rest!  (hint: try focusing on one comment at a time, pass it then, move on to pass the next. also, the test cases are organized to match up with the three sections of the function)

__Passing Test Cases:__ you will use these tests to develop your replication of ```==```.  Copy-paste them into the console and hit enter.  to make sure they are loaded type ```test_cases``` into the console.
```js
test_cases = [
  { name: 'null, undefined', args: [null, undefined], expected: true},
  { name: 'undefined, null', args: [undefined, null], expected: true},
  { name: 'null, null', args: [null, null], expected: true},
  { name: 'undefined, undefined', args: [undefined, undefined], expected: true},
  { name: 'null, "anything else"', args: [null, "anything else"], expected: false},
  { name: 'undefined, "anything else"', args: [undefined, "anything else"], expected: false},
  { name: 'true, false', args: [true, false], expected: false},
  { name: 'false, false', args: [false, false], expected: true},
  { name: '3, 3', args: [3, 3], expected: true},
  { name: '3.0, 3', args: [3.0, 3], expected: true},
  { name: '+0, -0', args: [+0, -0], expected: true},
  { name: '"\t", "\t"', args: ["\t", '\t'], expected: true},
  { name: '-3, +3', args: [-3, +3], expected: false},
  { name: '3, "3"', args: [3, "3"], expected: true},
  { name: '"3", 3', args: ["3", 3], expected: true},
  { name: '"3", "3"', args: ["3", "3"], expected: true},
  { name: 'true, 1', args: [true, 1], expected: true},
  { name: 'false, 0', args: [false, 0], expected: true},
  { name: 'false, ""', args: [false, ""], expected: true},
  { name: '0, ""', args: [0, ""], expected: true},
  { name: '"e", true', args: ["e", true], expected: false},
  { name: 'undefined, ""', args: [undefined, ""], expected: false}
];
```

__Native Operation:__ Before moving on, copy-paste this code into the console and hit enter. Study the test results to build a first understanding of how ```==``` works. (if there are any red test cases, something went wrong!)
```js
function loose_equality(a, b) {
  return a == b;
}
run_tests(loose_equality, test_cases);
```

__Your Replication:__ Your turn!  Paste the code below into the console and begin developing your own replication of the ```==``` operator. Write little bits of code at once and run the code frequently.  Try perhaps implementing one comment at a time or to pass one test case at a time.   
Once you've passed all the tests, paste your code back into this markdown for studying later!
```js
function loose_replication(a, b) { 
  // if both a and b are null or undefined, return true
  // if only one is null or undefined, return false

  // if both arguments are the same type (num, string, or bool)
  //  compare them with === and return the result

  // if both are not the same type
  //  make sure both are type 'number'
  //  compare them with ===, and return the result
}
run_tests(loose_replication, test_cases);
```

[TOP](#implicit-coercion)

---

## Resources

* [avoid implicit coercion](https://eslint.org/docs/rules/no-implicit-coercion)
* [plus demystified](https://dmitripavlutin.com/javascriptss-addition-operator-demystified/)
* [javascript.info: comparisons](https://javascript.info/comparison)
* [MDN equality comparison table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness) - ignore the bottom row and farthest right column
* [interactive ```==``` table](https://janke-learning.org/equalities-coercion/)
* [codementor: double equals](https://www.codementor.io/javascript/tutorial/double-equals-and-coercion-in-javascript)
* [a complete replication of ==](https://gist.github.com/qntm/d899c00aa1ac2c663ac6db23bcffcaba)
* [double vs. triple equals](https://codeburst.io/javascript-double-equals-vs-triple-equals-61d4ce5a121a)


[TOP](#implicit-coercion)

___
___
### <a href="http://janke-learning.org" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/50098409-22575780-021c-11e9-99e1-962787adaded.png" width="40" height="40"></img> Janke Learning</a>
