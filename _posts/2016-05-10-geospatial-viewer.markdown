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

While working as a data engineer for [Mapbox](https://www.mapbox.com/), I built a tool for inspecting dense geospatial files on a browser. The tool become pretty handy for debugging, research, and analysis.

[MBTiles](https://docs.mapbox.com/help/glossary/mbtiles/) is an efficient file format to store layers of data that makes a map tile. You can build them out of many sources, slices, queries, and filters. But when it comes to [OpenStreetMap][OSM], the data is so rich and dense that it becomes cumbersome to upload to the Mapbox platform just for debugging. The ideal workflow would be to inspect locally and upload the final product to the Mapbox editor for styling and deployment.

Running `mbview` on OpenStreetMap sources will
show you how beautiful is the work that the OpenStreetMap
community has achieved over the years.

![rich and dense](/public/img/mbview-2.jpg)

### Takeaways

Thinking of software components as lego blocks allows you to quickly build new tools. I learned this when I was able to build the very first working version within a day just by reusing components of the Mapbox ecosystem.

OpenStreetMap is an incredible source of public data about our cities and spaces. Contributing and reusing is totally worth it.

### Metadata

- **project**: mbview
- **code**: [https://github.com/mapbox/mbview][mbview]
- **technologies**: {{ page.technologies | array_to_sentence_string }}
- **topics**: {{ page.topics | array_to_sentence_string }}

[OSM]: https://www.openstreetmap.org/
[mbview]: https://github.com/mapbox/mbview
