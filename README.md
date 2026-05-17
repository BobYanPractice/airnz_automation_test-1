# Air New Zealand interview take-home assignment.

A professional, scalable, and maintainable test automation framework for the Air New Zealand web application. The framework supports UI testing, API testing, and BDD (Behavior-Driven Development) using Cucumber, with AI-assisted development and automation capabilities.

## 📋 Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Running Tests](#running-tests)
- [Reporting](#reporting)
- [Best Practices](#best-practices)
- [Contributing](#contributing)

## ✨ Features

- **Multi-Browser Support**: Chrome, Firefox, Edge, Safari
- **Page Object Model (POM)**: Clean separation of page elements and test logic
- **API Testing**: RESTful API testing with RestAssured
- **BDD Support**: Cucumber integration with Gherkin syntax
- **Parallel Execution**: Run tests in parallel for faster execution
- **Cross-Environment**: Support for QA, Staging, and Production environments
- **Comprehensive Reporting**: Allure and Extent Reports integration
- **Screenshot Capture**: Automatic screenshots on test failure
- **Logging**: Detailed logging with Log4j2
- **Data-Driven Testing**: External test data management with JSON
- **CI/CD Ready**: Easy integration with Jenkins, GitHub Actions, etc.

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Test Layer                                │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │   UI Tests  │  │  API Tests  │  │  BDD Tests (Cucumber)   │  │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
├─────────────────────────────────────────────────────────────────┤
│                      Business Layer                              │
│  ┌─────────────────┐  ┌─────────────────┐  ┌────────────────┐   │
│  │   Page Objects  │  │   API Services  │  │ Step Definitions│  │
│  └─────────────────┘  └─────────────────┘  └────────────────┘   │
├─────────────────────────────────────────────────────────────────┤
│                       Core Framework                             │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐│
│  │ Config   │ │ Factory  │ │  Utils   │ │Listeners │ │Constants││
│  │ Manager  │ │(Browser) │ │ (Wait,   │ │          │ │         ││
│  │          │ │          │ │Screenshot│ │          │ │         ││
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └────────┘│
├─────────────────────────────────────────────────────────────────┤
│           Infrastructure (Selenium, RestAssured, TestNG)         │
└─────────────────────────────────────────────────────────────────┘
```

## 📦 Prerequisites

- **Java JDK 17** or higher
- **Maven 3.8+**
- **Chrome/Firefox/Edge** browser installed
- **Git** for version control
- **IDE**: Eclipse, IntelliJ IDEA, or VS Code

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/airnz/automation-test.git
cd automation-test
```

### 2. Install Dependencies

```bash
mvn clean install -DskipTests
```

### 3. Verify Installation

```bash
mvn test -Dtest=LoginTest#testLoginPageLoads
```

## 📁 Project Structure

```
airnz_automation_test/
│
├── src/
│   └── com/
│       └── airnz/
│           │
│           ├── core/                    # Framework core components
│           │   ├── config/              # Configuration management
│           │   │   ├── ConfigManager.java
│           │   │   └── DriverManager.java
│           │   ├── factory/             # Browser factory
│           │   │   └── BrowserFactory.java
│           │   ├── constants/           # Framework constants
│           │   │   └── FrameworkConstants.java
│           │   ├── listeners/           # TestNG listeners
│           │   │   └── TestListener.java
│           │   └── utils/               # Utility classes
│           │       ├── WaitUtils.java
│           │       ├── ScreenshotUtils.java
│           │       ├── JsonUtils.java
│           │       └── TestDataLoader.java
│           │
│           ├── pages/                   # Page Object classes
│           │   ├── BasePage.java
│           │   ├── HomePage.java
│           │   ├── BookingPage.java
│           │   ├── TicketPage.java
│           │   └── LoginPage.java
│           │
│           ├── api/                     # API testing components
│           │   ├── client/
│           │   │   └── ApiClient.java
│           │   ├── models/
│           │   │   ├── Ticket.java
│           │   │   └── BookingResponse.java
│           │   └── services/
│           │       └── BookingService.java
│           │
│           ├── tests/                   # Test classes
│           │   ├── ui/
│           │   │   ├── BookingTest.java
│           │   │   └── LoginTest.java
│           │   ├── api/
│           │   │   ├── BookingAPI.java
│           │   │   └── LoginApiTest.java
│           │   └── bdd/
│           │       ├── stepdefinitions/
│           │       │   ├── LoginSteps.java
│           │       │   ├── BookingSteps.java
│           │       │   └── Hooks.java
│           │       ├── runners/
│           │       │   └── TestRunner.java
│           │       └── features/
│           │           ├── Booking.feature
│           │           └── login.feature
│           │
│           └── resources/               # Test resources
│               ├── config/
│               │   ├── qa.properties
│               │   └── selenium.properties
│               ├── testdata/
│               │   ├── BookingData.json
│               │   ├── TicketData.json
│               │   └── loginData.json
│               └── log4j2.xml
│
├── reports/                             # Test reports output
├── logs/                                # Log files
├── pom.xml                              # Maven configuration
├── testng.xml                           # TestNG suite configuration
└── README.md                            # This file
```

## ⚙️ Configuration

### Environment Configuration

Edit `src/com/airnz/resources/config/qa.properties`:

```properties
base.url=https://www.airnewzealand.co.nz
api.base.url=https://api.airnewzealand.co.nz
```

### Selenium Configuration

Edit `src/com/airnz/resources/config/selenium.properties`:

```properties
browser=chrome
headless=false
implicit.wait=10
explicit.wait=15
```

### Test Data

Test data is stored in JSON files under `src/com/airnz/resources/testdata/`:

- `loginData.json` - Login test scenarios
- `BookingData.json` - Flight booking scenarios
- `TicketData.json` - Passenger and ticket data

## 🏃 Running Tests

### Run All Tests

```bash
mvn clean test
```

### Run Specific Test Class

```bash
mvn test -Dtest=LoginTest
```

### Run Specific Test Method

```bash
mvn test -Dtest=LoginTest#testValidLogin
```

### Run Tests by Profile

```bash
# Smoke tests
mvn test -Psmoke

# Regression tests
mvn test -Pregression

# API tests only
mvn test -Papi

# UI tests only
mvn test -Pui

# BDD/Cucumber tests
mvn test -Pbdd
```

### Run Tests with Parameters

```bash
# Different browser
mvn test -Dbrowser=firefox

# Headless mode
mvn test -Dheadless=true

# Different environment
mvn test -Denv=staging

# Combined parameters
mvn test -Dbrowser=chrome -Dheadless=true -Denv=qa
```

### Run Cucumber Tests with Tags

```bash
mvn test -Pbdd -Dcucumber.filter.tags="@smoke"
mvn test -Pbdd -Dcucumber.filter.tags="@regression"
mvn test -Pbdd -Dcucumber.filter.tags="@booking and not @wip"
```

## 📊 Reporting

### Allure Reports

Generate Allure report:

```bash
mvn allure:serve
```

Or generate HTML report:

```bash
mvn allure:report
```

Reports are generated in `target/site/allure-maven-plugin/`

### Cucumber Reports

Cucumber reports are generated in:
- HTML: `reports/cucumber-reports/cucumber-html-report.html`
- JSON: `reports/cucumber-reports/cucumber.json`

### Screenshots

Failed test screenshots are saved in `reports/screenshots/`

## 🎯 Best Practices

### Page Object Model

```java
public class LoginPage extends BasePage {
    @FindBy(css = "[data-testid='email-input']")
    private WebElement emailInput;
    
    public LoginPage enterEmail(String email) {
        type(emailInput, email);
        return this;
    }
}
```

### Fluent Interface Pattern

```java
homePage
    .selectReturnTrip()
    .enterOrigin("Auckland")
    .enterDestination("Wellington")
    .enterDepartureDate("15 Jun 2026")
    .searchFlights();
```

### Data-Driven Testing

```java
@DataProvider(name = "loginData")
public Object[][] loginDataProvider() {
    return new Object[][] {
        {"validLogin", true},
        {"invalidPassword", false}
    };
}
```

### BDD Scenarios

```gherkin
@smoke
Scenario: Successful login with valid credentials
  Given I am on the login page
  When I enter valid login credentials
  And I click the login button
  Then I should be logged in successfully
```

## 🔧 IDE Setup

### Eclipse

1. Import as Maven Project: `File > Import > Maven > Existing Maven Projects`
2. Select the project root directory
3. Install TestNG plugin from Eclipse Marketplace
4. Install Cucumber plugin for feature file support

### IntelliJ IDEA

1. Open project: `File > Open > Select pom.xml`
2. Enable auto-import for Maven
3. Install Cucumber and TestNG plugins

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 Code Standards

- Follow Java naming conventions
- Add Javadoc comments for all public methods
- Write meaningful test descriptions
- Keep methods focused and small
- Use descriptive variable names

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

For support, email automation-team@airnz.co.nz or create an issue in this repository.

---

**Built with ❤️ by the AirNZ Automation Team**
