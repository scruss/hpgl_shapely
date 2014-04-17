hpgl_shapely
============

Very crude HP-GL output from
[Shapely](http://toblerity.org/shapely/project.html "Shapely")
geometries in Python. Currently just oozes HP-GL to stdout.

Requirements
------------

* [Shapely](http://toblerity.org/shapely/project.html "Shapely") -
  most recent is recommended, as version in Debian/Ubuntu repos is old
* Python (unfortunately)
* something to view HP-GL with; I recommend a real pen plotter, but
  you can use [HP2XX](http://ruby.chemie.uni-freiburg.de/~martin/hp2xx/ "HP2XX")/[HP-GL viewer](http://service-hpglview.web.cern.ch/service-hpglview/ "HP-GL viewer")/[GhostPDL](http://www.ghostscript.com/GhostPCL.html "GhostPDL").

Usage
-----

`import hpgl_shapely`, and these are the functions:

### Setup functions ###
* `hpgl_shapely.init()` - sends initialization code (IN).
* `hpgl_shapely.trailer()` - lifts the pen and parks it.

### Drawing function ###
* `hpgl_shapely.plot(obj, pen)` - plots the Shapely geometry `obj`
  using the pen `pen`. Handles most 2D geometry types supported by Shapely.

### Utility function ###
* `hpgl_shapely.hatchbox(rect, angle, spacing)` - for the rectangle
  `rect`, create a hatch fill object with lines at `angle` separated
  by `spacing`. Most useful for creating a whole page, then clipping
  to your shape using the Shapely
  [intersection](http://toblerity.org/shapely/manual.html#object.intersection
  "intersection") function.

### Low-level Drawing functions ###

You likely won't need these, as `plot()` calls these depending on the
geometry type in use. The names, I hope, are self-explanatory:

* `hpgl_shapely.plot_point(pt, pen)`
* `hpgl_shapely.plot_linestring(line, pen)`
* `hpgl_shapely.plot_polygon(poly, pen)`
* `hpgl_shapely.plot_multipoint(multipt, pen)`
* `hpgl_shapely.plot_multilinestring(multi, pen)`
* `hpgl_shapely.plot_multipolygon(multipoly, pen)`
* `hpgl_shapely.plot_geomcollection(geomcollection, pen)`

Unit are assumed to be native HP-GL units (1/40 mm).

If you run the main `hpgl_shapely.py` source, it will output a simple demo.

Bugs
----

* many. Barely tested. 
* Fails crudely if it meets a geometry it doesn't understand.
* Uses recursion in a potentially ill-advised manner.

To Do
-----

* line types
* integration with
  [Chiplotle](http://music.columbia.edu/cmc/chiplotle/ "Chiplotle")
* more geometries
* support functions like spline curve drawing
* data import through [Fiona](http://toblerity.org/fiona/README.html "Fiona")

Author
------

Stewart C. Russell - http://scruss.com/blog/

Mad props to Víctor and Doug of the
[Chiplotle](http://music.columbia.edu/cmc/chiplotle/ "Chiplotle")
project for keeping the interest in pen plotters going.

Licence
-------

WTFPL. (Srsly; see COPYING.)
