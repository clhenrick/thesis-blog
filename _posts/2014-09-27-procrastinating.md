---
layout:     post
title:      Mapping & GIS as procrastination
date:       2014-09-27
summary:    Procrastinating on the methodological module prototype.
categories: procrastination portfolio-work
---

While feeling nervous about having to make a paper prototype for my web app idea, I ended up making a map of something I wanted to do for a while; 311 noise complaints mapped by neighborhood in NYC. Of course I had to do this the hard way by using PostGIS (an extension for the Postgres database) rather than just doing it all in QGIS. I ended up calculating the number of complaints per square kilometer by neighborhood to make this map which I did render in QGIS just to make something quick and dirty:
![]({{site.url}}/assets/nyc-hood-noise.png)

And of course whenever I'm teaching myself something new I need to document it so I don't forget what I did. I also find this helpful so that I can use the documentation to teach others at school or during the Maptime NYC meetups I help host.

<script src="https://gist.github.com/clhenrick/ebc8dc779fb6f5ee6a88.js"></script>

This (^) will actually be helpful for when I start coding the app as I will most likely store the user's data in a Postgres database using PostGIS. It's good to mess with these tools now so I can get more comfortable using them when the time comes to code.  

Now I feel like I can get on with doing this paper prototype!