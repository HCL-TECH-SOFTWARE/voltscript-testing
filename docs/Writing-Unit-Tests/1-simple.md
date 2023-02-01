# Simple Example


``` vbscript linenums="1"
Dim testRunner As New BaliTestRunner("Sample Tests")
Dim testSuite1 As New BaliTestSuite("Test Suite 1")
Dim testSuite2 As NEW BaliTestSuite("Test Suite 2")
Dim x as Integer

Call testRunner.addTestSuite(testSuite1)
Call testSuite1.describe("Test x = False").assertFalse(x)
x = -1
Call testSuite1.describe("Test x = True").assertTrue(x)

Call testRunner.addTestSuite(testSuite2)
Call testSuite2.describe("Test x = -1").assertEqualsInteger(-1,x)
Call testSuite2.describe("Test x less than 0").assertIsLessThan(0, x)
```

In line 1 we create a BaliTestRunner to hold our tests. In lines 2 and 3 we create two test suites.

In line 6 we add the first BaliTestSuite to the test runner. Then in the following lines we add tests. `describe()` is a fluent function that returns the testSuite1 variable. So we can call `describe()` and the subsequent assertion on the same line. Here we just use a basic boolean assertion.

In line 11 we add the second BaliTestSuite to the test runner. In line 12 we use an integer assertion and in line 13 assert that x is less than 0. Note that when using other numeric assertions and literal values, you may need to use the relevant conversion function (e.g. `CLng()`).

When using assertions that take an expected value, the order is always `expected` as the first parameter and `actual` as the second.

A more thorough example can be found in [BasicTester](../example_code/BasicTester.txt).
