---
layout: post
title:  "ES6 - (Presentation)"
published: true
---

(Major elements in this presentation have been adapted from https://github.com/lukehoban/es6features)

ECMAScript 6, also known as ECMAScript 2015, is the latest version of the ECMAScript standard. ES6 is a significant update to the language, and introduces features that bring it closer to other languages like C# and Java.

# Arrows
Arrows are a function shorthand using the `=>` syntax. They are syntactically similar to the related feature in C#, Java 8 and CoffeeScript. They support both statement block bodies as well as expression bodies which return the value of the expression. Unlike functions, arrows share the same lexical this as their surrounding code.

{% highlight js %}
var nums = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20];

// Expression bodies
var transformed = nums.map((v, i) => v + i);

console.log(transformed);

// Statement bodies
nums.forEach(v => {
  if (v % 5 === 0)
    console.log(v);
});

// Lexical this
var bob = {
  _name: "Bob",
  _friends: ["sam", "john"],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
}
{% endhighlight %}

# Class
ES6 classes are a simple sugar over the prototype-based OO pattern. Having a single convenient declarative form makes class patterns easier to use, and encourages interoperability. Classes support prototype-based inheritance, super calls, instance and static methods and constructors.

{% highlight js %}
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}
{% endhighlight %}

# Enhanced object literals
Object literals are extended to support setting the prototype at construction, shorthand for foo: foo assignments, defining methods, making super calls, and computing property names with expressions. Together, these also bring object literals and class declarations closer together, and let object-based design benefit from some of the same conveniences.

{% highlight js %}
var the_proto = {
  toString(){
    return "proto"
  },
};

var handler = function(){
  return "handler";
}

var obj = {
    // __proto__
    __proto__: the_proto,
    // Shorthand for ‘handler: handler’
    handler,
    // Methods
    toString() {
     // Super calls
     return "d " + super.toString();
    },
    // Computed (dynamic) property names
    [ 'prop_' + (() => 42)() ]: 42
};

console.log(obj.toString());

{% endhighlight %}

# Pattern Matching/Destructuring
Destructuring allows binding using pattern matching, with support for matching arrays and objects. Destructuring is fail-soft, similar to standard object lookup `foo["bar"]`, producing `undefined` values when not found.

{% highlight js %}
// list matching
var [a, , b] = [
  1,2,3
];

// object matching shorthand
// binds `op`, `lhs` and `rhs` in scope
var {a, b, c} = {
  a : 1,
  b: 2,
  c: 3
};

// Can be used in parameter position
function g({name: x}) {
  console.log(x);
}
g({name: 5})

// Fail-soft destructuring
var [a] = [];
a === undefined;

// Fail-soft destructuring with defaults
var [a = 1] = [];
a === 1;


{% endhighlight %}

# Default/Rest/Spread
Callee-evaluated default parameter values. Turn an array into consecutive arguments in a function call. Bind trailing parameters to an array. Rest replaces the need for arguments and addresses common cases more directly.

{% highlight js %}
//Default parameters
function f(x, y=12) {
  // y is 12 if not passed (or passed as undefined)
  return x + y;
}

f(3) == 15

//Rest
function f(x, ...y) {
  // y is an Array
  return x * y.length;
}

f(3, "hello", true) == 6


//Spread
function f(x, y, z) {
  return x + y + z;
}

// Pass each elem of array as argument
f(...[1,2,3]) == 6

{% endhighlight %}

# Generators/Iterators
Generators simplify iterator-authoring using `function*` and `yield`. A function declared as function* returns a Generator instance. Generators are subtypes of iterators which include additional next and throw. These enable values to flow back into the generator, so yield is an expression form which returns a value (or throws).

Note: Can also be used to enable ‘await’-like async programming, see also ES7 await proposal.

{% highlight js %}
var days = function* () {

    for (var i = 0; i < 10; i++) {

      var date = new Date();

      var day_val = date.getDate();
      date.setDate(day_val + i);

      yield {
        epoch: date.getTime()/1000,
        day_of_week: date.toString().split(" ")[0]
      };
    }
};

console.log(Array.from(days()));


{% endhighlight %}

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
