ATIP - a new "behave" binding library
===============

## Introduction

ATIP(Application Test in Python), a “behave” binding library as the bridge between application and BDD to “behave”, and use WebDriver and platform interfaces to implement detailed BDD steps for application. 

## Configuration

Environmental controls. In ATIP usage, you can write the environment initial processes in config file - environment.py. ATIP provides a template of "environment.py" for tests developers. This template supports running tests independently by "behave" tool.

In Crosswalk testing, the template need to know the some test vars, e.g. which device be tested? which test platform? Some WebDriver vars. the vars can be got by following ways:  

* By environment vars:  
  TEST_PLATFORM: android, tizen, chrome_ubuntu, others(if have)   
  DEVICE_ID    
  CONNECT_TYPE: adb, sdb   
  WEBDRIVER_VARS: webdriver_url, desired_capabilities, others  
  LAUNCHER: XWalkLauncher, CordovaLauncher

ATIP source provides a script "tools/set_env.sh" which can help you to setup those environment vars. Especially, the environment.py template can get those environment vars from Testkit-lite tool automatically:

A JSON config file which named "webdriver.json for environment vars sharing, a template provided for reference: "atip/tools/webdriver.*.json"  

* Configuration source layout
```
tools/
├── set_env.sh
├── webdriver.chrome.json
├── webdriver.xw_android_cordova.json
├── webdriver.xw_android_xwalk.json
└── webdriver.xw_tizen.json
```

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
  
A simple feature example as below
```
Feature: api tests
    Scenario: api test 001
        When launch "haha"
         And I go to "http://www.google.com"
         And I wait for 1 seconds
```

* steps.py  
  
A simple step example as below
```
@step(u'I go to "{url}"')
def i_visit_url(context, url):
    url = get_page_url(context, url)
    assert context.app.switch_url(url, True)
```

## ATIP Library  

* Functions Category  
  "web": web based(Webdriver API) functions  
  "native": native based functions (TBD)  
  "common": common operations cross different platforms, e.g. call python image lib to compare image files  
  "android": Android platform specific functions  
  "tizen": Tizen platform specific functions  

* "web" steps  
```
@step(u'I go to "{url}"')
@step(u'I reload')
@step(u'I go back')
@step(u'I go forward')
@step(u'The current URL should be "{text}"')
@step(u'I should see title "{text}"')
@step(u'I should see "{text}"')
@step(u'I should not see "{text}"')
@step(u'I should see "{text}" in {timeout:d} seconds')
@step(u'I should not see "{text}" in {timeout:d} seconds')
@step(u'I should see "{text}" in "{key}" area')
@step(u'I press "{key}"')
@step(u'press "{key_c}" in "{key_p}"')
@step(u'I click "{key}"')
@step(u'click "{key_c}" in "{key_p}"')
@step(u'I click coords {x:d} and {y:d} of "{key}"')
@step(u'I fill in "{key}" with "{text}"')
@step(u'I check "{key}"')
@step(u'I uncheck "{key}"')
@step(u'I should see an alert')
@step(u'I should not see an alert')
@step(u'I accept the alert')
@step(u'I should see an alert with text "{text}"')
```

* "common" steps  
```
@step(u'I wait for {timeout:d} seconds')
@step(u'launch "{app_name}"')
@step(u'I launch "{app_name}" with "{apk_pkg_name}" and "{apk_activity_name}"')
@step(u'switch to "{app_name}"')
@step(u'call "{js}" scripts') - TBD
@step(u'call PIL to handle "{image_file}"') - TBD
```

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

