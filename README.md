<img src="https://lh6.googleusercontent.com/-g15IPO9l9Rg/T9WNrqWeEiI/AAAAAAAAA54/U4qyuu_4npw/s800/coffee-icon128-by-aha-soft-license-free-NC.png" style="border:0px; margin:10px; margin-right:30px; float:left;">


#CoffeeMug - A concise, hands-on CoffeeScript Tutorial
##### *Now delivered with a cup of hot Coffee*

---

**author:** Lorenz Lo Sauer 2011 ( http://www.lsauer.com , @sauerlo), `CC-BY-SA 3` <img src="https://lh3.googleusercontent.com/-VTWii3A45L0/T9TRbQY9unI/AAAAAAAAA5k/eYik-kXRzUw/s800/cc_by_sa.png" style="border:0px;">

**description:** a concise tutorial for JavaScript, R or Python programmers

**about:** CoffeeScript (CS), released in 2010 by J. Ashkenas (@jashkenas), is dynamically typed, interpreted programming language. CS takes syntax inspirations from popular dynamic languages such as Haskell, JavaScript, Erlang, Perl, Python, Ruby and even YAML.

**release:** https://github.com/lsauer/coffeemug

**note:** 

- the tutorial is an excerpt from a free book: http://www.lsauer.com/2012/05/scalable-web-application-development.html - which is to be released soon.
- a brief overview of CoffeeScript's Pros and Cons is provided at the end
- if `toSource()` is missing on a specific JS-engine, simply declare `Object::toSource or= -> JSON.stringify this`
- live editor and more information at: http://coffeescript.org/
- share your mug of coffee!

**todo:** inline code experiments

---

*Following, the main aspects of CoffeeScript are demonstrated through short examples and accompanying notes.*

## 1.0 Basics
###1.1 Comments: via Hashes(`#`),similar to Python and Ruby

```coffeescript	
	#This line is commented out
	###
	Block comment similar to the popular syntax: `/*...*/`
	###
	a =3; `/*b=2*/`; c=1; #`b=2` is commented out
```
	
###1.2 Variable assignment - one per line!
####set multiple statements per line via line-termination `;`

```coffeescript	
	Integer = 42; str = 'test'
	a=10; b=5
	boolval = true
	objKey : 'objValue'
	c = obj : (k1:1, k2:'omg')
	a = 1, b = 2 #Error: unexpected ',' ...
```

###1.3 Nesting: CS is indentation sensitive!
####Nested Objects

```coffeescript	
	Point =
	  coord :
		 x : 100
		 y : 200
```
	
####Example: without proper identation, 'obj' is packed into 'c'

```coffeescript	
	c =
	objKey : 'objValue', objKey2 : .0
	obj : (k1:1, k2:'omg')
	;obj : (k1:1, k2:'omg') #'expected' behavior
	alert JSON.stringify(c)
```
	


####1.4 Variable assignment: Switching values via 'destructured assignment'

```coffeescript	
	alert [a,b] = [b,a]
	alert 0||3, 0 or 1, 0||(a=3) #logical-or operator; JS's comma ','-operator
	alert a
```
	

#####compute and asssign

```coffeescript	
	six = (one = 1) + (two = 2) + (three = 3) #results in `6`
	alert [one, two, three, two * three]
```

####Conditions / conditional assignment:

```coffeescript	
	integer = 42 if true

	if happy and knowsIt
	  clapsHands()
	  chaChaCha()
	else
	  showIt()
	
	options or= defaults #in JS: options || (options = defaults);
	
	eldest = if 24 > 21 then "Liz" else "Ike"
```
	

###1.5 Functions and variables: assigned according to lexical scope
####functions are executed in closures

```coffeescript	
	square = (x) -> x * x
```

####passing closures

```coffeescript	
	compute = (fn) -> alert fn()
	num = compute( -> window.x*10 )
	num = compute( (x) -> x*x )
```

####Anonymous functions:

```coffeescript	
	do -> x=5; x*x
```

####Arguments: Default values

```coffeescript	
	fill = (container, liquid = "coffee") -> ...
```

####'traditional' (i.e. bracketed) function invocation syntax

```coffeescript	
	alert( Object.toString(c))
```

####Arguments: splat-operator `...`:

```coffeescript	
	race = (winner, runners, others...) ->
	  print winner, others
```

#####expands after JavaScript transcompilation, to:
```javascript
    arguments[0], runners = 2 <= arguments.length ? __slice.call(arguments, 1) : [];
```
	  
	  
####Closures: bracket-operator `(...)` as a closure wrapper

```coffeescript	
	for filename in list
	  do (filename) ->
		fs.readFile filename, (err, contents) ->
		  compile filename, contents.toString()
```


###Implicit `return` of the last line within a block-statement: i.e. `R`-language like

```coffeescript	
	grade = (student) ->
	  if student.excellentWork
		"A+"
	  else if student.okayStuff
		if student.triedHard then "B" else "B-"
	  else
		"C"
```
	
###1.6 Arrays:

```coffeescript	
	list = [1, 2, 3, 4, 5]
```

#####smart multiline expansion 

```coffeescript	
	list =[1
	       2
	       3]
```

####slices

```coffeescript	
	numbers = [1,2,3,4,5]
	alert [1,2,3,4,5][0...3] #1,2,3
```


####copy

```coffeescript	
	copy    = numbers[0...numbers.length]
	arr[0...3] 	#JS: `arr.slice(0, 3)`
	arr[0..3] 	#JS: `arr.slice(0, 4)`
	numbers[3..6] = [-3, -4, -5, -6]
```


####Bitlists (increases readability of WebGL, etc.. -code)

```coffeescript	
	bitlist = 
	[ 1, 0
	  0, 0 ]
```

###1.7 JS's Bitwise operators: `| & ! ~ << >>`
###1.8 Trinity operator: Pythonian verbatim style

```coffeescript	
	date = if friday then sue else jill 
```

####'traditional' trinity operator performs as expected

```coffeescript	
	date = friday ? sue : jill 
```

####trinity operator in conditional assignment 

```coffeescript	
	typeof friday !== "undefined" && friday !== null ? friday : {sue: jill}
```

###1.9 Objects:

```coffeescript	
	math =
	  root:   Math.sqrt
	  square: square
	  cube:   (x) -> x * square x
```

####JSON Syntax

```coffeescript	
	singers = {Jagger: "Rock", Elvis: "Roll"}
```

#####Sidenote: Resolving JS-reserved name conflicts

```coffeescript	
	$('.account').attr class: 'active'
```


###1.10 Existence operator: `?` (i.e. not null or undefined):

```coffeescript	
	alert "I knew it!" if elvis?
```


##2.0 Looping and conditional statements
###2.1 Array comprehensions:

```coffeescript	
	cubes = (math.cube num for num in list)
	log 'current element:', food for food in ['toast', 'cheese', 'wine']
```

#### Loop conditions

```coffeescript	
	alert food for food in foods when food isnt 'chocolate'
```
#### Loop nesting

```coffeescript	
	plotPoint i for food in Points.x for j in Points.y for k in Points.z
```

####Example: The first ten properties of the global object `window`:

```coffeescript	
	globals = (name for name of window)[0...10]
```
	
#### Array-`ranges` with keyword `by`, to define the range-step. conditions are possible

- in JS, similar results can be obtained through `forEach`, `map`, `filter`, `apply`

```coffeescript	
  countdown = x:(num for num in [10..1]), y:(num for num in [0..10] by 2)
  #returns: {'x':[10,9,8,7,6,5,4,3,2,1], 'y': [0,2,4,6,8,10]}
```

###2.2 foreach loop:

```coffeescript	
	ages = for key, val of [x: 10, y: 100]
	"key: #{key} has value: #{val}"
```

####to check for hasOwnProperty...

```coffeescript	
	for own key, value of object
```


###2.3 while loop:

```coffeescript	
	if this.studyingEconomics
	  buy()  while supply > demand
	  sell() until supply > demand

	i=10; lyrics = while i--
	  "#{num} little monkeys, jumping on the bed.
		One fell out and bumped his head on the bed.\n"
```


###2.4 switch statement

```coffeescript	
	switch day
	  when "Mon", "Tue" then go work
	  else go work	#default
```



##3.0 CoffeScript Operators

- CS abolishes the transitive or implicit equality operator: `==` turns into (`→`) `===`

###3.1 Comparison:
	# `== → === ; != → !== ; is → === , isnt → !===`

###3.2 Boolean operators and aliases
	# not → ! ; and → && ; or → || ; bitwise: ~ | & << >> >>>
	# on → true ; yes → true ; off→ false; no → false (YAML) ; unless ... → if(!...)

###3.3 Conditional operators and *`@`* as `this-operator`

```coffeescript	
	# `then → while:if/else... switch/case`
	# `@ → this; this → this`
	Account = (customer, cart) ->
	  @customer = customer
	  @cart = cart
```


####Expressing the example above as JavaScript, the code expands to:

```coffeescript	
	Account = function(customer, cart) {
          this.customer = customer; return this.cart = cart;
	};
```


###3.3 `in` operator

```coffeescript	
	# `of → in` ; `in` → has no JS equivalent, see below
	winner = yes if pick in [47, 92, 13]
```


###3.4 chained comparison `x > y > z...`

```coffeescript	
	cholesterol = 127
	healthy = 200 > cholesterol > 60
	alert 10>2>3>1>-4>-7 #false
```


###3.5 `Existential` Operator `?` and `?.` overcomes JS's unassigned variable Errors

```coffeescript	
	mindexists = true if mind? and not world?
	ifspeedexistssetto ?= 75
	footprints = yeti ? "bear"
```

####OOP: Existantial Operator  `?.` for methods and attributes; 'soaks up' *`undefined`* Errors

```coffeescript	
	getattributeevenifMIA = starsystem.drawPlanet?().atmosphere?.constitution
```


####check for `b`'s existence and invoking b with window as an argument

```coffeescript	
	a = b? window #JS: a = typeof b === "function" ? b(window) : void 0;
```

####check for `b`'s existence assigning `b` or alternativly `window` 

```coffeescript	
	a = b ? window  #JS:a = typeof b !== "undefined" && b !== null ? b : window;
```



###3.6 Operator overview

<table>
      <tbody><tr><th>CoffeeScript</th><th>JavaScript</th></tr>
      <tr><td><tt>is</tt></td><td><tt>===</tt></td></tr>
      <tr><td><tt>isnt</tt></td><td><tt>!==</tt></td></tr>
      <tr><td><tt>not</tt></td><td><tt>!</tt></td></tr>
      <tr><td><tt>and</tt></td><td><tt>&amp;&amp;</tt></td></tr>
      <tr><td><tt>or</tt></td><td><tt>||</tt></td></tr>
      <tr><td><tt>true, yes, on</tt></td><td><tt>true</tt></td></tr>
      <tr><td><tt>false, no, off</tt></td><td><tt>false</tt></td></tr>
      <tr><td><tt>@, this</tt></td><td><tt>this</tt></td></tr>
      <tr><td><tt>of</tt></td><td><tt>in</tt></td></tr>
      <tr><td><tt>in</tt></td><td><i><small>no JS equivalent</small></i></td></tr>
</tbody></table>


###3.7 Examples

```coffeescript	
	stop() if idlemode is on
	letTheWildRumpusBegin() unless answer is no
	if car.speed < limit then accelerate()
	if car.speed < limit
	  accelerate()

	winner = yes if pick in [47, 92, 13]
	print inspect "My name is #{@name}"
```



##4.0 Object oriented programming in CS

- CS provides **OOP** through prototypal '*wrapping*'
- CS provides *named classes*, *inheritance*
- `super` invokes the superclass constructor

###4.1 Classes

```coffeescript	
	class Animal
	  constructor: (@name) ->
	  move: (meters) ->
		alert @name + " moved #{meters}m."
```


###4.2 Inheritance

```coffeescript	
	class Snake extends Animal
	  move: ->
		alert "Slithering..."
		super 5

	sam = new Snake "Sammy the Python"
	sam.move()
```


###4.3 Method assignment

```coffeescript	
	String::dasherize = ->
	  this.replace /_/g, "-"
```


###4.4 Function Binding: declaration and binding via the fat arrow *`=>`* operator


```coffeescript	
	#event-closure is called in the DOM-context of the clicked element
	$('.shopping_cart').bind 'click', (event) =>
	@customer.purchase @cart
```


##5.0 Advanced CS

###5.1 Destructured Assignment to any degree of complexity

```coffeescript	
	getPoint2D = (hexpos) ->
	  # Do computation... w. obj = {metadata:[h,s,l]}
	  [x, y, obj]

	[x, y, {metadata:[h,s,l]}] = getPoint2D "#223322"
```


####Destructured Assignment with splats

```coffeescript	
	tag = "<omics>"
	[firstletter,tagname...,lastletter] = tag.split("")
	console.log tagname.join() #omics
```



###5.2 Backtick Operator `...`: Pass through abitrary Javascript code

```coffeescript	
	hi = `function() {
	  return [document.title, "Hello JavaScript"].join(": ");
	}`
```



###5.3 Strings and Multiline strings
####Double-Quoted strings can extend over several lines (already shown) 
####interpolation via `#{...}` (**Ruby**-like)

```coffeescript	
	author = "Wittgenstein"
	quote  = "A picture is a fact. -- #{ author }"

	sentence = "#{ 22 / 7 } is a decent approximation of p"
```

#####`Heredoc` syntax

```coffeescript	
	html = """
		   <strong>
			 cup of coffeescript
		   </strong>
		   """
	#in JS: html = "<strong>\n  cup of coffeescript\n</strong>";
```


###5.3.1 Non-interpolated Multiline Comment Block

```coffeescript	
	###
	CoffeeScript Compiler v1.2.0
	Released under the MIT License
	###
```


	
###5.4 `Heregexes`: Heredoc-Regexes to comment-out complex Regular Expressions

```coffeescript	
	OPERATOR = /// ^ (  #starting with
		[^J]   #must not contain J i.e. letter absent from the periodic table
		[0-9   #cyclic connection quantifier and charge; e.g. [Co+3] or [Co+++]
		...
	) ///

```



###5.5 Error Handling
####CS does not type-conditional Error handling (yet)

```coffeescript	
	try
	  func()
	catch error
	  print error
	finally
	  cleanUp()
```


#### error handling inside a function call e.g. useful for JSONP

```coffeescript	
	alert(
	  try
		nonexistent / undefined
	  catch error
		"And the error is ... #{error}"
	)
```


<br />
	
---
##**Tutorial comment**

The tutorial is based on the great official tutorial provided by CoffeScript, and will be continuously improved by me and helpful others on github.

Any contributions and suggestions are always welcome.

---

##Pros and Cons of CoffeeScript

###**Pros:** 

- compact, typically 30% less code
- faster to write, with a more keyboard accessible character-set
- extends the powerful JavaScript language
- Class-based and prototypal inheritance model
- overcomes Javascript pitfalls
- slight performance increase through greater abstraction and encapsulation
- limited additional CS compiler error checking

###**Cons:** 

- harder to debug as the faulty Javascript code has to be traced back to CS
- additional 'language stack' increases complexity
- early adoption means less software infrastructure is available at the moment
- might decrease someones proficiency of Javascript over time 
