---
title: Margin Comparison Template
keywords: template
toc: false
summary: "This section contains margin Google Sheet that allow comparison of net income margins. The template shows how revenue and net income can be extracted from XBRL data."
sidebar: templates_sidebar
permalink: MarginCompareTemplate.html
folder: templates
---

Google Sheet version of the margin template linked here can be used for your analysis by doing the following: 

1. Create an online copy of the <a href="https://docs.google.com/spreadsheets/d/13nOp54sRr0T9VYdVF1_FUTc8MBeb-T5Ii48UPGKKlE0/edit?usp=sharing" target="_blank">Google Sheet</a> in your account. 

2. Replace the demo API key with your valid API key in the sheet (get a free API key from XBRL US at http://xbrl.us/apirequest). The demo key will expire, so copy your own key into the cell to replace the temporary API key.

3. Customize the analysis by changing the green cells for ticker symbol, time period or taxonomy elements selected, e.g., Revenues. Content in pink cells is reported XBRL data or calculated from XBRL data.

### Notes 
 The Google Sheet templates use [custom functions](gsheetFunctions) to pull the values from the API.  To get a copy of these functions take a copy of the spreadsheet using File>Make a Copy. This will duplicate the spreadsheets with  the custom functions.  These functions allow you to make up to 20,000 calls to the API.  In addition the function caches the results to conserve the number of calls made. The cache is flushed after 6 hours.
