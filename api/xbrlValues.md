
xbrlValues REST API
----
This API allows the user to fetch XBRL facts from the XBRL US database in an XML format, by passing financial statement parameters to define the data returned.

* **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlValues&Element=OperatingLeasesFutureMinimumPaymentsDueCurrent&Period=Y&Year=2014&CIK=0000732717&Ultimus=true&NoYears=1&DimReqd=false&API_Key=EnterKeyHere>

* **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlValues`

   `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>.

   **Optional:**

    ***Filing Parameters***

     `Accession=[alpha]`   - filing accession number. This is the accession number used by the SEC. This parameter does not allow a comma separated list.

     `AccessionID=[int]` - Internal Accession identifier used by the XBRL US database. This is returned by the API and can be used in subsequent calls.

    `CIK=[integer]`   - CIK of the Company. This must be 10 digits in length. This parameter allows a comma separated list.

     `Restated=[boolean]` - A value of false will exclude amounts subsequently restated, a value of true will include amounts that were restated. If no value is defined the API defaults to false.

    ***Element Parameters***

   `Element=[alphanumeric]` - The XBRL element. This parameter allows a comma separated list.

   `Axis=[alphanumeric]` - The XBRL axis element. This parameter allows a comma separated list. If defined the API will return facts which use this axis. If `DimReqd` is set to false this parameter will be ignored.

   `Member=[alphanumeric]` - The XBRL member element. This parameter allows a comma separated list. If defined the API will return facts which use this member. If `DimReqd` is set to false this parameter will be ignored.

   `Dimension=[alphanumeric]` - Axis and member i.e. DimensionID:IncomeTaxAuthorityAxi:AbasMember. A list of comma separated pairs can also be listed.

   `DimReqd=[boolean]`    - True returns all facts with and without dimensions associated with fact, false returns records with no dimensions. If no value is defined the API defaults to true.

    `ExtensionElement=[base|extension]` - base will return non extension elements and extension will return extension elements. If no value is provided then all elements are returned.

     `ExtensionAxis=[base|extension]` - base will return non extension axes and extension will return extension axes. If no value is provided then all axes are returned. If `DimReqd` is set to false this parameter is ignored.

     `ExtensionMember=[base|extension]` - base will return non extension members and extension will return extension members. If no value is provided then all members are returned. If `DimReqd` is set to false this parameter is ignored.

   ***Time Parameters***

   `PeriodID=[Y|1Q|2Q|3Q|3QCUM|4Q|1H|2H|Other]` - Period required, if not provided all periods are returned. This parameter allows a comma separated list.

   `StartYear=[integer]`  - First Year of  data to return a range used in conjunction with the `Year` parameter to define a range.

    `NoYears=[integer]`  - Use to define the number of years of data returned based on value provided for `Year`. For example if `NoYears`  is set to 3 and `Year` is set to 2014 then fact values will be returned for 2012, 2013, and 2014.  If `Year` is not provided then `NoYears` is ignored.

   `Year=[integer]`     - Year of the data required

   `Ultimus=[boolean]`    - True returns the latest value, false returns all values. If no value is defined the API defaults to true.

   ***Response Parameters***

    `Small=[boolean]` - If this parameter is set to true the size of the XML response is cut down. This is to help Excel users who may use the webservice function which returns the response into a single cell. These cells have size limitations.

   **Minimum:**

   All calls to the API must include at least a CIK or Filing Accession Number.  You can pull data for multiple entities by listing them as comma separated values.  It's not possible to call all values for an element such as Assets as the response will be too large.



* **Data Params**

    The API supports the same params as the URL.

* **Success Response (Normal):**

    ```XML
    <dataRequest date="2015-09-29T20:37:03-0400">
      <fact>
        <entity>
          <![CDATA[ APPLE INC ]]>
        </entity>
        <entityCode>0000320193</entityCode>
        <accessionID>72687</accessionID>
        <filingAccession>0001193125-13-300670</filingAccession>
        <elementName>SeniorNotes</elementName>
        <namespace>http://fasb.org/us-gaap/2013-01-31</namespace>
        <extensionflag>N</extensionflag>
        <axis>DebtInstrumentAxis</axis>
        <axisNamespace>http://fasb.org/us-gaap/2013-01-31</axisNamespace>
        <member>SeniorNotesDueTwentyEighteenMember</member>
        <memberNamespace>http://www.apple.com/20130629</memberNamespace>
        <units>USD</units>
        <amount>2000000000</amount>
        <decimals>-6</decimals>
        <fact>2000000000</fact>
        <period>3Q</period>
        <year>2013</year>
        <periodStart/>
        <periodEnd/>
        <periodInstant>2013-06-30</periodInstant>
        <filingDate>2013-07-24</filingDate>
        <aligned/>
        <factID>47622920</factID>
        <secURL>
          http://www.sec.gov/Archives/edgar/data/320193/000119312513300670/0001193125-13-300670-index.htm
        </secURL>
        <dimensions>
          <dimensionPair>
            <axisLocalName>DebtInstrumentAxis</axisLocalName>
            <memberLocalName>SeniorNotesDueTwentyEighteenMember</memberLocalName>
          </dimensionPair>
        </dimensions>
        <dimensionCount>1</dimensionCount>
        <url>
            http://csuite.xbrl.us/php/dispatch.php?Task=htmlExport&FactID=47622920
        </url>
        </fact>
        <count>282</count>
      <count>1</count>
    </dataRequest>
    ```

    `dataRequest - date` - The data request date attribute is the date that the data was generated. It is not the date of the query.  Data is cached once it is requested and is returned from cache if available. The data remains in cache for a day from the request. This means that data could be up to a day old if it has been previously requested.


* **Success Response (Small):**

    ```XML
    <dataRequest date="2015-09-29T20:38:20-0400">
      <fact>
        <entity>
        <![CDATA[ APPLE INC ]]>
        </entity>
        <accessionID>129603</accessionID>
        <elementName>SeniorNotes</elementName>
        <namespace>http://fasb.org/us-gaap/2014-01-31</namespace>
        <axis>DebtInstrumentAxis</axis>
        <axis_namespace>http://fasb.org/us-gaap/2014-01-31</axis_namespace>
        <member>SeniorNotesDueTwentySixteenMember</member>
        <member_namespace>http://www.apple.com/20150328</member_namespace>
        <units>USD</units>
        <amount>1000000000</amount>
        <period>Y</period>
        <year>2014</year>
        <dimensions>
        <dimensionPair>
        <axisLocalName>DebtInstrumentAxis</axisLocalName>
        <memberLocalName>SeniorNotesDueTwentySixteenMember</memberLocalName>
        </dimensionPair>
        </dimensions>
        <dimensionCount>1</dimensionCount>
      </fact>
      <count>1</count>
    </dataRequest>
    ```

* **Error Response:**

    An error is returned if the CIK value entered is not numeric.

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
              <error>
                  <date>Fri, 21 Aug 2015 18:11:08</date>
                  <status>Error - Insufficient Parameters</status>
                  <message><![CDATA[This call returns too much data. Please revise the attributes to include at least a CIK or Accession Number.]]></message>
              </error>
    ```
    An error is returned if the value for the CIK value is not numeric.

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
          <error>
              <date>Fri, 21 Aug 2015 18:15:08</date>
              <status>Error - Bad Parameter</status>
              <message><![CDATA[The value entered for the CIK of abcd is not valid.]]></message>
          </error>
    ```

    An error is returned if the value for the `Year` or `StartYear` is not a 4 character number after 1900.

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
          <error>
              <date>Fri, 21 Aug 2015 18:20:39</date>
              <status>Error - Bad Parameter</status>
              <message><![CDATA[The value entered for the Year of 1800 is not a valid year.]]></message>
          </error>
    ```

* **Notes:**

  Any parameters defined that are not in the list above will be ignored.

  For questions contact support@xbrl.us.
