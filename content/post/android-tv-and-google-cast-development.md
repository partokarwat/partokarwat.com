+++
description = "Deploy for Android TV and Google Cast"
title = "Android TV and Google Cast development"
date = "2017-04-02"
topics = ["Development"]
tags = ["udacity","android", "android tv", "google cast", "ubiquitous"]

+++

This content is taken from the corresponding udacity course.

# Table of Contents
1. [Living Room](#living-room)
2. [Google Cast](#google-cast)
2. [Android TV](#android-TV)

# Living Room

Average TV-Viewer spends 3h/day!

- Google Cast: Protocol that integrates multiple devices with Android, iOS, Web
- Android TV: Extrend Android App

First extend you app with **Google Cast Support**, then extend with **leanback library** to allow users to control your app from Android TV.

# Google Cast

Send = cast to Receiver (Android TV, Chromecast). Senders are Android, iOS, Web.

Google Cast is a connecting technologie.

Use the Cast SDK, to make your App a Sender.

The Cast SDK creates a menu item with cast icon. With it you can establish a connection with your Cast device.

Explore the [sample apps](https://developers.google.com/cast/docs/downloads) to learn about Google Cast.

Become a Google Cast Developer costs 5$ and can be accomplished in the [Google Cast SDK Developer Console](cast.google.com/publish). Then you can register your receiver Applications and your cast devices = device's serial number.

*Cast isn't supported by the emulator!* Use a real Android and a real Cast device for development.

Follow the [Google's visual design checklist](https://developers.google.com/cast/docs/design_checklist/). 

Use Cast Companion Library (CCL).

Provide start and stop control casts for users at any time. Always show playback controls when casting (ex. minicontroler or fullscreen). Even show playback controls, when the device is locked and over notifications while you app is out of focus. Also user should always be able to disconnect from the device.

If multiple users are connected, only stop the actual cast when the last user disconnects.

If the connection is lost, automatically reconnect users when they're in your app.

If your app is killed, always try to rejoin the existing session, if it's still running.

2 ways to start casting:

- Connect and Play
- Play and Connect

The **Sender** always show the **action**. The **Receiver** always shows the **state**. Don't confuse your users! Think at remote control and TV.

Fade your Receiver UI away after 5 seconds.

## Receiver 

They are written in HTML5 and JavaScript.

Receivers get an URL generated from the Application ID by the chrome cast. The Sender sends the Application ID to the chrome cast.

Types of receiver applications:

- Default Media Receiver 
 - without Application Id 
 - for Simple Media
 - no styling and customization possible
- *Styled Media Receiver*
 - with Application Id 
 - for Simple Media
 - hosted by google and designed for streaming audio and video content
 - custom style with your own CSS
 - Recommended option
- Custom Receiver with
 - Application Id for custom Media
 - advanced capabilities like DRM
 - have full control of all aspects of the behavior of your application

## Sender 
The sender's lifecycle:
![Parto Karwat](/media/sender-lifecycle.png)

1. Manifest
 - minSdkVersion >= 9
 - set the correct Application Theme
 - Add ACCESS_NETWORK_STATE and ACCESS_WIFI_STATE in the production app
1. menu.xml 
 - Add the Cast button
1. Activiy
 - Initialize the Cast API in onCreate()
 - Assign the the MediaRouteSeletor to MediaRouteActionProvider in onCreateOptionsMenu() 
 - Add MediaRouterCallback to the MediaRouter instance in onStart()
 - Remove MediaRouterCallback in onStop() to conserve battery power
 - ...

Example Cast API initialization:
 ```
 mMediaRouter = MediaRouter.getInstance(getApplicationContext());
 mMediaRouteSelector = new MediaRouteSelector.Builder().addControlCategory(CastMediaControlIntent.categoryForCat("794B7BBF")).build();
 mMediaRouterCallback = new MyMediaRouterCallback();
 ```

 Code for Cast button menu item:
 ```
 <item
 	android:id="@+id/media_route_menu_item"
 	android:title="Play on..."
 	app:actionProviderClass="android.support.v7.app.MediaRouteActionProvider"
 	app:showAsAction="always"/>
```
Again use CCL (Cast Companion Library)! 

Try out a [cast codelab](http://cast-codelab.appspot.com/)! :)

# Android TV

Use leanback library, it does the most.

Use TV emulator, it's possible. :)

In your manifest:

- Add LEANBACK_LAUNCHER intent-filter to your Manifest within your TvActivity
- Use Theme.Leanback for your TvActivity

Use RecyclerView because of large list and limited memory on your Android TV.


