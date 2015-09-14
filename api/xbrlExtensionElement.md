xbrlExtensionElement REST API
----
This API allows the user to fetch details of extension Elements from company extensions in an XML format, by passing the element name and/or namespace in the API.

* **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlExtensionElement&Element=ResearchDevelopmentAndRelatedExpenses&API_Key=EnterKeyHere>

* **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlExtensionElement`

   `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

   **Optional:**

    `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.

    `Namespace=[url]` - The namespace of the company filing the data is requested for. For example http://www.ovt.com/20150430.

   **Minimum:**

   All calls to the API must include at least an element name.  If no namespace is selected all elements will be returned with their respective namespaces.


* **Data Params**

    The API supports the same params as the URL.

* **Success Response (Normal):**

    ```XML
    <dataRequest date="2015-09-11T17:05:35-0400">
      <extensionElement>
        <elementName>ResearchDevelopmentAndRelatedExpenses</elementName>
        <namespace>http://www.ovt.com/20150430</namespace>
        <abstract>false</abstract>
        <periodType>Duration</periodType>
        <balance>Debit</balance>
        <nillable>true</nillable>
        <documentation>
          <language>en-US</language>
          <labelValue>
          <![CDATA[
          Research, development and related expenses consist primarily of compensation and personnel-related expenses, non-recurring engineering costs related principally to the costs of the masks purchased when the company releases new product designs to the manufacturing foundry, costs for purchased materials, designs, tooling, depreciation of computers and workstations, and amortization of acquired intangible intellectual property and computer aided design software. Related costs include expenses associated with patent, copyright, trademark and trade secrets.
          ]]>
          </labelValue>
          <labelRole>http://www.xbrl.org/2003/role/documentation</labelRole>
        </documentation>
        <standard>
          <language>en-US</language>
          <labelValue>Research Development and Related Expenses</labelValue>
          <labelRole>http://www.xbrl.org/2003/role/label</labelRole>
        </standard>
      </extensionElement>
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



* **Notes:**

  Any parameters defined that are not in the list above will be ignored.

  For questions contact support@xbrl.us.
