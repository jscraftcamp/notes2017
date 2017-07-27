# testing-frameworks

## Test Runners
* [Jasmine](https://jasmine.github.io/) - behavior driven testing with `describe`, `it` and `expect`. Uses global 
namespace, searches for test files and runs them
* [Jest](https://facebook.github.io/jest/) - like Jasmine, adds snapshot testing and tries to infer your setup
* [Mocha](http://mochajs.org/) - injects describe and it in global namespace
* [Tape](https://github.com/substack/tape) - exports a function to create tests
  ```javascript
  const test = require("tape");
  test("something should be true", t => {
    t.equal(something, true);
  });
  ```
* [Ava](https://github.com/avajs/ava) - transpiles your code, feels like tape, runs tests in parallel

## Assertion libraries?
* [chai](http://chaijs.com/) - can be used in BDD or TDD style. 
  ```javascript
  expect(something).to.be.true;
  // or
  assert.equal(a, b, "a equals b");
  ```
* [must](https://github.com/moll/js-must) - like chai, but with function calls instead of properties in BDD style. Feels
[safer than chai](https://github.com/moll/js-must#asserting-on-property-access).
  ```javascript
  expect(something).to.be.true();
  ```
* [unexpected](http://unexpected.js.org/) - uses strings for equality. It gives detailed error / diff messages
  ```javascript
  expect(true, "to equal", 5);
  ```
* [where.js](https://github.com/dfkaye/where.js) - use comments as data tables for tests. Useful for simple cases?
* [power-assert](https://github.com/power-assert-js/power-assert) - uses regular `assert` and analyzes the code to give 
descriptive error messages. General opinion: It is great but hard to setup with Typescript, JSX, etc.

## Mocking libraries
I'd say that in our discussion, most people preferred sinon over manual mocking.

* [nock](https://github.com/node-nock/nock) - for mocking network requests in node.
* [sinon](http://sinonjs.org/) - seems like the standard approach
* "manual" mocking/stubbing - just make stubs for your own services / API.

## "Brute force" / Monkey-based testing
Just do anything that a user might be able to do on a webpage and see if it still works.
* [Gremlins.js](https://github.com/marmelab/gremlins.js) - Monkey testing

## Mutation-based testing
A bit "like gremlins" which changes your code and sees if your tests catch this.
* [Stryker](http://stryker-mutator.github.io/) - mutates object randomly to see effectiveness of your tests.

## Property-based testing
You write down rules that should be true for all kinds of inputs. For example "The 'plus1' function should result in a 
higher number for all possible integers".
* [JS Verify](http://jsverify.github.io/) - Gives you generators to test your properties with.
  ```javascript
  // forall (f: string -> nat, arr: array string),
  sortBy(sortBy(arr, f), f) ≡ sortBy(arr, f).
  var sortIdempotent =
    jsc.forall("string -> nat", "array string", function (f, arr) {
      return _.isEqual(_.sortBy(_.sortBy(arr, f), f), _.sortBy(arr, f));
    });
  
  jsc.assert(sortIdempotent);
  // OK, passed 100 tests
  ```

## Frontend-testing / visual regression test
Make a screenshot, check if it still looks similar. We stopped here and did not go into details. One project came to 
mind:
* [backstop.js](https://github.com/garris/BackstopJS)

## Side notes
There were a few abbreviations thrown in to help structuring your test code:

* **AAA** - **A**rrange, **A**ct, **A**ssert
* **See** - **S**etup, **E**xecute, **E**xpect
* **GWT** - **G**iven, **W**hen, **T**hen
  ```javascript
  // Arrange | Setup   | Given
  const func = require("x");
  
  // Act     | Execute | When
  const result = func();
  
  // Assert  | Expect  | Then
  assert(result === something);
  ```
