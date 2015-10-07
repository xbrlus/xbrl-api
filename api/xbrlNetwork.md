xbrlNetwork REST API
----
This API allows the user to fetch details about a report (Group/Network/Extended link role) in an XBRL filing that an element appears in. This could return multiple results. The user passes an element and filing number/CIK and the report url will be returned. The API allows the user to specify the different linkbases associated with a report.  For example  a user can request the calculation network for those reports that contain Assets for company ABC.

* **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlNetwork&Element=Assets&AccessionID=143908s&API_Key=EnterKeyHere>

* **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlNetwork`

   `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

    `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.

   **Optional:**

    `Linkbase=[Calculation|Definition|Presentation]` - The type of network relationship. This could be a Presentation, Calculation or Definition. If this is not entered then all will be returned.

    `AccessionID=[int]` - Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one comapny will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

    `Accession=[alpha]` - Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter does not allow a comma separated list.

    `CIK=[integer]`   - CIK of the Company. This must be 10 digits in length. This parameter allows a comma separated list.

   **Minimum:**

   All calls to the API must include the `Element` parameter name and at least an `AccessionID` or an `Accession` number or a `CIK` parameter.


* **Data Params**

    The API supports the same params as the URL.

* **Success Response (Normal):**

    ```XML
    <dataRequest date="2015-10-06T19:34:20-0400">
      <fact>
        <entity>
          <![CDATA[ APPLE INC ]]>
        </entity>
        <entityCode>0000320193</entityCode>
        <accessionID>22871</accessionID>
        <filingAccession>0001193125-09-153165</filingAccession>
        <filingDate>2009-07-22</filingDate>
        <elementName>Assets</elementName>
        <extendedLinkRole>
          http://www.apple.com/taxonomy/role/statement/IMetrix_StatementOfFinancialPositionClassified
        </extendedLinkRole>
        <networkID>1797733</networkID>
        <networkName>
          12 - Statement - Statement Of Financial Position Classified
        </networkName>
        <linkType>http://www.xbrl.org/2003/arcrole/parent-child</linkType>
      </fact>
      <count>1</count>
    </dataRequest>
    ```

* **Error Response:**

    An error is returned if no value is defined for an element name.

    ```XML
    <error>
        <date>Fri, 04 Sep 2015 17:06:50</date>
        <status>Error - Bad Parameter</status>
        <message>
          <![CDATA[
          The value entered for the Element of is not valid.
          ]]>
        </message>
    </error>
    ```
    An error is returned if an incorrect parameter is provided.

    ```XML
    <error>
      <date>Fri, 04 Sep 2015 17:08:00</date>
      <status>Error - Bad Parameter</status>
      <message>
        <![CDATA[
        The parameter of mith with a value of 2 is not valid.
        ]]>
      </message>
    </error>
    ```
    An error is provided if a filing number or CIK is not provided.

    ```XML
    <error>
      <date>Tue, 06 Oct 2015 19:43:06</date>
      <status>Error - Insufficient Parameters</status>
      <message>
        <![CDATA[
        This call returns too much data. Please revise the attributes to include at least a CIK or Accession Number.
        ]]>
      </message>
    </error>
```



* **Notes:**

  Any parameters defined that are not in the list above will result in an error.

  For questions contact support@xbrl.us.
