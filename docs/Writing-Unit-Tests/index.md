# Writing Unit Tests

There are two hierarchies:

- **BaliTestRunner** for aggregating multiple test suites. The default output format is HTML. This will output multiple HTML files, one for each test suite, with an index.html to bootstrap them. If the output format is set to "XML", a single XML file file is generated in JUnit format. This can be used by Jenkins. The output format can be set to "BOTH" to output HTML and XML files.
- **BaliTestSuite** for creating a single test suite containing multiple tests. If it has not been added to a BaliTestRunner, a standalone HTML file will be created. This is an easy mistake to make and if your HTML file is not where you expect, this could be the cause!

## BaliTestRunner - Multiple HTML Files aggregated with index.html

[Simple Example](./1-simple.md) uses this approach.

1. Add `Use "BaliTestRunner"` to incorporate the Bali Unit Test script.
1. Declare a `New BaliTestRunner` to aggregate all test suites, passing a label. This will be combined with the run-time timestamp for the directory name containing the HTML files, in format "MyTitle-20220331T123000". Spaces will be removed, but no other modifications to the title - it is the developer's responsibility to ensure no invalid characters, best practice is to use only alphanumeric characters. The files will be placed in the sub-directory `unit-test-reports` under the run context. The output location can be overridden using the `outputTo()` function. Changing this at the BaliTestRunner will filter down to all BaliTestSuites added to the BaliTestRunner.
1. For best clarity, a separate function is used for each test suite, with the test runner passed as an argument to each function.
1. Instantiate a BaliTestSuite object, passing a name for the tests. This will be used for the filename of the HTML file, in format MyTests.html. The file will be in the same directory as the index.html. Spaces will be removed, but no other modifications to the title - it is the developer's responsibility to ensure no invalid characters, best practice is to use only alphanumeric characters.
1. Add the BaliTestSuite object to the BaliTestRunner object, using `MyBaliTestRunner.addTestSuite(MyBaliTestSuite)`. As an alternative to steps 5 and 6, there is a method `BaliTestRunner.createTestSuite("Test Title")`, which will return a newly-created BaliTestSuite object.

## Standalone BaliTestSuite HTML File Output

[SimpleBeforeAfterTester](./2-BeforeAfterTester.md) uses this approach.

1. Add `Use "BaliTestSuite"` to create a set of tests.
1. Instantiate the BaliTestSuite object, passing a name for the tests. This will be combined with the run-time timestamp for the filename of the HTML file, in format "MyTests-20220331T123000.html". Spaces will be removed, but no other modifications to the title - it is the developer's responsibility to ensure no invalid characters. The output location can be overridden using the `outputTo()` function.

## Writing Tests

1. Write your tests using syntax `Call BaliTestSuite.describe(|My Test Name|).assertTrue(True)`. For assertions available, see assertions in [BaliTestSuite class documentation](../project-docs/balidoc/index.html) documentation. All assertions have error handling in-built and will give a full stack trace for VoltScript.
1. Each assertion returns a true / false for success, which can be utilised, if required.
1. After all tests have been run, the BaliTestSuite has a `ranSuccessfully()` function that returns a boolean to identify if all tests ran successfully. If you want to access the results, these are in a `results` List, where the label is the test name (corrected as appropriate for uniqueness).

## Location of Unit / Integration Tests

In experience, test suites are best written as functions in the same script as the functions they are testing. This allows use of private variables e.g. to mock actual objects, route logic differently, write errors elsewhere etc. A separate unit test / integration script can be used to trigger the test functions.

## Class APIs

For more details of classes etc in use, see [BaliDoc](../project-docs/balidoc/index.html).
