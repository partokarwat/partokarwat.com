+++
title = "Developing Android Apps"
topics = ["Development"]
date = "2017-02-19"
tags = ["udacity","android"]
description = "This is my summary of the same spelling udacity course."

+++

You can find the corresponding course [at udacity] (https://www.udacity.com).

# Table of Contents
1. [Hard facts](#hard-facts)
1. [Basics](#basics)
1. [Data Storage](#data-storage)

# Hard facts

Key Mobile challenges: 

- low processor power
- limited RAM
- intermittent, low bandwidth, high latency data connections
- impact on battery life

Android 1.0 launched in 2008.

Android OS structure from top to bottom:

1. Application Layer
1. Application Framework
1. C/C++ Libs, Android Runtime
1. Linux Kernel

App generation/deployment process:

![Parto Karwat](/media/app-generation-process.png)

Use responsive design for Android Apps, because your app will run on many different devices with different screen sizes. Provide at least small phone, medium phone and tablet/large phone design.

Have a mobile first policy. Mobile experience is the first consideration when building products. Most internet users come from mobile. Even children use mobiles not desktops to access the internet.

# Basics

## Layouts

Layouts all extend from **ViewGroup**. All layouts are LayoutManagers (?).

- LinearLayout: Use for stacking vertically or horizontally 
- RelativeLayout: Powerful layout with tons of possibilities. Layout elements relative to one another.
- FrameLayout: Use if only 1 child view
- GridLayout

ScrollView can have only one child.

## ListView
1. Create visible items + 1 invisible above and underneath
1. Create new items just in time and hold all created items (visible + invisible) in memory

<span style="color:firebrick">&#x26a0; The more items, the more memory!</span> 

## RecyclerView
1. Create visible items + 1 above and underneath
1. New list item comes into view: Udapte data in recycle bin before destroying invisible item

<span style="color:green">++ Less memory overhead, less view management, smoother scrolling</span>

## Adapter
Knows how many list items are in the data set and how to build them. ListView asks the size of the data set and then asks what items to build. 

## Intents Framework

Intents are like envelopes:

- explicit has exact adress on it with data inside
- implicit has action on it with data inside

### Explicit Intent

> ```new Intent(context, DetailActivity.class)```

Often used in ```startActiviy(intent)```

### Implicit Intent

> ```new Intent(Intent.ACTION_VIEW);```

Possible actions to perform are VIEW, PICK, DIAL, MUSIC, CAMERA, ...

#### Share Intent

Is the most used implicit intent.

Write a ShareActionProvider to make it work.

Share Intents will be addressed to anyone who can perform action SEND.  

<pre><code>Intent shareIntent = new Intent(Intent.ACTION_SEND);
shareIntent.addFlage(Intent.FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET); 
shareIntent.setType("text/plain");
shareIntent.putExtra(Intent.EXTRA_TEXT, string);

ShareActionProvider mShareActionProvider = (ShareActionProvider) MenuItemCompat.getActionProvider(menuItem);

if(mShareActionProvider != null) {
	mShareActionProvider.setShareIntent(shareIntent);
} else {
	Log.e("ShareActionProvider null?");
}
</code></pre>

```FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET``` prevents the activity we are sharing to run completely, when we press back, we come back to our app, not back in the shared app. 

#### Broadcast Intents

Broadcast a message to many apps.

Use ```sendBroadcast()```method to implement it.

##### Broadcast Receiver

Broadcast Receiver best use in:

- Monitoring changes to internet connectivity
- Charging status (ACTION_POWER_CONNECTED) (Ex. send data when connected to..)

Implementation:
<pre><code>public class MyReceiver extends BroadcastReceiver {
	@Override
	public void onReceive(Contect c, Intent i) {
		//Handle receive
	}
}
</code></pre>

Ways to register your BroadcastReceiver:

1. in Manifest: *triggered when app running and terminated*
2. in Code/dynamically in Activity: triggered *only when app running*

###### Manifest registration
<pre><code>&lt;receiver
	android:names=".MyReceiver"&gt;
	&lt;intent-filter&gt;
	...
	&lt;/intent-filter&gt;
&lt;/reciver&gt;
</code></pre>

Example: *GCM with Syncadapter*

###### Dynamic registration

<pre><code>IntentFilter intentFilter = new IntentFilter("com.myapp.MEW_LIFEFORM");
registerReceiver(myReceiver, intentFilter);
</code></pre>

Example: *Headphones unplugged/plugged change while hearing music*

### Intent Filters

Define ```<intent-filter>``` for every Activity that should be launchable from an implicit intent. (In your manifest.xml)

<pre><code>&lt;intent-filter&gt;
	&lt;action:name="android.intent.action.VIEW"/&gt;
	&lt;data android:scheme="geo"/&gt;
&lt;/intent-filter&gt;
</code></pre>

## Settings

Settings can always be added later. Less settings at the beginning are better.

### Common Preferences 
- CheckBoxPreference
- ListPreference
- EditTextPreference

### SharedPreferences

Store private primitve data in key-value pair with a SharedPreference.

## Activity Lifecycle

![Parto Karwat](/media/Android_Activity_LifeCyle.png)

- Active Lifetime: Active &#x21c4; Paused
- Visible Lifetime: Active &rarr; Paused &rarr; Stopped &rarr; Restored &rarr; Visible &rarr; Active
- Screen rotation leeds to: onPause &rarr; onStop &rarr; onDestroy &rarr; onCreate &rarr; onStart &rarr; onResume 

<span style="color:firebrick">&#x26a0; Save your app state in Bundle instance in onStop(). Like this it is guaranteed to be called before your app may be terminated by the runtime.</span> 

- onSaveInstanceState is called before onPause
- onRestoreInstanceState is called after onCreate

### Best practice

- **No Exit Menu item** in Android! Exit is the back button.
- Include **menu items with semantic meaning**: Exit a session should be available by a menu item "logout", "sign-out" or similar.
- Background apps shouldn't consume ressources.
- Always prepare background apps to die.

# Data Storage

|          |             |    |
| ------------- |:-------------:| -----:|
|                       | **DB Helper**       | **Content Provider** |
| **Data Contract**     | **SQLite Database** |   Content Provider Test |
|                       | Database Test       |    URIMatcher Test |


The Database Test is a write-read test on the database.

Data Contract defines all tables with its columns.

DBHelper extends SQLiteOpenHelper. DBHelper makes the database with a version number and a database filename.

*Manually increment version numbers* each time you release an updated database with a new schema.

```onCreate()``` creates the DB as SQL statement executed with ```.execSQL(..)```.

Implement ```onUpgrade()``` method called, when version number has changed. Use ALTER TABLE or DROP TABLE

## Content Provider

Content Provider makes your data accessible without needing to know how you stored it. So it makes it easy to switch out the datasource.

Widgets and Search need Content Provider. Ex.: GMail Widget, Play Store Search.

SyncAdapter (Get Data from your Server) and CursorLoader (Get data from your Database) need Content Provider too.

It also exists a SharedContentProvider.

The Content Provider Implementationsteps:

1. Determine URIs
1. Update Contract
1. Fill out URIMatcher
1. Implement Funktions

### Determine URIs
| CONTENT://     | COM.EXAMPLE.ANDROID.SUNSHINE.APP/ |  WEATHER/  | 64111  |
| --------------- |:-------------:| -----:| -----:|
| SCHEME         | AUTHORITY       | LOCATION | QUERY  |
|                | PACKAGE NAME    | DB TABLENAME | is optional!  |

ContentObserver refreshes automatically with URI.

- Base URIs = without Query, are for writing the DB.
- Special URIs are for reading/quering the DB

### Update Contract

Add URIs to Contract and create corresponding methods. (??)

### Fill out URIMatcher

- \# a number
- \* any string

Implement URIMatcher in ContentProvider class

Add the ContentProvider to the Manifest

<pre><code>&lt;provider
	android:authorities=[PACKAGENAME]
	android:name=[CONTENT_PROVIDER_CLASS]
/&gt;
</code></pre>
### Implement Funktions

Implementation order:

1. ```onCreate()```
1. ```getType(Uri)```
1. ```query(..)```
1. ```insert(..)```, ```update(..)```, ```delete(..)``` 
1. optional: ```bulkInsert(..)```

```insert(..)```, ```update(..)```, ```delete(..)``` are the write operations

### Content Resolver

Access the data via Content Provider with Content Resolver.

Use Content Provider for example in an async task:

```Cursor myCursor = mContext.getContentResolver().query(..);```