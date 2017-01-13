# SEP-000X - SunPy Base Objects

| SEP           | X |
|---------------|---|
| title         | SunPy Base Objects  |
| author(s)     | Steven Christe |
| contact email | stuart@cadair.com |
| date-creation | 2017-01-13 |
| type          | standard |
| discussion    |  |
| status        |  |

## Introduction:

This document describes a new way to organize in a self-consistent way SunPy objects.

| Spatial | Temporal | Spectral | Note |
|--------|-------|----------|------|
| **SpaceSeries** (1d spatial data, e.g. slice from a map) |   |   |  does not exist |
| **SpaceSequence** (slit spectrogram where x is main axis) | | | does not exist |
|**XMap**    | **XTimeSeries** | **XSpectrum** | Base object, X is name of the instrument |
| **MapCollection** (renames current CompositeMap) | **TimeSeriesCollection** | **SpectrumCollection** | a collection of data usually taken at the same time but by different instruments |
| **MapSequence** (replaces current MapCube, Mapcubed would subclass this) | **TimeSeriesSequence** (ex. spectrogram where t is main axis) | **SpectrumSequence** (ex. spectrogram where freq/energy is main exist) | a series of related measurements such as as a function of time (MapSequence) or a function of energy (TimeSeriesSequence) |


# Decision Rational
