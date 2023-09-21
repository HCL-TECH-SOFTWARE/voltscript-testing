# FAQs

## Where do I find the output?

The output, by default, is in a `unit-test-reports` directory defined by the `BASE_REPORT_LOC` constant in `TestRunner.vss`. The directory is under the directory of the program running the tests.

## How do I change the output directory?

If you wish to change the output directory for every test runner using the script, change the `BASE_REPORT_LOC` constant.

If you wish to change the output directory for a single set of tests:

- If using a TestRunner, call `TestRunner.outputTo()`.
- If just using a TestSuite independent of a test runner, call `TestSuite.outputTo()`.

## I set `outputTo` for a TestSuite, but why is it not working?

Make sure that the test suite has been added to a TestRunner so that the location for the TestRunner overrides any setting in the test suite. Otherwise, the `index.html` won't map to the test suite's output.

## I'm using a TestRunner, but why is the TestSuite's output not in the TestRunner's subdirectory?

The usual cause is omitting to call `TestRunner.addTestSuite()`.

## What are missing assertions?

This means you have called `describe()` but a corresponding assertion - or call to `addResult()` or `addError()` - has not been included. This could be because other code after the `describe()` call has generated an error and needs fixing.

## I am using a `CustomBeforeAfter`, but why is the assertion not taking into account the value from the `beforeEach()`?

Make sure your code isn't running a function that modifies a value being modified in the `beforeEach`, such as `assertEqualsDouble(f, CDbl(a))`, where `a` is incremented in the `beforeEach()`. In the above line, the order of processing would be:

1. CDbl(a)
2. Call to assertion.
3. Run `beforeEach()`, incrementing `a`.
4. Run assertion.

If `beforeEach()` is a pure function, that is it just instantiates dummy data and doesn't modify any global variables, you could manually call `beforeEach()` _before_ modifying the value that you are passing into the assertion. Alternatively, just compare against the value _before_ the `beforeEach()` has run.

## What's the recommended best practice for test suites?

Creating a separate function for each TestSuite gives the greatest clarity. It also allows aborting a run if a key TestSuite fails. Each TestSuite is usually designed to test a specific process or self-contained aspect of the code or application.

TestSuites for unit tests and integration tests are typically also separated. Unit tests are used to test functions that don't depend on specific environmental aspects, such as specific users and specific data. In other technologies, unit tests include [mocking](#how-can-we-mock-data-or-users).

Integration tests are used to test code that requires specific data to be available, specific user access to be in place, real-world testing of external systems.

## How can we mock data or users?

[Before/After code](../howto/BeforeAfterTester.md) can create data specifically for testing. These would then become integration tests.

Java has Mockito framework because sub-classing is always possible and API calls can be intercepted. That's not an option here. TestSuite functions are best written in the same file as the functions being tested. The same approach is used for Rust and has the added benefit of documenting how the functions are intended to be used.

If non-LSX custom classes are used as parameters, this may allow sub-classing with a mocked object to test a complete function. More commonly, branching logic needs to be added to the functions to route differently if the callee is a test. If the tests are in the same file as the functions being called, private variables can be used to determine if a test is being run or determine if an error should be thrown.

## Does testing means I have to write my functions differently

Yes, it probably will. Writing code is one thing, writing _testable_ code is a completely different beast, and not specific to any one language. It's not hard to find [articles](https://www.toptal.com/qa/how-to-write-testable-code-and-why-it-matters) written about this.
