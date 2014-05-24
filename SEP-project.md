* **author(s)**: Pritish Chakraborty
* **contact email**: chakrabortypritish@gmail.com
* **date-creation**: 2014-05-18
* **date-last-revision**: 2014-05-24
* **type**: standard
* **status**: TBA
* **discussion**: https://groups.google.com/forum/m/#!topic/sunpy-gsoc-2014/hKWRYe1ND00

## Abstract
SunPy's sunpy.wcs is to be phased out and re-implemented as sunpy.coordinates, through
the use of the API that Astropy's APE5 puts forward. Since the Astropy community have 
merged the APE5 pull request, we should review what these changes mean for this project. 

## Detailed Description
As part of my project, I am to use the framework defined by APE5 to create sunpy.coordinates,
which will do the job of the older sunpy.wcs in a more efficient and acceptable manner. The
first port of call will be to understand and chalk out use-cases from the APE5 branch that
would be relevant to this project. I have summarized the project well in my GSoC proposal, 
which can be found [here](http://www.google-melange.com/gsoc/proposal/public/google/gsoc2014/vaticancameos/5629499534213120).
Secondly, by putting this SEP online, I am inviting constructive criticism and alternative 
ideas and approaches, in a bid to improve the project design.

### IPython Notebooks

I have hosted the notebooks in the form of GitHub Gists using the IPython Notebook Viewer. They
can be found at -:

1. [Coordinates API](http://nbviewer.ipython.org/gist/VaticanCameos/4a39e60df9f479c54ff1)
2. [Playing With Frames](http://nbviewer.ipython.org/gist/VaticanCameos/b1612ec8c35f0d2a266a)

The first notebook describes the relevant use-cases from the Astropy Coordinates API. It also
touches a bit on what the APE5 aims to introduce and how we will be using the same. The second
notebook describes the test run of two example frame classes, created by subclassing the 
`BaseCoordinateFrame` class in `astropy.coordinates.baseframe`. Any comments on both notebooks
are welcome!

### Discussion & Examples

Following from the second notebook, I propose that we implement the three coordinate systems,
 i.e., the heliographic, heliocentric and helioprojective systems in the form of low-level
frame classes - `HelioGraphic`, `HelioCentric` and `HelioProjective`. These will be made to
subclass from `BaseCoordinateFrame` and inherit its methods and properties.
Furthermore, since the `SkyCoord` object does not yet support frames that have the preferred
representation set to `CartesianRepresentation`, I propose that we build our own high-level
wrapper class, possibly named `SolarCoord`, which can wrap over solar-coordinate frames. We
can subclass `SkyCoord` to obtain its convenience methods, but we will, according to the
Astropy community, have to build our own transformation graph if we take this route.

The transformation graph is an important feature of Astropy's coordinates framework. It stores
as an edge between two coordinate systems (as nodes) a possible way of transformation between the
two. Types of transforms include `DynamicMatrixTransform`, `FunctionTransform`, etc. Each of
the coordinate transformations is defined in a method which is preceded by a decorator that
identifies it as a transformation method. The graph or registry is automatically updated with
the new transformation at this point. Having to build our own graph means greater design freedom
to mould it to solar cooordinate system usage, and implement our own version of Dijkstra's or
possibly even the A* algorithm to find shortest paths between two systems, and cache the results.
(Astropy uses the Dijkstra algorithm and also caches the results)

Some examples of usage -:

```from sunpy.coordinates.solarframes import HelioGraphic, HelioCentric
SolarCoord sc = SolarCoord(HelioGraph(...))
sc.represent_as(Stonyhurst)
sc.represent_as(Carrington)

sc2 = None
if sc.is_transformable_to(HelioCentric):
    sc2 = sc.transform_to(HelioCentric) # Transforms to HelioCentric with Earth Equitorial as preferred rep.```

and so on.


## Decision Rationale

