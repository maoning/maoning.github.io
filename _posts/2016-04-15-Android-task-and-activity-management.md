---
layout: post
title: Android Task and Activity Management
excerpt: "How to manage tasks and activities in Android."
categories: Android
comments: true
---

Definition of tasks and activities

### Defining Launch Mode

#### Manifest file
Specified in <activity> element's launchMod attribute.

<!-- Code example goes here -->

* standard (default)
    * creates a new instance of the activity in the task every time
    * each instance of the activity can belong to multiple tasks
    * each task can have multiple instances of activity
* singleTop
    * If activity already exists at the top of the current task, intent is routed to that instance through a call to its onNewIntent()
    * User is not able to press back button to go to the state before the new intent, because there is only one activity instance

    This means that no 2 instances of same activity can exists next to each other on the stack
* singleTask
    * Only one instance of activity can exist at a time. Later intents are routed to the existing instance through a call to its onNewIntent() method
    * Back button still returns the user to the previous activity contained in an existing task (may or may not be the same task the intent is called from), may create confusion?

    Android Browser application declares that the web browser activity should always open in its own task.

* singleInstance
    * The activity is always the single and only member of its task
    * Any activities started by this activity open in a separate task

#### Intent flags

* FLAG_ACTIVITY_NEW_TASK == singleTask

* FLAG_ACTIVITY_SINGLE_TOP == singleTop

* FLAG_ACTIVITY_CLEAR_TOP
    * If the activity is already running in the current task, then the intent is delivered to the resumed instance of the activity through onNewIntent() and all the activities above it are destroyed.

    FLAG_ACTIVITY_CLEAR_TOP + FLAG_ACTIVITY_NEW_TASK => locating an existing activity in another task and putting it in a position where it can respond to the intent.
    
<!-- Code example goes here -->


<!-- Questions
1. Inside the same app, could multiple instance of tasks exist?
-->

[You can see the official Android reference page here.]( http://developer.android.com/guide/components/tasks-and-back-stack.html)
