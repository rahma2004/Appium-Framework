# Mobile App Automation Framework (Appium)

A cross-platform mobile test automation framework built with Java, Appium, and TestNG. Supports both Android and iOS, runs against a local Appium server, and produces Extent Reports for test results.

Built and maintained by **Rahma**.

## Tech Stack
- Java
- Appium (java-client)
- TestNG
- Page Object Model design
- Extent Reports
- Maven

## Features
- Page Object Model structure, separated by platform (`pageObjects/android`, `pageObjects/ios`)
- Platform-specific base test classes (`AndroidBaseTest`, `IOSBaseTest`) handling Appium driver setup/teardown
- Automatic local Appium server bootstrap via `AppiumServiceBuilder`
- Extent Reports integration with TestNG listeners for HTML test reporting
- Screenshot capture on test failure
- JSON-based test data loading (Jackson)
- Hybrid app testing support (native + webview via chromedriver)
- Configurable TestNG suites for Regression and Smoke runs (`testNGSuites/`)
- Maven profiles to run different suites

## Project Structure
```
AppiumFrameworkCloud/
├── src/main/java/org/rahma/pageObjects/   - Page Object classes (Android & iOS)
├── src/main/java/org/rahma/utils/         - Shared Appium utilities, Android/iOS action helpers
├── src/main/java/org/rahma/resources/     - data.properties (device, ports, paths)
├── src/test/java/org/rahma/               - Test classes (Android, iOS, hybrid e-commerce flows)
├── src/test/java/org/rahma/TestUtils/     - Base test classes, Extent reporting, TestNG listeners
├── src/test/java/org/rahma/testData/      - JSON test data
├── src/test/java/org/rahma/resources/     - App binaries (.apk / .app) used as test fixtures
└── testNGSuites/                          - TestNG suite XML files (regression, smoke)
```

## Prerequisites
- JDK 8+
- Maven
- Node.js with Appium 2 installed (`npm install -g appium`)
- Appium drivers: `appium driver install uiautomator2` (Android) and `appium driver install xcuitest` (iOS, macOS only)
- Android SDK with an emulator or a real device (USB debugging enabled)
- Xcode + iOS Simulator (for iOS tests, macOS only)

## Configuration

Update `src/main/java/org/rahma/resources/data.properties` to match your local environment:

```
ipAddress=127.0.0.1
port=4723
browser=chrome
AndroidDeviceNames=<your device/emulator name>
nodeBinPath=<path to your Node.js bin directory>
appiumMainJsPath=<path to your Appium main.js>
chromedriverPath=<path to your chromedriver executable>
```

The framework starts the Appium server for you using these paths — no need to start it manually.

## Running Tests

Full regression suite (Android e2e, error validations, iOS):
```
mvn test -PRegression
```

Smoke suite (tests tagged with the `Smoke` group):
```
mvn test -PSmoke
```

Run a single suite file directly:
```
mvn test -Dsurefire.suiteXmlFiles=testNGSuites/testng.xml
```

## Reports
After a run, the Extent HTML report is generated under `reports/` — open `index.html` in a browser. Screenshots for failed tests are attached automatically via the TestNG listener.
