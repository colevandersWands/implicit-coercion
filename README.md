# Implicit Coercion

Operators in JavaScript are designed to never throw errors.  This means that if you try to operate on values of different types, JS needs to do some work behind the scenes to avoid causing any errors.  That work is called __implicit coercion__.  JavaScript perform type conversions on the values before trying to compare, add, divide, whatever. 

To understand implicit coercion, it's helpful to realize that the rules are same as with explicit coercion (Number(x), String(x), Boolean(z), void a) but just happens without you writing it by hand. 

Because emplicit coercion is 'simply' applying explicit coercion in a well-defined way, the best way to understand implicit coercion is to try replicating native operators.

### Index:
* exercises
    * [study the ```+``` operator](./study-the-plus-operator.md)
    * [replicate the ```==``` operator](./replicate-loose-equality.md)
* [resources](#resources)

---

## Resources

* [avoid implicit coercion](https://eslint.org/docs/rules/no-implicit-coercion)
* [plus demystified](https://dmitripavlutin.com/javascriptss-addition-operator-demystified/)
* [javascript.info: comparisons](https://javascript.info/comparison)
* [MDN equality comparison table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness) - ignore the bottom row and farthest right column
* [interactive ```==``` table](https://janke-learning.org/equalities-coercion/)
* [interactive ```+``` table](https://janke-learning.org/arithmetic-coercion/)
* [codementor: double equals](https://www.codementor.io/javascript/tutorial/double-equals-and-coercion-in-javascript)
* [a complete replication of ==](https://gist.github.com/qntm/d899c00aa1ac2c663ac6db23bcffcaba)
* [double vs. triple equals](https://codeburst.io/javascript-double-equals-vs-triple-equals-61d4ce5a121a)


[TOP](#implicit-coercion)

___
___
### <a href="http://janke-learning.org" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/50098409-22575780-021c-11e9-99e1-962787adaded.png" width="40" height="40"></img> Janke Learning</a>
