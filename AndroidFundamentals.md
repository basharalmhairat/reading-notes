## AndroidFundamentals

Android apps can be written using Kotlin, Java,
and C++ languages. The Android SDK tools compile your code along with any data and resource files into an APK or an Android App Bundle.
An Android App Bundle, which is an archive file with an .aab suffix, contains the contents of an Android app project including some additional metadata
that is not required at runtime. An AAB is a publishing format and is not installable on Android devices, it defers APK generation and signing to a later stage.
When distributing your app through Google Play for example, Google Play's servers generate optimized APKs that contain only the resources and
code that are required by a particular device that is requesting installation of the app.

Each Android app lives in its own security sandbox, protected by the following Android security features:
![image](https://user-images.githubusercontent.com/97823170/164977962-38cc140d-d36a-4e49-a921-53cd6e1c514d.png)

The Android operating system is a multi-user Linux system in which each app is a different user.
By default, the system assigns each app a unique Linux user ID (the ID is used only by the system and is unknown to the app).
The system sets permissions for all the files in an app so that only the user ID assigned to that app can access them.
Each process has its own virtual machine (VM), so an app's code runs in isolation from other apps.
By default, every app runs in its own Linux process.
The Android system starts the process when any of the app's components need to be executed,
and then shuts down the process when it's no longer needed or when the system must recover memory for other apps.
The Android system implements the principle of least privilege.
That is, each app, by default, has access only to the components that it requires to do its work and no more.
This creates a very secure environment in which an app cannot access parts of the system for which it is not given permission.
However, there are ways for an app to share data with other apps and for an app to access system services:

![image](https://user-images.githubusercontent.com/97823170/164977989-1a26e039-8d8a-45b1-b75a-8f616e24db9f.png)

It's possible to arrange for two apps to share the same Linux user ID, in which case they are able to access each other's files.
To conserve system resources, apps with the same user ID can also arrange to run in the same Linux process and share the same VM.
The apps must also be signed with the same certificate.
An app can request permission to access device data such as the device's location, camera, and Bluetooth connection. 
The user has to explicitly grant these permissions. For more information, see Working with System Permissions.
The rest of this document introduces the following concepts:

![image](https://user-images.githubusercontent.com/97823170/164977936-3693651b-f129-48ba-aae6-27f38063aa37.png)

The core framework components that define your app.
The manifest file in which you declare the components and the required device features for your app.
Resources that are separate from the app code and that allow your app to gracefully optimize its behavior for a variety of device configurations.

### App components
App components are the essential building blocks of an Android app. Each component is an entry point through which the system or a user can enter your app. Some components depend on others.

There are four different types of app components:

Activities
Services
Broadcast receivers
Content providers

Activities: It deals with the UI and the user interactions to the screen. In other words, it is a User Interface that contains activities. These can be one or more depending upon the App. It starts when the application is launched. At least one activity is always present which is known as MainActivity. The activity is implemented through the following.  

Syntax:

public class MainActivity extends Activity{
  // processes
}
To know more Activities please refer to this article: Introduction to Activities in Android

Services: Services are the background actions performed by the app, these might be long-running operations like a user playing music while surfing the Internet. A service might need other sub-services so as to perform specific tasks. The main purpose of the Services is to provide non-stop working of the app without breaking any interaction with the user. 

Syntax:

public class MyServices extends Services{
  // code for the services
}
To know more Services please refer to this article: Services in Android with Example

Broadcast Receivers: A Broadcast is used to respond to messages from other applications or from the System. For example, when the battery of the phone is low, then the Android OS fires a Broadcasting message to launch the Battery Saver function or app, after receiving the message the appropriate action is taken by the app. Broadcast Receiver is the subclass of BroadcastReceiver class and each object is represented by Intent objects. 

Syntax:  

public class MyReceiver extends BroadcastReceiver{
   public void onReceive(context,intent){
 }
To know more Broadcast Receivers please refer to this article: Broadcast Receiver in Android With Example

Content Provider: Content Provider is used to transferring the data from one application to the others at the request of the other application. These are handled by the class ContentResolver class. This class implements a set of APIs(Application Programming Interface) that enables the other applications to perform the transactions. Any Content Provider must implement the Parent Class of ContentProvider class. 

Syntax:  

public class MyContentProvider extends ContentProvider{
   public void onCreate()
   {}
}
