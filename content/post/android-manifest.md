+++
description = "Explore all the options for AndroidManifest.xml"
title = "Android App Manifest"
date = "2017-05-14"
topics = ["Development"]
tags = ["API Guides","android"]

+++

My resume is up to date for API 25 and based on [this](https://developer.android.com/guide/topics/manifest/manifest-intro.html) documentation.  

# activity

### android:launchMode

Set Activity with multiple instantiations:

- *standard* New intent creates new instance. Is the *default*.
- *singleTop* Create only a new instance if no instance of the activity is existing on the top of the stack. The same behavior can be reached if the up intent contains ```FLAG_ACTIVITY_CLEAR_TOP```

Make Activity always the root of the activity stack. The device can only hold one instance of the activity at a time:

- *singleTask* Allows other activities to be part of its task
- *singleInstance* No other activities to be part of its task. If it starts another activity, that activity is assigned to a different task — as if ```FLAG_ACTIVITY_NEW_TASK``` was in the intent.
