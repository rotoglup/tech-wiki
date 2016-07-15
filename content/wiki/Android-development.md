+++
date = "2016-07-15T12:10:48+02:00"
draft = true
title = "Android development"

+++

Permissions
================================================

`uses-permission` must be outside the `application` block in manifest, e.g. :

```
<manifest ...>
    <application
    	...
    </application>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
</manifest>

For API 23+ you need to request the read/write permissions even if they are already in your manifest, 
see http://stackoverflow.com/questions/8854359/exception-open-failed-eacces-permission-denied-on-android
