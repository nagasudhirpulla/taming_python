## Skill - Automated tests in python with unittest module

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)

Please go through the above skills if necessary for reference or revision
<hr/>

* Python `unittest` module is useful to create and run automated tests in python
* `unittest` module generally comes included with python installation. So no need to install the module separately.

Python unittest module is useful to create and run automated tests in python

### Why do Software testing?
-   Software testing can help to verify whether the code is working in an expected way without errors by running various testing scenarios.
-   This can help to identify bugs by the developer before the end user uses it.

### Why use an Automated Testing Framework?
-   Using an automated testing framework like `unittest` module, we can easily run many tests again and again
-   This can help to run all the tests and ensure the application is working correctly every time the code is modified

### "TestCase" Class with test methods
-   `TestCase` class can have multiple tests as methods. Each test method should start with a prefix “test”
-   “setUp” and “tearDown” methods are special methods inside a TestCase class. These methods are optional.
-   “setUp” method will be called before each test method is executed. So any initialization tasks common to all the test methods can be written in this method
-   “tearDown” method will be called after each test method is executed. So any disposal tasks common to all the test methods can be written in this method

The following is an example of a simple TestCase class in python using unittest module
```python
# test_logic.py
import datetime as dt
import unittest

class TestLogic(unittest.TestCase):
    def setUp(self):
        # this method is called before executing each test method
        # common initialization activities like fetching database connections, api tokens etc. before starting each test method can be done here
        print("\\nsetup called...")
        self.start = dt.datetime.now()

    def testSum(self) -> None:
        """This is a test method that tests addition
        """
        result = 1+8
        self.assertTrue(result == 9)
        self.assertEqual(result, 9)
        self.assertNotEqual(result, 8)

    def testMultiply(self) -> None:
        """This is a test method that tests multiplication
        """
        result = 5*9
        self.assertTrue(result == 45)

    def tearDown(self):
        # this method is called after each test method is executed
        # any common disposal activities like disposing connections, tokens etc. can be done in this method
        print("\\ntear down called...")
        print(f"executed in {dt.datetime.now()-self.start}")

if __name__ == '__main__':
    # run the test case class when this python script is run directly
    # this is optional, you can run tests using command line also, like python -m unittest discover -s "." -p "test*.py"
    unittest.main()

```

-   `unitest.main()` in the above script will run the tests in the TestCase class when the script is run in command line
-   As shown in the above example, each test method can call one or more assert methods. The test method will fail if any one of the assert method fails.
-   The following table shows the various assert methods that can be called inside a test method of a TestClass

| Method | Checks that |
| --- | --- |
| assertTrue(x) | bool(x) is True |
| assertFalse(x) | bool(x) is False |
| assertEqual(a, b) | a == b |
| assertNotEqual(a, b) | a != b |
| assertIsNone(x) | x is None |
| assertIsNotNone(x) | x is not None |
| assertIs(a, b) | a is b |
| assertIsNot(a, b) | a is not b |
| assertIn(a, b) | a in b |
| assertNotIn(a, b) | a not in b |
| assertIsInstance(a, b) | isinstance(a, b) |
| assertNotIsInstance(a, b) | not isinstance(a, b) |

### Run Test Cases in all python files inside a folder with Test Discovery
-   The following command can run all the tests defined in multiple files at once
```bash
python -m unittest discover -s "./tests" -p "test_*.py"
```

-   The above command discovers all the tests from python files starting with “test_” inside a folder named “tests”. The folder name is specified using `-s` flag and filename pattern is specified using `-p` flag

### VS Code support for running and visualizing tests
-   Visual studio code supports unittest framework and provides user-friendly interface to run tests directly from the editor
-   The following steps can be followed to enable unittest support in VS code
    -   Open command palette by pressing Ctrl+Shift+P
    -   Search for “python: configure tests”
    -   Select the testing framework as unittest, select the folder that contains all the tests, select the test files filename pattern. Now the tests support should be enabled in VS Code.
    -   After enabling the tests support in VS Code, the testing preferences will be saved in the “settings.json” file inside the “.vscode” folder. An example “settings.json” file can be as shown below
    ```json
    {
        "python.testing.unittestArgs": [
            "-v",
            "-s",
            ".",
            "-p",
            "test_*.py"
        ],
        "python.testing.pytestEnabled": false,
        "python.testing.unittestEnabled": true
    }    
    ```
-   After setting up tests, the TestCases classes and test methods can be visualized and run in VS Code under the “Testing” tab of the Primary Side bar as shown in the image below
    
    ![vscode_test_menu_demo.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/vscode_test_menu_demo.png)
    
    ### References
-   TestCase class methods setup and teardown - [](https://docs.python.org/3/library/unittest.html#unittest.TestCase)[https://docs.python.org/3/library/unittest.html#unittest.TestCase](https://docs.python.org/3/library/unittest.html#unittest.TestCase)
    
-   Tests Discovery command - [](https://docs.python.org/3/library/unittest.html#test-discovery)[https://docs.python.org/3/library/unittest.html#test-discovery](https://docs.python.org/3/library/unittest.html#test-discovery)

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1MjA5OTA0NCwtMjA4NTAxODkxMl19
-->