Node Workshop - Lesson 2
=
`=> github.com/rsp/nw2`
-

Lesson 2 of the
Node.js Workshop by Rafał Pocztarski at inFullMobile.

* Prev: https://github.com/rsp/nw1
* Next: https://github.com/rsp/nw3

About us
=
[<img src="https://infullmobile.com/wp-content/themes/ifm_simple/img/svg/logo_dark.svg" width="500">](https://infullmobile.com/)

**inFullMobile** is a digital product design and development studio based in Warsaw, Poland.

Doing mobile, web, IoT and hardware projects from the idea to a final product.

https://infullmobile.com/

About me
=
[<img src="https://github.com/rsp.png" height="80">](https://pocztarski.com/)

**Rafał Pocztarski** is a Senior Node.js Developer and Team Leader at inFullMobile.

Programming since 1986, commercially since 1996.

Programming in Node since watching the first Node.js presentation by Ryan Dahl in 2009.

Enjoys writing about Node.js on Stack Overflow, holding a rare Gold Node.js Badge.

https://pocztarski.com/

Global object
=
The JavaScript global object
(that has all global variables as properties)
is called `global` in Node,
`window` in the browser
and `self` in Web Workers.

During the workshop I forgot about my own module on npm that returns the global object in all of those three environments, to normalize the name:

* https://www.npmjs.com/package/the-global-object

Number type
=
As I said during the workshop,
the standard `Number` type in JavaScript is:

* 64-bit floating point (the [IEEE 754 double precision floating-point number](https://en.wikipedia.org/wiki/IEEE_754-1985#Double-precision_64_bit) - see: [ECMA-262 Edition 5.1, Section 8.5](http://www.ecma-international.org/ecma-262/5.1/index.html#sec-8.5) and [ECMA-262 Edition 6.0, Section 6.1.6](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-ecmascript-language-types-number-type))

More numeric types are defined in
[WebAssembly](https://www.w3.org/community/webassembly/),
[typed arrays](https://developer.mozilla.org/en-US/docs/JavaScript/Typed_arrays)
and [asm.js](http://asmjs.org/).

My answer on Stack Overflow with more details:

* [Difference between floats and ints in Javascript?](https://stackoverflow.com/questions/5179836/difference-between-floats-and-ints-in-javascript/5179886#5179886)

String literals
=

Template literals (the backtick strings) documentation:

* https://developer.mozilla.org/Web/JavaScript/Reference/Template_literals

Node compatibility:

* https://node.green/#ES2015-syntax-template-literals

Babel for experiments:

* https://babeljs.io/
* ([link to my backtick example code in Babel REPL](http://babeljs.io/repl/#?babili=false&browsers=&build=&builtIns=false&code_lz=DYUwLgBAHhC8EAMCGAjAxhAJAbwIwQGoJcAGAXwgBMQAzAKAHMALASwQG4g&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=true&fileSize=false&lineWrap=false&presets=latest%2Creact%2Cstage-2&prettier=false&targets=&version=6.26.0&envVersion=))

Benchmarks
-
Parsing file with a million strings `'x';` using single quotes, double quotes and backticks, using Node 9.5:

```sh
$ time node msq.js # parsing million single quotes

real  0m0.305s
user  0m0.252s
sys   0m0.051s

$ time node mdq.js # parsing million double quotes 

real  0m0.307s
user  0m0.253s
sys   0m0.051s

$ time node mbt.js # parsing million backticks

real  0m0.686s
user  0m0.526s
sys   0m0.154s
```

It seems that backtick parsing takes two times longer than single and double quotes
but it is still less than a microsecond.
This is the speed of compilation that is done once
on program startup.

The usage of backticks vs single or double quotes
doesn't seem to make any difference during runtime:

```sh
$ time node psq.js # processing single quote concats

real  0m1.058s
user  0m0.983s
sys   0m0.042s

$ time node pdq.js # processing double quote concats

real  0m1.054s
user  0m0.984s
sys   0m0.043s

$ time node pbt.js # processing backtick concats

real  0m1.056s
user  0m0.985s
sys   0m0.043s

$ time node pno.js # empty loop for comparison

real  0m0.151s
user  0m0.133s
sys   0m0.016s
```

The above test was 100 million string concatenations, 15% of the time is the loop overhead so it's about 9 nanoseconds per operation.

The JS files used in the tests are in the repository for reference.

Number precision
=
My answers on Stack Overflow on how to deal
with rounding errors:

* [Avoiding problems with JavaScript's weird decimal calculations](https://stackoverflow.com/questions/5037839/avoiding-problems-with-javascripts-weird-decimal-calculations/5037927#5037927)
* [Node giving strange output on sum of particular float digits](https://stackoverflow.com/questions/44949148/node-giving-strange-output-on-sum-of-particular-float-digits/44949594#44949594)

Some libraries for arbitrary precision numbers in JS:

* https://github.com/MikeMcl/big.js/
* https://github.com/MikeMcl/decimal.js/
* https://github.com/charto/bigfloat
* https://github.com/josdejong/mathjs
* https://github.com/vukicevic/crunch

More searches on npm:

* https://www.npmjs.com/browse/keyword/precision
* https://www.npmjs.com/browse/keyword/bignum
* https://www.npmjs.com/browse/keyword/bigint

TC39 BigInt proposal:

* https://github.com/tc39/proposal-bigint

TypeScript
=
TypeScript by Microsoft is JavaScript + static typing.

* https://www.typescriptlang.org/

Unexposed
=
My module on npm that exposes the `AsyncFunction` constructor that is usually unexsposed, as I discussed on the workshop:

* https://www.npmjs.com/package/unexposed

Without this module:

```js
> x = function () {};
[Function: x]
> x instanceof Function;
true
> x = async function () {};
[AsyncFunction: x]
> x instanceof AsyncFunction;
ReferenceError: AsyncFunction is not defined
```

With this module:

```js
> x = function () {};
[Function: x]
> x instanceof Function;
true
> x = async function () {};
[AsyncFunction: x]
> x instanceof AsyncFunction;
true
```


[github-follow-url]: https://github.com/rsp
[github-follow-img]: https://img.shields.io/github/followers/rsp.svg?style=social&label=Follow
[twitter-follow-url]: https://twitter.com/intent/follow?screen_name=pocztarski
[twitter-follow-img]: https://img.shields.io/twitter/follow/pocztarski.svg?style=social&label=Follow
[stackoverflow-url]: https://stackoverflow.com/users/613198/rsp
[stackexchange-url]: https://stackexchange.com/users/303952/rsp
[stackexchange-img]: https://stackexchange.com/users/flair/303952.png
