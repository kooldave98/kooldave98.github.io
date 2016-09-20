---
layout: post
title:  "ES6 - (non-exhaustive)"
published: true
---

(Adapted from https://github.com/lukehoban/es6features)

ECMAScript 6, also known as ECMAScript 2015, is the latest version of the ECMAScript standard. ES6 is a significant update to the language, and introduces features that bring it closer to other languages like C# and Java.

# Arrows
Arrows are a function shorthand using the `=>` syntax. They are syntactically similar to the related feature in C#, Java 8 and CoffeeScript. They support both statement block bodies as well as expression bodies which return the value of the expression. Unlike functions, arrows share the same lexical this as their surrounding code.

# Class
ES6 classes are a simple sugar over the prototype-based OO pattern. Having a single convenient declarative form makes class patterns easier to use, and encourages interoperability. Classes support prototype-based inheritance, super calls, instance and static methods and constructors.

# Enhanced object literals
Object literals are extended to support setting the prototype at construction, shorthand for foo: foo assignments, defining methods, making super calls, and computing property names with expressions. Together, these also bring object literals and class declarations closer together, and let object-based design benefit from some of the same conveniences.

# Pattern Matching/Destructuring
Destructuring allows binding using pattern matching, with support for matching arrays and objects. Destructuring is fail-soft, similar to standard object lookup `foo["bar"]`, producing `undefined` values when not found.

# Default/Rest/Spread
Callee-evaluated default parameter values. Turn an array into consecutive arguments in a function call. Bind trailing parameters to an array. Rest replaces the need for arguments and addresses common cases more directly.

# Generators/Iterators
Generators simplify iterator-authoring using `function*` and `yield`. A function declared as function* returns a Generator instance. Generators are subtypes of iterators which include additional next and throw. These enable values to flow back into the generator, so yield is an expression form which returns a value (or throws).

Note: Can also be used to enable ‘await’-like async programming, see also ES7 await proposal.

# Let's build a simple LINQ implementation

{% highlight js %}
var minions = [
  {name: 'orc', hp: 100},
  {name: 'troll', hp: 40},
  {name: 'bunny', hp: 1},
  {name: 'skeleton', hp: 31},
  {name: 'peon', hp: 10}];

var query = minions
  .toLinqable()
  .where(m => m.hp > 30)
  .select(m => m.name);
{% endhighlight %}
