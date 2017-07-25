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

Learning to learn = train neuronal nets with neuronal nets

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

Live debugging for network usage, cpu usage, ... 

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

# 18th

## No one likes crashing or janky apps! Engineer for high performance with tools from Android & Play

App *stability and bugs* are for 50% the critic points on *1 star* app reviews. **5 star** reviews are 60% caused by **speed, design or usability**.

Android vitals dashboard is your tool to get better reviews. Pay attention at the following critical performance points:

- Stability
 - ANR Rate (app not responding = frozen and no response for 5 seconds)
 - Crash Rate
- Battery
 - Stuck Wake Logs (identify bad use of wake locks)
 - Excessive Wakeups
- Rendering
 - Slow Rendering (60 frames per second = 1 frame every 16ms, if the rendering takes 17ms, 1 frame is dropped) 
 - Frozen Frames (App appears frozen when rendering takes 700ms)

Best practices:

- Not do blocking operations in the UI thread, use for ex. AsyncTasks instead
- Finish processing when you are a broadcast receiver
- Be mindful when introducing deadlocks to your app
- Use standard wake lock names for each distinct wake lock in your application in order for them to be debuggable in case they become stuck wake locks
- Avoid using wake locks entirely. They were introducted in the early days of Android and since then many of the use cases for which you needed a wake lock, you no longer need a wake lock for. Examples: 
 - Long running download, use Download Manager
 - Synchronizing data with an external server, use Sync Adapter
 - Need to run a background task, use Job Dispatcher
 - You hold a wake lock so that you can process an intent before the device goes to sleep, use the new Job Intent Service fro Support Lib v26
- If you eventhough nevertheless need a wake lock
 - keep the logic around it very simple, any error in the logic can tead to them getting stuck
 - try to do as little as possible where you are holding this wake lock
 - use defensive error handling
- Use Firebase JobDispatcher instead of Wakeups

## Architecture Components - Introduction

Architecture Guide now available on developer.android.com

LifecycleOwner can be used by extending Activities from LifecycleActivity. LifecycleActivity is just a temporary class until these components reach 1.0 then everything in support library will implement this LifecycleOwner interface. Then use @OnLifecycleEvent(ON_START) void start(){}

LifecycleObserver

You can extend your Listeners from LifeData<T> class 

# 19th

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
