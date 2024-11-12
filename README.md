# Android Notes:

## Execution state of an android activity
The Activity Lifecycle and Its Execution States
An Android activity goes through several states from creation to destruction. These states are managed by a series of lifecycle methods that are called in response to various user and system actions. Here's a breakdown of the key execution states an activity can be in during its lifecycle:

- onCreate(): Activity is being created. Initial setup like views and variables is done here.
- onStart(): Activity becomes visible but not yet interactive.
- onResume(): Activity is in the foreground and interactive with the user.
- onPause(): Activity is partially obscured by another activity; save data and release resources.
- onStop(): Activity is no longer visible. More resources are released.
- onRestart(): Activity is coming back into the foreground after being stopped.
- onDestroy(): Activity is being destroyed. Final cleanup occurs.

### State Transitions and Scenarios

#### Normal Flow:

Launch → onCreate() → onStart() → onResume() → (User interacts) → onPause() → onStop() → onDestroy().
#### User Navigates Back:

If the user presses back to go back to a previously opened activity, the lifecycle transitions from onPause() → onStop() → onRestart() → onStart() → onResume().
#### Activity is Interrupted:

If a new activity (like a dialog or a new app) takes focus, the current activity transitions from onPause() → onStop(). If the user returns, it will go from onRestart() → onStart() → onResume().
#### Activity is Finished:

The activity can be finished manually by calling finish(), which triggers the destruction sequence: onPause() → onStop() → onDestroy().


### Lifecycle Flow:
onCreate() → onStart() → onResume()
onPause() → onStop() → onRestart() → onStart() → onResume()
onDestroy() when the activity is finished.
This lifecycle helps manage resources, ensure smooth user interaction, and handle transitions effectively.

+--------------------+      onStart()      +------------------+
|    onCreate()      |------------------->|    onStart()     |
+--------------------+                      +------------------+
           |                                      |
           v                                      v
     onResume()                                  onPause()
           |                                      |
           v                                      v
     +------------+       onStop()      +------------------+
     |   onPause() |------------------->|    onStop()      |
     +------------+                      +------------------+
           |                                      |
           v                                      v
    +-------------+     onRestart()       +------------------+
    | onDestroy() |<----------------------|    onRestart()   |
    +-------------+                        +------------------+




## Android Activity:
The Android Activity lifecycle represents the various states an activity (screen) goes through from its creation to destruction. Understanding these states is essential for managing resources effectively and ensuring the app’s performance and responsiveness.

Here’s a breakdown of each state:

onCreate(): This is the first callback invoked when an activity is created. It's where you should initialize components (e.g., UI elements, variables) and set up resources.

onStart(): The activity is now visible to the user but is not yet in the foreground or interactive.

onResume(): The activity is now in the foreground and interactive. This is where you resume any tasks paused in onPause().

onPause(): Called when another activity comes to the foreground. The activity is still partially visible but not active. You should pause ongoing tasks and release system resources (like sensors, GPS).

onStop(): The activity is no longer visible. This is where you release resources or save data to persist the current state, as it might be destroyed afterward.

onDestroy(): Called before the activity is completely destroyed. This is the final call that an activity receives and is usually invoked when the app is closed or the activity is finished.

onRestart(): Called after onStop() if the activity is going to be started again, without being destroyed. This can happen if the user navigates back to the activity.

Diagram of the Android Activity Lifecycle
I'll provide a visual representation based on the standard flow of states and transitions:

Start (launch activity) → onCreate()
onCreate() → onStart()
onStart() → onResume()
onResume() → onPause()
If another activity comes in: onPause() → onStop()
If coming back: onStop() → onRestart() → onStart() → onResume()
onStop() → onDestroy() (if the activity is ending)
This structure helps Android developers manage UI components and system resources efficiently across different states. Let me know if you’d like a digital or diagram version of this for better clarity!

## Layouts

In Android development, a layout defines how the UI components (views) are arranged on the screen of an app. Every app’s user interface is built using layouts that provide structure to the views within it. These layouts ensure that elements are positioned correctly, respond to user interactions, and adapt to different screen sizes and orientations.

### ey Concepts:
**View:** A basic UI element in Android (e.g., Button, TextView, ImageView). Every visual component on the screen is a view.
**ViewGroup:** A special type of view that can hold multiple other views (child views). Layouts are generally subclasses of ViewGroup and serve as containers for UI elements.

#### Layout Attributes:
layout_width and layout_height specify the dimensions of a layout or view.
match_parent: Takes up all available space.
wrap_content: Takes up only as much space as needed by the content inside.

### Types of Layouts in Android
Here’s an overview of the most commonly used layouts and their use cases:

1. LinearLayout
Description: A layout that arranges its child views either in a horizontal or vertical direction. The orientation attribute controls whether the elements are stacked vertically or horizontally.
Use Case: Ideal for simple, single-row or single-column structures where each element is aligned in one direction.
Example: A vertical list of buttons stacked one below the other.

2. RelativeLayout
Description: This layout allows views to be positioned relative to each other or to the parent layout. You can align views to the left, right, top, bottom, or center of other views or the parent container.
Use Case: Suitable for complex UI designs where positioning of elements depends on other elements’ positions.
Example: A text field placed below a label or a button placed to the right of an image.

3. ConstraintLayout
Description: A more advanced layout that allows flexible and efficient positioning of views. Views are positioned using constraints rather than a strict hierarchical positioning system. It provides the ability to create complex UIs with flat view structures.
Use Case: Best for creating complex UIs, as it provides more control over the layout while keeping the hierarchy flat (reducing the need for nested layouts).
Example: A UI with buttons aligned at the top, text fields placed at the center, and images fixed at the bottom.

4. GridLayout
Description: A layout that arranges its child views in a grid-like format, where you can define the number of rows and columns.
Use Case: Suitable for applications that require a tabular layout, like a calculator or image gallery, where items are organized in a matrix.
Example: A 3x3 grid of buttons or images.GridLayout
Description: A layout that arranges its child views in a grid-like format, where you can define the number of rows and columns.
Use Case: Suitable for applications that require a tabular layout, like a calculator or image gallery, where items are organized in a matrix.
Example: A 3x3 grid of buttons or images.

## Manifest and its important tags

### Android Manifest File (`AndroidManifest.xml`)

The **AndroidManifest.xml** file is a crucial part of every Android application. It provides essential information about the app to the Android system, such as app components, permissions, and configurations. It acts as a bridge between the app and the Android system, enabling the system to understand how to launch and manage the app.

### Key Components of the Manifest

1. **`<manifest>`**: The root element that wraps the entire manifest file and contains attributes like `package` (the app’s unique identifier) and `xmlns:android` (the XML namespace).

2. **`<application>`**: Contains details about the application, such as the app’s icon, label, theme, and components (activities, services, etc.).
   
   - **Important attributes**:
     - `android:name`: Defines the class of the application.
     - `android:icon`: Sets the app's icon.
     - `android:label`: Defines the app's name displayed to the user.
     - `android:theme`: Defines the theme for the application.

3. **`<activity>`**: Declares an activity in the app, which represents a single screen with a user interface.
   
   - **Important attributes**:
     - `android:name`: Specifies the activity class name.
     - `android:label`: Defines the name of the activity.
     - `android:theme`: Optionally sets a custom theme for the activity.
     - `android:exported`: Specifies whether the activity can be invoked by components of other apps (required for activities targeting Android 12 or later).

4. **`<service>`**: Declares a service, which is a component that runs in the background to perform long-running operations.
   
   - **Important attributes**:
     - `android:name`: Specifies the service class name.
     - `android:exported`: Indicates whether the service can be accessed by other apps.

5. **`<receiver>`**: Declares a broadcast receiver, which listens for system-wide or app-specific events (e.g., incoming messages or system shutdown).
   
   - **Important attributes**:
     - `android:name`: Specifies the receiver class name.
     - `android:exported`: Indicates whether the receiver can receive broadcasts from other apps.

6. **`<provider>`**: Declares a content provider, which handles data sharing between apps.
   
   - **Important attributes**:
     - `android:name`: Specifies the provider class name.
     - `android:authorities`: Defines the provider’s authority (URI).

### Important Tags and Attributes

1. **`<uses-permission>`**: Declares the permissions the app needs to function, such as accessing the internet or reading contacts.
   
   - **Example**: 
     ```xml
     <uses-permission android:name="android.permission.INTERNET" />
     ```

2. **`<intent-filter>`**: Specifies the types of intents that an activity, service, or broadcast receiver can handle. It determines how the app interacts with other apps or system events.
   
   - **Example for an activity**:
     ```xml
     <activity android:name=".MainActivity">
         <intent-filter>
             <action android:name="android.intent.action.MAIN" />
             <category android:name="android.intent.category.LAUNCHER" />
         </intent-filter>
     </activity>
     ```

3. **`<uses-sdk>`**: Specifies the minimum and target SDK versions for the app, ensuring compatibility with specific versions of Android.
   
   - **Example**:
     ```xml
     <uses-sdk android:minSdkVersion="21" android:targetSdkVersion="30" />
     ```

4. **`<supports-screens>`**: Specifies which screen sizes and densities the app supports, helping optimize the UI for different devices.
   
   - **Example**:
     ```xml
     <supports-screens
         android:smallScreens="true"
         android:normalScreens="true"
         android:largeScreens="true"
         android:xlargeScreens="true" />
     ```

5. **`<activity-alias>`**: Provides an alias for an existing activity, allowing different entry points into the app without creating a new activity.

6. **`<meta-data>`**: Defines arbitrary values that can be used by app components or external libraries.
   
   - **Example**:
     ```xml
     <meta-data android:name="com.example.API_KEY" android:value="your-api-key-here" />
     ```

### Summary of Important Tags:
- **`<manifest>`**: The root element defining app's package name.
- **`<application>`**: Defines the application and its components.
- **`<activity>`**: Declares activities (screens) in the app.
- **`<service>`**: Declares services (background tasks).
- **`<receiver>`**: Declares broadcast receivers.
- **`<provider>`**: Declares content providers for data sharing.
- **`<uses-permission>`**: Specifies the permissions required by the app.
- **`<intent-filter>`**: Defines the types of intents that components can respond to.

The **AndroidManifest.xml** file is essential for an Android app's functionality, ensuring the app’s components are correctly defined and system resources (like permissions) are properly requested.
