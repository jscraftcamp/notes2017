# testing-frameworks

Runners
* Jasmine
* Jest
* Mocha
* Tape
* Ava

Brute force-based testing
* Gremlins.js

Mutation-based testing
-> "like gremlins" try to break your stuff.
* Stryker

Property-based testing?
* js verify

Assertion libraries?
* chai
* must
* unexpected
* where.js -> for simple cases?
* power-assert -> great but hard to setup

Mocking libraries
* nock
* sinon
* "manual" mocking/stubbing

Frontend-testing / visual regression test
* backstop.js

expect(true, "to equal", 5);

AAA -> Arrange Act Assert
See -> Setup, execute, expect
GWT -> Given When Then

// given
const ...

// when
const result = func(...)

// then
expect(result === ...)


const test = require("tape");
test("....", t => {
...
})