Jukin Media Test Automation
===

This is test automation developed to automate Jukin Media consumer site scenarios on Windows, MAC and Device (Android and iOS) browsers.

## JukinMedia Test Automation Configuration & Execution Instructions

### Prerequisites:

1. Maven should be installed to run project.

2. Groovy should be installed in MAC/Windows.

3. Ensure below browsers are installed -

   a. MAC and Windows - Firefox browser > version 57
   
   b. iOS device - Safari browser <min. version>
   
   c. Android -  Chrome browser <min. version>

### SetUp on Desktop (MAC/Windows) execution

     a. Firefox browser version 57 or above should be installed.
	  b. Download geckodriver  - 'geckodriver-v0.19.1-macos.tar.gz' on MAC using https://github.com/mozilla/geckodriver/releases
	  c. Extract folder using command 'tar -xvf geckodriver-v0.19.1-macos.tar.gz' from Terminal
	  d. Setup the environment variable for above geckodriver path using below steps- 
	   1. Open bash file using command 'open ~/.bash_profile'
	   2. add export PATH = $PATH:<MAC gecodriver path> command in bash file.
	   3. Save file & then execute 'source ~/.bash_profile' commands to save changes
	   4. Verify path with command 'echo $PATH'
	  e. For Windows, No need to do any setting. Because geckodriver.exe file is kept in project folder and will be read programiticaly.

### SetUp for device execution

#### A. Setup on MAC for iOS and Android devices:

1.	Download Appium server(appium-1.2.7.dmg) from link https://github.com/appium/appium-desktop/releases and install. 
2.	To download SDK-    
    a. (android-studio-ide-171.4443003-mac.dmg) from URL - https://developer.android.com/studio/index.html                
    b. Extract folder and set the path of bin folder in PATH environment variable.   
       If there is no "platform-tools" folder, than -     
  	c. Execute command 'sdkmanager "platform-tools" "platforms;android-26"' from terminal                      
	  d. Set the path of 'platform-tools' folder in PATH environment variable       

3.	Create ANDROID_HOME and JAVA_HOME as an environment variables and add in to .bash_profile file-    
    a. Open bash file using command 'open ~/.bash_profile' (If file is not exist please create it)     
    b. add both variable using export commands.   
       for examples:    
	     export Android_HOME=/Users/techm/AndroidSDK/Platform-tools    
       export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_60    
   	c. Save file & then execute 'source ~/.bash_profile' commands to save changes   
  	d. Check path with command 'echo $PATH'   
  
4.  Install Groovy using  'brew install groovy' command

5.  Run below Terminal Commands to install required dependency:         
	  a. brew install libimobiledevice    
	  b. brew install carthage    
	  c. npm install -g ios-deploy     
	  d. brew install ios-webkit-debug-proxy    

6.  Install “SafariLauncherApp” on iPhone:    
    To build, install “SafariLauncherApp” app, we need to add provisioning profile/P12 Certificate & Bundle Identifier that can be used     to deploy the SafariLauncher App on device. (Based on device iOS version, we can build & deploy App from Xcode)     
    Please refer - http://appium.io/docs/en/drivers/ios-uiautomation-safari-launcher/index.html

7.  Install WebDriverAgent:    
    1. Open WebDriverAgent in xcode    
    2. Applications/Appium.app/Contents/Resources/app/node_modules/appium/node_modules/appium-xcuitest-driver/WebDriverAgent and click         on webdriverAgent.xcodeproj     
    3. Select “WebdriverAgentRunner” in Xcode & Select Target as iPhone      
    4. Add bundle identifier & valid certificate (p.12)     
       (Targets)     
       a. WebDriverAgentLib (Add bundle Identifier)     
       b. WebdriverAgentRunner (Add bundle Identifier)      
       c. Unit Tests (Add bundle Identifier)     
       d. IntegrationTets_1 (Add bundle Identifier & Target App as “IntegrationApp”)    
       e. IntegrationTets_2 (Add bundle Identifier & Target App as “IntegrationApp”)    
       f. IntegrationTets_3 (Add bundle Identifier & Target App as “IntegrationApp”)    
       g. IntegrationApp (Add bundleIdentifire)     


8.	Open Appium.app by double click from Applications folder and set the Host name as 127.0.0.1 and port 4723.     

9.  Ensure Chrome browser is installed in Android device.    

10. Ensure Safari browser is installed and running in iOS device.   

#### B. SetUp on Windows:

1.  Download Appium server(appium-1.2.7.exe) from link https://github.com/appium/appium-desktop/releases and install.    

2.	To download Android SDK-    
    a. (android-studio-ide-171.4443003-windows.exe for Windows 64 bit) from URL - https://developer.android.com/studio/index.html    
	  b. Extract folder and set the path of bin folder in PATH environment variable.      
    If there is no "platform-tools" folder, than -    
	  c. Execute command 'sdkmanager "platform-tools" "platforms;android-26"' from command line      
	  d. Set the path of 'platform-tools' folder in PATH environment variable.   
	
3.  Create  ANDROID_HOME and JAVA_HOME as an environment variables using System->Advance System Settings-> Environment variables-> New    	  for examples:    
	  Android_HOME=D:\android-sdk_r24.4.1-windows\android-sdk-windows    
    JAVA_HOME=C:\Program Files\Java\jdk1.8.0_660    
	  PATH = D:\Technical\android-sdk_r24.4.1-windows\android-sdk-windows\platform-tools; C:\Program Files\Java\jdk1.8.0_660\bin    
       
4.	For real device connection: Use below commands from command prompt-    
      adb kill-server    
      adb start-server   
      adb devices    
      
5.  Open Appium.exe and set the Host name as 127.0.0.1 and port 4723  

6.  Install Chrome browser in Android device if not already there.   

### Change Configuration and Environment
 
1. Update src/test/resources/Config.groovy file for device capabilities value like Device ID/Udid, OS platform version etc. as per below    given steps:
   
   Mobile Device Capabilities data: Open “src/test/resources/Config.groovy” file, in notepad or eclipse and change the below device        capabilities data in relevant Android and iOS Capabilities section.

   //# For Android Capabilities -   
   aDeviceName = 'HTC One'  (Optional)   
   aPlatformVersion = '6.0.1'    
   aDeviceID = '4100b553f25ea267'    
   
   //# For IOS Capabilities. -   
   iDeviceName = 'iPhone 6s'   
   iPlatformVersion = '11.2'   
   iUdid = '7f22c27b2bdcc2c3d2e35587de243ccf4ed9bd7c'   

   To get Android device ID: To get the Device ID for Android device, execute “adb devices” in command prompt and copy the first long digit number like '4100b553f25ea267' and past as device id value  
   
   To get Android device ID: To get UDID for iOS device, use iTunes. (please refer "https://www.innerfence.com/howto/find-iphone-unique-device-identifier-udid")  

### How To build project

	1. Download or clone 'JukinMediaConsumerSiteTest' project from Git repository to local machine.  
	2. Navigate to 'JukinMediaConsumerSiteTest' project folder from terminal or command prompt.   
	3. Execute below command-   
       mvn clean install  
   
	   Note - This command is required to execute with every changes you made in project (like data, configuration etc.), 

### Execution Steps  

#### Execution on Desktop (MAC and Windows):

    mvn -Dtest=CrossBrowserJukinVideoSubmission_WinNMac_Spec test
	
#### Execution on iOS device:

1. To execute iOS scripts, Start Appium server.  

2. Connect iphone device using USB cable   

3. Enable UI Automation on iOS (Settings > Developer)    

4. Start iOS webkit debug proxy:    
   ios-webkit-debug-proxy -c <device-udid>: 27753  
	
5. Open terminal and navigate to JukinMediaConsumerSiteTest folder or Local project repository folder.   

6. Execute below commands from command prompt/Terminal-   
    
	mvn -Dtest=CrossBrowserJukinVideoSubmission_iOS_Spec test   

#### Execution for Android device:  

1.	To execute Android scripts, Start Appium server.   

2.  Connect Android device using USB cable.  

3.	Open command prompt and navigate to JukinMediaConsumerSiteTest folder or Local project repository folder.    

4.	Execute below commands from command prompt/Terminal-   

    mvn -Dtest=CrossBrowserJukinVideoSubmission_Android_Spec test   

### Setup test Data  

To change the test data for executing test script in mobile device browser(Android and iOS devices) and MAC browser please follow below steps-  

#### Setup Test Data for MAC browser test script:  

 Open  "CrossBrowserJukinVideoSubmission_WinNMac_Spec" Spec file in notepad or eclipse from “JukinMediaConsumerSiteTest\src\test\groovy\com\jukinmedia\test” path,and change the data in ‘where’ block of Spec file as per below   given example-  
 
  for ex.

  where: "Input Data to submit the video

  url   |firstname  | lastname |  useremail         | phone

 '"www.youtube.com"| "Antonys" | "resha"  | "auto123@yahoo.com"| "1234567890"'

  *Number of data rows will trigger number of execution cycles.

#### Setup Test Data for Android and iOS browser test scripts:  

Open  "CrossBrowserJukinVideoSubmission_Android_Spec" Spec file in notepad or eclipse from “JukinMediaConsumerSiteTest\src\test\groovy\com\jukinmedia\test” path,and change the data in ‘where’ block of Spec file as per below given example-

  for ex.

  where: "Input Data to submit the video

  mp4videoname   |firstname  | lastname |  useremail         | phone

  '"VID-See.mp4"| "Antonys" | "resha"  | "auto123@yahoo.com"| "1234567890"'

  *Number of data rows will trigger number of execution cycles.
