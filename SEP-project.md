* **author(s)**: Pritish Chakraborty
* **contact email**: chakrabortypritish@gmail.com
* **date-creation**: 2014-05-18
* **date-last-revision**: 2014-05-18
* **type**: standard
* **status**: TBA
* **discussion**: https://groups.google.com/forum/m/#!topic/sunpy-gsoc-2014/hKWRYe1ND00

# Abstract
SunPy's sunpy.wcs is to be phased out and re-implemented as sunpy.coordinates, through
the use of the API that Astropy's APE5 puts forward. Since the Astropy community have 
merged the APE5 pull request, we should review what these changes mean for this project. 

# Detailed Description
As part of my project, I am to use the framework defined by APE5 to create sunpy.coordinates,
which will do the job of the older sunpy.wcs in a more efficient and acceptable manner. The
first port of call will be to understand and chalk out use-cases from the APE5 branch that
would be relevant to this project.
IPython notebooks of these use-cases will be created for the benefit of the community. These
will contain the examples necessitated by the SEP template.

# Decision Rationale
This is a great idea because...