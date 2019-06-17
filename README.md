# protractor_starter
A starter for Protractor which is an end to end automation test framework.

## Features
### Test Like a User
Protractor is built on top of WebDriverJS, which uses native events and browser-specific drivers to interact with your application as a user would.
### For Angular Apps
Protractor supports Angular-specific locator strategies, which allows you to test Angular-specific elements without any setup effort on your part.
### Automatic Waiting
You no longer need to add waits and sleeps to your test. Protractor can automatically execute the next step in your test the moment the webpage finishes pending tasks, so you don’t have to worry about waiting for your test and webpage to sync.

## How Protractor work
Although Protractor documentation has a detailed explanation on how the process works, I would like to brief the whole process in short,

Protractor Tests <----> Selenium Server <----> Browser(Chrome, Firefox etc.,)

Selenium server can be a standalone server or a sauce lab server which will be getting requests from tests and makes a REST API Call(Webdriver JSON Protocol) to Browser and performs actions. Every action in tests is a REST call to browser by Selenium server. For example,
```javascript
element(by.css('button.myclass')).click();
```
The equivalent REST call from Selenium server to browser will be,

* /session/:sessionId/execute_async - First, Protractor tells the browser to run a snippet of JavaScript. This is a custom command which asks Angular to respond when the application is done with all timeouts and asynchronous requests, and ready for the test to resume.

* /session/:sessionId/element - Then, the command to find the element is sent.

* /session/:sessionId/element/:id/click - Finally the command to perform a click action is sent.

Awesome documentatoin given by Protractor team, check it out [here](https://www.protractortest.org/#/infrastructure). 



