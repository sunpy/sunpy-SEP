# Header
* **nickname**: Meta Class
* **author(s)**: Steven Christe
* **contact email**: steven.d.christe@nasa.gov
* **date-creation**: 2014-04-19
* **date-last-revision**:
* **type**: standard
* **status**: discussion
* **discussion**:

# Abstract
All SunPy data objects (e.g. Map, Timeseries, Spectrum) should provide a
standard interface to metadata. A unified interface will provide users a
consistent way to access metadata and will enable easy export and saving of
the metadata to standard file formats such as FITS. This SEP describes the
requirements for a new meta class which would provide this functionality.

# Detailed Description

The primary goal of the meta class is to provide a consistent and easy-to-use
interface to information about the data across all data objects as well as data
sources. Therefore it should not be tied to any particular standard (such as
FITS) though it may be informed by them. The class shall be able to output to
standard formats (such as FITS). No one wants to have to remember what CRVAL1
means! The meta class can also be used to define a minimum required set of meta
information as well as provide consistency checking. This would also be the
primary place to parse and fix non-standard compliant headers. Other
requirements for the meta class include

  * Shall be able to be created using a fits header
  * Shall always store all the information provided
  * Shall behaves like a dictionary but also provides property shortcuts
  * Shall be able to output to FITS and other formats
  * Shall take the the number of dimensions of the data as input
  * Shall be able to accept a wcs object on creation
  * should be a fits-wcs meta
  * Shall be able to allow comments to be added
  * Shall provide methods to update the meta (e.g. resample)
  * Shall sign of all its output
  * Shall always output using standards but be able to read-in non-standard headers
  * Shall have a pluggable parser for input and pluggable output
  * Shall not be able to open a file directly (should never have access to the data)

# Minimum Meta List

The meta class shall define a minimum set of meta data needed on creation. The
following list strives to define what that minium set consists of.

Name            | Description                          |
----------------| -------------------------------------|
time range      | the time range of the observation    |
units           | units of the data                    |
source          | the name of the data provider        |
source url      | the url of the data provider         |
url             | the source url for the data          |
telescope       | the satellite or observation platform|
instrument      | the instrument name                  |
frequency range | the spectral range of the observation|
level           | the level of the data                |
publisher       | the publisher of the data            |
publisher url   | the url to the publisher of the data |
publish date    | the date the data was published      |
resource url    | url to more resources about the data |
checksum        | a hash of the data                   |
location        | where the data was recorded          |
bad data        | the value used to denote bad data    |
----------------|--------------------------------------|

# Subclasses

    * fits-wcs class

# Decision Rational
This is a great idea because...
