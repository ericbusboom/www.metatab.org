---
title: "Metatab Add-On"
date: 2016-10-10T22:03:17+00:00
draft: false
author: "eric"
---

The Metatab Google Spreadsheets Add-On is a simple extension that loads Metatab templates, adds basic Metatab term validation, and can produce a JSON representation of Metatab metadata. The Add On is not publicly released yet — it is still early stage software — but you can visit the [Chrome Webstore Application ](<https://chrome.google.com/webstore/detail/metatab/hgjehbojelifockaelbagmemdppcdfef>)page directly to get an install link. Clicking on the "Install" button will create a new Spreadsheet with the Add-on installed and present a pop-up help note on how to get started. [box type="info"] Problems? Visit our [Github Issues page](<https://github.com/CivicKnowledge/metatab/issues>) to submit a ticket or ask for help. [/box] [![add-on-menus](/uploads/2/2016/10/Add-On-Menus.png)](</uploads/2/2016/10/Add-On-Menus.png>) Use the single Add On menu to initialize a template or convert to JSON. After installing, you will have a new Spreadsheet with a "Metatab" entry in the "Add-ons" menu. Your options are: 

  * Initialize from a blank template
  * Initialize from a filled example template
  * Convert the current metadata, in the 'Meta' tab, to JSON format.

The application is very simple, but illustrates the major functions: 
  * The first column hold Metatab metadata terms, and has pull-down list and validation to ensure the terms are correct. Terms are validated per section, and incorrect terms are flagged.
  * Some of the term values ( currently only the `Format` term ) have validation for the value.

The templates are drawn from Google Spreadsheets, one for the[ blank template](<https://docs.google.com/spreadsheets/d/1pJpHrwscdJDyLmQJM40TymaZe3Zr97d7S1sFhZNmZnU/edit?usp=sharing>), and one for the [filled template](<https://docs.google.com/spreadsheets/d/1kAyhtgClMkNQutFHjb7oNzPjSVxMwroAQlPn1SPNnx0/edit?usp=sharing>). In production deployment, these templates could be configured by an organization. Another configuration point is the `Declares` term, which references a Metatab document that sets which terms are valid in each section, and how to convert the Metatab document to JSON. With an [appropriate configuration](<https://github.com/CivicKnowledge/metatab/blob/master/test/data/datapackage_profile.csv>), the JSON can be emitted in `package.json` format.
