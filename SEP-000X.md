# SEP-000X - SunPy Base Objects

| SEP           | X                   |
|---------------|---------------------|
| title         | SunPy Base Objects  |
| author(s)     | Steven Christe      |
| contact email | stuart@cadair.com   |
| date-creation | 2017-01-13          |
| type          | standard            |
| discussion    |  -                  |
| status        |  -                  |

## Introduction:

This document describes a new way to organize base SunPy objects which bring
consistency. This naming draws from the following Python abstract base classes
* Collection - an unordered list
* Sequence - an ordered list

| Dimensions | 1D Spatial | Image (2D spatial) | Temporal | Spectral | Note |
|------------|----------|--------|-------|----------|------|
| 1          | **SpaceSeries** (e.g. slice from a image) |  NA | **TimeSeries**  | **Spectrum** | |
| 2          | **SpaceSeriesCollection** | NA | **TimeSeriesCollection** | **SpectrumCollection** | |
| 2          | **SpaceSeriesSequence** (slit spectrogram where x is main axis) | **Map** | **TimeSeriesSequence** (e.g. spectrogram with time as main axis)| **SpectrumSequence** (e.g. spectrogram where freq./energy is main exist)| |
| 3          | **MapCollection**    | |  | | |
| 3          | **MapSequence** | | | | | |

## Renaming of Current Classes
MapSequence replaces current MapCube while CompositeMap replaces MapCollection.

# Decision Rational
