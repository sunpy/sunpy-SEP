* **author(s)**: Pritish Chakraborty
* **contact email**: chakrabortypritish@gmail.com
* **date-creation**: 2014-05-18
* **date-last-revision**: 2014-05-24
* **type**: standard
* **status**: TBA
* **discussion**: https://groups.google.com/forum/m/#!topic/sunpy-gsoc-2014/hKWRYe1ND00

## Abstract
This SEP describes the implementation of a sunpy.coordinates package powered by
astropy.coordinates. This new subpackage will replace the solar coordinate transformations
currently implemented in sunpy.wcs.
Since the Astropy community have merged the APE5 pull request, we should review what these
changes mean for SunPy at this stage. 

## Detailed Description
We are to use the framework defined by APE5 to create sunpy.coordinates, which will 
do the job of the older sunpy.wcs in a more efficient and acceptable manner. The
first port of call will be to understand and chalk out use-cases from the APE5 branch that
would be relevant to this project. 
We require the use of classes such as `CoordinateRepresentation` and `BaseCoordinateFrame`.
These will be subclassed to generate our own frames and representations, according to the
solar coordinate systems.

### The astropy.coordinates Sub-Package

Beginning with Astropy v0.4, the `coordinates` subpackage has undergone a complete overhaul.
The coordinate class hierarchy has been split into three sets of classes -:

1. **Data Representation**: These classes are to be used to represent the data in a form 
meaningful to the Astropy/SunPy user. They are subclassed from the `CoordinateRepresentation`
abstract class. They are made to store the actual spatial information of a coordinate as a 
set of `Quantity` subclasses. They also provide methods to invoke transformations between
systems. 
2. **Low-Level**: These classes are to serve as descriptions of both coordinate frames and
act as containers around the data. They subclass from `CoordinateFrame`. Note that a pure 
frame is one that does not have any coordinate data, while a frame that does have such data 
becomes a coordinate.
3. **High-Level**: These classes wrap around the low-level classes and use their functionality.
They provide additional functionality to make the low-level classes easier to use. Astropy uses
the `SkyCoord` class to this end.

Additionally, a coordinate object is said to have the following components -:

1. **Coordinate Representation**: It is a particular way of describing a unique point in a vector
space (usually 3D space). Some examples of significance to SunPy are the Cartesian and Cylindrical
representations.
2. **Reference System**: It is a scheme used to orient points in a space. It is used to describe
how a point is transformed from system to system. Examples from the Astropy codebase are the ICRS
and equitorial coordinates (mean equinox) systems.
3. **Coordinate Frame**: This is a specific realization of a reference system. Some systems may have
only one meaningful frame while yet others may have several different frames. A tentative example in
the proposed SunPy subpackage would be that of the helioprojective coordinates, with Stonyhurst and
Carrington realizations.


I have hosted some IPython notebooks in the form of GitHub Gists using the IPython Notebook 
Viewer. They can be found at the following and be used for reference -:

1. [Coordinates API](http://nbviewer.ipython.org/gist/VaticanCameos/4a39e60df9f479c54ff1)
2. [Frame Classes](http://nbviewer.ipython.org/gist/VaticanCameos/b1612ec8c35f0d2a266a)


### The Proposed sunpy.coordinates Sub-Package

It is proposed that we implement the three coordinate systems, i.e., the heliographic, heliocentric and helioprojective systems in the form of low-level frame classes - `HelioGraphic`, 
`HelioCentric` and `HelioProjective`. These will be made to subclass from 
`BaseCoordinateFrame` and inherit its methods and properties.

Astropy's `SkyCoord` provides support for Cartesian, Spherical, UnitSpherical and
Cylindrical representations. Thus, one would simply have to wrap around SunPy's 
low-level frame classes with `SkyCoord` for immediate usage.

Some examples of usage -:

    from sunpy.coordinates.frames import HelioGraphicStonyhurst, HelioCentric
    from astropy.coordinates import SkyCoord
    from astropy import units as u

    # Some ways to initialize a `SkyCoord` object.
    # In Heliographic Stonyhurst frames, one can declare so -:
    sc = SkyCoord(
        1*u.deg, 1*u.deg, 1*u.km, frame='heliographicstonyhurst', 
        dateobs='2011/01/01T00:00:45'
    )
    print(sc)
    # We can represent the data as another frame.
    print(sc.represent_as('heliocentric'))

    # One could also not give the distance/radius input, and it will
    # default to solar radius.
    sc = SkyCoord(
        1*u.deg, 1*u.deg, frame='heliographicstonyhurst', 
        dateobs='2011/01/01T00:00:45'
    )
    print(sc)

    # It is also possible to provide the representation-specific args as a 
    # `BaseRepresentation` object.
    from sunpy.coordinates.representation import SphericalWrap180Representation
    sc = SkyCoord(
        SphericalWrapRepresentation180(1*u.deg, 1*u.deg, 1*u.km), 
        frame='helioprojective', dateobs='2011/01/01T00:00:45'
    )
    print(sc)
    
    sc2 = None
    if sc.is_transformable_to('heliocentric'):
        sc2 = sc.transform_to('heliocentric') # Transforms to HelioCentric with Earth Equitorial as preferred rep.


## Decision Rationale

