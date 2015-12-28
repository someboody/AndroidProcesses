# AndroidProcesses

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.jaredrummler/android-processes/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.jaredrummler/android-processes) [![License](http://img.shields.io/:license-apache-blue.svg)](LICENSE.txt) [![API](https://img.shields.io/badge/API-4%2B-blue.svg?style=flat)](https://android-arsenal.com/api?level=4) <a href="http://www.methodscount.com/?lib=com.jaredrummler%3Aandroid-processes%3A1.0.2" target="_blank"><img src="https://img.shields.io/badge/method count-224-e91e63.svg"></img></a> <a href="http://www.methodscount.com/?lib=com.jaredrummler%3Aandroid-processes%3A1.0.2" target="_blank"><img src="https://img.shields.io/badge/size-22 KB-e91e63.svg"></img></a>

A small library to get the current running processes on Android
___

Why would I need this?
----------------------

As of Android 5.0, it has become increasingly difficult to get a list of running apps. [`getRunningTasks(int)`](http://developer.android.com/intl/zh-cn/reference/android/app/ActivityManager.html#getRunningTasks(int)) is now deprecated. Android 5.1.1+ killed [`getRunningAppProcesses()`](http://developer.android.com/intl/zh-cn/reference/android/app/ActivityManager.html#getRunningAppProcesses()) (as of Android 5.1.1+ it only returns your app). The documentation hasn't changed and Google is ignoring requests to either update the documentation or restore the original implementation. 

Using [UsageStatsManager](https://developer.android.com/reference/android/app/usage/UsageStatsManager.html), it is possible to get a list of running apps. However, this requires the user to grant your application special permissions in Settings. It has been reported that some OEMs have removed this setting.

This library gets a list of running apps and doesn't require any permissions. See the [sample](https://github.com/jaredrummler/AndroidProcesses/blob/master/sample/src/main/java/com/jaredrummler/android/processes/sample/activities/MainActivity.java) application for details. Download the sample [APK](https://github.com/jaredrummler/AndroidProcesses/blob/master/sample-apk/sample.apk?raw=true).

Usage
-----

**Get a list of [RunningAppProcessInfo](http://developer.android.com/reference/android/app/ActivityManager.RunningAppProcessInfo.html):**

```java
List<ActivityManager.RunningAppProcessInfo> appProcesses = ProcessManager.getRunningAppProcessInfo(context);
```

**Check if your app is in the foreground:**

```java
if (ProcessManager.isMyProcessInTheForeground()) {
  // do stuff
}
```

**Get running apps and some information about them:**

```java
List<AndroidAppProcess> processes = ProcessManager.getRunningAppProcesses();
for (AndroidAppProcess process : processes) {
  String processName = process.name;
  
  Stat stat = process.stat();
  int pid = stat.getPid();
  int parentProcessId = stat.ppid();
  long startTime = stat.stime();
  int policy = stat.policy();
  char state = stat.state();

  Statm statm = process.statm();
  long totalSizeOfProcess = statm.getSize();
  long residentSetSize = statm.getResidentSetSize();
}
```

Download
--------

Download [the latest AAR](https://repo1.maven.org/maven2/com/jaredrummler/android-processes/1.0.2/android-processes-1.0.2.aar) or grab via Gradle:

```groovy
compile 'com.jaredrummler:android-processes:1.0.2'
```
or Maven:
```xml
<dependency>
  <groupId>com.jaredrummler</groupId>
  <artifactId>android-processes</artifactId>
  <version>1.0.2</version>
  <type>aar</type>
</dependency>
```

License
--------

    Copyright (C) 2015, Jared Rummler

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
