# protractor_starter
A starter for Protractor which is an end to end automation test framework. 
This explanation is not intended to tell, how to write a protractor test. I am emphasizing more on how protractor works, it's setup and common problems during setup.

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

Selenium server can be a standalone server or a sauce lab server which will be getting requests from tests and makes a REST API Call([JSON Wire Protocol](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol)) to Browser and performs actions. Every action in tests is a REST call to browser by Selenium server. For example,
```javascript
element(by.css('button.myclass')).click();
```
The equivalent REST call from Selenium server to browser will be,

* /session/:sessionId/execute_async - First, Protractor tells the browser to run a snippet of JavaScript. This is a custom command which asks Angular to respond when the application is done with all timeouts and asynchronous requests, and ready for the test to resume.

* /session/:sessionId/element - Then, the command to find the element is sent.

* /session/:sessionId/element/:id/click - Finally the command to perform a click action is sent.

Awesome documentatoin given by Protractor team, check it out [here](https://www.protractortest.org/#/infrastructure). 

## Getting Started
### Start Selenium Server
Use npm to install Protractor globally with
```
npm install -g protractor
```
This will install two command line tools, *protractor* and *webdriver-manager*. Try running *protractor --version* to make sure it's working.

The *webdriver-manager* is a helper tool to easily get an instance of a Selenium Server running. Use it to download the necessary binaries with:
```
webdriver-manager update
```
Now start up a server with:
```
webdriver-manager start
```
This will start up a Selenium Server and will output a bunch of info logs. Your Protractor test will send requests to this server to control a local browser. Leave this server running to run tests. You can see information about the status of the server at http://localhost:4444/wd/hub.

### Write your first protractor test
Follow this [link](http://www.protractortest.org/#/tutorial) to write your first test. 

### Run your test
```
 protractor <<path to the protractor configuration file>>
```
## Common Issues
1) > _E/launcher - session not created: This version of ChromeDriver only supports Chrome version 75_ .

* Selenium webdriver is an executable which drives system browser. Every version of browser will have its own selenium webdriver. 
* Webdriver manager installs latest browser specific webdriver, irrespective of what version of browser available in the system. If both browser and selenium webdriver versions are mismatched, we get the above issue.

_Resolution would be, either update system browser to latest version or install appropriate selenium webdriver,
To install appropriate version of selenium webdriver (command below works for chrome) :_
```
webdriver-manager update --version.chrome <<browser version>>
```

2) > E/launcher - Error code: 135
[10:05:45] E/launcher - Error message: ECONNREFUSED connect ECONNREFUSED 127.0.0.1:4444
[10:05:45] E/launcher - Error: ECONNREFUSED connect ECONNREFUSED 127.0.0.1:4444 .

* It says selenium server is not running.

_Resolution would be, start selenium server (Refer to start selenium server step above)._

## Clone this project
Clone this project to start writing tests for protractor. Checkout [protractor api](http://www.protractortest.org/#/tutorial) to start writing tests. This link has all the required documentaion references to play with protractor.

Enjoy Protractor folks!! 



