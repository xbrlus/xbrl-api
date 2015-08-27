
xbrlCIKLookup REST API
----
This API allows the user to fetch CIK information about a company by providing a companies ticker symbol.

* **URL**

  <http://test.xbrl.us/php/dispatch.php?Task=xbrlCIKLookup&Ticker=aapl>

* **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlCIKLookup`

   `Ticker=[alphanumeric]` - The Ticker of the company.



* **Data Params:**

    The API supports the same params as the URL.

* **Success Response:**

    1. Valid Ticker

    ```XML
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
    ```XML
    <dataRequest date="2015-08-26T21:32:51-0400">
      <tickerLookup>
        <cik>No CIK found for this Ticker.</cik>
        <ticker>12</ticker>
        <name/>
        <sic/>
      </tickerLookup>
    </dataRequest>
    ```

* **Error Response:**

    An error is returned if any parameter than Ticker is provided.

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <error>
        <date>Wed, 26 Aug 2015 21:15:15</date>
        <status>Error - Bad Parameter</status>
        <message><![CDATA[The parameter of Ticks with a value of asp is not valid.]]></message>
    </error>
    ```

    An error is returned if no ticker value is provided.

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <error>
        <date>Wed, 26 Aug 2015 21:13:30</date>
        <status>Error - Bad Parameter</status>
        <message><![CDATA[No value was entered for the Ticker.]]></message>
    </error>
    ```



* **Notes:**

  For questions contact campbell.pryde@xbrl.us.
