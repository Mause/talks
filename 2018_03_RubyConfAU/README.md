# References

⚠️  WARNING ⚠️

Are you watching this talk live? Is Katie currently up on stage explaining things to you?

Then please don't read ahead and spoil the answers

This resource is provided to you to help you learn, but it's no fun if I ask you to raise your hand to guess the answers when you ahave the answer key in front of you. 

Enjoy the talk. Read this later. 


...


Is the talk over yet?

Are you sure?

Good!

⬇️  Click to reveal ⬇️

<details>

## JavaScript

### Implicit Type Coercion

```
> 4 - "2"
2
```

https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html#implicitly-strings----numbers

> The `-` operator is defined only for numeric subtraction, so [4 - "2"] forces ["2"]'2 value to be coerced to a number

```
> 4 + "2"
42
```

https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html#implicitly-strings----numbers

> According to the ES5 spec, section 11.6.1, the + algorithm (when an object
> value is an operand) will concatenate if either operand is either already a
> string ...


```
> 1 == "1"
True
```

https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html#loose-equals-vs-strict-equals

> == allows coercion in the equality comparison and === disallows coercion.


http://2ality.com/2012/01/object-plus-object.html

https://www.ecma-international.org/ecma-262/#sec-addition-operator-plus

## Interlude: Ducks

https://www.destroyallsoftware.com/talks/wat

## Ruby

https://ruby-doc.org/core-2.5.0/doc/syntax/precedence_rdoc.html

https://whatthefuckruby.tumblr.com/post/70164947137/irb-not-true-false-true-irb-not-true

## Python

Amy Hanlon "Investigating Python Wats", PyCon US 2015

https://www.youtube.com/watch?v=sH4XF6pKKmk

## Haskell

http://adamesterline.com/haskell/2015/01/03/Fibonacci-in-Haskell

## Bash

https://ryanstutorials.net/bash-scripting-tutorial/bash-arithmetic.php

## Elixir

http://www.cursingthedarkness.com/2015/10/the-definitive-all-dancing-all-complete.html


## Go

(removed for time, but interesting)

https://twitter.com/pasiphae_goals/status/923821863222079488

https://twitter.com/rozaliev/status/923919964720988166

https://golang.org/ref/spec#Operators

> The one exception to this rule is that if the dividend x is the most negative
value for the int type of x, the quotient q = x / -1 is equal to x (and r = 0)
due to two's-complement integer overflow

https://golang.org/ref/spec#Integer_overflow

### Scala

Default functionality 


### Python

[Source](www.youtube.com/watch?v=sH4XF6pKKmk)

### Java

[Source](http://stackoverflow.com/a/2001861/124019)

### Perl

Source: original research. [Explanation](http://stackoverflow.com/a/14046720/124019)

### PHP

[Source](http://phpsadness.com/sad/30)

http://php.net/manual/en/language.operators.comparison.php#language.operators.comparison.ternary

### Powershell

Source: original research. [Documentation](http://fuckpowershell.tumblr.com/post/31777924330/fuck-using-standard-operands)


## Images

'wat' duck, [wat](https://www.destroyallsoftware.com/talks/wat), Gary Bernhardt

'wat' duck, Sydney, [hofman](https://imgur.com/gallery/gqilq)

https://www.florentijnhofman.nl/


# Further Reading

[Contempt Culture](https://blog.aurynn.com/2015/12/16-contempt-culture), auyrnn shaw

[Why I love Legacy DevOps](https://recompilermag.com/issues/issue-4/why-i-love-legacy-devops/), Katie McLaughlin, [The Recompiler, Issue 4](https://recompilermag.com/issues/issue-4/)


</details>
