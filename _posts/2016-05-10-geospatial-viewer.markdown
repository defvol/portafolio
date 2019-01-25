---
layout: post
title:  "Visualizing gigabytes of geospatial data in your browser"
date:   2016-05-10 19:41:14 -0800
categories: posts
technologies:
- javascript
- node.js
- mapbox.js
topics:
- Mapbox
- geospatial data
- OpenStreetMap
---

![visualizing geospatial data](/public/img/mbview-1.jpg)

While working as a data engineer for [Mapbox](https://www.mapbox.com/), I built a tool for inspecting dense geospatial files locally. This command-line program, called [mbview][mbview], came pretty handy for debugging, research, and analysis.

[MBTiles](https://docs.mapbox.com/help/glossary/mbtiles/) is an efficient file format for storing layers of data that makes a map tile. You can build them out of many sources, slices, queries, and filters. But when it comes to [OpenStreetMap][OSM], the data is so rich and dense that the development cycle on a cloud editor such as Mapbox, becomes cumbersome. With `mbview` you can prepare your data locally and upload the final product to the Mapbox editor for further styling and deployment.

You get some pretty cool results when running dense OpenStreetMap sources. See how beautiful is the work that the mapping
community has achieved over the years.

![rich and dense](/public/img/mbview-2.jpg)

### Takeaways

Designing software components as _lego blocks_ allows you to quickly iterate over new tools. I learned this myself when I was able to put together the very first version within a day by mixing components of the Mapbox ecosystem.

OpenStreetMap is an incredible source of public data about our cities and spaces. Contributing and reusing is totally worth it.

### Metadata

- **project**: mbview
- **code**: [https://github.com/mapbox/mbview][mbview]
- **technologies**: {{ page.technologies | array_to_sentence_string }}
- **topics**: {{ page.topics | array_to_sentence_string }}

[OSM]: https://www.openstreetmap.org/
[mbview]: https://github.com/mapbox/mbview
