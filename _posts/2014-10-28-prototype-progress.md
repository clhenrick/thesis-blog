---
layout:     post
title:      Prototype Progress
date:       2014-10-28
summary:    Making progress on the NYC property transaction extractor.
categories: portfolio-work prototypes evaluative-module
---

## NYC Property Transaction Extractor

I made some progress on the backend of the app which uses Node JS with the Express framework, Jade and Postgres with PostGIS. Now a user can draw a rectangle or a simple polygon on the map and tax lots will be returned from the Postgres database for the selected area.

![]({{site.url}}/assets/nyc-property-extractor-prototype-v0a.jpg)
*the view of the map when opening the page*

![]({{site.url}}/assets/nyc-property-extractor-prototype-v0b.jpg)
*zooming in and selecting an area by drawing a rectangle*

![]({{site.url}}/assets/nyc-property-extractor-prototype-v0c.jpg)
*tax lot data returned from the database for the selcted area.*

![]({{site.url}}/assets/nyc-property-extractor-prototype-v0e.jpg)
*zooming in to the selected data*

![]({{site.url}}/assets/nyc-property-extractor-prototype-v0d.jpg)
*hovering over a tax lot reveals information such as its address, owner name, year built and primary zoning.*

## To Do:

__Refine the UI:__

- add some elements that explain purpose of the site and how to use it. This might be an interactive guided tour of the site.

__Develop Further Interaction__

- user selects area with drawing tools
  - add a UX caveat: they must be at a zoom level > x so they don’t select too much data and bog down the map or server.

- tax lots are displayed with mouse hover interaction.

_Next Steps:_

- user is asked to confirm selection. Meanwhile they can hover over lots to explore their properties (refine this?)

- when user hits a submit button the ACRIS transaction histories are queried for each lot

- CSV files are generated, zipped and sent to user's browser for download. 
  - perhaps the user gets an email when this step is complete with a link to dl if it takes too long?

- last but not least host on AWS or Heroku!