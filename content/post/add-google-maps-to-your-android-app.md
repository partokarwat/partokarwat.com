+++
topics = ["Development"]
tags = ["udacity","android","google","maps"]
description = "Discover the world with Google Maps"
date = "2017-04-09"
title = "Add Google Maps to your Android App"

+++

You can find the corresponding udacity course [here] (https://www.udacity.com/course/add-google-maps-to-your-android-app--ud876-4).

# Table of Contents
1. [Play services](#play-services)
1. [Maps](#maps)
1. [Markers](#markers)
1. [StreetView](#streetView)

# Play services

To use them add to the build.gradle:

```compile 'com.google.android.gms:play-services:10.2.1'```

Then add to the Manifest:

```
<meta-data 
	android:name="com.google.gms.version"
	android:value="@integer/google_play_services_version"/>
<uses-permission
	android:name="android.permission.ACCESS_FINE_LOCATION"/>
```

Create GoogleApiClient in ```onCreate()```

Connect GoogleApiClient in ```onStart()``` to Location Service (or other relevant API)

Overwrite ```onConnectionFailed()``` and ```onConnectionSuspend()``` in Location Service

Write ```onConnected()``` and create a LocationRequest that queries the Location Service

Write ```onLocationChanged()``` and get the Location object which you can then use

# Maps

Generate a SHA 1 Key from the terminal by typing:
```
cd ~/.android

keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
```

Go to developers console. Create a project. Activate Maps API. Generate an API Key for Andorid App and enter your SHA 1 and packagename.

## Maps fragment
Create an xml fragment with
```
android:name="com.google.android.gms.maps.MapFragment"
```

Set attributes on the map fragment:

```
xmlns:map="http://schemas.android.com/apk/res-auto"
map:cameraBearing="112.5"
map:cameraTargetLat="40.7484"
map:cameraTargetLng="-73.9857"
map:cameraTilt="65"
map:cameraZoom="17"
```
## Google maps object

Allows you to change your map while the app is running.

[Look here](https://developers.google.com/android/reference/com/google/android/gms/maps/GoogleMap)

## Camera Position Options

- Zoom: Determines how much of the map you will see. 0 is see whole earth. 17-21 is street level.
- Latitude
- Longitude
- Target defines the center of your map by Lat and Lon
- Bearing is the direction the camera is facing. Specified in degrees clockwise from the north (East is 45˚).
- Tilt how much the camera is tilted. By default 0. Is given in degrees.

Use ```moveCamera()``` instantaniously move to a target. Use ```animateCamera()``` to go to a target with a fly over effect.

# Markers

```
MarkerOptions myPlace = new MarkerOptions()
	.position(new LatLng(47.489805, -122.120502))
	.title("My Place")
```

- ```position``` takes a LatLng
- ```title``` takes a String

### Custom Markers

Add icon property to MarkerOptions with ```.icon(BitmapDescriptionFactory.fromResource(R.drawable.ic_launcher));```

## Polylines

Creates a trace for all the LatLng you add to the Polyline with:

```PolylineOptions().geodesic(true).add(LatLng);```

Get to the initial one back at the end to get a Polygone.

## Circles

In ```onMapReady()``` add:

<pre><code>m_map.addCircle(new CircleOptions()
     .center(new LatLng(47.489805, -122.120502))
     .radius(5000) // = 5 km
     .strokeColor(Color.GREEN)
     .fillColor(Color.argb(64,0,255,0)));
</pre></code>

# StreetView

- setPosition
- getLocation
- getPanoramaCamera

By default these 3 options are enabled, manage them with the following, if you like:

- Street Names: isStreetNamesEnabled(), setStreetNamesEnabled(boolean)
- Zoom Gestures: isZoomGesturesEnabled(), setZoomGesturesEnabled(boolean)
- User Navigation: isUserNavigationEnabled(), setUserNavigationEnabled(boolean)

User interaction:

- Detect Camera changes: setOnStreetViewPanoramaCameraChangeListener
- Detect User Touches on Panorama: setonStreetViewPanoramaClickListener
- Detect changes to the Panorama: setOnStreetViewPanoramaChangeListener
