# How to Write a Standalone TestSuite

[SimpleBeforeAfterTester](./BeforeAfterTester.md) uses this approach.

1. Add `Use "TestSuite"` to create a set of tests.
1. Instantiate the TestSuite object, passing a name for the tests. This will be combined with the run-time timestamp for the filename of the HTML file, in format "MyTests-20220331T123000.html". Spaces will be removed, but no other modifications to the title - it is the developer's responsibility to ensure no invalid characters. The output location can be overridden using the `outputTo()` function.