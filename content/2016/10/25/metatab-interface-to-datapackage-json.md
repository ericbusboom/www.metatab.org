---
title: "Metatab Interface to datapackage.json"
date: 2016-10-25T22:59:26+00:00
draft: false
categories: ["Metatab"]
author: "eric"
---

One of the inspirations for Metatab was the [Frictionless Data](<http://frictionlessdata.io/>) project, from [Open Knowledge International](<https://okfn.org/>), the creators of CKAN. The [project's specification](<http://frictionlessdata.io/data-packages/>) for data packages covers all of the common metadata for a dataset, and is extensible for less common needs. However, it is written in JSON, which was unfamiliar to a lot of the data creators that we worked with. That need for data creators who worked primarily in Excel to have a metadata format was the need that we started from. However, most metadata definitions will have the same structure, and it turned out that the most sensible structure for a Metatab file, combined with the most sensible way to turn metatab into JSON, resulted in output that was almost identical to the `datapackage.json` format. With the addition of a small `Declare` file, Metatab can directly output `datapackage.json.` Here is an excerpt of an example Metatab file, formatted for export to `datapackage.json `format. (You can get the whole file [online from github](<https://raw.githubusercontent.com/CivicKnowledge/metatab-py/master/test-data/datapackage_ex1_web.csv>). ) The `Declare` term specifies another Metatab file which adjust some of the terms, so the JSON output will be correct.  Declare | https://library-metatab-org.s3.amazonaws.com/assets.metatab.org/datapackage.csv |  |   
---|---|---|---  
title | Registered Voters, By County |  |   
description | Percent of the eligible population registered to vote and the percent who voted in statewide elections. |  |   
name | cdph.ca.gov-hci-registered_voters-county |  |   
version | 1.3.4 |  |   
|  |  |   
|  |  |   
Section | Resources | type | description  
resource | http://example.com/resource1.csv |  |   
.title | First Resource |  |   
.name | the-first-resource |  |   
.mediatype | text/csv |  |   
.format | csv |  |   
|  |  |   
schema |  |  |   
field | id | string | description  
field | state | string | description  
field | income | string | description  
You can test the conversion, after installing the [Python module and the metatab program](<https://github.com/CivicKnowledge/metatab-py>), by running: 

> $ metatab -j https://raw.githubusercontent.com/CivicKnowledge/metatab-py/master/test-data/datapackage_ex1_web.csv

The resulting output is a valid[ datapackage.json file](<https://share.civicknowledge.com/index.php/s/PS04nLAltFCHRWB/download>), although it isn't ordered as sensibly as it would have been had it been hand-written. We'll be adding this conversion to the [Spreadsheet Add-Ons](</projects/metatab-add-on/>) and web API, with a goal of providing an automatic conversion when Excel files in Metatab format are converted to ZIP archives of CSV files.
