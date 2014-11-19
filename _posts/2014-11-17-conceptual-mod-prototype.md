---
layout:     post
title:      Conceptual Module Prototype
date:       2014-11-17  
summary:    Documenting the Prototype for the Conceptual Module.
categories: conceptual-module prototypes portfolio-work
---

*last updated: 11/18/14*

## Am I Rent Stabilized? website
A significant component related to the issue of residential displacement from luxury development is that current rent stabilized units are being lost due to destabilization and erroneous practices by landlords. There is currently no system that makes sure landlords are reporting rent stabilized units to the local or state governments and charging the correct amount of rent to their tenants. Thus tenants or their lawyers must request their rent history from the New York State Division of Housing and Community Renewal (DHCR) and then file a complaint if they believe they are being over charged. Therefore the goal of the conceptual module is to create a simple one page, mobile friendly app to educate people about rent stabilization and how to find out if their apartment is rent stabilized. This app could be promoted as a go to guide about rent stabilization for tenants in NYC.

![]({{site.url}}/assets/am-i-rent-stabilized00.jpg)
Detail of visualization in CartoDB of all properties with likely rent stabilized units.

![]({{site.url}}/assets/am-i-rent-stabilized01.jpg)
Landing page for website.

![]({{site.url}}/assets/am-i-rent-stabilized02.jpg)
User enters their address and selects borough.

![]({{site.url}}/assets/am-i-rent-stabilized03.jpg)
User hits submit to run the query.

![]({{site.url}}/assets/am-i-rent-stabilized04.jpg)
If the query returns JSON data representing a tax lot that is likely rent stabilized then a message is displayed.

![]({{site.url}}/assets/am-i-rent-stabilized04a.jpg)
If the query returns no data then the user is alerted they are likely not rent stabilized.

![]({{site.url}}/assets/am-i-rent-stabilized05.jpg)
Javascript console showing the steps of geocoding the user input and retrieving data from the CartoDB SQL API.

## Methodology
The first step for working with the Map Pluto data was to set up a local Postgres database with PostGIS. PostGIS is an extension for Postgres that integrates GIS functionality into the Structured Query Language (SQL), a common programming language for use with relational database models. The Map Pluto dataset was imported into Postgres using the OGR2OGR utility, part of the Geospatial Data Abstraction Library (GDAL); a tool set for manipulating both vector and raster geospatial data on a command line interface. Working with the data in Postgres allows for faster querying and manipulation as the dataset is fairly large. 

The NYC Property Data Extractor app was created using Node.js with the Express framework. This allows for the connection of the app to the Postgres database. Leaflet.js, a free and open-source javascript library for creating interactive web maps was used for map interaction. A third party plug-in called Leaflet Draw was also utilized to allow a user to visually query the Map Pluto data by drawing a polygon on the map. When the polygon is drawn on the map its coordinates are passed to the server and used to perform a spatial query against the Map Pluto data. Data that intersects the user's query is then returned to the client and rendered on the map. From here the user may hover over tax lots to inspect information about them such as the owner, year built, zoning, etc. A video demo of the app may be viewed [on Vimeo](http://vimeo.com/110615218).

Map Pluto data was again utilized for the Am I Rent Stabilized website. Using Postgres a simple query was used to find out all properties that were built prior to 1975 and have more than 6 residential units. This query was performed on each Map Pluto borough layer and exported from Postgres to a generic ESRI Shapefile format. Each of the borough layers were then merged into a single layer and imported into CartoDB. An interactive visualization of these layers may be viewed [on CartoDB](http://cdb.io/1vfzSDJ). 

Once the data was stored in CartoDB, the platform's SQL API could be leveraged to return queried attribute data to the client. Prior to passing the user's input to CartoDB's SQL API the user's input is geocoded to a latitude longitude coordinate. Because of its reliability and accuracy the Google Maps API geocoder was used to handle the process of geocoding. After a user selects their borough, enters their address and hits the submit button, the form input is sent to the Google Maps API and geocoded. The geocoded point is then passed to the CartoDB SQL API wrapped in an SQL query on the Map Pluto data containing likely stabilized tax lots. If the point intersects the data then JSON data representing the tax lot is returned to the client and a message is displayed to the user informing them that they may be rent stabilized. If their address does not match they are notified that they may not be rent stabilized.

## Findings and Next Steps
The next steps to finish developing the website are:

- Finish designing the "take action" part of the website.
- User test and submit to various community groups such as NWB, Prospect Park East Network, MTOPP, etc. for feedback.
- Buy the domain name AmIRentStabilized.nyc and host the app online. This will be accomplished using GitHub's free web hosting.
- One person suggested adding an option to determine if the building has been registered with DHCR, if it hasn't and the building is likely rent stabilized the user could be notified of this.