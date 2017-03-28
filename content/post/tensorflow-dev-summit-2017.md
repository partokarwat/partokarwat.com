+++
date = "2017-03-26"
title = "TensorFlow Dev Summit 2017"
topics = ["new technologie"]
tags = ["google","artifical intelligence", "neuronal networks", "machine learning", "tensorflow"]
description = "This are my notes for the TensorFlow Dev Summit 2017 Livestream"

+++

Please find the Livestram from TensorFlow Dev Summit 2017 [here](https://www.youtube.com/watch?v=LqLyrl-agOw&list=PLOU2XLYxmsIKGc_NBoIhTn2Qhraji53cv&index=19).

The TensorFlow Dev Summit 2017 took place at 9:30am Pacific Time on February 15th, 2017.

Feel free to visit the [projects webpage](https://www.tensorflow.org/).

# Table of Contents
1. [Introduction](#introduction)
1. [XLA](#xla)
1. [TensorBoad](#tensorboad)
1. [API](#api)
1. [Uses](#uses)
1. [Distributed TensorFlow](#distributed-tensorflow)

# Introduction (Jeff Dean, Rajat Monga, Megan Kacholia)

TensorFlow is an open-source machine learning platform for everyone and many platforms. It is open-scoured since 2016.

At the root of TensorFlow was DistBelief.

TensorFlow works very well in Google Cloud (DIY, Managed).

TensorBoad is a TensorFlow tool that visualizes data to better analyze it.

TensorFlow is at v1.0 and backwards compatibility is guaranteed.

TensorFlow can be used with all kings of systems also Android.

XLA (accelerated linear algebra) is an Experimental TensorFlow Compiler. Can be used for just in time compilation or ahead of time compilation.

Example usage of TensorFlow on a mobile app to translate a text on a street sign:
![Parto Karwat](/media/example-tensorflow-mobile.png)

TensorFlow is also used for app recommandations in the play store or as spam filter. But there are many more use cases.

You can use TensorFlow to sort materials like cucumbers.

TensorFlow can be used for diagnosis on captures from procedural imaging in medicine. Examples: Eyes background in diabetic retinography; Recognize skin melanoma; diagnose psychiatric brain disorder on MRIs,...

TensorFlow can also paint or make music. 

The most TensorFlowProjects are written in **Python**, but many languages like Jave, Go, C, ... are supported.

# XLA (Todd Wang)

Is the TensorFlow compiler.

Build your TensorFlow project with XLA just-in-time (JIT) compiler (experimental)!

Not all TensorFlow ops compile. It's still early days!

Fusions allow less memory operations while operating on data.

XLA program is a set of static, decomposed TF operations. 

Use JIT compilation when protoyping. Use Compilation caching as you scale. Use AoT (Ahead-of-time) compilation for mobile/embedded & latency minimizations. 

Read the XLA documentation [here](https://www.tensorflow.org/performance/xla).

Define your feeds and fetch in the config file in proto.

Compile your graph using the tf_library bazel build macro.

# TensorBoad (Dandelion Mané)

Find the example [here](https://goo.gl/San2uR)

Use FileWriter, a Python class that writes data for TensorBoard.

First clean the graph by giving node names and name scopes. Then same structures in the graph, have the same color. You can also color by device if you use CPU and GPU. 

A summary is a specialized TensorFlow op that takes data and outputs a protocol buffer containing "summarized" data. Then pass a summary to FileWriter to get it to disk.

The Embedding Visualizer takes your data and makes it a 3D-diagram. T-SNE show how the identified data items are grouped, can be very useful. 

Future: Debugger, plugins, shareable TensorBoard for an entire organisation.

# API (Martin Wicke)

The Estimator is a model that has a training operation, an evaluation operation and predictions. The model gets inputs and labels to work with. 

You can also export your model to a saved model, that is a data format with wich you can use your model directly in tensorflow serving.

Estimators will be released in v1.1 in core, it is already usable in from contrib. The releases will take 6 to 8 weeks. 

## Keras API (François Chollet)

Keras is an API spec for building deep learning models across many platforms.

Access it by ```tf.keras.```

Keras will be in core at v1.2. For v1.1 you can test it from contrib with ```tf.contrib.keras```

# Uses

## Google DeepMind (Daniel Visentin)

TF for optimizing the cooling infrastructure at google.

TF used in Gorila = general reinforcement learning architecture.

AlphaGo uses TF.

WaveNet uses TF. WaveNet creates human natural speech by machine. It can also generate music.

Learning to Learn uses TF.

## Skin Cancer (Brett Kuprel)

Dataset was 129k images with 2k melanoma.

Research from Stanford. On Nature Cover 02/2017.

## Mobile and Embedded Devices (Pete Warden)

Offer unique UX. 

Real-time translation, predict letters on keyboard, foto scan, snapchat features, ...

Support Android, iOS and Raspberry Pi.

### Android

TF can be used from Android Studio directly:

Grab an TF Android example [here](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/android).

To go more in deepth and do more complex building: 

1. Install TF from [here](https://www.tensorflow.org/install/) 
1. Install Bazel from [here](https://bazel.build/versions/master/docs/install.html)
1. Download Android SDKs 23+ and NDK 12b+
1. Set up WORKSPACE file
1. Run Bazel

TF core is written in C++, Android Apps are written in Java. Use the Android Inference Library.

### iOS

1. Have Xcode 8, automake and libtool
1. One-shot build
1. Iterative builds
1. Use the -Os flag for optimization and use Apple's accelerate framework.
1. Link your own apps and compile with -force_load flag

### Raspberry Pi

1. Install with ```sudo apt-get insta;; -y autoconf automake lovtool gcc-4.8 g++-4.8```, always build on directly on the raspberry pi, even it's slow
1. Build with ```make -f```
1. Use NEON acceleration for optimization

Tensorflow increases APK by 12MB, but can be reduced by including only the ops that you are actually using. Results in for ex. under 2MB.

# Distributed TensorFlow (Derek Murray)

Allows to use multiple machines to use for one big model.

Distributed is a TF mode.

You can create Sessions and Servers.

## TF Ecosystem (Jonathan Hseu)

Integrate TF with your infrastructure.

Run a cluster manager and a distributed storage.

Only Python can be used for Training library.

## TF Serving (Noah Fiedel)

Share your models in production.

Serving is how you apply a ML model after you've trained it.

Most common way is a RPC Server. Like this the model can always be online and updated.

## ML Toolkit (Ashish Agarwal)

Have algorithms that work out of the box with ML Toolkit. Ex.: KMeans, GMMs,...

