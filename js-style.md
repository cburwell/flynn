JavaScript Style Guide
======================

This guide doesn't cover everything as such a document is far too large. A
style guide should only take a few minutes to go over, not a few hours. The aim
here is to set the bare minimum amount of rules to produce consistent code.
This document will be modified as needed.

## Basics

1. Each project must contain a jshintrc file, and it's a good idea to setup
	 [jsxhint](http://www.jsxhint.com/) to run on save.

2. Use a single tab for indentation:

	```javascript
	function myFunction () {
		// Note the indentation
	}
	```

3. Define each `var` definition on it's own line. This is more declarative,
	 doesn't break indentation, and results in cleaner diffs.

	```javascript
	var myFirstVar = 1;
	var mySecondVar = 2;
	var myThirdVar = 3;
	```

4. Use `lowerCamelCase` for `function` and `var` identifiers.

5. Use `UpperCamelCase` for constructor `function` identifiers.

6. Use `UPPER_SNAKE_CASE` for constants.

7. Use `lower_snake_case` in JSON.

8. Don't use hoisting, and use `var` to define functions:

	```javascript
	// Bad
	var foo = 1;
	bar(foo, 1);
	function bar(a, b) {
		return a + b;
	}

	// Good
	var foo = 1;
	var bar = function (a, b) {
		return a + b;
	};
	bar(foo, 1);
	```

9. Use descriptive `var` names, only use single character names in `for` loops
	 (and `forEach` etc):

	```javascript
	// Bad
	var App = function () {
		this.s = {};
	};
	App.prototype.run = function () {
		this.s.started = true;
	};

	// Bad
	var arr = [1, 2, 3];
	for (var index = 0; i < arr.length; i++) {
		console.log(arr[index]);
	}

	// Good
	var App = function () {
		this.state = {
			started: false
		};
	};
	App.prototype.run = function () {
		this.state.started = true;
	};

	// Decent
	var numbers = [1, 2, 3];
	for (var i = 0, len = numbers.length; i < len; i++) {
		console.log(numbers[i]);
	}

	// Good
	var numbers = [1, 2, 3];
	numbers.forEach(function (n) {
		console.log(n);
	});
	```

10. Never assign `undefined` to anything, and only use it to check if an
		identifier is undefined. In most cases you should use `null`:

	```javascript
	// Bad
	var someVar;
	// ...
	if (someVar == null) {
		someVar = 1;
	}
	// ...
	someVar = undefined;

	// Good
	var someVar = null;
	// ...
	if (someVar === null) {
		someVar = 1;
	}
	// ...
	someVar = null;
	```

11. Always use `===`, never `==`.

12. Avoid using `!someVar` unless it's a boolean.

13. Avoid using multiple types with the same var (an exception is `null` unless
		it's a boolean):

	```javascript
	// Bad
	var someVar = 1;
	// ...
	someVar = {};

	// Good
	var someVar = 1;
	var someOtherVar = null;
	// ...
	someOtherVar = 'foo';
	```

14. Use single quotes (`'`), an exception is JSX attribute definitions which
		should use double quotes (`"`):

	```jsx
	// Bad
	var myString = "foo";
	<div id='foo' onClick={function(){ alert(myString +" clicked"); }}>Click me</div>

	// Good
	var myString = 'foo';
	var handleClick = function (e) {
		e.preventDefault();
		alert(myString +' clicked';
	};
	<div id="foo" onClick={handleClick}>Click me</div>
	```

15. Add a single space of padding on either side when using `!someExpression`
		within an `if` statement:

	```javascript
	// Bad
	var isSomething = false;
	if (!isSomething) {
		// ...
	}

	// Good
	var isSomething = false;
	if ( !isSomething ) {
		// ...
	}
	```

16. Avoid deep nesting, if the scope isn't immedietly obvious you're probably
		nesting too deeply.

17. Always use [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).

## Modules

Use the ES6 module syntax when breaking code up into multiple files. Here are a
few guidelines around doing so:

```javascript
// Bad
import * as foo from 'foo.js';
export * from 'foo';
export function add (a, b) {
	return a + b;
};

// Good
import { Person, Cat } from 'entities';

var add = function (a, b) {
	return a + b;
};

export { add };
export { Person, Cat };
```

Keep in mind, everything within a module is implicitly in [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).

## Other ES6

Anything supported by all major browsers (Firefox, Chrome, Safari, IE) for at
least one stable releases is fair game. For now modules are the only thing
being transpiled.
