# This repository contains the solutions to the two tasks in Tech-Test-Web:

## First task - testing currency conversion form

The answers to the questions on the first currency conversion form testing task is provided within the Word document titled `TechTestWeb.docx` at the root directory.

## Second task - E2E Test Project

Collection of E2E tests for WTW User Journeys in the second task is build with the Jest framework and used Chrome DevTool's Puppeteer protocol as the runner. 

## Background
- The  scenarios provided in the challenge are organised in one test suite spec file.
- Only the happy path of the user journey is mainly focussed with a few assertions in the flow; the rationale is that the E2E test should be minimal in a test pyramid and should be kept as such in order to eneble faster feedback and hence be used mainly in CI/CD pipeline - the rest of the tests should be covered at a lower layer of the test pyramid
- The reporting of tests results with breakdown is integrated with allure. 


## Installation & Setup

### System Dependencies
Make sure node is installed in your system e.g. for macOS `brew install node`. For running the tests in Chrome browser the path to the Chrome executable should be set correctly. This can be verified by going to `chrome://version/` on your browser and copying the path from there to the `puppeteer.config.json` file at the root directory of this project. If you want to generate additional reporting with allure, the system should have allore server installed with command like `brew install allure` and for accessing from npm `npm install -g allure-commandline`

### Test setup
If you are accessing the project in this directory for the first time, please run `npm install` to install all the dependencies.
Once the installation is complete, run the tests using `npm test`
After running the tests, you can find the generated screenshots in the `screenshots` directory.

## Available Automation Commands
- `npm test` - run tests in command-line
- `npm run report` - see report in browser with [Allure server](https://github.com/allure-framework/allure2)

## puppeteer.config.json

- `incognito` - when true the test will run in incognito window
- `puppeteer.launch` - options to pass to [puppeteer.launch](https://pptr.dev/#?product=Puppeteer&version=v2.1.0&show=api-puppeteerlaunchoptions)
- `puppeteer.connect` - options to pass to [puppeteer.connect](https://pptr.dev/#?product=Puppeteer&version=v2.1.0&show=api-puppeteerconnectoptions)

### Example:

```
{
  "incognito": true,
  "puppeteer.connect": {
    "browserWSEndpoint": null,
    "ignoreHTTPSErrors": true
  },
  "puppeteer.launch": {
    "product": "chrome",
    "headless": false,
    "devtools": false,
    "ignoreHTTPSErrors": true,
    "slowMo": 30,
    "args": [
      "--start-maximized",
      "--ignore-certificate-errors"
    ],
    "executablePath": "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
  }
}
```
## TODO w.r.t Limitation, Improvements, and thought process of choosing the platform
- Although the suites in this test project are ready to be integrated in a CI/CD pipeline e.g. CircleCI, a dockarized version with tests running against a local instance of the website will improve the performance.
- Additionally, instead of running these tests against the real production API, in an ideal world I'd prefer to run these against a mocked API using PACT contracts
- In summary, in this project I've demonstrated the possibility of utilising jest+puppeteer as a potential solution for executing the E2E tests for the  Website. This has potential for faster and reliable development of test code and can act as a layer on top of existing tests e.g. with Cypress and/or co-exist as an additional layer in the CI/CD pipeline. Collecting some metrics on the test run and error handling will also be important to consider using this framework in comparison to others.


#