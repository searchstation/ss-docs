---
layout: default
title: Call Tracking
parent: Analytics
grand_parent: Processes
nav_order: 3
---

# Call Tracking
{: .no_toc}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### Introduction
There are three aspects to be considered in order to successfully pull Call Tracking off. The two platforms used for Call Tracking are Google Analytics 4 and the Infinity Hub. Hence, no GTM Configuration is required for the implementation of Call Tracking. It isn't complicated, but it is essential that all aspects need to be checked and double-checked as even the placement of a wrong letter at any point can hinder the process from sending, receiving and tracking data.

### Codebase
1. For this aspect, if you aren’t a developer, please ensure that you handle this with the assistance of a developer - or better yet, it should be confirmed by the developer. Incorrectly inserting or editing code in the head of a website could break the website.
2. From the Infinity Hub, go to the installation of the Website to be tracked select "Settings" on the lower left of the screen. Expand “Tracking” and select “Tracking Script“.
3. Place the Tracking Script on the right onto your website, before the closing </head> tag.
4. Ensure that the Tracking Scripts corresponds with the ID of the installation to be tracked.
5. The part of the website where the number is to be displayed is wrapped around an `InfinityNumber` class.
6. Note the format for event and event parameters. It is called snake case – all lowercase with underscore between words. It is highly recommended to abide by this for consistency and because Google advises it as part of their machine learning metric.

### Google Analytics 4 (GA4)
1. On the Data Stream section of the Website to be tracked, get the Measurement ID.
2. Then select "Select Measurement Protocol API Secrets". Then create and enter a nickname. This should be something relating to Infinity, for example “[Demo Website] Infinity Integration”. Then click 'Create'. This is becomes the API secret, take note of it.
3. At this point, go to the next section, set up the installation on Infinity Hub, and return to GA4.
4. To properly set dimensions for data coming from Infinity Hub, we have to take note of the parameters from Infinity Hub. These can be found in the "Event Parameters" section of the Search Station Master Tag Configuration.
5. As the call_duration event has a unit of seconds, check (Point 7 below).
6. From the "Admin" section of GA4, select "Custom Definitions". Then select "Create custom dimensions". From the canvas that slides into the screen, type in the parameter name in the "Dimension name" and "Event parameter" fields provided. Then "Save" the event parameter, do this for all events that are to be tracked (if they are not already existing).
7. If the received data has any kind of metric unit (e.g. currency, time, distance, etc) to be measured, Point 6 - above still applies, but instead, click on the "Custom metrics" and select "Create custom metrics". In this case the call_duration event should be set up using "Custom metrics".
8. GA4 has a "DebugView" feature which can be accessed from the "Admin" section of GA4. The entire tracking process of events and their respective data can be viewed in real time. This is helpful because, it takes a few hours for configurations made to GTM to track and send to GA4 for display.

### Infinity Hub
1. On the Infinity Hub, expand the “Integrations“ tab and select “Google Analytics“. Then select the “Add Google Analytics Account“.
2. Use an easy and appropriate name for the “Name” field (preferably the nickname used for the secret key can be used - [Demo Website] Infinity Integration) . The "Name" field is used to help identify the type of data being sent to Google Analytics, this data isn’t passed to Google Analytics.
3. Then enter the “API secret” (Secret Value) and “Measurement ID” taken from Google Analytics 4 admin section into the appropriate place
4. Once this is done, the Call Tracking event should be built based on the following standards;
    - The "Event Name" is "infinity_call".
    - The "Event Trigger" is "When the call has happened". 
    - The parameters should set as follows;
      - Field: Tracking Pool Name [Parameter Name: tracking_pool_name].
      - Field: Call Duration (seconds) [Parameter Name: call_duration].
      - Field: Conversion Page URL [Parameter Name: conversion_page_url].
5. Once this is done, "Save" the configuration, ensure that the integration is enabled on Infinity Hub and return to GA4.
