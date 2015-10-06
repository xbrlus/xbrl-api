xbrlBaseElement REST API
----
This API allows the user to fetch details of US GAAP Taxonomy elements from the XBRL US GAAP Taxonomy in an XML format, by passing the element name from the US GAAP taxonomy in the API.

* **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlBaseElement&Element=Assets&Namespace=http://fasb.org/us-gaap/2015-01-31&API_Key=EnterKeyHere>

* **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlBaseElement`

   `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

   **Optional:**

    `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.

    `Namespace=[url]` - The namespace of the taxonomy the data is requested for. For example http://fasb.org/us-gaap/2015-01-31.

   **Minimum:**

   All calls to the API must include at least an element name.  If no namespace is selected the latest namespace will be used.


* **Data Params**

    The API supports the same params as the URL.

* **Success Response (Normal):**

    ```XML
      <dataRequest date="2015-09-04T15:35:26-0400">
        <baseElement>
            <elementName>Liabilities</elementName>
            <namespace>http://fasb.org/us-gaap/2015-01-31</namespace>
            <abstract>false</abstract>
            <type>xbrli:monetaryItemType</type>
            <substitutionGroup>xbrli:item</substitutionGroup>
            <id>us-gaap_Liabilities</id>
            <periodType>instant</periodType>
            <balance>credit</balance>
            <nillable>true</nillable>
            <standard lang="en-US">Liabilities</standard>
            <documentation lang="en-US">        
                <![CDATA[
                Sum of the carrying amounts as of the balance sheet date of all liabilities that are recognized. Liabilities are probable future sacrifices of economic benefits arising from present obligations of an entity to transfer assets or provide services to other entities in the future.
                ]]>
            </documentation>
        </baseElement>
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
