# Implicit Coercion

Operators in JavaScript are designed to never throw errors.  This means that if you try to operate on values of different types, JS needs to do some work behind the scenes to avoid causing any errors.  That work is called __implicit coercion__.  JavaScript perform type conversions on the values before trying to compare, add, divide, whatever. 

To understand implicit coercion, it's helpful to realize that the rules are same as with explicit coercion (Number(x), String(x), Boolean(z), void a) but just happens without you writing it by hand. 

Because emplicit coercion is 'simply' applying explicit coercion in a well-defined way, the best way to understand implicit coercion is to try replicating native operators.

### Index:
* [plus --> +](#plus)
    * [plus replicated](#plus-replicated)
    * [a + b](#a-plus-b)
    * [a + b + c](#a-plus-b-plus-c)
    * [a + (b + c)](#a--b--c)
* [loose equality --> ==](#loose-equality)
    * [study it](#study-it)
    * [replicate it](#replicate-it)
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

[TOP](#implicit-coercion)

---

## Loose Equality


### Study It

Study [this comparison table](https://dorey.github.io/JavaScript-Equality-Table/).     
Play around with this [interactive table](https://janke-learning.org/equalities-coercion/).    
Then test yourself with [this quiz](https://eqeq.js.org).  



### Exercise

It's your turn.  In this exercise you'll write your own replication of the == operator for primitive values 'number', 'string', 'boolean', 'null' and 'undefined'.  We've provided you with a whole bunch of test cases and a commented starter function.  It's up to you to do the rest!  (hint: try focusing on one test case at a time, pass it then move on to pass the next. also, the test cases are organized to match up with the three sections of the function)

```js
/* your function must pass all of these tests

   null, undefined            ->   true
   undefined, null            ->   true
   null, null                 ->   true
   undefined, undefined       ->   true
   null, (anything else)      ->   false
   undefined, (anything else) ->   false

   true, false                ->    false
   false, false               ->    true
   3, 3                       ->    true
   3.0, 3                     ->    true
   +0, -0                     ->    true
   "\t", '\t'                 ->    true
   -3, +3                     ->    false

   3, "3"                     ->    true
   "3", 3                     ->    true
   "3, "3"                    ->    true
   true, 1                    ->    true
   false, 0                   ->    true
   false, ""                  ->    true
   0, ""                      ->    true
   "e", true                  ->    false
   undefined, ""              ->    false
   
*/
```

[on pytut](http://www.pythontutor.com/live.html#code=/*%20your%20function%20must%20pass%20all%20of%20these%20tests%0A%20%20%0A%20%20null,%20undefined%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20true%0A%20%20undefined,%20null%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20true%0A%20%20null,%20null%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20true%0A%20%20undefined,%20undefined%20%20%20%20%20%20%20-%3E%20%20%20true%0A%20%20null,%20%28anything%20else%29%20%20%20%20%20%20-%3E%20%20%20false%0A%20%20undefined,%20%28anything%20else%29%20-%3E%20%20%20false%0A%20%20%0A%20%20true,%20false%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20false%0A%20%20false,%20false%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%203,%203%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%203.0,%203%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20%2B0,%20-0%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20%22%5Ct%22,%20'%5Ct'%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20-3,%20%2B3%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20false%0A%20%20%20%20%20%20%20%0A%20%203,%20%223%22%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20%223%22,%203%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20%223,%20%223%22%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20true,%201%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20false,%200%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20false,%20%22%22%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%200,%20%22%22%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20true%0A%20%20%22e%22,%20true%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20false%0A%20%20undefined,%20%22%22%20%20%20%20%20%20%20%20%20%20%20%20%20%20-%3E%20%20%20%20false%0A*/%0A%0Aconst%20a%20%3D%20,%20b%20%3D%20%3B%0A%0Aconst%20native%20%3D%20a%20%3D%3D%20b%3B%0Aconst%20replication%20%3D%20lose_equality%28a,%20b%29%3B%0A%0Aconsole.assert%28native%20%3D%3D%3D%20replication,%20%22replication%20%3D%3D%3D%20%22%20%2B%20replication%29%3B%0A%0Afunction%20loose_equality%28x,%20y%29%20%7B%20%0A%20%20//%20if%20both%20a%20and%20b%20are%20null%20or%20undefined,%20return%20true%0A%20%20//%20if%20only%20one%20is%20null%20or%20undefined,%20return%20false%0A%0A%20%20//%20if%20both%20arguments%20are%20the%20same%20type%20%28num,%20string,%20or%20bool%29%0A%20%20//%20%20compare%20them%20with%20%3D%3D%3D%20and%20return%20the%20result%0A%0A%20%20//%20if%20both%20are%20not%20the%20same%20type%0A%20%20//%20%20make%20sure%20both%20are%20type%20'number'%0A%20%20//%20%20compare%20them%20with%20%3D%3D%3D,%20and%20return%20the%20result%0A%7D&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-live.js&py=js&rawInputLstJSON=%5B%5D&textReferences=false)
```js
{
  const a = , b = ;

  const native = a == b;
  const replication = lose_equality(a, b);

  console.assert(native === replication, "replication === " + replication);

  function loose_equality(x, y) { 
    // if both a and b are null or undefined, return true
    // if only one is null or undefined, return false

    // if both arguments are the same type (num, string, or bool)
    //  compare them with === and return the result

    // if both are not the same type
    //  make sure both are type 'number'
    //  compare them with ===, and return the result
  }
}
```

[TOP](#implicit-coercion)

---

## Resources

* [avoid implicit coercion](https://eslint.org/docs/rules/no-implicit-coercion)
* [plus demystified](https://dmitripavlutin.com/javascriptss-addition-operator-demystified/)
* [MDN equality comparison table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness) 
* [codementor: double equals](https://www.codementor.io/javascript/tutorial/double-equals-and-coercion-in-javascript)
* [a complete replication of ==](https://gist.github.com/qntm/d899c00aa1ac2c663ac6db23bcffcaba)
* [double vs. triple equals](https://codeburst.io/javascript-double-equals-vs-triple-equals-61d4ce5a121a)


[TOP](#implicit-coercion)

___
___
### <a href="http://janke-learning.org" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/50098409-22575780-021c-11e9-99e1-962787adaded.png" width="40" height="40"></img> Janke Learning</a>
