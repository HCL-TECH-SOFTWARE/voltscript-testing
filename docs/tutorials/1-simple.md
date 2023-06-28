# Create a TestRunner

<!--Simple Example
This simple example creates a TestRunner with two TestSuites. It outputs HTML reports.-->

The tutorial guides you in creating a TestRunner with two TestSuites and outputs HTML reports.

## To create a TestRunner

1. Add the `VoltScriptTesting.bss` script to your project directory. 

    !!!tip
        The best practice structure for the project directory is the `src` directory for main runnable scripts, `libs` directory for VoltScript dependencies, and `test` for unit and integration test runnable scripts. In this structure, `VoltScripttesting.bss` would go into `libs`.

2. Create a .bss script file in `test`.
3. Add `Use "../libs/VoltScriptTesting"` at the top. This navigates up a directory, across to the `libs` directory and down to the `VoltScriptTesting.bss` within it. Your `Use` statement shouldn't include the .bss suffix.

    !!!tip
        Best practice options settings to add are `Option Declare`. You can also add `Option Public` to make all methods and classes public by default.

4. Add a `Sub Initialize` and its closing `End Sub` statement.
5. Add the following code within the `Sub Initialize`:

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
    
    !!!info "Code explanation"

        Line 1 creates a TestRunner to hold the tests. Lines 2 and 3 create two test suites.
        Line 6 adds the first TestSuite to the test runner. The following lines add tests. 
        
        `describe()` is a fluent function that returns the `testSuite1` variable so you can call `describe()` and the subsequent assertion on the same line. Here, you can just use a basic boolean assertion.

        Line 11 adds the second TestSuite to the test runner. Line 12 uses an integer assertion. Line 13 asserts that `x` is less than 0.

        When using other numeric assertions and literal values, you may need to use the relevant conversion function such as `CLng()`. When using assertions that take an expected value, the order is always `expected` as the first parameter and `actual` as the second. 

6. Run the code. 

<!--In line 1, we create a TestRunner to hold our tests. In lines 2 and 3 we create two test suites.

In line 6 we add the first TestSuite to the test runner. Then in the following lines we add tests. `describe()` is a fluent function that returns the testSuite1 variable. So we can call `describe()` and the subsequent assertion on the same line. Here we just use a basic boolean assertion.

In line 11 we add the second TestSuite to the test runner. In line 12 we use an integer assertion and in line 13 assert that x is less than 0. Note that when using other numeric assertions and literal values, you may need to use the relevant conversion function (e.g. `CLng()`).

When using assertions that take an expected value, the order is always `expected` as the first parameter and `actual` as the second.-->

## Expected result 

The test results will be generated to a unit-test-reports directory in the runtime directory. If running from the command line, this will be the current directory. If running from Visual Studio Code, it will be the directory open in VS Code.

You can find a more thorough example in [BasicTester](../assets/example_code/BasicTester.txt).