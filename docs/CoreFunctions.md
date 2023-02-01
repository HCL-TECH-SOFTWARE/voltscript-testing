---
hide:
    - navigation
---
# Core Language Functions Used

Core Functions in BaliUnit Script Library

`%REM` and `%END REM` are used throughout. `'` for a single-line comment is also used.

When listing keywords, sub/function names where the keyword is used are in brackets. Sub/function location is not used for common functions, datatypes or As.

In Declarations the following language keywords are used:

- Type
- End Type
- As
- String
- Const

## Private makeDirsBaliUnit Function

This is a function to create directories in a managed way.

Language keywords used:

- Sub
- End Sub
- As
- String
- On Error GoTo
- MkDir
- CurDir
- Exit Sub
- If...Then
- End If
- Err
- Error
- MsgBox
- Cstr
- Erl
- Resume Next

## Private FormatTimeForOutput Function

This is a function to format a date variable.

Language keywords used:

- Function
- End Function
- As
- Variant
- String
- Format(Variant of Date Type, String format). String format is `yymmddThhnnss`

## AbstractBaliCustomBeforeAfter

This is an abstract class and contains no code.

Language keywords used:

- Class
- End Class
- Sub
- End Sub

## AbstractBaliCustomTester

This is a basic class with minimal code.

Language keywords used:

- Class
- End Class
- Public
- As
- Sub
- End Sub
- New
- Function
- End Function
- Set (addBaliUnit)
- Me (addBaliUnit)
- Boolean
- Error (runTests)

## BaliTestRunner

This is the class for outputting a number of HTML files, with an index.html wrapping them.

Language keywords used:

- Class
- End Class
- Private
- Public
- As
- List
- String
- Variant
- Sub
- End Sub
- New
- Me
- Now
- Delete
- Call
- Erase (Delete)
- Right
- FullTrim
- And
- Set
- Replace (getFilePath, printoutReport)
- Integer
- On Error GoTo (printoutReport)
- FreeFile (printoutReport)
- Open (printoutReport)
- For Output As (printoutReport)
- Forall...In (printoutReport)
- End ForAll (printoutReport)
- Dim (printoutReport)
- If...Then (printoutReport)
- ElseIf (printoutReport)
- Else (printoutReport)
- End If (printoutReport)
- Cstr (printoutReport)
- Print fileNum, String (printoutReport)
- Close (printoutReport)
- MsgBox (printoutReport)
- Error (printoutReport)
- Err (printoutReport)
- Erl (printoutReport)
- Resume (printoutReport)

## BaliTestSuite

This is the class for a set of tests.

Language keywords used:

- Class
- End Class
- Public
- As
- String
- Private
- Integer
- List
- Double
- Boolean
- Variant
- Sub
- End Sub
- New
- Me
- Function
- End Function
- Variant
- Set
- Delete
- Now (Delete, checkStarted)
- On Error GoTo (Delete)
- If...Then (Delete, checkStarted, convertErrorStack, runBeforeEach, runAfterEach, various assertions)
- Else (Delete, convertErrorStack, various assertions)
- End If (Delete, checkStarted, runBeforeEach, runAfterEach, various assertions)
- Not (Delete, checkStarted, convertErrorStack, runBeforeEach, runAfterEach, various assertions)
- Is Nothing (Delete, checkStarted, runBeforeEach, runAfterEach)
- Dim
- Format(Variant of Date Type, String format). String format is `yymmddThhnnss` (Delete)
- Now (Delete)
- Call
- Exit Sub (Delete)
- MsgBox (Delete)
- Error (Delete)
- Err (Delete)
- Erl (Delete)
- CStr
- Resume (Delete, assertEqualsPrimitive)
- While (makeDescriptionUnique)
- Wend (makeDescriptionUnique)
- IsElement (makeDescriptionUnique)
- True (checkStarted, various assertions)
- \* (checkStarted)
- \- (checkStarted)
- Right
- FullTrim
- And
- Round (duration)
- IsArray (convertErrorStack, assertNotEqualPrimitiveOrPrimitiveArray, testArrays)
- For...To (convertErrorStack, processArray, assertNotEqualPrimitiveOrPrimitiveArray)
- Next (convertErrorStack, processArray, assertNotEqualPrimitiveOrPrimitiveArray)
- UBound (convertErrorStack, processArray, assertNotEqualPrimitiveOrPrimitiveArray, testArrays)
- False (various assertions)
- = (various assertions)
- <> (various assertions)
- LCase (assertEqualsString, assertIs, assertIsNot)
- Long (assertEqualsLong, assertNotEqualLong)
- Single (assertEqualsSingle, assertNotEqualSingle)
- IsNumeric (assertEqualsNumeric, assertNotEqualNumeric)
- CDbl (assertEqualsNumeric, assertNotEqualNumeric, assertEqualsPrimitive)
- TypeName (assertIs, assertIsNot, assertEqualsPrimitive, assertNotEqualPrimitiveOrPrimitiveArray)
- On Error _ErrNum_ GoTo (assertEqualsPrimitive)
- Select (assertEqualsPrimitive)
- End Select (assertEqualsPrimitive)
- CBool (assertEqualsPrimitive)
- CInt (assertEqualsPrimitive)
- CLng (assertEqualsPrimitive)
- CSng (assertEqualsPrimitive)
- Exit Function (assertEqualsPrimitive)
- ReDim Preserve (processArray)
- Join (processArray, assertNotEqualPrimitiveOrPrimitiveArray, testArrays)
- FullTrim (addResult, addError)

## BaliTestSuiteReport

This is the class for writing out an HTML file for a BaliUnit.

Language keywords used:

- Class
- End Class
- Private
- As
- String
- Sub
- End Sub
- New
- If...Then (New, printoutReport)
- Else (New)
- End If (New, printoutReport)
- Me
- Dim (printoutReport)
- String arrays (printoutReport)
- Integer
- On Error GoTo (printoutReport)
- Forall...In (printoutReport)
- End ForAll (printoutReport)
- CStr (printoutReport)
- FreeFile (printoutReport)
- Call
- Replace (printoutReport)
- Open (printoutReport)
- For Output As (printoutReport)
- Print (printoutReport)
- Close (printoutReport)
- Exit Sub
- MsgBox (printoutReport)
- Error (printoutReport)
- Err (printoutReport)
- Erl (printoutReport)
- Resume (printoutReport)
