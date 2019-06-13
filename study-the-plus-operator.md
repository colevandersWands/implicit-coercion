# Plus

Explaining and talking about implicit coercion is certainly helpful, but the ultimate test for how well you understand JS is the JS interpreter itself.  Before moving on play around with this [interactive coercion table](https://janke-learning.github.io/arithmetic-coercion/), let JavaScript show you how + behaves.

### Index:
* [plus replicated](#plus-replicated)
* [a + b](#a-plus-b)
* [a + b + c](#a-plus-b-plus-c)
* [a + (b + c)](#a--b--c)
* [+a](#plus-a)

---

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

[TOP](#plus)

---

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

  console.log(typeof_a + ' + ' + typeof_b + ' -> ' + typeof native_plus);
  console.assert(native_plus === replication, replication);
}
```

[TOP](#plus)

---

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

  console.log(typeof_a+' + '+typeof_b+' + '+typeof_c+' -> '+typeof native_plus);
  console.assert(native_plus === replication, replication);
}
```

[TOP](#plus)

---

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

  console.log(typeof_a+' + ('+typeof_b+' + '+typeof_c+') -> '+typeof native_plus);
  console.assert(native_plus === replication, replication);
}
```

[TOP](#plus)

---

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

   const a =  ;
   const typeof_a = typeof a;

   const native_plus = +a;
   const replication = Number(a);

   console.log('+'+typeof_a+' -> '+typeof native_plus);
   console.assert(native_plus === replication, replication);
}
```

[TOP](#plus)


___
___
### <a href="http://janke-learning.org" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/50098409-22575780-021c-11e9-99e1-962787adaded.png" width="40" height="40"></img> Janke Learning</a>
