---
title: "Java Note"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Android
  - Log
---

I was thinking how to use log on Android properly, and can control it without re-compile your app.
Here is what I found.

Long story for short, you should do something like this in you code (An example from AOSP [LocationManagerService.java](
https://android.googlesource.com/platform/frameworks/base/+/d22261fef84481651e12995062105239d551cbc6/services/core/java/com/android/server/LocationManagerService.java)

```java
public class LocationManagerService extends ILocationManager.Stub {
    private static final String TAG = "LocationManagerService";
    public static final boolean D = Log.isLoggable(TAG, Log.DEBUG);

    ....

    public void systemRunning() {
        synchronized (mLock) {
            if (D) Log.d(TAG, "systemRunning()");
            // fetch package manager
            mPackageManager = mContext.getPackageManager();
            ..
```            

Then you can use log.tag.TAG to set the logging level like this `adb shell setprop log.tag.LocationManagerService VERBOSE`. 
For details, check the document here [isLoggable](https://developer.android.com/reference/android/util/Log.html#isLoggable(java.lang.String,%20int) 

Why don't wrap those `if (D) Log.d(TAG, "...")` to another function, so it can handle the log logic internally?
You can find the reason from the comments of android.util.Log.java:

> when you're building the string to pass into Log.d, the compiler uses a
> StringBuilder and **at least three allocations occur**: the StringBuilder
> itself, the buffer, and the String object. Realistically, there is also
> another buffer allocation and copy, and even more pressure on the gc.
> That means that if your log message is filtered out, **you might be doing
> significant work** and incurring significant overhead.

