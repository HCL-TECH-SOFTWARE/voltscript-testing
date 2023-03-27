---
hide:
    - navigation
---
# Bali Unit Testing Framework

Bali Unit Testing Framework is a framework for testing code written using VoltScript, the evolution of LotusScript delivered as part of HCL Volt MX Go. The framework can also be used for LotusScript, with modifications (see below on new language functions used).

There are deliberately no dependencies on any LotusScript Extensions (LSX, e.g nlsxbe.dll). None should be added, it will make it dependent on a particular implementation.

Output can be set as either HTML files, XML files or both. HTML files are designed for your project reporting. The XML files are in standard JUnit format, which your build automation processes (e.g. Jenkins) can leverage to determine whether the build is successful or not.

## Using BaliUnit for Validation

The BaliTestSuite has a `suppressReport` boolean property, which can be used to prevent report output. The use case for this is to create a BaliTestSuite and use it to validate content within code, e.g. a JSON file. You can set `suppressReport = true`, then create your tests and check `testSuite.ranSuccessfully()` to verify all tests were successful.

## Writing BaliUnit Tests

See [Writing Units Tests](Writing-Unit-Tests/index.md).

## Core Functions Used

Obviously the code runs certain core language functions. If anything is broken for these, the unit testing cannot run. These are documented in [Core Functions](CoreFunctions.md)

## Reference

See project docs for class documentation, examples of the HTML and XML reports and the corresponding unit tests.

## FAQs

If unexpected behaviour is occurring, check the FAQs.
