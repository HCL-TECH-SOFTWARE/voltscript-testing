# How to Use VoltScript Testing Framework for Validation

Imagine we have the following class:

``` vbscript
Class Person
    Public firstName as String
    Public lastName as String
    Public age as Integer

    Sub New()
      
    End Sub
End Class
```

We may want to validate that a Person has been set up correctly, because properties are not set and validated during the constructor.

## Setting up Person

```vbscript
Dim person as New Person()
person.firstName = "John"
person.lastName = "Doe"
person.age = 42
```

We will create the Person and set property values, ready for validation. In reality, this might be a JSON object received or a VoltScript object pre-populated outside the script that wants to validate it.

## Test Code

```vbscript linenums="1"
Dim testSuite as New TestSuite("Validator")
testSuite.suppressReport = True
Call testSuite.describe("fname").assertNotEqualString("", person.firstName)
Call testSuite.describe("lname").assertNotEqualString("", person.lastName)
Call testSuite.describe("age > 0").assertIsGreaterThan(0.0, CDbl(person.age))
Call testSuite.describe("age > 0 alt").assertTrue(person.age > 0)
Call testSuite.describe("age sensible").assertTrue(person.age < 110)
```

We need to pass a name to the TestSuite in line 1, even though it's not being used. The key is line 2, where we suppress the report. If we did not, when the code finishes and the TestSuite is deleted, the HTML reports would be generated - unnecessarily.

In lines 3 - 8 we run the tests. Age is an integer, so could potentially be a negative integer, or much bigger than the age a person could be.

## Checking The Validation Ran

```vbscript linenums="1"
If testSuite.ranSuccessfully() Then
    Print "Person valid"
Else
    errMsg = "Person not valid"
    ForAll test in testSuite.results
      If (test.outcome <> "Passed") Then
        errMsg = errMsg & Chr(10) & ListTag(test) & ": " & test.errorMsg
      End If
    End ForAll
    Error 1001, errMsg
End If
```

Checking validation worked is straightforward and done by calling the `ranSuccessfully()` function in line 1. If it wasn't successful, you want to identify what went wrong. This is done in lines 5 - 9. We loop through the results, which gives us access to the TestCase object. If the outcome was not "Passed", we capture the reason - the TestCase's errorMsg. This would be something like "Expected: 1, but was: 3".