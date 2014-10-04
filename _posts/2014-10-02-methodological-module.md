---
layout: post
title: Methodological Module
date: 2014-10-02
summary: Summary of the methodological module.
categories: methodological-module presentations prototypes design-briefs
---

## Presentaton
Link to the presentation [here]({{site.url}}/assets/method-present/index.html).

## Prototype
For this module I began to think about how to streamline the user experience of adding media to a map, or adding a spatial component to media. As a starting point I began to paper prototype an app:
![]({{site.url}}/assets/method-present/img/paper-prototype01.gif)

----------

This helped me to start thinking about refinements to the UI:
![]({{site.url}}/assets/dashboard_draft01.jpg)

The user should be able to import geotagged photos in one of 3 methods:  

1. drag and dropping photos that are already geotagged.
2. batch uploading multiple photos at a time that are already geotagged.
3. manually setting the location for an un-tagged photo.

In steps one and two server side software will be able to extract a photo's latitude and longitude coordinates from the photo's meta data (exif-information). 

The third option for manually setting a location could be accomplished by the user in one of two ways:  

- the user enters the name of place (country, state/province, city, neighborhood).
- the user interacts with a web-map interface to add and place a marker.

The third option could be utilized for either single or multiple photos. More paper prototyping and user testing will help determine how to make this process more intuitive.

## Design Brief
*to do...*