# From Untestable Code to Testable

Functions may need to be changed or written differently. It's easy to convert an example on a [blog post about writing testable code](https://www.toptal.com/qa/how-to-write-testable-code-and-why-it-matters) for VoltScript. Imagine the following function:

```vbscript
Function getTimeOfDay() as String

    Dim nowTime as Variant
    nowTime = Now()
    If (Hour(Now) < 8) Then
        getTimeOfDay = "Night"
    ElseIf (Hour(Now) < 12) Then
        getTimeOfDay = "Morning"
    ElseIf (Hour(Now) < 6) Then
        getTimeOfDay = "Afternoon"
    Else
        getTimeOfDay = "Night"
    End If

End Function
```

This function is untestable, unless you are willing to test at multiple times of day or change the system time. Rewriting the function slightly can make it eminently testable:

```vbscript
Function getTimeOfDay(nowTime as Variant) as String

    If (Hour(Now) < 8) Then
        getTimeOfDay = "Night"
    ElseIf (Hour(Now) < 12) Then
        getTimeOfDay = "Morning"
    ElseIf (Hour(Now) < 6) Then
        getTimeOfDay = "Afternoon"
    Else
        getTimeOfDay = "Night"
    End If

End Function
```

Now it can be tested easily:

```
Dim testSuite as New BaliTestSuite("Testing time of day")
Dim nowTime as Variant
nowTime = TimeNumber(4,30,04)  ' Fine because we're only interested in the time
Call testSuite.describe("Test Night am").assertEqualsString("Night", getTimeOfDay(nowTime), True)
nowTime = TimeNumber(8,30,04)
Call testSuite.describe("Test Morning").assertEqualsString("Morning", getTimeOfDay(nowTime), True)
nowTime = TimeNumber(13,30,04)
Call testSuite.describe("Test Afternoon").assertEqualsString("Afternoon", getTimeOfDay(nowTime), True)
nowTime = TimeNumber(20,30,04)
Call testSuite.describe("Test Night pm").assertEqualsString("Night", getTimeOfDay(nowTime), True)
```
