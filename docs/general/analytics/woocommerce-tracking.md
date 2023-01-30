---
layout: default
title: WooCommerce Tracking
parent: Analytics
grand_parent: General
nav_order: 2
---

# WooCommerce Tracking
{: .no_toc}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### Introduction
There are four aspects to be considered in order to successfully pull Woocommerce (& Custom Event) Tracking off. It is a quite different from Event Tracking especially with the additional step and the fact that most of the parameters are pushed from WooCommerce, but it still isn't complicated. Regardless, it is essential that all aspects need to be checked and double-checked as even the placement of a wrong letter at any point can hinder the process from sending, receiving and tracking data.

### Codebase
1. For this aspect, if you aren’t a developer, please ensure that you handle this with the assistance of a developer - or better yet, it should be confirmed by the developer. Incorrectly inserting or editing code in the head of a website could break the website.
2. From Google Tag Manager, create a container for the site to be tracked (if a container does not exist already). This container would have a corresponding Google Tag Manager script. This script can be gotten from the container settings - “Installation Instructions”.
3. As stated in the “Installation Instructions” suggests, these scripts should be inserted in the "<head>" and "<body>" section of the codebase. This should be confirmed in the header.php file. The container ID has the format – “GTM-XXXXXXX”, ensure also that this matches with that on the script in the header.php of the site whose events you want to track.
4. Any event, that isn't predominantly a WooCommerce action/ activity, to be tracked is pushed by the following code snippet;
    ```js
    window.dataLayer.push({
        'event': 'event_pushed',
        'event_parameter1': parameter1,'event_parameter2': parameter2, 
        'event_parameter3' : 'String'
    });
    ```
5. Note the format for event and event parameters. It is called snake case – all lowercase with underscore between words. It is highly recommended to abide by this for consistency and because Google advises it as part of their machine learning metric.

### Google Tag Manger (GTM)
1. This aspect can be managed by the marketing manager, regardless, it would be done with events and parameters set by the developer and pushed from the website.
2. The first thing to do is to create a "Configuration Tag" that would measure the Data Stream from Google Analytics 4. On the GTM Workspace, click on "Tag" and then "New", then click "Tag Configuration", from the canvas that slides in select "Google Analytics: GA4 Configuration".
3. Once this is done, the following should be edited;
    - Instead of "Untitled Tag", the title of the Config tag should take the form - (GA4 Config - WooCommerce - [Website Tracked]). E.g. (GA4 Config - WooCommerce - [Website Tracked]) can be changed to (GA4 Config - WooCommerce - [Demo WooCommerce Website]).
    - The Measurement ID on the Tag Configuration canvas. Check "point 6." below to see where to get this from.
    - Then click on "Triggering", and choose "All Pages". Then "Save" the tag configuration.
4. On the Google Tag Manager platform, in the container created for the website to be tracked, import the Search Station WooCommerce Master Tag that contains a preset of WooCommerce events and custom triggers for events to be tracked (in line with a standard coding naming system). Download the Search Station WooCommerce Master Tag by [clicking this link](https://github.com/marvinoka4/ss-documentation/blob/567d2d8cfefb27dfdde85ccb5ccaa605dbafec22/assets/tags/GTM-SearchStationMasterTag.json).
5. Then go to the "Admin" section of GTM. Select "Import Container". On the canvas that slides in, "Choose container file" and upload the downloaded WooCommerce Master Tag. Choose workspace by selecting "Existing" and choosing the "Default Workspace" from the canvas that slides in. The import option to be chosen is "Merge". Then select "Overwrite conflicting tags, triggers and variables", then "Confirm".
6. Once the WooCommerce Master Tag has been imported, go back to the Workspace tab,select "Tags", go into the newly imported WooCommerce  Master Tag and click on it. Then click "Configuration Tag", and point it to the tag (as created from Point 2 - above) that contains the Measurement ID of the GA4 Data Stream. Then "Save".
7. From Google Analytics 4, set up the property of the site to be tracked (if the property isn't already set-up). In the course of setting up the property, a data stream would be created, this data stream contains a Measurement ID with the format "G-XXXXXXXXXX". Take note of this Measurement ID. If the property exists, the Measurement ID can be gotten from the "Admin" section, there you'd see "Data Streams". Select the data stream of the website to be tracked. Copy the Measurement ID from the Data Stream in GA4 and paste it in the Tag Configuration-Measurement ID section of GTM (as created from Point 2 - above).
8. Once this has been set up, ensure that the Search Station WooCommerce Master Tag points to the configuration tag. As in the case of the example above - (GA4 Config - WooCommerce - [Demo WooCommerce Website]). Then use the GTM "Preview" feature to test that GTM is connected and the desired events are tracked. Once satisfied, use the "Submit" feature to publish, add a descriptive name to the version and "Publish".

### WordPress
1. Ensure the "Google Tag Manager for WordPress Plugin (GTM4WP)" is installed and activated on the WooCommerce site.
2. Go to the plugin settings and paste the container ID with the format – “GTM-XXXXXXX” to the "Google Tag Manager ID" section of the plugin settings. Ensure that there are no spaces before of after the container ID.
3. Still on the settings of the plugin, ensure that the "Container code ON/OFF" section is "Off". The reason for this is that the code base already has the GTM script. Then "Save Changes".
4. Then go to the "Integration" tab, click on "WooCommerce" and tick the "Track enhanced e-commerce" checkbox. Then "Save Changes".

### Google Analytics 4 (GA4)
1. Once GTM and WordPress have been set up, the parameters have been tested using the GTM "Preview" feature, and the configuration has been "Published", we go to the GA4 platform to set "Dimensions" so that it can properly receive the data sent to it from GTM. Please note that setting dimensions is only necessary for **"Custom Events"**, not **"WooCommerce Events"**. Woocommerce already passes data from their events to GA4 in a way that doesn't require defining custom dimensions or metrics. 
2. To properly set dimensions for data coming from GTM, we have to take note of the parameters from the Search Station Master Tag. These can be found in the "Event Parameters" section of the Search Station Master Tag Configuration.
3. From the "Admin" section of GA4, select "Custom Definitions". Then select "Create custom dimensions". From the canvas that slides into the screen, type in the parameter name in the "Dimension name" and "Event parameter" fields provided. Then "Save" the event parameter, do this for all events that are to be tracked (if they are not already existing).
4. If the received data has any kind of metric unit (e.g. currency, time, distance, etc) to be measured, Point 3 - above still applies, but instead, click on the "Custom metrics" and select "Create custom metrics".
5. GA4 has a "DebugView" feature which can be accessed from the "Admin" section of GA4. Used with GTM's "Preview" feature, the entire tracking process of events and their respective data can be viewed in real time. This is helpful because, it takes a few hours for configurations made to GTM to track and send to GA4 for display.