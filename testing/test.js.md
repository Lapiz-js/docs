## Lapiz/testing/test.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Test](#Lapiz.Test)
  * [Lapiz.Test.Run](#Lapiz.Test.Run)
* [Result](#Result)
  * [Result.children](#Result.children)
  * [Result.defined](#Result.defined)
  * [Result.failed](#Result.failed)
  * [Result.fullName](#Result.fullName)
  * [Result.passed](#Result.passed)
  * [Result.ran](#Result.ran)
  * [Result.test](#Result.test)
    * [Result.test.failed](#Result.test.failed)
    * [Result.test.fullName](#Result.test.fullName)
    * [Result.test.log](#Result.test.log)
    * [Result.test.name](#Result.test.name)
    * [Result.test.passed](#Result.test.passed)
    * [Result.test.ran](#Result.test.ran)
    * [Result.test.time](#Result.test.time)
* [TestDependencies](#TestDependencies)
* [TestFunction](#TestFunction)
* [TestName](#TestName)
* [TestObject](#TestObject)
  * [TestObject.error](#TestObject.error)
  * [TestObject.fail](#TestObject.fail)
    * [TestObject.failed](#TestObject.failed)
  * [TestObject.log](#TestObject.log)
  * [TestObject.passed](#TestObject.passed)

### <a name='Lapiz.Test'></a>Lapiz.Test
```javascript
Lapiz.Test(TestName, TestDependencies, TestFunction)
Lapiz.Test(TestName, TestFunction)
```
Defines a test.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Test.Run'></a>Lapiz.Test.Run
```javascript
Lapiz.Test.Run()    
```
Runs all the tests and returns a Result object. The children of the
Result object form a tree containing all the tests.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Result'></a>Result
```javascript
Result
```
Results form a tree where each Result may be associated with a test and
may have children. The leaves of the tree are all tests with no children.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Result.children'></a>Result.children
```javascript
Result.children[]
```
If the Result is a group, the child tests and groups will be listed
here.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Result.defined'></a>Result.defined
```javascript
Result.defined
```
How many tests were defined

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Result.failed'></a>Result.failed
```javascript
Result.failed
```
Number of tests that failed

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Result.fullName'></a>Result.fullName
```javascript
Result.fullName()
```
Only set if the result is a group. It will be full group name ending
with "/".

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Result.passed'></a>Result.passed
```javascript
Result.passed
```
How many tests passed

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Result.ran'></a>Result.ran
```javascript
Result.ran
```
How many tests ran

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Result.test'></a>Result.test
```javascript
Result.test
```
If a Result has a test, it's data is collected here

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Result.test.failed'></a>Result.test.failed
```javascript
Result.test.failed
```
True if the test failed

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Result.test.fullName'></a>Result.test.fullName
```javascript
Result.test.fullName()
```
Full name, including groups

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Result.test.log'></a>Result.test.log
```javascript
Result.test.log()
```
Gets all data written to the test log while the test was running.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Result.test.name'></a>Result.test.name
```javascript
Result.test.name
```
Returns just the test name, not the groups

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Result.test.passed'></a>Result.test.passed
```javascript
Result.test.passed
```
True if the test passed

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Result.test.ran'></a>Result.test.ran
```javascript
Result.test.ran()
```
True if the test ran

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Result.test.time'></a>Result.test.time
```javascript
Result.test.time()
```
How long the test took to run

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='TestDependencies'></a>TestDependencies
```javascript
TestDependencies
["name", "group/", "group/subgroup/"]
```
Dependencies is defined as a slice of strings. A string can indicate a
specific test or a group of tests. To indicate a group, the string should
end with a slash. If a dependency fails, the test will be skipped. The
test runner will figure out the correct order to run the tests. An error
will be thrown if dependencies are missing or if a circular dependency
exists.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='TestFunction'></a>TestFunction
```javascript
TestFunction
function(TestObject)
```
This is the function that will be invoked when the test runs.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='TestName'></a>TestName
```javascript
TestName
"name"
"group/name"
"group/subgroup/name"
```
A test requires a name. Test groups can be nested to an arbitrary
depth.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='TestObject'></a>TestObject
```javascript
TestObject
```
A test object will be passed into each test.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='TestObject.error'></a>TestObject.error
```javascript
TestObject.error(args...)
```
Causes the test to fail and logs the arguments.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='TestObject.fail'></a>TestObject.fail
```javascript
TestObject.fail()
```
Causes the test to fail.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='TestObject.failed'></a>TestObject.failed
```javascript
TestObject.failed()
```
Returns a bool indicating if the test has failed.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='TestObject.log'></a>TestObject.log
```javascript
TestObject.log()
TestObject.log(args...)
```
If no arguments are given, the log is returned as a slice of strings.
If an arguments are given, they will be concatenated into a string and
appended to the log.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='TestObject.passed'></a>TestObject.passed
```javascript
TestObject.passed()
```
Returns a bool indicating if the test is currently passing.

<sub><sup>[&uarr;Top](#__top)</sup></sub>