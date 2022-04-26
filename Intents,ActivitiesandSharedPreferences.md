# Intents, Activities, and SharedPreferences

A task is a collection of activities that users interact with when trying to do something in your app.
These activities are arranged in a stack—the back stack—in the order in
which each activity is opened. For example, an email app might have one activity to show a list of new messages

When do![image](https://user-images.githubusercontent.com/97823170/165354740-8b5ce5f5-2c96-411c-8625-5d18b1c97253.png)
ing a job, users engage with a task, which is a set of actions. The activities are stacked in the order in which they are opened in
a stack called the back stack. One action in an email app, for example, maybe to display a list of fresh messages. When the user picks a message,

a new activity appears in which the user may read the message. This new action has been sent to the back of the queue. When the user clicks the Back button,
the new action is completed and removed from the stack. When numerous applications are running in a multi-windowed environment,
which is allowed in Android 7.0 (API level 24) and above, the system maintains tasks for each window individually; each window may contain several tasks.
The system organizes tasks, or groups of tasks, on a per-window basis for Android apps running on Chromebooks.
![image](https://user-images.githubusercontent.com/97823170/165354613-acadce7f-8914-4974-ae02-48593b0c8d44.png)


For most tasks, the device’s Home screen is the starting point. The work of an app is brought to the front when the user taps an icon in the app launcher (or a shortcut on the Home screen). If no task for the app exists (because it hasn’t been used recently), a new task is created, and the app’s “main” activity is opened as the stack’s root activity. 

When the current activity switches to a new one, the new activity is pushed to the top of the stack and takes control of the attention.
The preceding action is still there in the stack, but it is no longer active. When a task is completed, the system saves the current state of the user interface.
The current activity is plucked off the top of the stack (the activity is destroyed) when the user hits the Back button, and the prior activity restarts
(the previous state of its UI is restored). The activities in the stack are only pushed onto and popped off the stack—pushed into the stack when the current activity
starts it and popped off when the user exits it using the Back button. As a result, the back stack is an object structure that is “last in, first out.”
Figure 1 depicts this behavior using a timeline that shows the progression of activities as well as the current back stack at each point in time
![image](https://user-images.githubusercontent.com/97823170/165354707-55af05b4-b375-490e-b27e-5a600aa44ea3.png)

A task is a logical unit that may be sent to the “background” when users start a new task or press the Home button to return to the Home screen.
All operations in the task are paused while it is in the background, but the task’s back stack remains intact—the task has just lost focus while another task
is being performed, as seen in figure 2. A task can then be brought back into the “foreground,” allowing users to resume their work where they left off. Assume
that the current task (Task A) contains three activities in its stack, two of which are underneath the current activity. The user hits the Home button, then
opens the app launcher and selects a new app. Task A is pushed to the background when the Home screen appears.
When a new app is launched, the system creates a task (Task B) for it, which has its own set of activities. After interacting with that app, the 
user goes back to Home and picks the app that launched Task A in the first place. Task A now appears in the forefront, with all three activities in
its stack intact and the activity at the top of the stack resumed. The user may now return to Task B by navigating to Home and choosing the app icon
that initiated the task (or choosing the app’s task from the Recents page). On Android, this is an example of multitasking.
![image](https://user-images.githubusercontent.com/97823170/165354670-4007f434-068f-47c7-9e50-11453b8d7ca8.png)

Because the activities in the back stack are never reorganized if your app allows users to launch a specific activity from multiple 
activities, a new instance of that activity is produced and placed onto the stack (rather than bringing any previous instance of the activity to the top).
As a result, a single activity in your app may be invoked many times (even from distinct jobs). As a result, if the user uses the Back button to browse backward,
each instance of the activity will be presented in the sequence in which it was accessed (each with its own UI state). If you don’t want an activity to
be created more than once, however, you may change this behavior. In the section on Managing Tasks, we’ll go through how to accomplish that. To describe the
default behavior for activities and tasks, consider the following:
![image](https://user-images.githubusercontent.com/97823170/165354639-8af87f34-90e7-48ef-be0e-97b7a05f38fc.png)
