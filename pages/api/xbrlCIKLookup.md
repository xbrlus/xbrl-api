---
title: xbrlCIKLookup REST API
keywords: api
summary: "This API allows the user to fetch CIK information about a company by providing a ticker symbol."
sidebar: api_sidebar
permalink: xbrlCIKLookup.html
folder: api
---
### **Sample URL**
 Replace text "EnterKeyHere" (without quotes) with your API key to return data in your browser window: 

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlCIKLookup&Ticker=aapl>

### **Method**

  The API supports the following

  `GET` | `POST`

### **URL Params**

   **Required:**

  `TASK=xbrlCIKLookup`

  `Ticker=[alphanumeric]` - The Ticker of the company.



### **Data Params:**

  The API supports the same params as the URL.

### **Success Response:**

1. Valid Ticker

```xml
      <dataRequest date="2015-08-26T20:25:11-0400">
        <tickerLookup>
          <cik>0000732717</cik>
          <ticker>t</ticker>
          <name>AT&T INC.</name>
          <sic>4813</sic>
        </tickerLookup>
      </dataRequest>
  ```

2. Invalid Ticker

```xml
    <dataRequest date="2015-08-26T21:32:51-0400">
      <tickerLookup>
        <cik>No CIK found for this Ticker.</cik>
        <ticker>12</ticker>
        <name/>
        <sic/>
      </tickerLookup>
    </dataRequest>
```

### **Error Response**

  An error is returned if any parameter other than a Ticker is provided.

```xml
    <?xml version="1.0" encoding="utf-8"?>
    <error>
        <date>Wed, 26 Aug 2015 21:15:15</date>
        <status>Error - Bad Parameter</status>
        <message><![CDATA[The parameter of Ticks with a value of asp is not valid.]]></message>
    </error>
```

  An error is returned if no ticker value is provided.

```xml
    <?xml version="1.0" encoding="utf-8"?>
    <error>
        <date>Wed, 26 Aug 2015 21:13:30</date>
        <status>Error - Bad Parameter</status>
        <message><![CDATA[No value was entered for the Ticker.]]></message>
    </error>
```
