---
title: "Metatab Metadata for the US Census"
date: 2016-12-02T23:26:29+00:00
draft: false
categories: ["Metatab"]
author: "eric"
---

The decennial US Census and the annual American Community Survey are the most important sources for demographic data in the US, and are the largest public datasets used to explore social issues. Each release of the ACS has 104 ZIP archives, each with 244 files, over 25,000 files in total. These files hold 1035 tables with almost 23,000 columns and 600,000 rows, for a total size of about 250GB. This size makes it an excellent test of data processing techniques, because if a tool can handle an ACS release, it can handle any dataset in the social sciences. So, we wrote a[ short program](<https://github.com/CivicKnowledge/metatab-py/blob/master/examples/census/make-census-metatab.py>) to create Metatab metadata for the 5 year release of the 2014 American Community Survey. Because the ACS is so large, the metatab representation is broken in the three files, with the top level package metadata file referencing the other two by inclusion. The three files are online: 

  * [acs20145-metadata.csv](<https://raw.githubusercontent.com/CivicKnowledge/metatab-py/master/examples/census/acs20145-metadata.csv>). The top level file

  * [acs20145-sources.csv](<https://raw.githubusercontent.com/CivicKnowledge/metatab-py/master/examples/census/acs20145-sources.csv>). The source file information

  * [acs20145-schema.csv](<https://raw.githubusercontent.com/CivicKnowledge/metatab-py/master/examples/census/acs20145-schema.csv>). The tables and columns


The metatab representation has some very important advantages over the metadata included in ACS releases. The most important is that the Metatab files are simultaneously human readable and trivial to use in a program. Metatab can be automatically converted to JSON, and the [JSON version of the Metatab files](<https://github.com/CivicKnowledge/metatab-py/blob/master/examples/census/acs20145.json?raw=true>) can be read and processes in any computing environment. With the [Metatab python module installed](<https://github.com/CivicKnowledge/metatab-py>), the `metatab` program can be used to download all three files, by referencing the top level file, and convert them to JSON: 
[code]
    $ metatab -j https://library-metatab-org.s3.amazonaws.com/assets.metatab.org/examples/acs20145-metadata.csv
    
[/code]

Note that by referencing the top level file, the Metatab parser downloads the other two, returning to the caller a data structure with all of the URLs to data files along with all of the tables, columns and other schema metadata. All of the information required to programmatically import the whole ACS release is available from a reference to a single URL. For instance, using the `[objectpath](<http://objectpath.org/>)` program to query JSON directly, we can return the URLs for the ZIP Archives for Nevada: ``
[code] 
    $ objectpath acs20145.json -e "$.datafile[@.state is 'NV'].@value"
    ["http://www2.census.gov/.../Nevada_Tracts_Block_Groups_Only.zip",
    "http://www2.census.gov/.../Nevada_All_Geographies_Not_Tracts_Block_Groups.zip"]
    
[/code]

Or, use Python to list all of the tables that have 'child' in the title: 
[code]
    $ python 
    >>> import json
    >>> [ t['name'] for t in json.load(open('acs20145.json'))['table'] 
        if 'child' in t['title'].lower()]
    [u'B05009', u'B05010', u'B09002', u'B09005', u'B09008', u'B09010', 
    u'B09018', u'B10001', u'B10002', u'B10010', u'B10050', u'B10051', 
    ...
    u'B23010', u'B25012', u'B25115', u'B99102', u'B99103', u'B99104']
    >>> 
    
[/code]

As a further demonstration, we'll be creating Metatab files for the [census extracts we're creating for the Amazon public data project](<https://github.com/CivicKnowledge/census-extract>).
