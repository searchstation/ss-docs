---
layout: default
title: Event Tracking
parent: Analytics
grand_parent: General
nav_order: 1
---

# Event Tracking
{: .no_toc}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### Introduction
There are three aspects to be considered in order to successfully pull Event (& Custom Event) Tracking off. It isn't complicated, but it is essential that all aspects need to be checked and double-checked as even the placement of a wrong letter at any point can hinder the process from sending, receiving and tracking data.

### Codebase
1. For this aspect, if you aren’t a developer, please ensure that you handle this with the assistance of a developer - or better yet, it should be confirmed by the developer. Incorrectly inserting or editing code in the head of a website could break the website.
2. From Google Tag Manager, create a container for the site to be tracked (if a container does not exist already). This container would have a corresponding Google Tag Manager script. This script can be gotten from the container settings - “Installation Instructions”. 
3. As stated in the “Installation Instructions” suggests, these scripts should be inserted in the "<head>" and "<body>" section of the codebase. This should be confirmed in the header.php file. The container ID has the format – “GTM-XXXXXXX”, ensure also that this matches with that on the script in the header.php of the site whose events you want to track. 
4. Any event to be tracked is pushed by the following code snippet;
    ```js
    window.dataLayer.push({
        'event': 'event_pushed',
        'event_parameter1': parameter1,'event_parameter2': parameter2, 'event_parameter2' : 'String'
    });
    ```
5. Note the format for event and event parameters. It is called snake case – all lowercase with underscore between words. It is highly recommended to abide by this for consistency and because Google advises it as part of their machine learning metric.

### Google Tag Manger (GTM)
1. This aspect can be managed by the marketing manager, regardless, it would be done with events and parameters set by the developer and pushed from the website. 
2. On the Google Tag Manager platform, in the container created for the website to be tracked, import the Search Station Master Tag that contains a preset of custom triggers for events to be tracked (in line with a standard coding naming system). Download the Search Station Master Tag by [clicking this link](https://github.com/marvinoka4/ss-documentation/blob/567d2d8cfefb27dfdde85ccb5ccaa605dbafec22/assets/tags/GTM-SearchStationMasterTag.json). 
3. Then go to the "Admin" section of GTM. Select "Import Container". On the canvas that slides in, "Choose container file" and upload the downloaded Master Tag. Choose workspace by selecting "Existing" and choosing the "Default Workspace" from the canvas that slides in. The import option to be chosen is "Overwrite". Then "Confirm".
4. Once this is done, the following should be edited;
   - The title of the Config tag - GA4 Config - [Website Tracked] - can be edited when selected from the "Tag" section of the GTM platform. E.g. (GA4 Config - [Website Tracked]) can be changed to (GA4 Config - [Demo Website]).
   - The Measurement ID on the Tag Configuration canvas. Check "point 5." below to see where to get this from.
   - Ensure that the Search Station Master Tag points to the configuration tag. As in the case of the example above - GA4 Config - [Demo Website].
5. From Google Analytics 4, set up the property of the site to be tracked (if the property isn't already set-up). In the course of setting up the property, a data stream would be created, this data stream contains a Measurement ID with the format "G-XXXXXXXXXX". Take note of this Measurement ID. If the property exists, the Measurement ID can be gotten from the "Admin" section, there you'd see "Data Streams". Select the data stream of the website to be tracked. Copy the Measurement ID from the Data Stream in GA4 and paste it in the Tag Configuration-Measurement ID section of GTM.
6. Once this has been set up, use the GTM "Preview" feature to test that GTM is connected and the desired events are tracked. Once satisfied, use the "Submit" feature to publish, add a descriptive name to the version and "Publish".

### Google Analytics 4 (GA4)
1. Once GTM has been set up, the parameters have been tested using the GTM "Preview" feature, and the configuration has been "Published", we go to the GA4 platform to set "Dimensions" so that it can properly receive the data sent to it from GTM.
2. To properly set dimensions for data coming from GTM, we have to take note of the parameters from the Search Station Master Tag. These can be found in the "Event Parameters" section of the Search Station Master Tag Configuration.
3. From the "Admin" section of GA4, select "Custom Definitions". Then select "Create custom dimensions". From the canvas that slides into the screen, type in the parameter name in the "Dimension name" and "Event parameter" fields provided. Then "Save" the event parameter, do this for all events that are to be tracked (if they are not already existing). 