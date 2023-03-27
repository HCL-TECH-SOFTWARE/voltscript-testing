# How to Write a Custom Tester

## Custom Class

A custom tester can be used to run multiuple tests. The custom tester is a Class that extends `AbstractCustomTester`. It needs a `runTests()` function that returns a boolean.

```vbscript linenums="1"
Private Class DateTimeTester As AbstractCustomTester
	
	Function runTests As Boolean

		Dim dateTime As Variant
		Dim mon As Integer
		
		Call Me.testSuite.checkStarted()
		
		dateTime = CDat(|30/01/2022|)
		Call checkIsDateTime(Datetime)
		
		mon = Month(dateTime)
		checkMonthLessThan13(mon)
		
		Call Me.testSuite.describe(|Check dateTime is before Now|).assertIsLessThan(Now(), CDbl(dateTime))
		
	End Function

End Class
```

This is a custom class extending `AbstractCustomTester`. The only function we need to add is `runTests()`. The function can return a boolean if successful. But here, the outer code is only interested in whether or not the TestSuite ran successfully, which the TestSuite class handles internally. So no return value is passed out of the function.

This is the first test for the TestSuite, so on line 8, we call the `checkStarted` function of the TestSuite, which is a property of the parent class. This sets the timer for the TestSuite and, if appropriate, runs a custom `beforeAll()` function. We then call two internal functions - `checkIsDateTime()` and `checkMonthLessThan13()` and finally run an inline assertion. These are:

```vbscript linenums="1"
Function checkIsDateTime(dateTime As Variant) As Boolean
	checkIsDateTime = Me.testSuite.describe(|Check is DateTime Variant|).assertIs(|DATE|, dateTime)
End Function
	
Function checkMonthLessThan13(mon As Integer)

	Try
		Call Me.testSuite.describe(|Check month is less than 13|)
		If (mon < 13) Then
			Call Me.testSuite.addResult(True, "")
			checkMonthLessThan13 = True
		Else
			Call Me.testSuite.addResult(False, "Expected less than 13, was " & mon)
			checkMonthLessThan13 = False
		End If
	Catch
		Call testSuite.addError(testSuite.getErrorMsg, GetThreadInfo(12))
	End Try
		
End Function
```

The first function runs a simple assertion. The second one is more complex. A result is added (true or false), with the appropriate message. If there is an error - which should not happen in this scenario - the test is errored.

## Using the Class

Using the class is very straightforward. We create a TestSuite and an instance of the custom tester class. We then add the TestSuite to the tester and call the tester's `runTests()` function.

```vbscript
Dim TestSuite As New TestSuite(|DateTime Tests|)
Dim DateTimeTester As New DateTimeTester
	
Call DateTimeTester.addTestSuite(TestSuite).runTests()
```

If we wished, additional tests could be run before or after calling the tester's `runTests()` function.