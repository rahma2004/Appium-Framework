# Mobile App Automation Framework (Appium + Cloud)

A cross-platform mobile test automation framework built with Java, Appium, and TestNG. Supports both Android and iOS, runs locally or on BrowserStack's cloud device grid, and produces Extent Reports for test results.

## Tech Stack
- Java
- Appium (java-client)
- TestNG
- Page Object Model design
- Extent Reports
- BrowserStack (cloud device execution)
- Maven

## Features
- Page Object Model structure, separated by platform (`pageObjects/android`, `pageObjects/ios`)
- Platform-specific base test classes (`AndroidBaseTest`, `IOSBaseTest`) handling Appium driver setup/teardown
- Local Appium server bootstrap via `AppiumServiceBuilder`
- Cloud execution support via BrowserStack (`browserstack.yml`, `browserstack-java-sdk`)
- Extent Reports integration with TestNG listeners for HTML test reporting
- JSON-based test data loading (Jackson)
- Screenshot capture on test actions
- Configurable TestNG suites for Regression and Smoke runs (`testNGSuites/`)
- Maven profiles to run different suites: `mvn test -PRegression` or `mvn test -PSmoke`

## Project Structure
```
src/main/java/org/rahulshettyacademy/pageObjects/    - Page Object classes (Android & iOS)
src/main/java/org/rahulshettyacademy/utils/          - Shared Appium utilities, Android/iOS action helpers
src/main/java/org/rahulshettyacademy/resources/      - data.properties (device, ports, paths)
src/test/java/org/rahulshettyacademy/                - Test classes (Android, iOS, hybrid e-commerce flows)
src/test/java/org/rahulshettyacademy/TestUtils/       - Base test classes, Extent reporting, TestNG listeners
src/test/java/org/rahulshettyacademy/testData/        - JSON test data
src/test/java/org/rahulshettyacademy/resources/       - App binaries (.apk / .app) used as test fixtures
testNGSuites/                                          - TestNG suite XML files (full regression, smoke)
```

## Configuration

Update `src/main/java/org/rahulshettyacademy/resources/data.properties` to match your local environment:

```
ipAddress=127.0.0.1
port=4723
browser=chrome
AndroidDeviceNames=<your device/emulator name>
nodeBinPath=<path to your Node.js bin directory>
appiumMainJsPath=<path to your Appium main.js>
chromedriverPath=<path to your chromedriver executable>
```

The iOS app path in `IOSBaseTest.java` (`options.setApp(...)`) currently points to a local file path and will need to be updated to match wherever the `.app` bundle is located on your machine.

## Running Tests

```
mvn test -PRegression
```
or
```
mvn test -PSmoke
```

Each profile points to a different TestNG suite XML file under `testNGSuites/`.

## Reporting

Test results are captured via Extent Reports (HTML) and TestNG's default reporting output, generated in `test-output/` after a run (excluded from version control).

## Note on test app binaries
This repo includes small Android (`.apk`) and iOS (`.app`) demo applications used purely as test fixtures for the automation scripts. They are not part of the framework's source code.
