
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

   `Element=[alphanumeric]` - The XBRL element. This parameter allows a comma separated list.

   `PeriodID=[Y|1Q|2Q|3Q|3QCUM|4Q|1H|2H|Other]` - Period required, if not provided all periods are returned. This parameter allows a comma separated list.

   `Year=[integer]`     - Year of the data required

   `StartYear=[integer]`  - First Year of  data to return a range used in conjunction with the `Year` parameter.

   `CIK=[integer]`   - CIK of the Company. This must be 10 digits in length. This parameter allows a comma separated list.

    `Accession=[alpha]`   - filing accession number. This is the accession number used by the SEC. This parameter does not allow a comma separated list.

   `Ultimus=[boolean]`    - True returns the latest value, false returns all values. If no value is defined the API defaults to true.

   `NoYears=[integer]`  - Years of data to returned based on value provided for `Year`. If `Year` is not provided then `NoYears` is ignored.

   `DimReqd=[boolean]`    - True returns all facts with and without dimensions associated with fact, false returns records with no dimensions. If no value is defined the API defaults to true.

   `Axis=[alphanumeric]` - The XBRL axis element. This parameter allows a comma separated list.

   `Member=[alphanumeric]` - The XBRL member element. This parameter allows a comma separated list.

   `Dimension=[alphanumeric]` - Axis and member i.e. DimensionID:IncomeTaxAuthorityAxi:AbasMember. A list of comma separated pairs can also be listed.

   `Restated=[boolean]` - A value of false will exclude amounts subsequently restated, a value of true will include amounts that were restated. If no value is defined the API defaults to false.

   `ExtensionElement=[base|extension]` - base will return non extension elements and extension will return extension elements. If no value is provided then all elements are returned.

    `ExtensionAxis=[base|extension]` - base will return non extension axes and extension will return extension axes. If no value is provided then all axes are returned.

    `ExtensionMember=[base|extension]` - base will return non extension members and extension will return extension members. If no value is provided then all members are returned.

    `Small=[boolean]` - If this parameter is set to true the size of the XML response is cut down. This is to help Excel users who may use the webservice function which returns the response into a single cell. These cells have size limitations.

   **Minimum:**

   All calls to the API must include at least a CIK or Filing Accession Number.  You can pull data for multiple entities by listing them as comma separated values.  It's not possible to call all values for an element such as Assets as the response will be too large.



* **Data Params**

    The API supports the same params as the URL.

* **Success Response (Normal):**

    ```XML
    <dataRequest>
    <fact>
          <entity><![CDATA[APPLE INC]]></entity>
          <entityCode>0000320193</entityCode>
          <accessionID>22881</accessionID>
          <filingAccession>0001193125-11-282113</filingAccession>
          <elementName>Assets</elementName>
          <namespace>http://fasb.org/us-gaap/2011-01-31</namespace>
          <extensionflag>N</extensionflag>
          <axis>StatementBusinessSegmentsAxis</axis>
          <member>JP</member>
          <units>USD</units>
          <amount>991000000</amount>
          <decimals>-6</decimals>
          <fact>991000000</fact>
          <period>Y</period>
          <year>2010</year>
          <filingDate>2011-10-26</filingDate>
          <aligned>false</aligned>
          <factID>10610385</factID>
          <dimensions>
            <dimensionPair>
              <axisLocalName>StatementBusinessSegmentsAxis</axisLocalName>
              <memberLocalName>JP</memberLocalName></dimensionPair>
          </dimensions>
          <dimensionCount>1</dimensionCount>
        <url>http://test.xbrl.us/php/dispatch.php?Task=htmlExport&amp;FactID=10610385</url>
        </fact>
      <count>
        <elementName>Number of Rows: 1</elementName>
        </count>
    </dataRequest>
    ```

* **Success Response (Small):**

    ```XML
  <dataRequest date="2015-09-01T20:08:02-0400">
      <fact>
        <entity>
        <![CDATA[ 3M CO ]]>
        </entity>
        <accessionID>146436</accessionID>
        <elementName>Assets</elementName>
        <namespace>http://fasb.org/us-gaap/2014-01-31</namespace>
        <axis/>
        <member/>
        <units>USD</units>
        <amount>31269000000</amount>
        <period>Y</period>
        <year>2014</year>
        <dimensions/>
        <dimensionCount>0</dimensionCount>
      </fact>
      <count>1</count>
  </dataRequest>
    ```

* **Error Response:**

    An error is returned if no value is defined for a CIK or an accession number.

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



* **Sample Call:**

    ```
    <mx:HTTPService id="ElementValue_HTTPRequest" url="{SERVERNAME}{SERVERPATH}dispatch.php"
    		 useProxy="false"
    		 method="POST"  
    		 showBusyCursor="true"
    		 result="{globalResultEventHandler(event)}{generateColsForAxis(event)}"
    		 fault="Alert.show(HTTP_REQUEST_ERROR +
    		 		event.fault.faultString, 'Connection Error')">
        <mx:request xmlns="">
        <Task>ElementUseMultipleGet</Task>
        <Element>{sendFilterSettings.elementUseID}</Element>
        <CIK>{sendFilterSettings.entityUseID}</CIK>
        <Axis>{sendFilterSettings.axisUseID}</Axis>
        <Member>{sendFilterSettings.memberUseID}</Member>
        <Period>{sendFilterSettings.period}</Period>
        <Year>{sendFilterSettings.endYear}</Year>
        <StartYear>{sendFilterSettings.startYear}</StartYear>
        <NoYears>{sendFilterSettings.noYears}</NoYears>
        <Restated>{sendFilterSettings.latestID}</Restated>
        <Accession>{sendFilterSettings.accessionUseID}</Accession>
        <Dimension>{sendFilterSettings.dimensionUseID}</Dimension>
        <ExtensionMember>{sendFilterSettings.selectedTaxonomiesMemberValuePostVariable}</ExtensionMember>
        <ExtensionAxis>{sendFilterSettings.selectedTaxonomiesAxisValuePostVariable}</ExtensionAxis>
        <ExtensionElement>{sendFilterSettings.selectedTaxonomiesValuePostVariable}</ExtensionElement>
        <Ultimus>{sendFilterSettings.ultimus}</Ultimus>
        <DimReqd>{!sendFilterSettings.defaultValuesOnly}</DimReqd>

    ```

* **Notes:**

  Any parameters defined that are not in the list above will be ignored.

  For questions contact support@xbrl.us.
