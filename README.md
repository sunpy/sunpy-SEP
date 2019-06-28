# SEPs: SunPy Proposal for Enhancement

# What is a SEP?
SEP stands for SunPy Enhancement Proposal. A SEP is a design document modeled
after the Python Enhancement Proposal which describes a new SunPy feature,
process, or major changes to existing processes or features. *Anyone* can
submit a SEP by making a pull request to this repository. You can find the
official definition of SEPs in [SEP-0001](./SEP-0001.md).
The full list of SEPs can be found in [SEP-0000](./SEP-0000.md).

# Process
Discussion is expected to take place using existing mechanisms and eventually
a decision is made regarding whether the proposal should be accepted or rejected
by a vote by the SunPy Board.


# Index

For a complete index see [SEP-0000](SEP-0000.md) this is reproduced here for convenience of navigation.

| Number | Title                                                       |
|--------|-------------------------------------------------------------|
|      1 | [SEP Purpose and Guidelines](./SEP-0001.md)                 |
|      2 | [SunPy Organization Definition](./SEP-0002.md)              |
|      3 | [Physical Units in SunPy](./SEP-0003.md)                    |
|      4 | [Packages Affiliated with the SunPy Project](./SEP-0004.md) |
|      5 | [Coordinates Module](./SEP-0005.md)                         |
|      6 | [SunPy Board Membership List](./SEP-0006.md)                |
|      7 | [Lightcurve Factory Refactor](./SEP-0007.md)                |
|      8 | [Astropy Time](./SEP-0008.md)                               |

# Uploading an SEP to Zenodo

Go to https://zenodo.org/deposit/new, upload the .md file, and set the fields to the following:

|Zenodo field                 | Value                                                  |
|-----------------------------| -------------------------------------------------------|
|Communities                  | The SunPy Project                                      |
|Upload type                  | Publication                                            |
|Publication type             | Technical note
|Publication Date             | The accepted date of the SEP|
|Title                        | SunPy Proposal for Enhancement <number>: <title> (SEP <number>)|
|Authors                      | The SEP authors (directly from the SEP text with ORCIDs if possible)|
|Description                  | The SEP description (usually the introduction)|
|Keywords                     | SunPy, Python, Solar, Astronomy
|License                      | CC-Attribution|
|Related/alternate identifiers| Github link to the SEP *at the latest commit* as "is supplemented by this upload". If this is a revised version, this should be the URL of the commit where the SEP was revised.|
  
Also add to the SunPy Project community.
