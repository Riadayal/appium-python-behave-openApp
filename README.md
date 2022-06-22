# How to close/open the app during a session in Real Devices on [LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=LT-appium-python-behave-openApp) using the Appium Python Behave Framework

While performing automation testing with Appium on LambdaTest Grid, you might face a scenario where you'd want to close the application or open the application during a test run. 
This can be essential sometimes to see how your application behaves in different scenarios. Let's see how we can leverage Appium's commands to achieve it on LambdaTest.

**Tip:**

- If you do not have any **.apk** or **.ipa** file, you can run your sample tests on LambdaTest by using our sample :link: [Android app](https://prod-mobile-artefacts.lambdatest.com/assets/docs/proverbial_android.apk) or sample :link: [iOS app](https://prod-mobile-artefacts.lambdatest.com/assets/docs/proverbial_ios.ipa).
- Response of above cURL will be a **JSON** object containing the `App URL` of the format - <lt://APP123456789123456789> and will be used in the next step.
- Alternatively you can also use the `Custom ID` that you defined in your own words.

## Run Your First Test

Once you are done with the above-mentioned steps, you can initiate your first Python test on LambdaTest.

### Configuring Your Test Capabilities

You can update your custom capabilities in test scripts. In this sample project, we are passing platform name, platform version, device name and app url (generated earlier) along with other capabilities like build name and test name via capabilities object. The capabilities object in the sample code are defined as:

<Tabs className="docs__val">

<TabItem value="ios-config" label="iOS" default>

```
import sys
import os
path = os.getcwd()
sys.path.append(os.path.abspath(os.path.join(path, os.pardir)))
from time import time
from behave import given
from appium import webdriver
import appConfig as appConf
from appium.webdriver.common.mobileby import MobileBy
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

@given("Start the android app automation test")
def startAndroidAppAutomationTest(self):
    if os.environ.get("LT_USERNAME") is None:
        username = "username" #Enter LT username here if environment variables have not been added
    else:
        username = os.environ.get("LT_USERNAME")
    if os.environ.get("LT_ACCESS_KEY") is None:
        accesskey = "accesskey" #Enter LT accesskey here if environment variables have not been added
    else:
        accesskey = os.environ.get("LT_ACCESS_KEY")

    driver = webdriver.Remote(
        command_executor="https://"+username+":"+accesskey+"@beta-hub.lambdatest.com/wd/hub",
        desired_capabilities=appConf.app_android_desired_caps
        )
    try:
        colorElement = WebDriverWait(driver,20).until(EC.element_to_be_clickable((MobileBy.ID,"com.lambdatest.proverbial:id/color")))
        colorElement.click()

        textElement = WebDriverWait(driver,20).until(EC.element_to_be_clickable((MobileBy.ID,"com.lambdatest.proverbial:id/Text")))
        textElement.click()

        #Close the application being tested
        driver.close_app()

        #Open the application being tested
        driver.open_app()

        toastElement = WebDriverWait(driver,20).until(EC.element_to_be_clickable((MobileBy.ID,"com.lambdatest.proverbial:id/toast")))
        toastElement.click()

        notification = WebDriverWait(driver,20).until(EC.element_to_be_clickable((MobileBy.ID,"com.lambdatest.proverbial:id/notification")))
        notification.click()

        driver.quit()
    except:
        driver.quit()
```

For more information on the Appium Commands used here, head over to:
* [Launch App | Appium](https://appium.io/docs/en/commands/device/app/launch-app/)
* [Close App | Appium](https://appium.io/docs/en/commands/device/app/close-app/)

## Executing The Tests

Install the required dependencies using the following command:

```bash
pip3 install -r requirements.txt
```

Execute the following command to run your test on LambdaTest platform:

**Android:**

```bash
behave --tags @androidApp
```

**IOS:**

```bash
behave --tags @iosApp
```

</TabItem>

</Tabs>

Your test results would be displayed on the test console (or command-line interface if you are using terminal/cmd) and on the [LambdaTest App Automation Dashboard](https://appautomation.lambdatest.com/build).

## Additional Links

- [Advanced Configuration for Capabilities](https://www.lambdatest.com/support/docs/desired-capabilities-in-appium/)
- [How to test locally hosted apps](https://www.lambdatest.com/support/docs/testing-locally-hosted-pages/)
- [How to integrate LambdaTest with CI/CD](https://www.lambdatest.com/support/docs/integrations-with-ci-cd-tools/)

## Documentation & Resources :books:
      
Visit the following links to learn more about LambdaTest's features, setup and tutorials around test automation, mobile app testing, responsive testing, and manual testing.

* [LambdaTest Documentation](https://www.lambdatest.com/support/docs/?utm_source=github&utm_medium=repo&utm_campaign=LT-appium-python)
* [LambdaTest Blog](https://www.lambdatest.com/blog/?utm_source=github&utm_medium=repo&utm_campaign=LT-appium-python)
* [LambdaTest Learning Hub](https://www.lambdatest.com/learning-hub/?utm_source=github&utm_medium=repo&utm_campaign=LT-appium-python)
* [LambdaTest Community](http://community.lambdatest.com/)    

## LambdaTest Community :busts_in_silhouette:

The [LambdaTest Community](https://community.lambdatest.com/) allows people to interact with tech enthusiasts. Connect, ask questions, and learn from tech-savvy people. Discuss best practises in web development, testing, and DevOps with professionals from across the globe 🌎

## What's New At LambdaTest ❓

To stay updated with the latest features and product add-ons, visit [Changelog](https://changelog.lambdatest.com/) 
      
## About LambdaTest

[LambdaTest](https://www.lambdatest.com) is a leading test execution and orchestration platform that is fast, reliable, scalable, and secure. It allows users to run both manual and automated testing of web and mobile apps across 3000+ different browsers, operating systems, and real device combinations. Using LambdaTest, businesses can ensure quicker developer feedback and hence achieve faster go to market. Over 500 enterprises and 1 Million + users across 130+ countries rely on LambdaTest for their testing needs.    

### Features

* Run Selenium, Cypress, Puppeteer, Playwright, and Appium automation tests across 3000+ real desktop and mobile environments.
* Real-time cross browser testing on 3000+ environments.
* Test on Real device cloud
* Blazing fast test automation with HyperExecute
* Accelerate testing, shorten job times and get faster feedback on code changes with Test At Scale.
* Smart Visual Regression Testing on cloud
* 120+ third-party integrations with your favorite tool for CI/CD, Project Management, Codeless Automation, and more.
* Automated Screenshot testing across multiple browsers in a single click.
* Local testing of web and mobile apps.
* Online Accessibility Testing across 3000+ desktop and mobile browsers, browser versions, and operating systems.
* Geolocation testing of web and mobile apps across 53+ countries.
* LT Browser - for responsive testing across 50+ pre-installed mobile, tablets, desktop, and laptop viewports
    
[<img height="53" width="200" src="https://user-images.githubusercontent.com/70570645/171866795-52c11b49-0728-4229-b073-4b704209ddde.png">](https://accounts.lambdatest.com/register)
      
## We are here to help you :headphones:

* Got a query? we are available 24x7 to help. [Contact Us](support@lambdatest.com)
* For more info, visit - [LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=LT-appium-python-behave-openApp)