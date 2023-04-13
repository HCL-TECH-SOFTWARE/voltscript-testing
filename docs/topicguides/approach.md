# Challenges

## Before/After Functions: No Lambdas

VoltScript does not have the concept of [anonymous functions or lambdas](https://en.wikipedia.org/wiki/Anonymous_function). So code cannot be passed to a `beforeAll()` function. But developers _will_ need to run code before / after individual tests or all tests.

So how do we enable this?

The approach was one used for a previous HCL open source project, Volt MX LotusScript Toolkit, and used in other VoltScript projects: to use an abstract class which specific functions that should be overridden.

The `AbstractCustomBeforeAfter` class provides the template for this. Rather than modify this class in the VoltScriptTesting.bss module every time, developers are expected to create a [derived class](https://help.hcltechsw.com/dom_designer/12.0.2/basic/LSAZ_DERIVED_CLASSES.html) that extends `AbstractCustomBeforeAfter`. Then override the relevant functions. In the test code, create an instance of the class and pass it to the TestSuite. The TestSuite can then call the functions.

## Mocking Code

VoltScript Extension classes and core functions cannot be extended. So whereas other languages can create a mock class, that cannot be done in VoltScript. And it's not possible to re-route the language functions to alternate code during a test run.

The approach is one similar to the Rust language, namely to include tests in the same VoltScript library module (.bss). This allows you to use private variable (e.g. FORCE_ERROR, RUN_TESTS) to identify if tests are running or if you want to force an error, and put specific code in your functions accordingly.

You may also need to change the way your functions are written so objects are passed in. That allows a unit or integration test to create those objects outside of the function, and test the result based upon different objects.

## Identifying Tests

VoltScript cannot use annotations, so there's not a way to identify unit or integration test functions in a way that the VoltScript runtime can automatically identify. The idiom is to add your tests at the end of the VoltScript library module.