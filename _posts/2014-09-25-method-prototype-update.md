---
layout:     post
title:      Methodological Module Prototype Update
date:       2014-09-25
summary:    Sketching out a workflow for the prototype.
categories: Methodological-Module Prototypes
---

Today I began sketching out the workflow for a web app idea for my thesis. Realizing that currently there is no *easy* (and opensource) way for typical internet users to add media such as photos, video or sound to a map, I began thinking about making a minimalistically designed app that would allow for such a process. Below are some sketches of initial workflows I began thinking about for the app.

![]({{site.url}}/assets/workflow-scenarios.jpg)

Initially I'm envisioning three possible scenarios of how someone would use the app. They are:  

1. Creating data through the UI
2. Uploading existing data
3. Connecting to social media (such as Instagram, Flickr, Pinterest, etc.)

I then started with the first scenario, where a user would manually add points and media to a map, and worked out the steps for this process. Below is the sketch of the process mapped out:

![]({{site.url}}/assets/gui-design-scenario-one-workflow.jpg)

In this process I see the following steps:  

1. Navigating to the part of the world to add points / markers (and later possibly lines and polygons).  
This could be done by either:  
  - entering a location in a search box.
  - using the current IP adress of the user.
  - manually zooming and panning the map.
2. Adjust the cropping of the map area by zooming and panning.
3. Toggle an 'add data' functionality to add points to the map.
4. Add markers / points to the map by clicking on a place on the map.
5. Allow the user to adjust the location of the marker by dragging it.
6. Add media to associate with the marker. (An area of the UI would be devoted to this.)
7. User selects the location of their media, either by uploading a file or entering a URL.
8. The file is uploaded / added to the marker.
9. Option to repeat the last couple steps in order to add more than one piece of media.
10. Save the current marker / point.
11. Repeat the above steps or save the project and exit.

The tricky part will be to design an intuitive UI to make this an easy to accomplish task for the user. The next step will be designing some actual paper prototypes and doing some user testing.