+++
description = "Use location within your apps"
date = "2017-04-23"
title = "Google Location Services on Android"
topics = ["Development"]
tags = ["udacity","android","google","location services"]

+++

Please find the corresponding udacity course [here] (https://www.udacity.com/course/google-location-services-on-android--ud876-1).

# Table of Contents
1. [Play services](#play-services)
1. [Location and context](#location-and-context)
1. [Location example](#location-example)
1. [Activity recognition example](#activity-recognition-example)
1. [Geofencing](#geofencing)

# Play services

Use them by adding to build.gradle:

```compile 'com.google.android.gms:play-services:10.2.1'```

**Always use full version number like 10.2.1**

Then add to the Manifest:

```
<meta-data 
	android:name="com.google.gms.version"
	android:value="@integer/google_play_services_version"/>
```

Create GoogleApiClient in ```onCreate()```

Connect GoogleApiClient in ```onStart()``` to Location Service (or other relevant API)

Overwrite ```onConnectionFailed()``` and ```onConnectionSuspend()``` in Location Service

Write ```onConnected()``` and create a LocationRequest that queries the Location Service

Write ```onLocationChanged()``` and get the Location object which you can then use

# Location and context

## Fused Location Provider

Access sensors to determine your location by analyzing your 

- GPS
- cellular connection
- wifi connection.

### Fine and Coarse Location

#### Fine

Fine location involves using GPS, Cell and WiFi to get the most accurate possible position. Costing you extra battery life.

Add ```<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/> ``` to you manifest for fine location.

#### Coarse

Coarse location uses Cell or WiFi signal. Is less fine, but costs less battery. 

Add ``` <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/> ``` to you manifest for coarse location.

## Activity Recognition

Access sensors to determine your activity. It determines if you are

- in a vehicle
- on a bicycle
- on foots
- standing still
- tilting (geneigt).

# Location example

Add ```implements GoogleApiClient.ConnectionCallbacks, GoogleApiClient.OnConnectionFailedListener, LocationListener ``` to your Activity.

Add the following variables:
```
private GoogleApiClient mGoogleApiClient; 
private LocationRequest mLocationRequest;
``` 

In ```onCreate()``` build your GoogleApiClient by

```
mGoogleApiClient = new GoogleApiClient.Builder(this)
                .addApi(LocationServices.API)
                .addConnectionCallbacks(this)
                .addOnConnectionFailedListener(this)
                .build();
```

In ```onStart()``` add 

```
mGoogleApiClient.connect();
```

In ```onStop()``` add 

```
if (mGoogleApiClient.isConnected()) {
	mGoogleApiClient.disconnect();
}
```

In ```onConnected()``` add

```
mLocationRequest = LocationRequest.create();
mLocationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
mLocationRequest.setInterval(1000); // Update location every second

LocationServices.FusedLocationApi.requestLocationUpdates(mGoogleApiClient, mLocationRequest, this);
```

This updates location periodically. Use last location to get location only once
```
LocationServices.FusedLocationApi.getLastLocation(mGoogleApiClient);
```

Other priorities are 

- ```PRIORITY_BALENCED_POWER_ACCURACY``` Gives an accuracy to about 100m. Nick name "block accuracy"
- ```PRIORITY_HIGH_ACCURACY``` Gives the finest possible location
- ```PRIORITY_LOW_POWER``` Gives city level location about 10km
- ```PRIORITY_NO_POWER``` Best possible accuracy at no power cost. Gets for example the informations from other clients that requested already.

The interval within you read the sensors has a huge impact on battery life. Do you really need to update your location every second? Try to get the best for an appropriate user experience.

Grab your location from ```onLocationChanged(Location location)```

# Activity recognition example

*Work-Queue-Processor* design pattern. Example: IntentService (start a service, service handles each intent using a worker thread, stops itself when it runs out of work). [Read here](https://en.wikipedia.org/wiki/Thread_pool) for more details.

1. Create an Intent Service ```DetectedActivitiesIntentService extends IntentService```
 1. Implement ```onHandleIntent()```
 1. Add service to your manifest.xml
1. Implement your MainAcitvity
 1. Make your activity implement ConnectionCallbacks and OnConnectionFailedListener
 1. Implement onConnected
 1. Implement onConnectionSuspended
 1. Implement onConnectionFailed
1. Create nested BroadcastReceiver within your MainAcitvity
 1. Implement onReceive
 1. Declare Receiver class on MainActivity as member variable ```mBroadCastReceiver```
 1. Instantiate Receiver variable in 
1. Set up the GoogleApiClient
 1. Connect and disconnect the client in onStart()/onStop() 
 1. Unregister the broadcast receiver in onPause()
 1. Register the broadcast receiver in onResume()

# Geofencing

Draw a virtual fence around a location in the real world and generate events when devices enter or exit the fence. Here are some examples:

- Parents: Get a notification when a your or a member of your family has arrived home. 
- Groups: Use geofencing for social check-in.
- Games: Virtually hide loots.
- Shop: Get notifications of special offers (like "Come in the next 5 minutes and you get your coffee for half price") if the user gets close to the store. Remove notification if user exists the geofence.

## Properties

Define a Geofence with the builder on the Geofence object and the following properties

- Latitude and Longitude to defines the location
- Radius: defines how close the user has to be
- Expiration time: How long the Geofence will be alive, you can also create permanent once
- ID: is unique

Create a GeofencingRequest with addGeoFences holding an ArrayList of Geofences.


