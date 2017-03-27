+++
description = "This is my summary for the second part of the Go Ubiquitous Lessons"
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


# Android TV

