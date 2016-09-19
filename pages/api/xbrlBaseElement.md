---
title: xbrlBaseElement REST API
keywords: api
summary: "This API allows the user to fetch details of US GAAP Taxonomy elements from the XBRL US GAAP Taxonomy in an XML format, by passing the element name from the US GAAP taxonomy in the API."
sidebar: api_sidebar
permalink: xbrlBaseElement.html
folder: api
---
## **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlBaseElement&Element=Assets&Namespace=http://fasb.org/us-gaap/2015-01-31&API_Key=EnterKeyHere>

## **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

  **Required:**

  `TASK=xbrlBaseElement`

  `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

  **Optional:**

  `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.

  `Namespace=[url]` - The namespace of the taxonomy the data is requested for. For example http://fasb.org/us-gaap/2015-01-31. If no namespace is provided the API will take the latest taxonomy.

  **Minimum:**

  All calls to the API must include at least an element name.  If no namespace is selected the latest namespace will be used.


## **Data Params**

  The API supports the same params as the URL.

## **Success Response (Normal):**

```xml
      <dataRequest date="2016-06-04T15:35:26-0400">
        <baseElement>
          <elementName>Assets</elementName>
            <namespace>http://fasb.org/us-gaap/2016-01-31</namespace>
            <changeLabel2016 lang="en-us">
                <![CDATA[ [2015-11] {Modified References} ]]>
            </changeLabel2016>
            <abstract>false</abstract>
            <standard lang="en-us">
                <![CDATA[ Assets ]]>
            </standard>
            <type>xbrli:monetaryItemType</type>
            <substitutionGroup>xbrli:item</substitutionGroup>
            <id>us-gaap_Assets</id>
            <periodType>instant</periodType>
            <balance>debit</balance>
            <nillable>true</nillable>
            <totalLabel lang="en-us">
                <![CDATA[ Assets, Total ]]>
            </totalLabel>
            <documentation lang="en-us">
                <![CDATA[
                Sum of the carrying amounts as of the balance sheet date of all assets that are recognized. Assets are probable future economic benefits obtained or controlled by an entity as a result of past transactions or events.
                ]]>
            </documentation>
        </baseElement>
    </dataRequest>
```

  `dataRequest - date` - The data request date attribute is the date that the data was generated. It is not the date of the query.  Data is cached once it is requested and is returned from cache if available. The data remains in cache for a day from the request. This means that data could be up to a day old if it has been previously requested.

  The API will return all of the labels that are associated with the element. In the example above the API returns the documentation label, the totalLabel and the changeLabel2016. The order of the labels will not be consistent.

## **Error Response:**

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

## **Notes:**

  Any parameters defined that are not in the list above will be ignored.
