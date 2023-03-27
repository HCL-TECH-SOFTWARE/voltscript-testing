# How to Write Code to BeforeAll, BeforeEach etc

The full code can be found in [SampleBeforeAfterTester](../assets/example_code/SampleBeforeAfterTester.txt).

## BeforeAfter Code

``` vbscript linenums="1"
Class IntegerIncrementBeforeAfter As AbstractCustomBeforeAfter
	
	Sub beforeAll()
		a = 0
		b = 0
	End Sub
	
	Sub beforeEach()
		a++
	End Sub
	
	Sub afterEach()
		b++
	End Sub
	
	Sub afterAll()
		Print |a is | & a & |, b is | & b
	End Sub

End Class
```

This CustomBeforeAfterTester uses all four methods. The variables `a` and `b` are not declared in the class, because they are needed in the actual tests. As a result, they are declared as global private variables.

The `beforeAll()` method starting at line 3 is only for explicit instantiation of the integers. If not explicitly set, they will be 0 anyway.

In the `beforeEach()` method starting at line 8 we increment `a`. In the `afterEach()` method starting at line 12 we increment `b`.

Finally, we use the `afterAll` to print out `a` and `b`.

## Test Code

``` vbscript linenums="1"
Dim testSuite As New TestSuite(|Custom BeforeAfter Tester|)
Dim beforeAfter As New IntegerIncrementBeforeAfter

Call testSuite.addCustomBeforeAfter(beforeAfter)

'a = 1, b = 0
testSuite.describe(|Test b is false|).assertFalse(b)

'a = 2, b = 1
Call testSuite.describe(|Test a equals 2|).assertEqualsInteger(2, a)

'a = 3, b = 2
Call testSuite.describe(|Test b equals 2 primitive|).assertEqualsPrimitive(2, b)

'a = 4, b = 3
Dim f As Double
f = 3.0
Call testSuite.describe(|Test CDbl(b) = 3.0|).assertEqualsDouble(f, CDbl(b))

'a = 5, b = 4
Dim c As Single
c = 4
Call testSuite.describe(|Test CSngl(b) = 4|).assertEqualsSingle(c, CSng(b))

'a = 6, b = 5
Dim d As Long
d = 5
Call testSuite.describe(|Test CLng(b) = 5|).assertEqualsLong(d, CLng(b))

'a = 7, b = 6
Dim e As Integer
e = b + 1
Call testSuite.describe(|Test a numeric = b + 1|).assertEqualsNumeric(e, a)
```

In line 1 we just create a TestSuite without a TestRunner, because we are only running a single test suite. In line 2 we create a instance of the custom BeforeAfter class, and in line 4 we add it to the test suite. Now we are ready to start running tests. Many of the tests are straightforward, but some deserve further comment.

On lines 16 and 17 we create a double to pass to the `assertEqualsDouble()`. This is because we cannot just pass `3.0`. We could use `assertEqualsNumeric()`, which proxies off to `assertEqualsDouble()`, but on this occasion we're using the lower level assertion.

Note on line 18 we compare `b`. If we were to test `a`, we would need to expect the value to be _3_, not _4_. This is because, although the `CDbl()` function is _inside_ the assertion, it is executed _before_ the assertion - and thus before the `beforeEach()` is triggered. The result of the executation passed to the assertion, at which point the `beforeEach()` will run. As a result, for ease of fourth-dimensional thinking, we just compare against the value modified in the `afterEach()` function.