+++
date = "2017-05-17"
topics = ["conference"]
tags = ["google","android", "conference"]
description = "Read my notes on the most important developer conference for Android developers"
title = "Google I/O 2017"

+++

The conference starts on May 17th and ends on May 20th 2017 (GMT+2). I join the conference via [live stream](https://events.google.com/io/live). 

# 17th

## Google Keynote

2 billion active Android devices (smartphone & tablets) today.

Mobile first to **AI first** approach. Deep learning is the base.

Touch, voice and vision are the available inputs to computers.

Image recognition has now a lower vision error rate than humans! Noisy pictures can made clear that humans can reduce their error rate too. Removing objects like fences from pictures is also possible. 

Google Lens is a new product, that can understand what you're looking at and help you take action on it. Example: Point your phone camera on a flower and google lens can tell you what flower it is.

Google builds AI first data centers.

Training and Inference are the two pars of AI. Training is very costful. Google Compute Engine provides for this new Cloud TPUs in its AI first data centers.

For the new AI content has been created [google.ai](https://google.ai/). It provides Research, Tools an Applied AI.

Learning to lean = train neuronal nets with neuronal nets

Other applications for ML with vision and AI can be pathology analysis or DNA Sequencing.

Google translate will have visual translation.

The iPhone has now the Google assistent "ok google". With Google Assistant SDK everyone can integrate "ok google" to its products. If products have it, they will have the label "google assistent build in".

Google Photos has now among others a Photo Book option.

Youtube has now a super chat option. It's a live chat, where you can also donate.

Android O release comes later this summer. In O double tap in text on address, places or similar will select the entire address, place... string.

TensorFlow Lite available for Android.

Vitals in O stand for security enhancements, os optimizations and developer tools: 

- Apps upcomping to playstore are scanned with machine learing based algorithms. To make this more perceptible they created Google Play Protect.
- Twice as fast boot time with O on Pixel
- Play Console Dashboard pins issues on your App to the developer
- Android Studio Profilers allow you to analyze network, memory and cpu in very deep detail and at runtime.
- [Kotlin](https://kotlinlang.org/) will be supported by Android

The beta release of O can be found [here](https://android.com/beta).

Android Go for users with minimal resources. Ex.: Youtube Go, ...

Add Lite variants of you app, they will be highlighted in the play store. Find the guidelines [here](https://developer.google.com/billions).

Daydream is the VR/AR product from Google.

HTC is leader in VR. Lenovo will also be a partner on VR.

GPS can get you to the door. VPS can get you to the exact item that you need for example in a store.

Google Expeditions + AR for learning on schools.

Google will have a job searching feature.

## Developer Keynote

First class support for Kotlin. Use as much Kotlin as you want from 0 to 100%.

Languages are the tools we use to express our thoughts.

Java 8 is supported now. You can also ignore Kotlin and use for example lambdas from Java 8.

The team behind Kotlin is the same team that created intelliJ (JetBrains).

The IDE convertes Java code to Kotlin if you paste java code in a .kt file.

Live debugging. 

No separate SDK Manager anymore, all is distributed via maven repositories.

Instant Apps explore an App without installing it.

Modularize Tool in Android Studio can help to devide your app in separated features, that can be used to provide an instant app version. It takes 4 to 6 weeks with the latest tools to build an instant app version of an existing app project.

Use also Space-Saving Shared Libraries, Optimized Asset Delivery or On-The-Wire Compression to shrink your instant app.

Finally publish your instant app version in the play console.

App Directory from the Google Assistant.

Custom shortcuts to start an app with the Google Assistant.

Actions on Google Developer Console is a new developer console.

TPU = Tensor Processing Unit

TensorFlow Research Cloud registration can be found [here](https://g.co/tpusignup)

Lighthouse is a chrome extention and can help analyze your website.

Firebase has now cloud functions.

Firebase Performance monitoring can help you to improuve your app in for example starting time. The beta version is available from today.

## Assisting the Driver: From Android Phones to Android Cars

Android Auto app available for cars that don't have a build in navigation system.

Audi Q8 integrates Android. (Talk by Alfons Pfaller with very limited english)

Volvo is also partnering with Android. (Talk by Henrik Green)

## New release & device targeting tools or: how I learned to stop worrying & love Android diversity!

Test your new app updates with Open Beta.

Staged rollout is possible for new releases.

You can now download older apk releases from the developer console.

Release notes can be entered by copy&paste to developer console.

The Release Dashboard from developer console allows you to compare against previous releases and analyze the state.

New Device Catalog UI in the developer console.

## What's new in Google's IoT platform? Ubiquitous computing at Google

IoT = Internet of Things

IoT plattform from Google is Android Things and can be found [here](https://developer.android.com/things)

You can build your own hardware boards with Android Things. Google Assistant SDK allows you to build custom machines.

Find an example of Android Things & TensorFlow [here](https://github.com/androidthings/sample-tensorflow-imageclassifier)

## What's New in Android

Picture in Picture can be set as flag in the manifest activity tag

Color management with new utilities andorid.graphics.Color, ColorSpace, ColorLong, Half

Multi-Display mode available for android with O. Test this feature with

```
$ adb shell dumpsys display
$ adb shell start <activity> --display <id>
```

getMetrics() now available on any Media

Playback has been improuved

WebView has now Safe Browsing and a Multi-Process option

Autofill

Put font-files directly in ```res/font``` dirctory. Use them with "@font/myfont" or R.font.myfont. Fonts are downloadable with Front Provider in Google Play Services v11. This gives you access to over 800 Googlefonts.

Auto-Sizing TextView will autoresize Text Size.

Castaway for findViewById(). ```TextView tv = findViewById(R.id.mytextview);``` works now.

Adaptive icons: give a background and a foreground, the system adapts then.

Notification channels allow to block some notifications of an app. This O you have to use channels, if not your notifications will be dropped!

Cached Data can be checked by getCacheQuotaBytes() and increased by allocateBytes()

Java Programming Language Updates: java.time, java.nio.file, java.lang.invoke 

EmojiCompat from SupportLibrary available

Physics based animations are now available

Alter windows has always to be type of TYPE_APPLICATION_OVERLAY

## What's New in Firebase


# 18th

## No one likes crashing or janky apps! Engineer for high performance with tools from Android & Play

## Architecture Components - Introduction

## Bringing Device Production to Everyone With Android Things

## Getting Started with Machine Perception using the Mobile Vision API

## Android Performance: An Overview

## Background Check and other insights into the evolution of the Android Operating System Framework

## ExoPlayer: Flexible media playback for Android

## What's new for Android TV

## Architecture Components - Solving the Lifecycle Problem

## Building apps for the Google Assistant

## Android Wear: What's new & Best Practices

## Best Practices to slim down your app size

## TensorFlow Frontiers

## VR and AR at Google

## What's new in Android Support Library

## Fragment Tricks

## Daydream in the classroom: immersive learning

## Effective TensorFlow for Non-Experts

## What's New in Android Development Tools

## Developing for Android Things using Android Studio

## Architecture Components - Persistence and Offline

## Introduction to Android Instant Apps

## Designing for the Next Billion Users: Accessibility UX Insights from the Developing World

## Open Source TensorFlow Models

# 19th

## What's new in Android Design Tools - New features and tools for rapid UI development

## Using Google Cloud and TensorFlow on Android Things

## Finding the Right Voice Interactions for your App

## What's new in Notifications, Launcher Icons and Shortcuts

## Home Automation with the Google Assistant

## Making the world your own with Google Maps APIs

## 10 Google Play Console secrets to optimize Android apps for stellar user retention

## Using Design Sprints to increase cross-functional collaboration

## Best practices to improve sign-in, payments, and forms in your apps

## Prototyping to Production: Bridging the Gap with a Common Tool

## Android meets TensorFlow: how to accelerate your app with AI

## Best Practices for Android Audio

## Pushing the boundaries of Machine Learning

## How words can make your product stand out

## Building for Your Next Billion Users

## Machine Learning APIs by Example

## Exploring Google Maps Solutions

## Introduction to Kotlin

Instances can be copied with default copy() function

Semicolons are optional

*when* block is like "case" in haskell. When can returned directly.

higher order (functions take functions as arguments) available 

Use *it* like in Groovy when you have a single parameter lambda expression

*filter* function is build-in 

green highlighting indicates smart cast. The casts are done by the compiler.

Kotlin compiles to JVM-Bytecode.

Kotlin allows multiplatform projects. 

Coroutines are extremely cheap.

## Understanding Color

## How well do you know the web?

## Notifications UX: What's New for Android O

## Tools and tips to boost user engagement and retention

## Android Sensors & Location: What's New & Best Practices

## Android Performance: UI

## Designing Great Apps for New Internet Users

## From Research to Production with TensorFlow Serving

## Project Magenta: Music and Art with Machine Learning

## Life is great and everything will be ok, Kotlin is here

MainActivity.ky Example

``` 
class MainActivity : Activity() {
	override fun onCreate(savedInstanceState: Bundle?) {
		super.onCreate(savedInstanceState)
	}
}
```

The kotlin typesystem models nullability

Getter and Setter are implicitly available in kotlin

Inline functions are possible, no anonymous classes needed

Operator functions have a special call syntax

Make db operations lazy

# 20th

## Android Wear UI development best practice

