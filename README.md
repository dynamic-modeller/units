# Simplest TypeQL Units Model

## Overview
This repo is the simplest TypeQL model of a units library. It contains the code and data needed to load a minimum example. It imports data froma series of csv, making it easy to add your own units.

## How it works
Units are defined by their string value, for example "kN.m", or "m2". This "unit" attribute, is also owned as a key by the ```unit_details``` relation, which contains all of the details for that particular unit. These details include conversion attributes, to enable conversion to the metric base unit. 

To create a measure, one needs to simply have a quantity and connect the unit to it in the schema
```measure isa attribute, value long, has unit```

Then, on import one just uses the simple syntax
```insert $m isa measure; $m 103.25; $m has unit "kPa";```

The unit is also connected to the dimensions, which define that measure. These dimensions also have the base unit name, attached to them. In addition to the usual SI dimensions (time, length, mass, current, temperature, moles, luminosity), there are two extra ones added for non-dimensional measures (radians, composition). The non-dimensional composition measures also connect to the unit they are compared on, for example m3/m3 has acomposition dimension of 1, and a length dimension of 3.

Non-base units, like "in2", are automatically connected to their base unit, "m2", so that conversions can be set up. At the moment, conversions are not implemented, as we are waiting for calculations before implementing them.

## Installing the Repo

### Prerequisites
To install the repo make sure that pipenv is installed in your Python. 

The implementation is tested on Python 3.8.

TypeDB must be running, and the system is setup to use the localhost. If you are using a different server, then its address need to be inserted in the clean_and_load.py.

### Installation
1. Run Pipenv shell
```pipenv shell```
2. Run pipenv install
```pipenv install```
3. Run clean_and_load.py
```python clean_and_load.py```

The installation implements some example measures, and these can be easily extended by adjusting the csv files from the spreadsheet