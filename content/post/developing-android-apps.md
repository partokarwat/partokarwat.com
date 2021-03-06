+++
title = "Developing Android Apps"
topics = ["Development"]
date = "2017-02-12"
tags = ["udacity","android", "google"]
description = "Learn the fundamentals of android app development"

+++

You can find the corresponding course [at udacity] (https://www.udacity.com/course/new-android-fundamentals--ud851).

# Table of Contents
1. [Hard facts](#hard-facts)
1. [Basics](#basics)
1. [Intent Framework](#intent-framework)
1. [Data Persistence in Android](#data-persistence-in-android)
1. [Settings or Preferences](#settings-or-preferences)
1. [Activity Lifecycle](#activity-lifecyle)
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

Use responsive design for Android Apps, because your app will run on many different devices with different screen sizes. Provide at least small phone, large phone, medium tablet and large tablet design.

Have a mobile first policy. Mobile experience is the first consideration when building products. Most internet users come from mobile. Even children use mobiles not desktops to access the internet.

A good app should work like a good buttler: Giving you what you want before you even have to ask for it! NO Refresh-Button or Save-Button. Though using a Refresh-Button for debugging is allowed.

The master-detail flow is one of the most used Android App patterns.

The 4 types of components make off apps:

- [Activity](#activity-lifecycle)
- Service
- [Content Provider](#content-provider)
- Broadcast Receiver

UI Thread needs 60 frames per second (FPS) < 17 ms computation time

# Basics

## Android Studio Hints

Press shift 2x to access the search everywhere.

## Layouts

Layouts all extend from **ViewGroup**. All layouts are LayoutManagers (?).

- LinearLayout: Use for stacking vertically or horizontally 
- RelativeLayout: Powerful layout with tons of possibilities. Layout elements relative to one another.
- FrameLayout: Use if only 1 child view
- GridLayout
- ScrollView: ScrollView can have only one child
- ConstraintLayout 

## Logging

The existing log levels are:

- error
- warn
- info
- debug
- verbose

## ListView
1. Create visible items + 1 invisible above and underneath
1. Create new items just in time and hold all created items (visible + invisible) in memory

<span style="color:firebrick">&#x26a0; The more items, the more memory!</span> 

## RecyclerView
1. Create visible items + 1 above and underneath
1. New list item comes into view: Udapte data in recycle bin before destroying invisible item

<span style="color:green">++ Less memory overhead, less view management, smoother scrolling</span>

### RecyclerView LayoutManagers

- Linear: Scroll items either vertically or horizontally. Vertically is the default
- Grid: Item are staggered in a Grid and can scroll either vertically or horizontally.
- StaggeredGrid: Commonly used for views with content of varying dimensions.
- Custom: Extend from LayoutManager and create your own.

## Adapter
Knows how many list items are in the data set and how to build them. ListView asks the size of the data set and then asks what items to build. 

# Intent Framework

Intents are like envelopes:

- explicit has exact adress on it with data inside
- implicit has action on it with data inside

## Explicit Intent

> ```new Intent(context, DetailActivity.class)```

Often used in ```startActiviy(intent)```

## Implicit Intent

> ```new Intent(Intent.ACTION_VIEW);```

Possible actions to perform are VIEW, PICK, DIAL, MUSIC, CAMERA, ...

### Share Intent

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

### Broadcast Intents

Broadcast a message to many apps.

Use ```sendBroadcast()```method to implement it.

#### Broadcast Receiver

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

##### Manifest registration
<pre><code>&lt;receiver
	android:names=".MyReceiver"&gt;
	&lt;intent-filter&gt;
	...
	&lt;/intent-filter&gt;
&lt;/reciver&gt;
</code></pre>

Example: *GCM with Syncadapter*

##### Dynamic registration

<pre><code>IntentFilter intentFilter = new IntentFilter("com.myapp.MEW_LIFEFORM");
registerReceiver(myReceiver, intentFilter);
</code></pre>

Example: *Headphones unplugged/plugged change while hearing music*

## Intent Filters

Define ```<intent-filter>``` for every Activity that should be launchable from an implicit intent. (In your manifest.xml)

<pre><code>&lt;intent-filter&gt;
	&lt;action:name="android.intent.action.VIEW"/&gt;
	&lt;data android:scheme="geo"/&gt;
&lt;/intent-filter&gt;
</code></pre>

# Data Persistence in Android

Data Persistence is the act of saving some data to the phone.

## Bundle

Temporary store. Only use it if the user is actively using your app = **while the app is open**. *Example: onSaveInstanceState*

The data is saved as a key-complexValue pair

## SharedPreferences

Saves Key-primitiveValue-Pairs to a **file** on the Android Filesystem. The data is persisted unless you install the app or break the preference file.

## SQLite Database

Organize more complicated text/numeric/boolean data. 

## Internal/External Storage

Save multimedia or large data files to the internal or external Storage. Internal Storage is on the phone. External storage can be an SD-Card or similar.

## Server

Servers are for data that multiple phones will access. The data can be persisted also when deleting the app or using a different phone. An example for a cloud service is Firebase.

# Settings or Preferences

Settings can always be added later. Less settings at the beginning are better. 

Generally the flow goes like this:

1. User edits and updates a preference.
1. *PreferenceChangeListener* triggered for that preference.
1. The new value is saved to the *SharedPreference file*.
1. *onSharedPreferenceChanged* listeners are triggered.

Adding a setting is easier for the user than removing a setting. Removing a setting risk having a subset of users angry about the feature being taken away from them.

## Should it be a setting?

![Parto Karwat](/media/should-it-be-a-setting.png)

## PreferenceFragment

Remark: PreferenceActivity is depricated since Honeycomb in favor of the more flexible fragment version!

1. Add dependency ```compile 'com.android.support:preference-v7:25.1.0'```
1. Create a SettingsFragment and extend it from PreferenceFragmentCompat.
1. Create a new resource directory called ```xml``` and create preference resource files in it like for example ```pref_main.xml```
1. Add```addPreferencesFromResource(R.xml.pref_main);``` to the onCreatePreferences() method
1. Add to your AppTheme ```<item name="preferenceTheme">@style/PreferenceThemeOverlay</item>```

### PreferenceScreen

Is the root of a Preference hierarchy. It is the **container** that holds a couple of Preferences like CheckBoxPreference, ListPreference, etc. or even PreferenceScreens.

### Common Preferences 
- CheckBoxPreference
- ListPreference
- EditTextPreference

## SharedPreferences

SharedPreferences describe the **file** where the preferences are stored. Store private primitve data in key-value pair with a SharedPreference.

Read your SharedPreferences file with ```PreferenceManager.getDefaultSharedPreferences(this)```

### SharedPreferences.Editor

Write your SharedPreferences with the Editor. ```SharedPreferences.Editor editor = sharedPreferences.edit(); editor.putBoolean(KEY, value); editor.apply();```

### onSharedPreferencesChangeListener

1. Let the concerned Activity implement SharedPreferences.OnSharedPreferenceChangeListener
1. Implement onSharedPreferenceChanged
1. Register the listener in onCreate with ```sharedPreferences.registerOnSharedPreferenceChangeListener(this);```
1. Unregister the listener in onDestroy with ```PreferenceManager.getDefaultSharedPreferences(this).unregisterOnSharedPreferenceChangeListener(this);```

## PreferenceChangeListener

Is triggered before a value is saved to the SharedPreferences file. Can prevent an invalid update to a preference.

1. Implement the Preference.OnPreferenceChangeListener in your activity. ```implements Preference.OnPreferenceChangeListener```
1. Attach the listener to the preference to listen from in onCreatePreferences with ```Preference preference = findPreference(getString(R.string.pref_name_key)); preference.setOnPreferenceChangeListener(this);```
1. Implement onPreferenceChange()


# Activity Lifecycle

![Parto Karwat](/media/Android_Activity_LifeCyle.png)

- Active Lifetime: Active &#x21c4; Paused
- Visible Lifetime: Active &rarr; Paused &rarr; Stopped &rarr; Restored &rarr; Visible &rarr; Active
- Screen rotation leeds to: onPause &rarr; onStop &rarr; onDestroy &rarr; onCreate &rarr; onStart &rarr; onResume 

<span style="color:firebrick">&#x26a0; Save your app state in Bundle instance within **onSaveInstanceState()**. Restore your app state in onCreate() if the Bundle is not null. Like this actions like rotating your device won't affect the user experience.</span> 

- onStop is always the last method called before the app is killed (for example if it is running in the background an more resources are needed). Clean up any resources that need an ordinary tear down in onStop and onPause to make your app a good citizen! 
- onSaveInstanceState is called before onPause
- onRestoreInstanceState is called after onCreate

## Loaders

Create one in 3 steps:

1. Create a Loader ID
1. Fill-in the Loader Callbacks
1. Init the Loader with the LoaderManager

### AsyncTaskLoader

Use an AsyncTaskLoader for threads bound to an Activity rather than AsyncTask. 

AsyncTaskLoader is a better choice for Activity-bound thread management, because it handles lifecycle changes correctly, delivering the result to the current active activity, preventing duplication of background threads, and helping to eliminate duplication of zombie activities.

The functions of AsyncTaskLoader:

- onStartLoading
- forceLoad: Force an asynchronous load
- loadInBackground: Called on a worker thread to perform the actual load and to return the result of the load operation
- deliverResult: Sends the result of the load to the registered listener

## Best practice

- **No Exit Menu item** in Android! Exit is the back button.
- Include **menu items with semantic meaning**: Exit a session should be available by a menu item "logout", "sign-out" or similar.
- Background apps shouldn't consume ressources.
- Always prepare background apps to die.

## AsyncTask

4 steps:

- onPreExecute()
- doInBackground(Params...)
- onProgressUpdate(Progress...)
- onPostExecute(Result)

execute(), onPreExecute(), onProgressUpdate() and onPostExecute() run on the main UI thread. onProgressUpdate() and doInBackground() run on a background thread.

# Storing Data in SQLite

|          |             |    |
| --------------------- |:-------------------:| -----------------------:|
|                       | **DB Helper**       | **Content Provider**    |
| **Data Contract**     | **SQLite Database** |   Content Provider Test |
|                       | Database Test       |    URIMatcher Test      |

The Database Test is a write-read test on the database.

Data Contract defines all tables with its columns.

DBHelper extends SQLiteOpenHelper. DBHelper makes the database with a version number and a database filename.

*Manually increment version numbers* each time you release an updated database with a new schema.

```onCreate()``` creates the DB as SQL statement executed with ```.execSQL(..)```.

Implement ```onUpgrade()``` method called, when version number has changed. Use ALTER TABLE or DROP TABLE

## Database operations (CRUD)

The following operations are available on any database and known by CRUD for

- Create
- Read
- Update
- Delete

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