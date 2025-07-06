#Testing 

## 🧪 **Test Automation Frameworks**

|Tool|Use / Description|Languages|Notes|
|---|---|---|---|
|**JUnit**|Unit testing for Java apps|Java|Core tool for Java testing|
|**TestNG**|More flexible than JUnit|Java|Parallel test execution, annotations|
|**PyTest**|Unit and functional testing in Python|Python|Fixtures, plugins, clear syntax|
|**GoogleTest (gtest)**|Unit testing C/C++|C++|Widely used for embedded or system-level C++|
|**Catch2**|Header-only C++ unit test framework|C++|Simple, modern syntax|
|**CUnit**|Lightweight testing for C|C|Low-level, basic assertion framework|
|**Mocha + Chai**|JavaScript test runner with assertions|JavaScript / Node.js|Used in web development|
|**Jest**|Full-featured JS testing with coverage, mocking|JavaScript|Made by Meta, great for React|
|**NUnit / xUnit**|Unit testing in .NET|C#, F#|NUnit is popular; xUnit is newer|
|**PHPUnit**|Unit testing in PHP|PHP|Common in Laravel & Symfony apps|


## 🛠️ **CI/CD Tools With Testing Integration**

|Tool|Description|Language Support|Notes|
|---|---|---|---|
|**GitHub Actions**|Workflow automation with test steps|Any (via runners/scripts)|Native with GitHub|
|**GitLab CI**|Built-in pipeline runner|Any|YAML config, container support|
|**CircleCI**|Fast pipelines with test integration|Any|Great for parallel tests|
|**Bamboo**|CI/CD from Atlassian|Java-based, runs any script|Integrates well with JIRA|
|**Jenkins**|Widely used automation server|Any|Powerful but needs maintenance|

## 📊 **Code Quality & Coverage Tools**

|Tool|Use|Languages|Notes|
|---|---|---|---|
|**SonarQube**|Code quality, security, coverage|Java, Python, JS, C++, more|Static analysis with UI|
|**Cobertura**|Java code coverage|Java|Often used with Jenkins|
|**gcov / lcov**|Coverage for C/C++|C/C++|Works with gcc|
|**Coverage.py**|Coverage for Python|Python|Integrates with PyTest|

## 🔄 **Mocking & Stubbing**

|Tool|Use|Languages|Notes|
|---|---|---|---|
|**Mockito**|Mocking framework|Java|Great for unit testing services|
|**unittest.mock**|Built-in mocking|Python|Simple, clean for patching|
|**Sinon.js**|Spies, mocks, and stubs|JavaScript|Common with Mocha/Jest|
|**GoogleMock**|Part of GoogleTest|C++|Needs a bit of setup|

### 📘 Bonus: Tools by Use Case

| Use Case              | Tools to Look Into                       |
| --------------------- | ---------------------------------------- |
| Web app E2E           | Cypress, Playwright, Selenium            |
| Unit testing (Java)   | JUnit, TestNG                            |
| Unit testing (Python) | PyTest, unittest                         |
| C/C++ code            | GoogleTest, Catch2, CMocka               |
| Mobile apps           | Appium, Espresso (Android), XCTest (iOS) |
| BDD (Behavior-Driven) | Cucumber, Behave, SpecFlow               |
| CI/CD integration     | Jenkins, GitHub Actions, GitLab CI       |