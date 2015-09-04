xbrlBaseElement REST API
----
This API allows the user to fetch details of US GAAP Taxonomy ELements from the XBRL US GAAP Taxonomy in an XML format, by passing the element name in the API.

* **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlBaseElement&Element=Assets&namespace=http://fasb.org/us-gaap/2015-01-31>

* **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlBaseElement`

   `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US.

   **Optional:**

    `Namespace=[url]` - The namespace of the taxonomy the data is requested for.

   **Minimum:**

   All calls to the API must include at least an element name.  If no namespace is selected the latest namespace will be used.



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

  For questions contact campbell.pryde@xbrl.us.
