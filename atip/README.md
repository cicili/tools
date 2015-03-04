ATIP - a new "behave" binding library
===============

## Introduction

ATIP(Application Test in Python), a “behave” binding library as the bridge between application and BDD to “behave”, and use WebDriver and platform interfaces to implement detailed BDD steps for application. 

## Configuration - environment.py

Environmental controls. In ATIP usage, you can write the environment initial processes on this file. ATIP provides a template of "environment.py" for tests developers. This template supports running tests independently by "behave" tool.

In Crosswalk testing, the template need to know the some test vars, e.g. which device be tested? which test platform? Some WebDriver vars. the vars can be got by following ways:

* By environment vars:  
  TEST_PLATFORM: android, tizen, chrome_ubuntu, others(if have)   
  DEVICE_ID    
  CONNECT_TYPE: adb, sdb   
  WEBDRIVER_VARS: webdriver_url, desired_capabilities, others  
  LAUNCHER: XWalkLauncher, CordovaLauncher

ATIP source provides a script "tools/set_env.sh" which can help you to setup those environment vars. Especially, the environment.py template can get those environment vars from Testkit-lite tool automatically:

A JSON config file which named "webdriver.json for environment vars sharing, a template provided for reference: "atip/tools/webdriver.*.json"

## Tests Development
Before below sections, you'd better already pretty familiar with the tests developing with "behave": "behave" docs. A typical "behave" based tests source layout as below:

```
tests/
  ├── environment.py

  ├── steps

  │   └── steps.py

  └── test.feature
```

* test.feature

* steps.py

## Features Status

* Features Done 
  Environment initialization from config file  
  Environment initialization from test tools/system environment vars  
  Support Crosswalk on Tizen and Android  
  Crosswalk application launching  
  Basic WebDriver based steps  

* Features In Plan


## Run Tests 

* Testkit-lite: Please check testkit-lite project for details
* Behave: setup test ENVs by set_env.sh or webdriver.json firstly, then run "behave" as:  
  cd path-to/tests  
  behave  

