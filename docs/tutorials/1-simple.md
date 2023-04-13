# Simple Example

This simple example creates a TestRunner with two TestSuites. It outputs HTML reports.

1. Add the "VoltScriptTesting.bss" script to your project directory. The best practice structure for the project directory will be `src` directory for main runnable scripts, `libs` directory for VoltScript dependencies and `test` for unit and integration test runnable scripts. in this structure, "VoltScripttesting.bss" would go into `libs`.
1. Create a .bss script file in `test`.
1. Add `Use "../libs/VoltScriptTesting"` at the top. This navigates up a directory, across to the "libs" directory and down to the VoltScriptTesting.bss within it. Your `Use` statement should not include the .bss suffix.
1. Best practice options settings to add are `Option Declare`. You can also add `Option Public` to make all methods and classes public by default.
1. Add a `Sub Initialize` and its closing `End Sub` statement.
1. Within the Sub Initialize, add the following code.

``` vbscript linenums="1"
Dim testRunner As New TestRunner("Sample Tests")
Dim testSuite1 As New TestSuite("Test Suite 1")
Dim testSuite2 As New TestSuite("Test Suite 2")
Dim x as Integer

Call testRunner.addTestSuite(testSuite1)
Call testSuite1.describe("Test x = False").assertFalse(x)
x = -1
Call testSuite1.describe("Test x = True").assertTrue(x)

Call testRunner.addTestSuite(testSuite2)
Call testSuite2.describe("Test x = -1").assertEqualsInteger(-1,x)
Call testSuite2.describe("Test x less than 0").assertIsLessThan(0, x)
```

In line 1 we create a TestRunner to hold our tests. In lines 2 and 3 we create two test suites.

In line 6 we add the first TestSuite to the test runner. Then in the following lines we add tests. `describe()` is a fluent function that returns the testSuite1 variable. So we can call `describe()` and the subsequent assertion on the same line. Here we just use a basic boolean assertion.

In line 11 we add the second TestSuite to the test runner. In line 12 we use an integer assertion and in line 13 assert that x is less than 0. Note that when using other numeric assertions and literal values, you may need to use the relevant conversion function (e.g. `CLng()`).

When using assertions that take an expected value, the order is always `expected` as the first parameter and `actual` as the second.

You can now run the code.

!!! note
    The test results will be generated to a unit-test-reports directory in the runtime directory. If running from the command line, this will be the current directory. If running from Visual Studio Code, it will be the directory open in VS Code.

A more thorough example can be found in [BasicTester](../assets/example_code/BasicTester.txt).