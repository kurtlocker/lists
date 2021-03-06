# [ l [ i [ s ] t ] s ]

**Full Version** | **[Homepage](http://kurtlocker.github.io/lists)**

Lists is a library of JavaScript higher-order functions for working with arrays and strings. The library was inspired  by Haskell's Data.List module by the powerful people over at [The University of Glasgow](http://www.gla.ac.uk/). You can view the original source [here](https://hackage.haskell.org/package/base-4.7.0.0/docs/src/Data-List.html). You could then scroll through each function closely and see a purposefully similar correlation between the Haskell implementation and [this](https://raw.githubusercontent.com/kurtlocker/lists/master/lists.js) implementation.

Pass functions to functions to functions to solve complex problems. Most of the functions featured in Lists produce new arrays, to reinforce the paradigm of stateless programming.

**Disclaimer**: Almost all of these functions are naive recursive definitions. The idea behind this library is to maximize problem-solving expressivity. This library provides an alternative toolbox by which to solve problems. This library should be sufficient for most projects but remember to monitor your heap memory space in the case of excessive function calls.

## Install

To import the entire library:

`npm install --save lists`

Using in your Node.js project:

```js
var lists = require('lists');
```

Using in your browser: 

Download the script source file `lists.min.js` and include it in your HTML. Lists is exported as a global object attached to `window`. Access functions by calling `lists` or `window.lists`.

```html
<script src='lists.min.js'></script>
<script>
	lists.head(["Hey!"]); // "Hey!"
</script>
```

## Practical Example Usage

Lets complete an easy task from [/r/dailyprogrammer](http://www.reddit.com/dailyprogrammer). [Here](http://www.reddit.com/r/dailyprogrammer/comments/29i9jw/6302014_challenge_169_easy_90_degree_2d_array/) is the task:

**Given a NxN size 2D array of numbers. Develop a way to rotate the data as if you rotated the data by 90 degrees clockwise.**

The challenge input is a 10x10 matrix that looks like this:

```js
var matrix = 
[[1,2,3,4,5,6,7,8,9,0],
 [0,9,8,7,6,5,4,3,2,1],
 [1,3,5,7,9,2,4,6,8,0],
 [0,8,6,4,2,9,7,5,3,1],
 [0,1,2,3,4,5,4,3,2,1],
 [9,8,7,6,5,6,7,8,9,0],
 [1,1,1,1,1,1,1,1,1,1],
 [2,2,2,2,2,2,2,2,2,2],
 [9,8,7,6,7,8,9,8,7,6],
 [0,0,0,0,0,0,0,0,0,0]];
```

Using **Lists**, we can reverse and then transpose this matrix to achieve the desired output:

```js
var l = require('lists');
l.transpose(l.rev(matrix));

// or using pipe (composing left)
var rotate90 = l.pipe(l.transpose, l.rev);
rotate90(matrix);

/* both of these functions yield
[[0,9,2,1,9,0,0,1,0,1], 
 [0,8,2,1,8,1,8,3,9,2], 
 [0,7,2,1,7,2,6,5,8,3], 
 [0,6,2,1,6,3,4,7,7,4], 
 [0,7,2,1,5,4,2,9,6,5], 
 [0,8,2,1,6,5,9,2,5,6],
 [0,9,2,1,7,4,7,4,4,7], 
 [0,8,2,1,8,3,5,6,3,8],
 [0,7,2,1,9,2,3,8,2,9], 
 [0,6,2,1,0,1,1,0,1,0]];
/*
```

## Type Signature Legend

* **arr | []** : Array 
* **obj | {}** : Object
* **str** : String 
* **num** : Number
* **f** : Function
* **x** : Variable
* **boolean** : boolean

A{ **1.** } Function number

B{ **tail** } Function name

C{ **[x]|str -> [x]** } Pseudo type signature

tail : [x]|str -> [x] 
- Takes an Array of Variables or a String and produces an Array of Variables ([x]).

map : [x] -> f -> [x]
- Takes an Array of Variables and a Function and produces an Array of Variables.

## Contents

**Basic Functions**

* [`append`](#append) : [x]|str -> [x]|str|num -> [x]|str
* [`head`](#head) : [x]|str -> x
* [`last`](#last) : [x]|str -> x
* [`init`](#init) : [x]|str -> [x]
* [`tail`](#tail) : [x]|str -> [x]
* [`nil`](#nil) : [x]|str -> boolean

-----

**List Transformations**

* [`map`](#map) : [x]|str -> f -> [x]
* [`rev`](#rev) : [x]|str -> [x]
* [`intersperse`](#intersperse) : x -> [x]|str -> [x]|str
* [`intercalate`](#intercalate) : [x] -> [[x]] -> [x]
* [`transpose`](#transpose) : [[x]] -> [[x]]
* [`subsequences`](#subsequences) : [x]|str -> [[x]]
* [`permutations`](#permutations) : [x]|str -> [[x]]|[str]

-----

**Reducing Lists (folds)**

* [`foldl`](#foldl) : x -> [x]|str -> f -> x
* [`foldl1`](#foldl1) : [x]|str -> f -> x
* [`foldr`](#foldr) : x -> [x]|str -> f -> x
* [`foldr1`](#foldr1) : [x]|str -> f -> x
* [`flatten`](#flatten) || [`concat`](#flatten) : [[x]]|[str] -> [x]|str
* [`concatMap`](#concatMap) : [x]|str -> f -> [x]|str
* [`and`](#and) : [boolean] -> boolean
* [`or`](#or) : [boolean] -> boolean
* [`any`](#any) : [x]|str -> f -> boolean
* [`all`](#all) : [x]|str -> f -> boolean
* [`sum`](#sum) : [num] -> num
* [`product`](#product) : [num] -> num
* [`maximum`](#maximum) : [num] -> num
* [`minimum`](#minimum) : [num] -> num
* [`maxList`](#maxList) : [[x]] -> [x]
* [`minList`](#minList) : [[x]] -> [x]

-----

**Building Lists**

* [`scanl`](#scanl) : x -> [x]|str -> f -> [x]
* [`scanr`](#scanr) : x -> [x]|str -> f -> [x]
* [`mapAccumL`](#mapAccumL) : x -> [x]|str -> f -> [x, [x]]
* [`mapAccumR`](#mapAccumR) : x -> [x]|str -> f -> [x, [x]]
* [`iterate`](#iterate) : x -> num -> f -> [x] 
* [`replicate`](#replicate) : x -> num -> [x]
* [`cycle`](#cycle) : [x]|str -> num -> [x]|str
* [`unfold`](#unfold) : f -> f -> f -> x -> [x]|str

-----

**Sublists**

* [`take`](#take) : num -> [x]|str -> [x]
* [`drop`](#drop) : num -> [x]|str -> [x]
* [`splitAt`](#splitAt) : num -> [x]|str -> [[x],[x]]
* [`takeWhile`](#takeWhile) : f -> [x]|str -> [x]
* [`dropWhile`](#dropWhile) : f -> [x]|str -> [x]
* [`span`](#span) : [x]|str -> f -> [[x], [x]|str]
* [`break`](#break) : [x]|str -> f -> [[x], [x]|str]
* [`stripPrefix`](#stripPrefix) : [num]|str -> [num]|str -> [num]|[str]
* [`group`](#group) : [num]|str -> [[num]]|[[str]]
* [`inits`](#inits) : [x]|str -> [[x]]
* [`tails`](#tails) : [x]|str -> [[x]]

-----

**Predicates**

* [`isPrefixOf`](#isPrefixOf) : [num]|str -> [num]|str -> boolean
* [`isSuffixOf`](#isSuffixOf) : [num]|str -> [num]|str -> boolean
* [`isInfixOf`](#isInfixOf) : [num]|str -> [num]|str -> boolean
* [`isSubsequenceOf`](#isSubsequenceOf) : [num]|str -> [num]|str -> boolean

-----

**Searching Lists**

* [`elem`](#elem) : num|str -> [num]|str -> boolean
* [`notElem`](#notElem) : num|str -> [num]|str -> boolean
* [`lookup`](#lookup) : num|str -> [[num|str,x]] -> boolean
* [`find`](#find) : [x]|str -> f -> x
* [`filter`](#filter) : [x]|str -> f -> [x]
* [`partition`](#partition) : [x]|str -> f -> [[x],[x]]

-----

**Indexing Lists**

* [`bang`](#bang) : num -> [x] -> x
* [`elemIndex`](#elemIndex) || [`indexOf`](#elemIndex) : num|str -> [num]|str -> num
* [`elemIndices`](#elemIndices) : num|str -> [num]|str -> [num]
* [`findIndex`](#findIndex) : [x]|str -> f -> num
* [`findIndices`](#findIndices) : [x]|str -> f -> [num]

-----

**Zipping and Unzipping Lists**

* [`zip`](#zip) || [`unzip`](#zip) : [[a,b,..,n],[c,d,..,n],..,n] -> [[a,c,..,n],[b,d,..,n],..,n]
* [`zipWith`](#zipWith) : [[a,b,..,n],[c,d,..,n],..,n] -> f -> [x]

-----

**Special Lists**

* [`lines`](#lines) : str -> [str]
* [`words`](#words) : str -> [str]
* [`unlines`](#unlines) : [str] -> str
* [`unwords`](#unwords) : [str] -> str
* [`nub`](#nub) || [`uniq`](#nub) || [`unique`](#nub) : [num|str]|str -> [num|str]
* [`delete`](#delete) : x -> [x]|str -> [x]
* [`difference`](#difference) || [`diff`](#difference) : [num|str]|str -> [num|str]|str -> [x]
* [`union`](#union) : [num|str]|str -> [num|str]|str -> [x]|str
* [`intersect`](#intersect) : [num|str]|str -> [num|str]|str -> [x]
* [`sort`](#sort) : [x]|str -> [x]
* [`insert`](#insert) : x -> [x] -> [x]

-----

**Generalized Functions**

* [`nubBy`](#nubBy) : [x]|str -> f -> [x]
* [`deleteBy`](#deleteBy) : x -> [x]|str -> f -> [x]
* [`deleteFirstsBy`](#deleteFirstsBy) : [x]|str -> [x]|str -> f -> [x]
* [`unionBy`](#unionBy) : [x] -> [x] -> f -> [x]
* [`intersectBy`](#intersectBy) : [x]|str -> [x]|str -> f -> [x]
* [`groupBy`](#groupBy) : [x]|str -> f -> [[x]]
* [`sortBy`](#sortBy) : [x]|str -> f -> [x]
* [`insertBy`](#insertBy) : x -> [x]|str -> f -> [x]
* [`maximumBy`](#maximumBy) : [x]|str -> f -> x
* [`minimumBy`](#minimumBy) : [x]|str -> f -> x

-----

**Extra Functional Utilities**

* [`genericExcludeChar`](#genericExcludeChar) : str -> str -> [str]
* [`forEach`](#each) || [`each`](#each) : x -> f -> x
* [`keys`](#keys) : obj -> [str]
* [`enumeration`](#enum) || [`enum`](#enum) : num -> num -> [num] 
* [`composeL`](#pipe) || [`pipe`](#pipe) : f[,..,f] -> f
* [`composeR`](#sequence) || [`sequence`](#sequence) : f[,..,f] -> f
* [`partial`](#partial) || [`part`](#partial) : f -> x[,..,x] -> f
* [`flip`](#flip) : f -> f
* [`compare`](#compare) : x -> x -> str
* [`bubbleSort`](#bubbleSort) : [num] -> [num]
* [`mergeSort`](#mergeSort) : [num] -> [num] 

------
<a name='append'></a>
## append : [x]|str -> [x]|str|num -> [x]|str

**Description**: A prefix-style Array.prototype.concat wrapper.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 an Array of Variables or a String or a Number. Get an Array of Variables or a String.

**Example Usage**:

```js
lists.append([1],[2]); /* [1,2] */ 
lists.append([1],2); /* [1,2] */ 
lists.append('a','b'); /* 'ab' */
```
------
<a name='head'></a>
## head : [x]|str -> x

**Description**: Retreive the first element of an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get a Variable.

**Example Usage**:

```js
lists.head([1,2]); /* 1 */ 
lists.head([[1,2],[3,4]]); /* [1,2]  */ 
lists.head('ab'); /* 'a' */
```
------
<a name='last'></a>
## last : [x]|str -> x

**Description**: Retreive the last element of an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get a Variable.

**Example Usage**:

```js
lists.last([1,2]); /* 2 */ 
lists.last([[1,2],[3,4]]); /* [3,4] */ 
lists.last('ab'); /* 'b' */
```
------
<a name='init'></a>
## init : [x]|str -> [x]

**Description**: Retreive all elements except the last of an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.init([1,2,3]); /* [1,2] */ 
lists.init([[1,2],[3,4],[5,6]]); /* [[1,2],[3,4]]  */ 
lists.init('abc'); /* ['a','b'] */
```
------
<a name='tail'></a>
## tail : [x]|str -> [x]

**Description**: Retreive all elements except the first of an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.tail([1,2,3]); /* [2,3] */ 
lists.tail([[1,2],[3,4],[5,6]]); /* [[3,4],[5,6]]  */ 
lists.tail('abc'); /* ['b','c'] */
```
------
<a name='nil'></a>
## nil : [x]|str -> boolean

**Description**: Test if an Array of Variables or a String is empty.

**Signature Definition**: Give arg 1 an Array of Variables or a String; Get a boolean.

**Example Usage**:

```js
lists.nil(null); /* true */ 
lists.nil([]); /* true */ 
lists.nil(''); /* true */ 
lists.nil('a'); /* false */ 
lists.nil([1]); /* false */
```
------
<a name='map'></a>
## map : [x]|str -> f -> [x]

**Description**: Array of Variables returned by applying f to each element of an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of Variables.

**Example Usage**:

```js
lists.map([1,2,3], function(x) { return x*2 }); /* [2,4,6] */
lists.map('abc', function(str) { return str.toUpperCase() }); /* ["A","B","C"] */
lists.map([{'S': 1}, {'u': 2}, {'p': 3}], function(obj) {
  return lists.flatten(lists.keys(obj))
}); /* ["S", "u", "p"] */
```
------
<a name='rev'></a>
## rev : [x]|str -> [x]

**Description**: Array of Variables returned by reversing the order of each element of an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.rev([1,2,3]); /* [3,2,1] */
lists.rev('abc'); /* ['c','b','a'] */
lists.rev([[2],[3]]); /* [[3],[2]] */
```
------
<a name='intersperse'></a>
## intersperse : x -> [x]|str -> [x]|str

**Description**: Array of Variables or a String returned by interspersing a given separator between elements of a given Array.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 an Array of Variables or a String. Get an Array of Variables or a String.

**Example Usage**:

```js
lists.intersperse(1,[5,5,5]); /* [5,1,5,1,5] */
lists.intersperse([1,2],[[6],[6]]); /* [[6],[1,2],[6]] */
lists.intersperse('b','ac'); /* 'abc' */
lists.intersperse({b:2},[{a:1},{b:3}]); /* [{a:1},{b:2},{c:3}] */
```
------
<a name='intercalate'></a>
## intercalate : [x] -> [[x]] -> [x]

**Description**: Array of Variables returned by flattening the result of interspersing an Array of Variables into an Array of an Array of Variables.

**Signature Definition**: Give arg 1 an Array of Variables. Give arg 2 an Array of an Array of Variables. Get an Array of Variables.

**Example Usage**:

```js
lists.intercalate([1],[[5],[5],[5]]); /* = lists.flatten(lists.intersperse([1],[[5],[5],[5]])) // [5,1,5,1,5] */
lists.intercalate(["abc"],[["efg"],["qrs"]]); /* ["efg", "abc", "qrs"] */
lists.intercalate([{a:1}],[[{b:1}],[{c:2}]]); /* [{b:1},{a:1},{c:2}] */
```
------
<a name='transpose'></a>
## transpose : [[x]] -> [[x]]

**Description**: Array of an Array of Variables returned by transposing rows and columns of given arguments.

**Signature Definition**: Give arg 1 an Array of an Array of Variables. Get an Array of an Array of Variables.

**Example Usage**:

```js
lists.transpose([[1,2,4],[3,4,4]]); /* [[1,3],[2,4],[4,4]] */
lists.transpose([["a","b","c"],["a","b","c"]]); /* [["a","a"],["b","b"],["c","c"]] */
```
------
<a name='subsequences'></a>
## subsequences : [x]|str -> [[x]]

**Description**: Array of an Array of Variables of all subsequences of a given arguement.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of an Array of Variables.

**Example Usage**:

```js
lists.subsequences('ab'); /* [[],['a'],['b'],['ab']] */
lists.subsequences([1,2,3]); /* [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]] */
```
------
<a name='permutations'></a>
## permutations : [x]|str -> [[x]]|[str]

**Description**: Array of an Array of Variables or Array of Strings returned by getting all permutations of a given arguement.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of an Array of Variables or an Array of Strings respectively.

**Example Usage**:

```js
lists.permutations('abc'); /* ["abc","acb","bac","bca","cab","cba"] */
lists.permutations([1,2,3]); /* [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]] */
```
------
<a name='foldl'></a>
## foldl : x -> [x]|str -> f -> x

**Description**: Variable returned reducing left to right by applying a binary operator Function (f) on a starting Variable (x), known as the accumulator, and an Array of Variables or a String.  

**Signature Definition**: Give arg 1 a starting Variable (usually a left identity of the binary operator). Give arg 2 an Array of Variables or a String. Give arg 3 a Function (binary operator). Get a Variable.

**Example Usage**:

```js
reverse = lists.foldl('','abc',function(x,y){ return y.concat(x); }); /* "cba" */
sum = lists.foldl(0,[1,2,3],function(x,y){ return x+y; }); /* 6 */
lists.foldl([], [[1,2],[3,4]], function(x,y) {return x.concat(y) }); /* [1,2,3,4] */
```
------
<a name='foldl1'></a>
## foldl1 : [x]|str -> f -> x

**Description**: Variant of foldl without a starting Variable (The accumulator begins with the 0th index of the passed Array of Variables or a String). Use with non-empty Arrays or Strings.

**Signature Definition**:  Give arg 1 an Array of Variables or a String. Give arg 2 a Function (binary operator). Get a Variable.

**Example Usage**:

```js
lists.foldl1('abc',function(x,y){ return x.concat(y).toUpperCase() }); /* "ABC" */
lists.foldl1([1,2,3],function(x,y){ return x+y }); /* 6 */
```
------
<a name='foldr'></a>
## foldr : x -> [x]|str -> f -> x

**Description**: Variable returned reducing right to left by applying a binary operator Function (f) on a starting Variable (x), known as the accumulator, and an Array of Variables or a String.  

**Signature Definition**: Give arg 1 a starting Variable (usually a right identity of the binary operator). Give arg 2 an Array of Variables or a String. Give arg 3 a Function (binary operator). Get a Variable.

**Example Usage**:

```js
lists.foldr(0,[1,2,3,4],function(x,y){ return x-y; }); /* -2 */
lists.foldr([],[[1,2],[3,4],[5,6]],function(x,y){ 
  return lists.rev(x).concat(y); 
}); /* [4,3,1,2,5,6] */
```
------
<a name='foldr1'></a>
## foldr1 : [x]|str -> f -> x

**Description**: Variant of foldr without a starting Variable (The accumulator begins with the 0th index of the passed Array or a String). Use with non-empty Arrays or Strings.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function (binary operator). Get a Variable.

**Example Usage**:

```js
lists.foldr1([1,2,3],function(x,y){ return x - y }); /* 3 */
lists.foldr1('aabbcc',function(x,y){ return x=='a'? x=y : x.concat(y)}); /* "bbcc" */
```
------
<a name='flatten'></a>
## flatten || concat : [[x]]|[str] -> [x]|str

**Description**: Flatten an Array of an Array of Variables or an Array of Strings into an Array of Variables or a String respectively.

**Signature Definition**: Give arg 1 an Array of an Array of Variables or an Array of Strings. Get an Array of Variables or a String.

**Example Usage**:

```js
lists.flatten(['abc']); /* 'abc' */
lists.flatten([[1,2],[3,4]]); /* [1,2,3,4] */
```
------
<a name='concatMap'></a>
## concatMap : [x]|str -> f -> [x]|str

**Description**: Array of Variables or a String returned by mapping a Function over an Array of Variables or a String and flattening the result.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function that produces an Array of Variables or a String. Get an Array of Variables or a String.

**Example Usage**:

```js
lists.concatMap(['bang','bang'], function(x){ return x+'!'}); /* "bang!bang!" */
lists.concatMap([1,2,3],function(x){ return [[x*2,x/2]] }); /* [[2,0.5],[4,1],[6,1.5]] */
lists.concatMap([{a:1},{b:2}], function(x){
  x.prop = 'hi';  
  return [x]
}); /* [{a:1,prop:"hi"},{b:2,prop:"hi"}]*/
```
------
<a name='and'></a>
## and : [boolean] -> boolean

**Description**: Boolean returned by the conjunction of an Array of booleans. True if all booleans are true. False if one or more booleans is false.

**Signature Definition**: Give arg 1 an Array of booleans. Get a boolean.

**Example Usage**:

```js
lists.and([5>1,5>2,5>3]); /* true */
lists.and([5>1,false,5>3]); /* false */
```
------
<a name='or'></a>
## or : [boolean] -> boolean

**Description**: Boolean returned by the disjunction of an Array of booleans. True if at least one boolean is true. False if all booleans are false.

**Signature Definition**: Give arg 1 an Array of booleans. Get a boolean.

**Example Usage**:

```js
lists.or([5<1,5<2,5>3]); /* true */
lists.or([5<1,5<2,5<3]); /* false */
```
------
<a name='any'></a>
## any : [x]|str -> f -> boolean

**Description**: Boolean returned by applying a predicate Function to each element in an Array of Variables or a String. True if at least one f(x) is true. False if all f(x) are false.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a predicate Function to be applied to each element of arg 1. Get a boolean.

**Example Usage**:

```js
lists.any([1,2,3],function(x) { return x < .5}); /* false */
lists.any('abc',function(x) { return x == 'b'}); /* true */
```
------
<a name='all'></a>
## all : [x]|str -> f -> boolean

**Description**: Boolean returned by applying a predicate Function to each element in an Array of Variables or a String. True if all f(x) are true. False if any f(x) are false.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a predicate Function to be applied to each element of arg 1. Get a boolean.

**Example Usage**:

```js
lists.all('abc', function(x){ return x==x.toUpperCase() }); /* false */
lists.all([2,4], function(x) { return x > 3 }); /* false */
lists.all([2,4], function(x) { return x%2==0 }); /* true */
```
------
<a name='sum'></a>
## sum : [num] -> num

**Description**: Number returned by summing the numbers of an Array together.

**Signature Definition**: Give arg 1 an Array of Numbers. Get a Number.

**Example Usage**:

```js
lists.sum([2,4,6]); /* 12 */
lists.sum([.2,.4,.6]); /* 1.2000000000000002 */
```
------
<a name='product'></a>
## product : [num] -> num

**Description**: Number returned by computing the product of the numbers of an Array.

**Signature Definition**: Give arg 1 an Array of Numbers. Get a Number.

**Example Usage**:

```js
lists.product([2,4,6]); /* 48 */
lists.product([.2,.4,.6]); /* 0.04800000000000001 */
```
------
<a name='maximum'></a>
## maximum : [num] -> num

**Description**: Maximum Number returned from numbers of an Array.

**Signature Definition**: Give arg 1 an Array of Numbers. Get a Number.

**Example Usage**:

```js
lists.maximum([2,4,6]); /* 6 */
lists.maximum([.2,.4,.6]); /* .6 */
```
------
<a name='minimum'></a>
## minimum : [num] -> num

**Description**: Minimum Number returned from numbers of an Array.

**Signature Definition**: Give arg 1 an Array of Numbers. Get a Number.

**Example Usage**:

```js
lists.minimum([2,4,6]); /* 2 */
lists.minimum([.2,.4,.6]); /* .2 */
```
------
<a name='maxList'></a>
## maxList : [[x]] -> [x]

**Description**: Array of Variables with the maximum length returned from an Array of an Array of Variables.

**Signature Definition**: Give arg 1 an Array of an Array of Variables. Get an Array of Variables.

**Example Usage**:

```js
lists.maxList([[1],[2,3]]); /* [2,3] */
lists.maxList([[1,2],[3]]); /* [1,2] */
```
------
<a name='minList'></a>
## minList : [[x]] -> [x]

**Description**: Array of Variables with the minimum length returned from an Array of an Array of Variables.

**Signature Definition**: Give arg 1 an Array of an Array of Variables. Get an Array of Variables.

**Example Usage**:

```js
lists.minList([[],[1]]); /* [] */
lists.minList([[1,2],[3]]); /* [3] */
```
------
<a name='scanl'></a>
## scanl : x -> [x]|str -> f -> [x]

**Description**: Array of Variables returned building left to right, starting with the accumulator (x) by applying a binary operator Function (f) on a starting Variable (x) and an Array of Variables or a String. 

**Signature Definition**: Give arg 1 a starting Variable. Give arg 2 an Array of Variables or a String. Give arg 3 a Function (binary operator). Get an Array of Variables.

**Example Usage**:

```js
lists.scanl('.','abc',function(x,y){return x + y}); /* [".",".a",".ab",".abc"] */
lists.scanl(0,[1,2,3],function(x,y){return x + y}); /* [0,1,3,6] */
```
------
<a name='scanr'></a>
## scanr : x -> [x]|str -> f -> [x]

**Description**: Array of Variables returned building right to left, starting with the accumulator (x) by applying a binary operator Function (f) on a starting Variable (x) and an Array of Variables or a String. 

**Signature Definition**: Give arg 1 a starting Variable. Give arg 2 an Array of Variables or a String. Give arg 3 a Function (binary operator). Get an Array of Variables.

**Example Usage**:

```js
lists.scanr('.','abc',function(x,y){return x + y}); /* ["abc.","bc.","c.","."] */
lists.scanr(0,[1,2,3],function(x,y){return x + y}); /* [6,5,3,0] */
```
------
<a name='mapAccumL'></a>
## mapAccumL : x -> [x]|str -> f -> [x, [x]]

**Description**: Builds an Array containing a accumulator (x) and the result of applying F to the supplied accumulator and each element of the supplied Array from left to right.

**Signature Definition**: Give arg 1 a starting Variable (accumulator). Give arg 2 an Array of Variables or a String. Give arg 3 a Function. Get an Array of Variable followed by Array of Variables.

**Example Usage**:

```js
lists.mapAccumL(5, [2,4,8], function(x,y){ return [x+y,x*y]}); /* [19, [10,28,88]]*/
lists.mapAccumL(5, [2,4,8], function(x,y){ return [y,y]}); /* [8, [2,4,8]] */
lists.mapAccumL(5, [5,5,5], function(x,y){ return [x,x]}); /* [5, [5,5,5]] */
```
------
<a name='mapAccumR'></a>
## mapAccumR : x -> [x]|str -> f -> [x, [x]]

**Description**: Builds an Array containing a accumulator (x) and the result of applying f to the supplied accumulator and each element of the supplied Array from right to left.

**Signature Definition**: Give arg 1 a starting Variable (accumulator). Give arg 2 an Array of Variables or a String. Give arg 3 a Function. Get an Array of Variable followed by Array of Variables.

**Example Usage**:

```js
lists.mapAccumR(5, [2,4,8], function(x,y){ return [x+y,x*y]}); /* [19, [34,52,40]]*/
lists.mapAccumR(5, [2,4,8], function(x,y){ return [y,y]}); /* [2, [2,4,8]] */
lists.mapAccumR(5, [5,5,5], function(x,y){ return [x,x]}); /* [5, [5,5,5]] */
```
------
<a name='iterate'></a>
## iterate : x -> num -> f -> [x]

**Description**: Builds an Array containing the successive application of f to the previous result of f(x) until the stop (num) reaches 0.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 a Number. Give arg 3 a Function. Get an Array of Variables.

**Example Usage**:

```js
lists.iterate('a',3,function(ch){return ch+'b'}); /* ["a","ab","abb"] */
lists.iterate([1,2],3,function(xs){return lists.intersperse(6,xs)}); /* [[1,2],[1,6,2],[1,6,6,6,2]] */
lists.iterate(2,4,function(x){ return x*x }); /* [2,4,16,256] */
```
------
<a name='replicate'></a>
## replicate : x -> num -> [x]

**Description**: Builds an Array containing replications of x until the stop (num) reaches 0.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 a Number. Get an Array of Variables.

**Example Usage**:

```js
lists.replicate(5,5); /* [5,5,5,5,5] */
lists.replicate([1,2],2); /* [[1,2],[1,2]] */
lists.replicate({a:1},2); /* [{a:1},{a:2}] */
```
------
<a name='cycle'></a>
## cycle : [x]|str -> num -> [x]|str

**Description**: Builds an Array containing replications of a flattened Array of Variables or a String until the stop (num) reaches 0.

**Signature Definition**: Give arg 1 an Array of Variables. Give arg 2 a Number. Get an Array of Variables.

**Example Usage**:

```js
lists.cycle('abc',3); /* "abcabcabc" */
lists.cycle([1,2],2); /* [1,2,1,2] */
```
------
<a name='unfold'></a>
## unfold : f -> f -> f -> x -> [x]|str

**Description**: Builds an Array from a seed value. Arg 1 is the predicate Function. If the predicate fails, return an empty Array, otherwise concatenate the result of Arg 2 (f) applied to Arg 4 (x) to the recursive call of unfold calling Arg 3 (f) to Arg 4 (x). This is a corecursive anamorphism.

**Signature Definition**: Give arg 1 an Function (predicate). Give arg 2 a Function. Give arg 3 a Function. Give arg 4 a Variable (seed).

**Example Usage**:

```js
function chop8(xs){ 
  return lists.unfold(lists.nil,lists.part(lists.take,8,undefined),lists.part(lists.drop,8,undefined),xs) 
}
chop8([1,2,3,4,5,6,7,8,9]); /* [[1,2,3,4,5,6,7,8],[9]] */

function unfoldMap(xs,f) { 
  return lists.unfold(
    lists.nil, 
    lists.part(lists.pipe(f,lists.head),undefined), 
    lists.part(lists.tail,undefined), 
    xs)
}
unfoldMap([1,2],function(x){ return x * 2 }); /* [2,4] */
```
------
<a name='take'></a>
## take : num -> [x]|str -> [x]

**Description**: Array of Variables returned by taking the first n (num) elements from an Array of Variables or a String.

**Signature Definition**: Give arg 1 a Number. Give arg 2 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.take(2,[1,2,3]); /* [1,2] */
lists.take(2,'abc'); /* ["a","b"] */
```
------
<a name='drop'></a>
## drop : num -> [x]|str -> [x]

**Description**: Array of Variables returned by dropping the first n (num) elements from an Array of Variables or a String.

**Signature Definition**: Give arg 1 a Number. Give arg 2 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.drop(2,[1,2,3]); /* [3] */
lists.drop(2,'abc'); /* ["c"] */
```
------
<a name='splitAt'></a>
## splitAt : num -> [x]|str -> [[x],[x]]

**Description**: Array of two Arrays returned. The first Array contains the first n elements of the supplied Array of Variables or a String. The second contains the rest.

**Signature Definition**: Give arg 1 a Number. Give arg 2 an Array of Variables or a String. Get an Array of two Arrays of Variables.

**Example Usage**:

```js
lists.splitAt(2,'abc') /* [['a','b'],['c']] */
lists.splitAt(2,[1,2,3]) /* [[1,2],[3]] */
```
------
<a name='takeWhile'></a>
## takeWhile : f -> [x]|str -> [x]

**Description**: Array of Variables returned by taking elements from an Array of Variables or a String that satisfy a supplied predicate Function until that predicate Function is unsatisfied.

**Signature Definition**: Give arg 1 a Function. Give arg 2 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.takeWhile([1,2,3,1], function(x){ return x < 3 }); /* [1,2] */
lists.takeWhile([1], function(x){ return x < 2 }); /* [1] */
lists.takeWhile('aabc', function(x){ return x =='a' }); /* ["a","a"] */
```
------
<a name='dropWhile'></a>
## dropWhile : f -> [x]|str -> [x]

**Description**: Array of Variables returned by dropping elements from an Array of Variables or a String that satisfy a supplied predicate Function until that predicate Function is unsatisfied.

**Signature Definition**: Give arg 1 a Function. Give arg 2 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.dropWhile([1,2,3,4], function(x){ return x < 3 }); /* [3,4] */
lists.dropWhile([1], function(x){ return x < 2 }); /* [] */
lists.dropWhile('aabc', function(x){ return x =='a' }); /* ["b","c"] */
```
------
<a name='span'></a>
## span : [x]|str -> f -> [[x], [x]|str]

**Description**: An Array of an Array of Variables and Array of Variables or a String (psuedo-tuple) is returned. The first element is the longest prefix of an Array of Variables or a String that satisfy a predicate Function f. The second element is the rest of the list.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of an Array of Variables and Array of Variables or a String (psuedo-tuple).

**Example Usage**:

```js
lists.span([1,2,3,4], function(x){return x < 3}); /* [[1,2],[3,4]] */
lists.span("abcde", function(x){return x == "a"}); /* [["a"],["b","c","d","e"]] */
lists.span([{a:2},{a:2},{b:2}], function(x){return x.a==2}); /* [[{a:2},{a:2}],[{b:2}]] */
```
------
<a name='break'></a>
## break : [x]|str -> f -> [[x], [x]|str]

**Description**: An Array of an Array of Variables and Array of Variables or a String (psuedo-tuple) is returned. The first element is the longest prefix of an Array of Variables or a String that do not satisfy a predicate Function f. The second element is the rest of the list.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of an Array of Variables and Array of Variables or a String (psuedo-tuple).

**Example Usage**:

```js
lists.break([1,2,3,4], function(x){return x < 3}); /* [[],[1,2,3,4]] */
lists.break("abcde", function(x){return x == "a"}); /* [[],"abcde"] */
lists.break([{a:2},{a:2},{b:2}], function(x){return x.a==2}); /* [[],[{a:2},{a:2},{b:2}]] */
```
------
<a name='stripPrefix'></a>
## stripPrefix : [num]|str -> [num]|str -> [num]|[str]

**Description**: Argument 1 is the prefix. Argument 2 is the target. The arguments must be of the same type. This function drops the prefix from the target and returns the representation as an Array of Numbers or an Array of Strings.

**Signature Definition**: Give arg 1 an Array of Numbers or a String. Give arg 2 an Array of Numbers or a String. Get an Array of Numbers or an Array of Strings.

**Example Usage**:

```js
lists.stripPrefix("abc","abcabce"); /* ["a","b","c","e"] */
lists.stripPrefix([1,2],[1,2,3,4]); /* [3,4] */
```
------
<a name='group'></a>
## group : [num]|str -> [[num]]|[[str]]

**Description**: An Array of an Array of Numbers or Strings returned where each nested Array contains only equal elements.

**Signature Definition**: Give arg 1 an Array of Numbers or a String. Get an Array of an Array of Numbers or Strings.

**Example Usage**:

```js
lists.group([1,1,2,3,3]); /* [[1,1],[2],[3,3]] */
lists.group("mississippi"); /* [["m"],["i"],["s","s"],["i"],["s","s"],["i"],["p","p"],["i"]] */
```
------
<a name='inits'></a>
## inits : [x]|str -> [[x]]

**Description**: An Array of an Array of Variables returned with all the initial segments of the argument, shortest first.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of an Array of Variables.

**Example Usage**:

```js
lists.inits([1,2,3]); /* [[],[1],[1,2],[1,2,3]] */
lists.inits("abc"); /* [[],["a"],["a","b"],["a","b","c"]] */
lists.inits([{a:2},{b:3}]); /* [[],[{a:2}],[{a:2},{b:3}]] */
```
------
<a name='tails'></a>
## tails : [x]|str -> [[x]]

**Description**: An Array of an Array of Variables returned with all the initial segments of the argument, longest first.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of an Array of Variables.

**Example Usage**:

```js
lists.tails([1,2,3]); /* [[1,2,3],[1,2],[1],[]] */
lists.tails("abc"); /* [["a","b","c"],["a","b"],["a"],[]] */
lists.tails([{a:2},{b:3}]); /* [[{a:2},{b:3}],[{a:2}],[]] */
```
------
<a name='isPrefixOf'></a>
## isPrefixOf : [num]|str -> [num]|str -> boolean

**Description**: Test if an Array of Numbers or a String is the prefix of an Array of Numbers or a String. The arguments must be of the same type.

**Signature Definition**: Give arg 1 an Array of Numbers or a String. Give arg 2 an Array of Numbers or a String. Get a boolean.

**Example Usage**:

```js
lists.isPrefixOf([1,2],[1,2,3]); /* true */
lists.isPrefixOf("abc","acd"); /* false */
lists.isPrefixOf("ab","abcd"); /* true */
```
------
<a name='isSuffixOf'></a>
## isSuffixOf : [num]|str -> [num]|str -> boolean

**Description**: Test if an Array of Numbers or a String is the suffix of an Array of Numbers or a String. The arguments must be of the same type.

**Signature Definition**: Give arg 1 an Array of Numbers or a String. Give arg 2 an Array of Numbers or a String. Get a boolean.

**Example Usage**:

```js
lists.isSuffixOf([1,2],[1,2,3]); /* false */
lists.isSuffixOf("cd","acd"); /* true */
lists.isSuffixOf("d","abcd"); /* true */
```
------
<a name='isInfixOf'></a>
## isInfixOf : [num]|str -> [num]|str -> boolean

**Description**: Test if an Array of Numbers or a String is the infix of an Array of Numbers or a String. The arguments must be of the same type.

**Signature Definition**: Give arg 1 an Array of Numbers or a String. Give arg 2 an Array of Numbers or a String. Get a boolean.

**Example Usage**:

```js
lists.isInfixOf([1,2],[1,3,2]); /* false */
lists.isInfixOf("cd","acde"); /* true */
lists.isInfixOf("a","abcd"); /* true */
```
------
<a name='isSubsequenceOf'></a>
## isSubsequenceOf : [num]|str -> [num]|str -> boolean

**Description**: Test if an Array of Numbers or a String is the subsequence of an Array of Numbers or a String. The arguments must be of the same type.

**Signature Definition**: Give arg 1 an Array of Numbers or a String. Give arg 2 an Array of Numbers or a String. Get a boolean.

**Example Usage**:

```js
lists.isSubsequenceOf([1,2],[1,3,2]); /* true */
lists.isSubsequenceOf("abc","123 abc"); /* true */
lists.isSubsequenceOf("Lol","Laugh out loud"); /* true */
```
------
<a name='elem'></a>
## elem : num|str -> [num]|str -> boolean

**Description**: Test if the Number or a String is in the Array of Numbers or a String.

**Signature Definition**: Give arg 1 a Number or a String. Give arg 2 an Array of Numbers or a String. Get a boolean.

**Example Usage**:

```js
lists.elem(2,[1,3,2]); /* true */
lists.elem("2","123 abc"); /* true */
```
------
<a name='notElem'></a>
## notElem : num|str -> [num]|str -> boolean

**Description**: Test if the Number or a String is not in the Array of Numbers or a String.

**Signature Definition**: Give arg 1 a Number or a String. Give arg 2 an Array of Numbers or a String. Get a boolean.

**Example Usage**:

```js
lists.notElem(0,[1,3,2]); /* true */
lists.notElem("a","abc"); /* false */
```
------
<a name='lookup'></a>
## lookup : num|str -> [[num|str,x]] -> boolean

**Description**: Retreive the value of a key in an Array of an Array of Variables where position 0 is the key and position 1 is the value (associative array).

**Signature Definition**: Give arg 1 a Number or a String. Give arg 2 an Array of an Array containing a Number or a String as the key and a Variable as the value. Get a Variable (value).

**Example Usage**:

```js
lists.lookup("a",[["a",2],["b",3]]); /* 2 */
lists.lookup("ab",[["ab",2],["b",3]]); /* 2 */
lists.lookup(1,[[1,{a:2}],["b",3]]); /* {a:2} */
```
------
<a name='find'></a>
## find : [x]|str -> f -> x

**Description**: Retreive a Variable by applying a predicate Function to an Array of Variables or a String. Returns "Nothing" if there is no match.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get a Variable.

**Example Usage**:

```js
lists.find([{a:2}], function(x) { return x.a == 2 }); /* {a:2} */
lists.find([[1,2]], function(x) { return x[0] == 1}); /* [1,2] */
lists.find([1,2,3], function(x) { return x == 0 }); /* "Nothing" */
```
------
<a name='filter'></a>
## filter : [x]|str -> f -> [x]

**Description**: An Array of Variables returned by applying a predicate Function to an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of Variables.

**Example Usage**:

```js
lists.filter([{a:1},{b:2}], function(obj) { return Object.keys(obj).length > 0 }); /* [{a:1},{b:2}] */
lists.filter("abc", function(char) { return char == "a" }); /* ["a"] */
lists.filter([[1],[1,2]], function(arr) { return arr.length > 1 }); /* [[1,2]] */
```
------
<a name='partition'></a>
## partition : [x]|str -> f -> [[x],[x]]

**Description**: An Array of two Arrays of Variables returned by applying a predicate Function to an Array of Variables. The Array of Variables at position 0 are the Variables that satisfy the predicate Function. The Array of Variables at position 1 are the Variables that do not satisfy the predicate Function.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of two Arrays of Variables.

**Example Usage**:

```js
lists.partition("Abc", function(char) { return char.startsWith("b") }); /* [["b"],["A","c"]] */
lists.partition([1,2,3,4], function(num) { return num % 2 == 0 }); /* [[2,4],[1,3]] */
lists.partition([{a:1},{b:2,a:2}], function(obj) { return obj.a == 2 }); /* [[{b:2,a:2}],[{a:1}]] */
```
------
<a name='bang'></a>
## bang : num -> [x] -> x

**Description**: Variable returned by fetching the Variable at the given index (Number).

**Signature Definition**: Give arg 1 a Number. Give arg 2 an Array of Variables. Get a Variable.

**Example Usage**:

```js
lists.bang(1,[0,{a:2},1]); /* {a:2} */
lists.bang(0,[[1,2],4]); /* [1,2] */
lists.bang(3,[1,2]); /* -1 */
```
------
<a name='elemIndex'></a>
## elemIndex || indexOf : num|str -> [num]|str -> num

**Description**: Returns the index Number of the first occurance of a Number or a String from an Array of Numbers or a String.

**Signature Definition**: Give arg 1 a Number or a String. Give arg 2 an Array of Numbers or a String. Get a Number.

**Example Usage**:

```js
lists.elemIndex(1,[1,2,1]); /* 0 */
lists.elemIndex("b","abc"); /* 1 */
lists.elemIndex(2,[0,1]); /* -1 */
```
------
<a name='elemIndices'></a>
## elemIndices : num|str -> [num]|str -> [num]

**Description**: Returns an Array of Numbers representing the indices of the Number or a String from an Array of Numbers or a String. 

**Signature Definition**: Give arg 1 a Number or a String. Give arg 2 an Array of Numbers or a String. Get an Array of Numbers.

**Example Usage**:

```js
lists.elemIndices(1,[1,2,1]); /* [0,2] */
lists.elemIndices("a","aba"); /* [0,2] */
lists.elemIndices(2,[0,1]); /* [] */
```
------
<a name='findIndex'></a>
## findIndex : [x]|str -> f -> num

**Description**: Returns the index Number of the first occurance of the result of applying a predicate Function to an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get a Number.

**Example Usage**:

```js
lists.findIndex([1,2,3], function(num){ return num % 2 == 0 }); /* 1 */
lists.findIndex([{a:2}], function(obj){ return obj.a == 2 }); /* 0 */
lists.findIndex("ab%c", function(char){ return char == "%" }); /* 2 */
```
------
<a name='findIndices'></a>
## findIndices : [x]|str -> f -> [num]

**Description**: Returns an Array of Numbers representing the indices of the result of applying a predicate Function to an Array of Variables or a String.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of Numbers.

**Example Usage**:

```js
lists.findIndices([1,2,3,4], function(num) { return num % 2 == 0 }); /* [1,3] */
lists.findIndices([{a:2},{b:3},{a:2}], function(obj) { return obj.a == 2 }); /* [0,2] */
lists.findIndices("AbAbA", function(char) { return char == "A" }); /* [0,2,4] */
```
------
<a name='zip'></a>
## zip || unzip : [[a,b,..,n],[c,d,..,n],..,n] -> [[a,c,..,n],[b,d,..,n],..,n]

**Description**: Takes an Array of an Array of Variables and returns an Array of an Array of Variables with corresponding Variables.

**Signature Definition**: Give arg 1 an Array of an Array of Variables. Get an Array of Variables.

**Example Usage**:

```js
lists.zip([[1,2],[3,4],[5,6]]); /* [[1,3,5],[2,4,6]] */
lists.zip(lists.zip([[1,2],[3,4],[5,6]])); /* unzip example [[1,2],[3,4],[5,6]] */
lists.zip([[1,'l'],[3,'o'],[5,'l']]); /* [[1,3,5],["l","o","l"]] */
```
------
<a name='zipWith'></a>
## zipWith : [[a,b,..,n],[c,d,..,n],..,n] -> f -> [x]

**Description**: Takes an Array of an Array of Variables and a Function and returns an Array of Variables with the results being the Function applied to the corresponding zipped Array of Variables.

**Signature Definition**: Give arg 1 an Array of an Array of Variables. Give arg 2 a Function. Get an Array of Variables.

**Example Usage**:

```js
lists.zipWith([[1,3],[1,2]],lists.sum); /* [2,5] */

function addThenMultiply(arr) {
  var res = 0; 
  lists.each(arr, function(num, i) {  
    i != 2 ? res += num : res *= num
  });
  return res;
}
lists.zipWith([[1,3],[1,2],[4,5]],addThenMultiply); /* [8, 25] */
```
------
<a name='lines'></a>
## lines : str -> [str]

**Description**: Returns an Array of Strings as the result of breaking a String at each new line character (\u000A). The resultant Array does not contain any new line characters.

**Signature Definition**: Give arg 1 a String. Get an Array of Strings.

**Example Usage**:

```js
lists.lines("l\no\nl"); /* ["l","o","l"] */
lists.lines("Hey\nthere"); /* ["Hey","there"] */
```
------
<a name='words'></a>
## words : str -> [str]

**Description**: Returns an Array of Strings as the result of breaking a String at each space character (\u0020). The resultant Array does not contain any space characters.

**Signature Definition**: Give arg 1 a String. Get an Array of Strings.

**Example Usage**:

```js
lists.words("break it up"); /* ["break","it","up"] */
```
------
<a name='unlines'></a>
## unlines : [str] -> str

**Description**: Returns a String with a new line character appended to each String of the Array that it joins.

**Signature Definition**: Give arg 1 an Array of Strings. Get a String.

**Example Usage**:

```js
lists.unlines(["break","it","up"]); /* "break\nit\nup\n" */
```
------
<a name='unwords'></a>
## unwords : [str] -> str

**Description**: Returns a String with a space character appended to each String of the Array that it joins.

**Signature Definition**: Give arg 1 an Array of Strings. Get a String.

**Example Usage**:

```js
lists.unwords(["break","it","up"]); /* "break it up " */
```
------
<a name='nub'></a>
## nub || uniq || unique : [num|str]|str -> [num|str]

**Description**: Remove duplicates from a String or an Array of Numbers and/or Strings. Keep the first occurence of each element.

**Signature Definition**: Give arg 1 a String or an Array of Numbers and/or Strings. Get an Array of Numbers and/or Strings.

**Example Usage**:

```js
lists.nub("abbc"); /* ["a","b","c"] */
lists.nub([1,2,"a","b","a",1]); /* [1,2,"a","b"] */
lists.nub([1,2,2,3]); /* [1,2,3] */ 
```
------
<a name='delete'></a>
## delete : x -> [x]|str -> [x]

**Description**: Return an Array of Variables from the result of removing the first occurence of a Variable from an Array of Variables or a String. Does not work with Objects.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.delete('a','bab'); /* ["b","b"] */
lists.delete([1],[[1,2],[1]]); /* [[1,2]] */
lists.delete(1,[2,1,2,1]); /* [2,2,1] */ 
```
------
<a name='difference'></a>
## difference || diff : [num|str]|str -> [num|str]|str -> [x]

**Description**: Return an Array of Variables whose elements are the difference between Argument 1 and Argument 2.

**Signature Definition**: Give arg 1 a String or an Array of Numbers and/or Strings. Give arg 2 a String or an Array of Numbers and/or Strings. Get an Array of Variables.

**Example Usage**:

```js
lists.difference(['acd',1],['acd']); /* [1] */
lists.difference('acd','ab'); /* ["c","d"] */
lists.difference([1,2],[1,2]); /* [] */ 
```
------
<a name='union'></a>
## union : [num|str]|str -> [num|str]|str -> [x]|str

**Description**: Return an Array of Variables whose elements are the union between Argument 1 and Argument 2.

**Signature Definition**: Give arg 1 a String or an Array of Numbers and/or Strings. Give arg 2 a String or an Array of Numbers and/or Strings. Get an Array of Variables or a String.

**Example Usage**:

```js
lists.union("a","b"); /* "ab" */
lists.union([1,4,'a'],[1,3,'b']); /* [1,4,"a",3,"b"] */
```
------
<a name='intersect'></a>
## intersect : [num|str]|str -> [num|str]|str -> [x]

**Description**: Return an Array of Variables whose elements are the intersection between Argument 1 and Argument 2.

**Signature Definition**: Give arg 1 a String or an Array of Numbers and/or Strings. Give arg 2 a String or an Array of Numbers and/or Strings. Get an Array of Variables.

**Example Usage**:

```js
lists.intersect('a','ba'); /* ["a"] */
lists.intersect([1,4,'a'],[1,3,'b']); /* [1] */
```
------
<a name='sort'></a>
## sort : [x]|str -> [x]

**Description**: Return an Array of Variables that are sorted by the Ordering Function `lists.compare`.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Get an Array of Variables.

**Example Usage**:

```js
lists.sort('acb'); /* ["a","b","c"] */
lists.sort([[3,4],[1,2]]); /* [[1,2],[3,4]] */
lists.sort([2,1,-1,1]); /* [-1,1,1,2] */
```
------
<a name='insert'></a>
## insert : x -> [x] -> [x]

**Description**: Inserts an element into the first position of the Array of Variables where the element is less than or equal (defined by `lists.compare`) to the Variable from the Array it is being compared to. 

**Signature Definition**: Give arg 1 a Variable. Give arg 2 an Array of Variables. Get an Array of Variables.

**Example Usage**:

```js
lists.insert(1,[2,1,2]); /* [1,2,1,2] */
lists.insert(4,[1,3,5,7,9]); /* [1,3,4,5,7,9] */
```
------
<a name='nubBy'></a>
## nubBy : [x]|str -> f -> [x]

**Description**: Remove duplicates from an Array of Variables or a String based on a user supplied Function defintion of equality. Keep the first occurence of each element. 

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of Variables.

**Example Usage**:

```js
lists.nubBy([8,7,5,3,2], function(x,y) { return x + y == 10 }); /* [8,7,5] */
lists.nubBy(["query=string, another=string","query=string, hey=man"], function(x,y) { 
  return x.split(',')[0] == y.split(',')[0]; // define equality on query=string 
}); /* ["query=string, another=string"] */
lists.nubBy([{a:1},{a:1, b:2},{b:2}], function(obj1, obj2) { 
  return obj1.b == obj2.b; // define equality on the b property
}); /* [{a:1},{a:1, b:2}] */
```
------
<a name='deleteBy'></a>
## deleteBy : x -> [x]|str -> f -> [x]

**Description**: Return an Array of Variables from the result of removing the first occurence of a Variable or a String that matches a user supplied Function definition of equality from an Array of Variables.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 an Array of Variables. Give arg 3 a Fucntion. Get an Array of Variables.

**Example Usage**:

```js
lists.deleteBy(4, [6,8,10,12], function(arg1,y) { return y % arg1 == 0 }); /* [6,10,12] */
lists.deleteBy(2, [{a:2},{b:2,e:2},{c:2}], function(arg1, obj) { return lists.keys(obj).length == arg1 }); /* [{a:2},{c:2}] */
```
------
<a name='deleteFirstsBy'></a>
## deleteFirstsBy : [x]|str -> [x]|str -> f -> [x]

**Description**: Return the first Array of Variables or String passed with the first occurence of each element from the second Array of Variables or String removed based on a user supplied Function definition of equality.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 an Array of Variables or a String. Give arg 3 a Fucntion. Get an Array of Variables.

**Example Usage**:

```js
lists.deleteFirstsBy([1,2,3,4,3],[3], function(x,y) { return x==y }); /* [1,2,4,3] */
lists.deleteFirstsBy("baba","a", function(x,y) { return x==y }); /* ["b","b","a"] */
```
------
<a name='unionBy'></a>
## unionBy : [x] -> [x] -> f -> [x]

**Description**: Return an Array of Variables as the union between Argument 1, Argument 2, and the user supplied Function definition of equality.

**Signature Definition**: Give arg 1 an Array of Variables. Give arg 2 an Array of Variables. Give arg 3 a Fucntion. Get an Array of Variables.

**Example Usage**:

```js
lists.unionBy([1,2,3,4],[4,6,9,10], function(x,y) { return x * 3 == y }); /* [1,2,3,4,4,10] */
lists.unionBy(["a","b","c"], ["d","e","f"], function(x,y) { 
	var same = y == 'd' ? 'a' : y; 
	return x == same; // "d" is the same as "a"
}); /* ["a","b","c","e","f"] */
```
------
<a name='intersectBy'></a>
## intersectBy : [x]|str -> [x]|str -> f -> [x]

**Description**: Return an Array of Variables as the intersection between Argument 1, Argument 2, and the user supplied Function definition of equality.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 an Array of Variables or a String. Give arg 3 a Fucntion. Get an Array of Variables.

**Example Usage**:

```js
lists.intersectBy([1,2,3,4],[4,8,12,16,20], function(x,y) { return x * x == y }); /* [2,4] */
```
------
<a name='groupBy'></a>
## groupBy : [x]|str -> f -> [[x]]

**Description**: Return an Array of Variables where each nested Array is a group of equal elements. Equality is defined by the user supplied Function.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Fucntion. Get an Array of an Array of Variables.

**Example Usage**:

```js
lists.groupBy([1,2,3,4,5,6,7,8,9], function(x,y){ return ((x*y) % 3) == 0}); /* [[1],[2,3],[4],[5,6],[7],[8,9]] */
lists.groupBy([1,2,3,4,5,6,7,8,9], function(x,y){ return x + 1 == y}); /* [[1,2],[3,4],[5,6],[7,8],[9]] */
```
------
<a name='sortBy'></a>
## sortBy : [x]|str -> f -> [x]

**Description**: Return an Array of Variables that are sorted based on the user supplied Ordering Function.

**Signature Definition**: Give arg 1 an Array of Variables or a String. Give arg 2 a Function. Get an Array of Variables.

**Example Usage**:

```js
function oddsFirst(x,y) { 
	return x % 2 == 1 ? 'LT' : 'GT'
}
lists.sortBy([1,2,3,4,5,6,7], oddsFirst); /* [1,3,5,7,6,4,2] */
```
------
<a name='insertBy'></a>
## insertBy : x -> [x]|str -> f -> [x]

**Description**: Inserts an element into the first position of the Array of Variables based on the user supplied Ordering Function.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 an Array of Variables or a String. Give arg 3 a Function. Get an Array of Variables.

**Example Usage**:

```js
function fn(x,y) { 
	return (x+y) < (x*y) ? 'LT' : 'GT'
}
lists.insertBy(4, [0,1,3,5,7,9], fn); /* [0,1,4,3,5,7,9] */
```
------
<a name='maximumBy'></a>
## maximumBy : [x]|str -> f -> x

**Description**: The largest element of a non-empty Array of Variables or a String where the definition of "largest" comes from the user supplied Ordering function.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 an Array of Variables or a String. Give arg 3 a Function. Get an Array of Variables.

**Example Usage**:

```js
lists.maximumBy([[1,3],[2]], lists.compare); /* [2] */
function compareLength(x,y) { 
	return  x.length > y.length ? 'GT' : 'LT'
}
lists.maximumBy([[1,3],[2]], compareLength); /* [1,3] */
```
------
<a name='minimumBy'></a>
## minimumBy : [x]|str -> f -> x

**Description**: The least element of a non-empty Array of Variables or a String where the definition of "least" comes from the user supplied Ordering function.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 an Array of Variables or a String. Give arg 3 a Function. Get an Array of Variables.

**Example Usage**:

```js
lists.minimumBy([[1,3],[2]], lists.compare); /* [1,3] */
function compareLength(x,y) { 
	return  x.length > y.length ? 'GT' : 'LT'
}
lists.minimumBy([[1,3],[2],[]], compareLength); /* [] */
```
------
<a name='genericExcludeChar'></a>
## genericExcludeChar : str -> str -> [str]

**Description**: Strips an arbitrary character (String) from a String. This function is the primary work horse of `lists.lines` and `lists.words`.

**Signature Definition**: Give arg 1 a String. Give arg 2 a String. Get a an Array of Strings.

**Example Usage**:

```js
lists.genericExcludeChar("a","abc"); /* ["bc"] */

function myLines(str) { return lists.genericExcludeChar('\u000A', str); };
myLines("abc\nd"); /* ["abc","d"] */
```
------
<a name='each'></a>
## forEach || each : x -> f -> x

**Description**: An enhanced polyfill of Array.prototype.forEach. Works for properties of Objects. This function is meant to alter mutable state.

each's arguments are:

Argument 1: Iterable Variable.
Argument 2: Function.
Argument 3: (optional) Caller (or context).

When called, each applies the Function to each iterable Variable with its optional caller. 

The Function's arguments are: 

Argument 1: The Variable of the iteration at the specific index.
Argument 2: The index at that specific iteration.
Argumnet 3: The original iterable Variable.

The original (unchanged) iterable Variable is returned.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 a Function. (optionally) Give arg 3 a Caller (this, self, etc.). Get a Variable.

**Example Usage**:

```js
var arr = [];
lists.forEach([1,2,3], function(num, index, array123) {
	arr.push(num * 2);
}); /* [1,2,3] */

console.log(arr); /* [2,4,6] */
```
------
<a name='keys'></a>
## keys : obj -> [str]

**Description**: A polyfill of `Object.keys`. Returns an Array of Strings representing the iterable properties of the Object not from its inherited chained properties.

**Signature Definition**: Give arg 1 an Object. Get an Array of Strings.

**Example Usage**:

```js
lists.keys({a:2, b:1}); /* ["a","b"] */
```
------
<a name='enum'></a>
## enumeration || enum : num -> num -> [num]

**Description**: Create an enumeration in the form of an Array of Numbers where Argument 1 is the start Number and Argument 2 is the stop Number.

**Signature Definition**: Give arg 1 a Number. Give arg 2 a Number. Get an Array of Numbers.

**Example Usage**:

```js
lists.enum(0,5); /* [0,1,2,3,4,5] */
```
------
<a name='pipe'></a>
## composeL || pipe : f[,..,f] -> f

**Description**: Return a Function that represents the composition of Functions passed as Arguments. These Functions will be applied from rightmost to leftmost to the returned Function's Argument.

**Signature Definition**: Give arg 1 N number of Functions. Get a Function.

**Example Usage**:

```js
var sumThenSqrt = lists.pipe(Math.sqrt, lists.sum);
sumThenSqrt([4,4,4,4]); /* 4 */
```
------
<a name='sequence'></a>
## composeR || sequence : f[,..,f] -> f

**Description**: Return a Function that represents the composition of Functions passed as Arguments. These Functions will be applied from leftmost to rightmost to the returned Function's Argument.

**Signature Definition**: Give arg 1 N number of Functions. Get a Function.

**Example Usage**:

```js
var sumThenSqrt = lists.sequence(lists.sum, Math.sqrt);
sumThenSqrt([4,4,4,4]); /* 4 */
```
------
<a name='partial'></a>
## partial || part : f -> x[,..,x] -> f

**Description**: Return a partially applied Function where any number of a Function's arguments may be left undefined using `undefined` as a filler variable to be filled when the Function is called.

**Signature Definition**: Give arg 1 a Function. Give arg 2,..,n a filled or unfilled Variable. Get a Function.

**Example Usage**:

```js
var myAny = lists.part(lists.any, undefined, function(x) { return x == 1 });
myAny([1,2]); /* true */
myAny([2]); /* false */
```
------
<a name='flip'></a>
## flip : f -> f

**Description**: Return an equivalent Function whose arguments are 'flipped' or reversed.

**Signature Definition**: Give arg 1 a Function. Get a Function.

**Example Usage**:

```js
var flippedAny = lists.flip(lists.any);
flippedAny(function(x){return x == 1}, [1,2]); /* true */
```
------
<a name='compare'></a>
## compare : x -> x -> str

**Description**: The only Ordering Function provided in Lists. Returns a String that is the representation of comparing both Arguments with the native JavaScript comparator operators. Ordering Functions are used to redefine how Variables are ordered.

**Signature Definition**: Give arg 1 a Variable. Give arg 2 a Variable. Get a String.

**Example Usage**:

```js
lists.compare(1,2); /* "LT" */
lists.compare(2,1); /* "GT" */
lists.compare("b","b"); /* "EQ" */
```
------
<a name='bubbleSort'></a>
## bubbleSort : [num] -> [num]

**Description**: A generic bubblesort algorithm for sorting an Array of Numbers.

**Signature Definition**: Give arg 1 an Array of Numbers. Get an Array of Numbers.

**Example Usage**:

```js
lists.bubbleSort([3,2,5,1]); /* [1,2,3,5] */
```
------
<a name='mergeSort'></a>
## mergeSort : [num] -> [num]

**Description**: A generic mergesort algorithm for sorting an Array of Numbers.

**Signature Definition**: Give arg 1 an Array of Numbers. Get an Array of Numbers.

**Example Usage**:

```js
lists.mergeSort([3,2,5,1]); /* [1,2,3,5] */
```
------
