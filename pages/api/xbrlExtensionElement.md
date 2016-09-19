---
title: xbrlExtensionElement REST API
keywords: api
summary: "This API allows the user to fetch details of about elements used in the company extensions in an XML format, by passing the element name, namespace and entity information in the API."
sidebar: api_sidebar
permalink: xbrlExtensionElement.html
folder: api
---
The API allows the user to get the attributes of an extension element and the associated labels.  If the filing information is provided the API will return the labels used by the company in their extension filing.  As a convenience it will also return the attributes of the US GAAP taxonomy.  

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

  `AccessionID=[int]` - Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one company will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

  `Accession=[alpha]` - Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter does not allow a comma separated list.

   **Minimum:**

   All calls to the API must include at least an element name.  If no namespace is selected all elements will be returned with their respective namespaces.


* **Data Params**

    The API supports the same params as the URL.

* **Return Values**

  All return values start with a lowercase letter. Only values that are available are returned.

  `entity` - The name of the company.

  `elementName` - The name of the xbrl base or extension element.

  `namespace` - The namespace of the base or extension element.

  `accessionID` - The internal number of the filing in the XBRL US database.

  `filingDate` - The date the filing was filed with the SEC.

  `filingAccession` - The accession number allocated to the filing by the SEC.

  `abstract` - True or false value. If the item is an abstract it is returned as true.

  `type` - The schema type of the XBRL elementNamee.e.g. monetaryItemType

  `periodType` - The period type of the element. Either "Instant" or "Duration".

  `balance` - The balance type of the element. Either "debit", "credit" or none.

  `nillable` - True or false value. If the item is nillable it is returned as true.

  `documentation` - The documentation label represented by http://www.xbrl.org/2003/role/documentation.

  `standard` - The standard label represented by http://www.xbrl.org/2003/role/label.

  `terse` - The terse label represented by http://www.xbrl.org/2003/role/terseLabel.

  `verbose` - The verbose label represented by http://www.xbrl.org/2003/role/verboseLabel.

  `total` - The total label represented by http://www.xbrl.org/2003/role/totalLabel.

  `negated` - The negated label represented by http://www.xbrl.org/2009/role/negatedLabel.

  `periodEnd` - The periodEnd label represented by http://www.xbrl.org/2003/role/periodEndLabel.

  `periodStart` - The periodStart label represented by http://www.xbrl.org/2003/role/periodStartLabel.


* **Success Response (Normal):**

```xml
    <dataRequest date="2015-09-11T17:05:35-0400">
      <baseElement>
        <entity>
          <![CDATA[ ADOBE SYSTEMS INC ]]>
        </entity>
        <elementName>ResearchAndDevelopment</elementName>
        <namespace>http://adobe.com/2010-03-05</namespace>
        <accessionID>28481</accessionID>
        <filingDate>2010-04-09</filingDate>
        <filingAccession>0000796343-10-000007</filingAccession>
        <abstract>false</abstract>
        <type>monetaryItemType</type>
        <periodType>Duration</periodType>
        <balance>Debit</balance>
        <nillable>true</nillable>
        <documentation lang="en-US">
          <![CDATA[
          Represents the expense recognized and included in Research and Development during the period arising from share-based compensation arrangements (for example, shares of stock, stock options or other equity instruments) with employees, directors and certain consultants qualifying for treatment as employees.
          ]]>
        </documentation>
        <standard lang="en-US">Research and development</standard>
        <verbose lang="en-US">Research and development</verbose>
        <terse lang="en-US">Research and development</terse>
        <negated lang="en-US">Research and development</negated>
        </baseElement>
    </dataRequest>
```

  `dataRequest - date` - The data request date attribute is the date that the data was generated. It is not the date of the query.  Data is cached once it is requested and is returned from cache if available. The data remains in cache for a day from the request. This means that data could be up to a day old if it has been previously requested.


* **Error Response:**

    An error is returned if no value is defined for an element name.

```xml
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

```xml
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
