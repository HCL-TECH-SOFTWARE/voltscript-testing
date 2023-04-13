# How to Write Tests

## Creating a Test

Each test needs a description. This is set by calling `Call TestSuite.describe(|My Test Name|)`. If this is omitted, the test name is "Test " + a unique number. Tests must be followed by an assertion. If this is accidentally forgotten, the test will fail with a "Missing Assertion" response.

The `describe()` function returns the TestSuite, so the assertion can be chained onto the end of the `describe` call, e.g. `Call TestSuite.describe(|My Test Name|).assertTrue(True)`. This is recommended for better readability.

## Assertions

### In-Built Assertions

All assertion functions begin `assert...`. The in-built assertions are:

- `assertTrue(actual as Boolean)` expects the expression or variable passed in is true or numeric not 0.
- `assertFalse(actual as Boolean)` expects the expression or variable passed in is false or numeric 0.
- `assertIs(expectedType as String, actual as Variant)` runs `TypeName()` on the actual value passed and compares its type to the expected type. For objects, this is the actual class name. For objects that are derived classes cannot be used to check if the object is an instance of a base class. For example, if you create your own custom tester class, you cannot use this to check if it is an instance of AbstractCustomTester. For best practice, pass the class name as upper case. However, internally, the code will `LCase()` both.
- `assertIsNot(expectedType as String, actual as Variant)` runs the opposite test.
- `assertEqualsString(expected as String, actual as String, caseInsensitive as Boolean)` expects the two strings to match. The third parameter can be used to force case-sensitive comparison. If `false` the two values are compared as lower case. This method is only intended for simple string comparisons. If pitch comparison is required, use `StrCompare` with the appropriate in-built assertion or a custom assertion function / custom tester.
- `assertNotEqualString(expected as String, actual as String, caseInsensitive as Boolean)` runs the opposite test.
- `assertEqualsDouble(expected as Double, actual as Double)` expects two doubles to match, running `CStr()` to avoid bit-level issues.
- `assertNotEqualDouble(expected as Double, actual as Double)` runs the opposite test.
- `assertEqualsInteger(expected as Integer, actual as Integer)` expects two integer to match.
- `assertNotEqualInteger(expected as Integer, actual as Integer)` runs the opposite test.
- `assertEqualsLong(expected as Long, actual as Long)` expects two longs to match, running `CStr()` to avoid bit-level issues.
- `assertNotEqualLong(expected as Long, actual as Long)` runs the opposite test.
- `assertEqualsSingle(expected as Single, actual as Single)` expects two singles to match, running `CStr()` to avoid bit-level issues.
- `assertNotEqualSingle(expected as Single, actual as Single)` runs the opposite test.
- `assertEqualsNumeric(expected as Variant, actual as Variant)` expects two numeric values to match, running `CStr()` to avoid bit-level issues.
- `assertNotEqualNumeric(expected as Variant, actual as Variant)` runs the opposite test.
- `assertIsBetween(expected1 as Double, expected2 as Double, actual as Double)` expects the actual to be greater than or equal to the first expected value and less than or equal to the second. This runs "between", not "strictly between". If you want to run a "strictly between" test, use `assertTrue()` or `assertFalse()` withg an expression, or a custom tester.
- `assertIsGreaterThan(expected as Double, actual as Double)` expects the actual to be greater than the expected value.
- `assertIsLessThan(expected as Double, actual as Double)` expects the actual to be less than the expected value.
- `assertEqualsPrimitive(expected as Variant, actual as Variant)` expects the two variables to match, ignoring data type and CStr-ing the values. So "1" and 1 will be considered equal, but "One" and "one" will not.
- `assertEqualsPrimitiveOrPrimitiveArray(expected as Variant, actual as Variant)` expects the two variables to match, running `assertEqualsPrimitive()` on each variable or array element. If one is an array and the other is not, the assertion will fail. If both are arrays, each element will be compared with the element at the same index.

All in-built assertions have error handling in-built and will give a full stack trace for VoltScript. Each assertion returns a true / false for success, which can be utilised, if required.

For more details of classes etc in use, see [API Documentation](../references/apidocs/index.html).

### Custom Assertions

If an assertion is required beyond the basic options, this can be achieved by performing a function on the appropriate variables and passing the result of the function to an `assertTrue()` or `assertFalse()`.

In simple cases this can be done inline. When doing so, be aware that an error in the function call (e.g. `CDbl` on a non-numeric value) will abort processing before the assertion is run. If more processing is required than can be done in a single function call, conditional processing can be used.

```vbscript linenums="1"
Dim dateVal as Variant
Try
	Call testSuite.describe(|Check month is less than 13|)
    dateVal = CDat(passedVal)
	If (Month(dateVal) < 13) Then
        If (Day(dateVal) < 32) Then
            If (Year(dateVal) > 1900 And Year(dateVal) < 2000)
    		    Call testSuite.addResult(True, "")
            Else
                Call testSuite.addResult(False, "Expected between 1900 and 2000, was " & Year(dateVal))
	    Else
		    Call testSuite.addResult(False, "Expected less than 31, was " & Day(dateVal))
    	End If
	Else
		Call testSuite.addResult(False, "Expected less than 13, was " & Month(dateVal))
	End If
Catch
    Call testSuite.addError(Error() & " on " & Erl(), GetThreadInfo(12))
End Try
```

This code expects a date string to be passed (`passedVal`, used in line 4). Rather than running multiple assertions checking various aspects of the date, it runs various conditional statements, failing the test if any part fails, succeeding if all conditionals are true, and adding an error on line 18 if the date conversion fails.

In other scenarios, a custom function that returns a boolean may be more appropriate, with an assertion on the result.

In very complex cases, a [custom tester class](./customtester.md) can be used.

If you have custom before/after code for tests, remember to call `TestSuite.runBeforeEach()` before running your test and `TestSuite.runAfterEach()` at the end.

### Custom Assertions as First Test

In-built assertions will always call `checkStarted()` at the start. This runs the `beforeAll()` function of a [AbstractCustomBeforeAfter class](./BeforeAfterTester.md) passed in. If your first test is not a built-in assertion, you will need to call `TestSuite.checkStarted()` first.

## TestSuite Pass / Fail

After all tests have been run, the TestSuite has a `ranSuccessfully()` function that returns a boolean to identify if all tests ran successfully. If you want to access the results, these are in a `results` List, where the label is the test name (corrected as appropriate for uniqueness).