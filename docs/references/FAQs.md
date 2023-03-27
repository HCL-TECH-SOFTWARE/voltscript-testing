# FAQs

## Where do I find the output?

The output will, by default, be in a "unit-test-reports" directory (defined by the `BASE_REPORT_LOC` constant in BaliTestRunner.bss) under the directory of the program running the tests.

## How do I change the output directory?

If you wish to change the output directory for every test runner using the script, change the `BASE_REPORT_LOC` constant.

If you wish to change the output directory for a single set of tests:

- If using a BaliTestRunner, call `BaliTestRunner.outputTo()`.
- If just using a BaliTestSuite independent of a test runner, call `BaliTestSuite.outputTo()`.

## I set outputTo for a TestSuite, but it's not working?

Has the test suite been added to a BaliTestRunner? If so, the location for the BaliTestRunner overrides any setting in the test suite - otherwise the index.html won't map to the test suite's output!

## I'm using a BaliTestRunner, but the BaliTestSuite's output is not in the BaliTestRunner's subdirectory

The usual cause is omitting to call `BaliTestRunner.addTestSuite()`.

## What are missing assertions?

This means you have called `describe()` but a corresponding assertion - or call to `addResult()` or `addError()` - has not been included. This could be because other code after the `describe()` call has generated an error and needs fixing.

## I am using a CustomBeforeAfter, but the assertion is not taking into account the value from the beforeEach()

Make sure your code is not running a function that modifies a value being modified in the beforeEach, e.g. `assertEqualsDouble(f, CDbl(a))`, where `a` is incremented in the `beforeEach()`. In the above line, the order of processing would be:

1. CDbl(a)
2. Call to assertion.
3. Run `beforeEach()`, incrementing a.
4. Run assertion.

If the `beforeEach()` is a pure function - i.e. it just instantiates dummy data and does not modify any global variables - you could manually call `beforeEach()` _before_ modifying the value that you are passing into the assertion. Alternatively. just compare against the value _before_ the `beforeEach()` has run.

## What is Recommended Best Practice for Test Suites?

In personal experience, creating a separate function for each BaliTestSuite gives greatest clarity. It also allows aborting a run if a key BaliTestSuite fails. Each BaliTestSuite is usually designed to test a specific process or self-contained aspect of the code or application.

BaliTestSuites for unit tests and integration tests are typically also separated. Unit tests are used to test functions that do not depend on specific environmental aspects - specific users, specific data etc. In other technologies, unit tests will also include [mocking](#how-can-we-mock-data-or-users).

Integration tests are used to test code that requires specific data to be available, specific user access to be in place, real-world testing of external systems etc.

## How Can We Mock Data or Users?

[Before/After code](Writing-Unit-Tests/2-BeforeAfterTester.md) can create data specifically for testing - these would then become integration tests.

Java has Mockito framework, because sub-classing is always possible and API calls can be intercepted. That is not an option here. From experience, BaliTestSuite functions are best written in the same file as the functions being tested. The same approach is used for Rust and has the added benefit of documenting how the functions are intended to be used.

If non-LSX custom classes are used as parameters, this may allow sub-classing with a mocked object to test a complete function. More commonly, branching logic needs to be added to the functions to route differently if the callee is a test. If the tests are in the same file as the functions being called, private variables can be used to determine if a test is being run or determine if an error should be thrown.

## Testing Means I Have to Write My Functions Differently

Yes, it probably will. Writing code is one thing, writing _testable_ code is a completely different beast, and not specific to any one language. It's not hard to find [articles](https://www.toptal.com/qa/how-to-write-testable-code-and-why-it-matters) written about this.
