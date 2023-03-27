## How to Mock Calls

Unlike other frameworks, the language engine does not permit bypassing API calls during testing. As a result, code may need to be [restructured to be testable](./untestable-to-testable.md). This is not completely unique to VoltScript. In other languages there are also cases where it is better to [refactor code to be more testable](https://www.baeldung.com/mockito-mock-static-methods#a-quick-word-on-testing-static-methods){: target="_new"}.

## Forcing an Error

Proper testing not only tests successful outcomes but also errors. Sometimes this can be done by passing invalid content into a function.

```vbscript linenums="1"
Function convertStringToInteger(passedVal as String) as Integer

    CInt(passedVal)

End Function
```

This can be tested by passing a non-numeric value.

Other times, it is less simple and errors may only occur because of invalid environmental causes. This can be mocked by setting a boolean variable, and checking for the existence of this variable in your code.

```vbscript linenums="1"
Dim FORCE_ERRORS as Boolean

Function doComplexProcessing()

    If FORCE_ERRORS Then Error 1001, "Invalid Content"
    ...

End Function
```

This scenario envisages that there is a lot of additionl content for the `doComplexProcessing()` function, which uses a lot of variables set elsewhere and refactoring the code is not desirable. Setting up all those other variables is difficult in unit testing and will be covered by integration testing. But testing the error is simple, the tester can set `FORCE_ERRORS` to true and expect an error.

!!! note
    Remember to reset FORCE_ERRORS afterwards.

### Creating Mock Data Inline

An alternative approach would be to use a `TEST_RUN` boolean variable and check for it. Code can then run `If TEST_RUN Then Call createMockDoc()`, running a function to create mock data inline. Tests can set that `TEST_RUN` variable at the start of processing.