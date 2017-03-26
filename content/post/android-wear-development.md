+++
date = "2017-03-19"
topics = ["Development"]
tags = ["udacity","android","wear", "ubiquitous"]
description = "This is my summary for the first part of the Go Ubiquitous Lessons"
title = "Android Wear development"

+++

You can find the corresponding udacity course [here] (https://www.udacity.com/course/android-wear-development--ud875A).

# Table of Contents
1. [Introduction](#introduction)
2. [Wear Notifications](#wear-notifications)
2. [Wear Apps](#wear-apps)
3. [Watch Faces](#watch-faces)

# Introduction

Ubiquitous computing principles:

- Create **1 service with multiple views** on wear, cars, tv's etc.
- Reduce distraction by **adapting technologie to humans**
- **Less is more.** Put the user before technologie.

The wearable interface has 2 components:

- Talk to wearable
- Wearable talks to the user

Wear inputs are:

- Voice
- Touch swipes

Phone wakes up the watch. Let the watch sleep as much as possible!

- GridViewPager: swipe left/right, up/down
- DotsPageIndicator: swipe left/right and see on wich page you are by an number of ... 

# Wear Notifications

Easiest way, App notifications go direct to the wear.

Add extra action button to notification will add the action to the wearable notification, but activating it, will run the action on the phone.

Run action on Wear, use ```WearableExtender```.

Set Notification backgrounds with ```WearableExtender.setBackground(mBitmap)```

Use 400x400 for static background and 640x400 for parallaxe background.

Store backgrounds in ```drawble-nodpi``` directory.

Create notification on the wearable is the only way to have the notification only on the wear and not on the phone.

## Example: Reply-Action wich voice

Use class RemoteInput with String key "extra_voice_reply" .

Then add the Reply-Action to a WearableExtender.

## Pages

Extend your notifications with ```.addPage(secondPageNotification)``` for multiple page notifications.

Create notification stacks with groups.

See more one [android developers page](https://developer.android.com/training/wearables/notifications/index.html).

```setLocalOnly(true)``` to make sure a notification only apears o the phone (ex. upload progress).

Go to ```Android Studio > File > Import Sample``` for multiple notification samples and find out whats possible.

# Wear Apps

Wear APK is embedded in the phone APK. Wearable App only exists with phone APK.

Wear App set up rules:

- Use *same package name and version number* for phone APK and wearable APK.
- Request *same permissions* in both wearable and phone APK.
- Sign wearable and phone APK always with the *same developer id*.

Use WatchViewStub for layouts. Use BoxInsertLayout for large amounts of text or data.

Communication between Phone App and Wear App via DataItems or Messages.

## DataItems

Create a service that extends from WearableListenerService. 

Add it to the manifest with intent filter.

## Messages

Messages are simpler. Overwrite/Create the methods. 

Messages are fast, but can be lost during transmission.


# Watch Faces

- Round & Square
- Interactive & Ambient[^1]
- Low Bit & OLED

[^1]: Ambient mode has a 95% black screen.

Start with a sample (Android Studio > File > Import Sample) or template. Use CanvasWatchFaceService. Engine with methods onCreate, onSurfaceChanged, onDraw. Set System UI Elements.

Design Interactive Mode & Ambient Mode separately.

Most of the time will be in Ambient Mode: **Design Ambient Mode thoughtfully**.

Use Low-Bit Mode in Ambient Mode: Only Black, White, Yellow, Blue, Red, Magenta, Cyan, Green

Only 5% pixels should be illuminated in ambient mode. Keep 95% of pixels truly black.

Avoid Solid Regions! No permanently on pixel. Danger to burn it.

System UI elements:
- Cards: Peek cards
- Indicators

**Context + Data = Design**