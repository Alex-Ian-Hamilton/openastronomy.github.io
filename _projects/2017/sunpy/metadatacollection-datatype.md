---
name: Generic Metadata Collection Datatype
desc: Generalize metadata storage when combining multiple files with different time ranges, coordinates or other properties, as a more generic class to the TimeSeriesMetaData class.
# add a short one line description of your project
requirements:
# Student requirements:
 - Knowledge of metadata as used in SunPy.
 - Familiar SunPy map and timeseries datatypes.
 - Some familiarity with 2D and 3D coordinate systems.
difficulty: intermediate
mentors:
# First person in contact; mentors may change before project starts.
 - Alex-Ian-Hamilton
initiatives:
 - GSOC
 - SOCIS
tags:
# Different technologies needed
 - python
collaborating_projects:
# suborganisation(s) to which this project belongs.
 - sunpy

#### Description

Metadata is an important aspect of dealing with observational data, generally represented as a series of key/value pairs (often stored as a dictionary), it provides information about the observations, observatory and instrument used.
When working with data you will often be using multiple observations, for example combining time series at different times or images at different wavelengths, and these often get merged together to form single files. In this case we need a way of storing the combined metadata in a way that allows you to trace the metadata for a given region of an image or timeseries.
The relevant metadata dictionaries should be able to be found for a given pixel or time, and properties like the map object used, here:
https://github.com/sunpy/sunpy/blob/master/sunpy/map/mapbase.py#L401

The TimeSeriesBase class uses a TimeSeriesMetaData object that is essentially a special case of this new metadata object, where the individual metadata dictionaries are stored in a list of tuples containing the time range and column names associated with the data.
In the case of the new object it would be able to be implemented in this way, but additionally you could use 2D coordinates to filter as well as time. In this case the TimeSeriesMetaData object essentially simply has a single coordinate for every metadata entry.
Note: ideally the implementation would support 3D coordinate systems, potentially sorted by reference pixel but ideally a sunpy.coordinates object (GenericMap.coordinate_frame).

The implementation will potentially store the data as a list of tuples of predefined length, each tuple (metadata entry) will have a metadata dictionary and then entries for all implemented filters in a defined orders (like TimeSeriesMetaData), where filters can include time range, coordinates, wavelengths or energies.
The MetaDataCollection base class may choose to implement the superset of all possible filters, or may choose to add those in sub-classes, consideration can be given to each option.
Consideration for sub-classes will be given, deciding if all implementations (I.E. in maps and timeseries) should contain all filters or if we limit some filters in sub-classes. E.G. do we have coordinate filters for timeseries data?
Methods should be defined that can access and manipulate data in the metadata dictionary/s, where filter values can be given to reduce the number of metadata dictionaries the match.
For general usage cases we would expect that given specific values we would get only one matching metadata entry, maintaining traceability.


#### Milestones (if any)

##### GSOC 2017 CODING STARTS

* Be awesome

##### GSOC 2017 MIDTERM

* Have done awesome stuff.

##### GSOC 2017 FINAL

* Finished the awesome stuff.
