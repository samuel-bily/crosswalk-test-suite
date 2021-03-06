## Introduction

This test suite is for testing cordova-webapp-android-tests specification
https://crosswalk-project.org/#wiki/Create-Sample-App-With-Crosswalk-Cordova-Android

## Pre-conditions

* Require Android API level 22
* Require the latest Cordova CLI, and must >= 5.0.0, install with command: `$ sudo npm install cordova -g`
* Get cordova_sampleapp.zip from internal release link, then unzip it to /tmp/cordova-sampleapp/
* Get latest plugman tool, steps as below:

  ```
  git clone https://git-wip-us.apache.org/repos/asf/cordova-plugman.git
  cd cordova-plugman
  sudo npm -g install
  ```

* If Build Cordova App with Crosswalk Canary, need these as follows

**Download canary crosswalk file**:

  ```wget https://download.01.org/crosswalk/releases/crosswalk/android/canary/<canary-version>/crosswalk-<canary-version>.aar```

**Install canary to local maven repo**:

  ```
  mvn install:install-file -DgroupId=org.xwalk -DartifactId=xwalk_core_library -Dversion=<canary-version> -Dpackaging=aar -Dfile=<crosswalk-path>/crosswalk-<canary-version>.aar -DgeneratePom=true

  canary-version: e.g. 13.42.319.0, it must be consistent with the dependencies version [testprefix-path]/opt/cordova-webapp-android-tests/tools/cordova-plugin-crosswalk-webview/src/android/xwalk.gradle

  crosswalk-path: the downloaded canary crosswalk file path
  ```

## Test Steps
1. unzip cordova-webapp-android-tests<version>.zip -d [testprefix-path]

2. cd [testprefix-path]/opt/wrt-apptools-android-tests/

3. update arch.txt if your run with 'x86' device

4. update mode.txt if your run with 'shared' mode pkg

5. update pack-type if your want to install cordova-plugin-crosswalk-webview from 'npm'

6. run test case

   ```
   testkit-lite -f [testprefix-path]/opt/cordova-webapp-android-tests/tests.xml -A
   -o [testprefix-path]/opt/cordova-webapp-android-tests/result.xml --comm localhost
   --testenvs "DEVICE_ID=Medfield3C6DFF2E;CONNECT_TYPE=adb" --testprefix=[testprefix-path]
   ```

   DEVICE_ID can also be multiple ids like "DEVICE_ID=Medfield3C6DFF2E,Medfield3C6DFF00".
   Query device id by command "adb devices -l" in host.

## Authors:

* Shen,Lin <linx.a.shen@intel.com>
* Lin, Wanming <wanming.lin@intel.com>

## LICENSE

Copyright (c) 2013 Intel Corporation.
Except as noted, this software is licensed under BSD-3-Clause License.
Please see the COPYING file for the BSD-3-Clause License.
