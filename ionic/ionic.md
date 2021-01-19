## Ionic IOS

- make sure you have xcode installed

### Add ios to platforms

- you can use this terminal command to add ios to your platforms
  - `ionic cordova platform add ios`
- you can build for ios using the below command line

  - `ionic cordova build ios`
  - this will create a build folder for yor app for ios
  - in your directory the folder should be in `platforms/ios`
  - There will be a file called `myApp.xcworkspace`
  - if you open the file it will launch and open file in xcode.

- In order to build Ios apps you will need to have a development team registered with apple through their developer program. If not you can only build to simulator
  - it will cost about \$100 a year to register as an ios developer.
  - **you do not have to pay this if you are not planning to launch the app in the appstore**
  - if you have a developer account you can sign in through xcode by clicking add account.
