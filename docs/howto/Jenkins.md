# How to Integrate with CI/CD

If the test is set to output an XML file, this can be automatically picked up by your CI/CD environment, e.g. Jenkins. This needs to be set on the highest level of the hierarchy, changing the output format.

If you are using a TestRunner, call `TestRunner.setOutputFormat()`. Otherwise, call `TestSuite.setOutputFormat()`. TestSuites assigned to a TestRunner take the same output format as the TestRunner.

To just output an XML file, call `setOutputFormat("XML")`. To output the HTML files and XML files, call `setOutputFormat("BOTH")`.

For a TestRunner, a single XML file is created that contains the XML for the TestRunner and all TestSuites allocated to it.

If a test suite fails, ensure an error is bubbled up to the runtime, with sufficient information to identify which test or tests failed. This ensures the VoltScript Runtime process exits with an error, which notifies CI/CD that that the build should be aborted.