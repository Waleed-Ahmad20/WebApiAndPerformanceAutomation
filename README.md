# Web API and Performance Test Automation

This repository contains automated test suites for both Web API testing and Performance testing against the [ReqRes](https://reqres.in/) sample REST API.

## Project Structure

```
22I2647_22I2642/
├── WebAPITestAutomation/        # REST API test automation project
│   └── GradleProjects/          # Gradle-based Java project
│       └── app/
│           └── src/
│               ├── main/java/com/reqres/
│               │   ├── payloads/ApiPayloads.java   # Request payload builders
│               │   └── utils/RestClient.java        # HTTP client wrapper
│               └── test/java/com/reqres/
│                   ├── UserApiTests.java            # User endpoint tests
│                   └── ResourceApiTests.java        # Resource endpoint tests
├── PerformanceTestAutomation/   # JMeter performance test plan
│   └── UserApiLoadTest.jmx      # Load test scenario
├── Documentation.pdf            # Project documentation
├── QualityAndTestingRequirements.pdf
└── setup.mp4                    # Setup walkthrough video
```

## Prerequisites

- **Java 21** (JDK)
- **Gradle 8.8+**
- **Apache JMeter** (for performance tests)

## Web API Test Automation

The API tests are written in Java using **REST Assured** and **JUnit 5**, with **Allure** for reporting. Tests cover the `/api/users` and `/api/unknown` (resources) endpoints of the ReqRes API.

### Test Coverage

**User API (`UserApiTests.java`)**
- List Users — `GET /api/users?page=2` (expects 200)
- Create User — `POST /api/users` (expects 201)
- Update User — `PUT /api/users/2` (expects 200)
- Delete User — `DELETE /api/users/2` (expects 204)

**Resource API (`ResourceApiTests.java`)**
- List Resources — `GET /api/unknown` (expects 200)
- Create Resource — `POST /api/unknown` (expects 201)
- Update Resource — `PUT /api/unknown/2` (expects 200)
- Delete Resource — `DELETE /api/unknown/2` (expects 204)

### Running the API Tests

```bash
cd 22I2647_22I2642/WebAPITestAutomation/GradleProjects
./gradlew test
```

To generate and open the Allure report after the test run:

```bash
./gradlew allureReport
./gradlew allureServe
```

### Key Dependencies

| Library | Version | Purpose |
|---|---|---|
| REST Assured | 5.3.0 | HTTP request/response handling |
| JUnit Jupiter | 5.10.0 | Test framework |
| Allure JUnit 5 | 2.21.0 | Test reporting |
| org.json | 20210307 | JSON payload construction |

## Performance Test Automation

Load testing is performed using **Apache JMeter**. The test plan (`UserApiLoadTest.jmx`) simulates concurrent user load on the ReqRes User API.

### Running the Performance Tests

1. Open JMeter and load `22I2647_22I2642/PerformanceTestAutomation/UserApiLoadTest.jmx`.
2. Configure thread count and ramp-up period as required.
3. Run the test plan and review the results in the JMeter listeners.

Alternatively, run headlessly from the command line:

```bash
jmeter -n -t 22I2647_22I2642/PerformanceTestAutomation/UserApiLoadTest.jmx -l results.jtl
```

## Documentation

- `Documentation.pdf` — Detailed project documentation covering design and implementation.
- `QualityAndTestingRequirements.pdf` — Quality and testing requirements specification.
- `setup.mp4` — Video walkthrough for setting up and running the project.
