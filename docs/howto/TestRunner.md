# Aggregate test suites

There are two hierarchies:

- **TestRunner** for aggregating multiple test suites. The default output format is HTML. This will output multiple HTML files, one for each test suite, with an index.html to bootstrap them.
- **TestSuite** for creating a single test suite containing multiple tests.

## TestRunner

[Simple Example](../tutorials/1-simple.md) uses this approach.

1. Add `Use "VoltScriptTesting"` to incorporate the VoltScript Testing script.
2. Declare a `New TestRunner` to aggregate all test suites, passing a label. 

    This will be combined with the run-time timestamp for the directory name containing the HTML files, in format "MyTitle-20220331T123000". Spaces will be removed, but no other modifications to the title. It's the developer's responsibility to ensure no invalid characters. The best practice is to use only alphanumeric characters. The files will be placed in the sub-directory `unit-test-reports` under the run context. The output location can be overridden using the `outputTo()` function. Changing this at the TestRunner will filter down to all TestSuites added to the TestRunner.

    !!!tip
        For best clarity, a separate function is used for each test suite, with the test runner passed as an argument to each function.

3. Instantiate a TestSuite object, passing a name for the tests. 

    This will be used for the filename of the HTML file, in format `MyTests.html`. The file will be in the same directory as the `index.html`. Spaces will be removed, but no other modifications to the title. It's the developer's responsibility to ensure no invalid characters. The best practice is to use only alphanumeric characters.

4. Add the TestSuite object to the TestRunner object, using `MyTestRunner.addTestSuite(MyTestSuite)`. 

    As an alternative<!--to steps 5 and 6-->, there is a `TestRunner.createTestSuite("Test Title")` method, which returns a newly created TestSuite object.