---
title: xbrlChildren REST API
keywords: api
summary: "This API allows the user to fetch the relationships in a network by passing the extended link role, an element name and the filing number/CIK."
sidebar: api_sidebar
permalink: xbrlChildren.html
folder: api
---
The API will return all children of the specified element plus attributes such as weight, order and preferred labels. It will return multiple results. The API also allows the user to specify the different linkbases and relationship types associated with a report or network. For example a user can request the calculation children of Assets in the balance sheet for company ABC.

If an element name is not provided then all the relationships for the entire network are returned. This includes the root node which will have a tree depth of zero. If no element name is provided no value is returned for calculationEffectiveWeight as there is no relative element. In addition the Leaf node attribute is currently not returned when no element name is provided.

* **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlChildren&AccessionID=135173&Element=IncomeStatementAbstract&GroupURI=http://www.ibm.com/role/StatementCONSOLIDATEDSTATEMENTOFEARNINGS&Linkbase=Presentation&API_Key=EnterKeyHere>

* **Method:**

  The API supports the following

  `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlChildren`

   `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

    `AccessionID=[int] OR Accession=[alpha]`
    - AccessionID: Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one company will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

    - Accession: SEC Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter does not allow a comma separated list.

  `GroupURI=[uri]`  - The extended link role in an XBRL report that is defined by the company. For example: http://www.babc.com/taxonomy/role/StatementOfFinancialPosition		

   **Optional:**

   `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.

    `Linkbase=[Calculation|Definition|Presentation]` - The type of network relationship. This could be a Presentation, Calculation or Definition. If this is not entered then the presentation relationship will be returned.

    `AccessionID=[int]` - Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one company will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

    `Accession=[alpha]` - Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter does not allow a comma separated list.

    `NetworkLink=[String]` - The relationship type that links two elements together. For example summation-item in the calculation linkbase or dimension-default in the definition linkbase.


   **Minimum:**

   All calls to the API must include the `Element` parameter name and at least an `AccessionID` or an `Accession` number. In addition the extended link role must be reported.


* **Data Params**

    The API supports the same params as the URL.

* **Success Response (Normal):**

```xml
    <dataRequest date="2015-10-06T19:34:20-0400">
      <fact>
        <entity>
          <![CDATA[ INTERNATIONAL BUSINESS MACHINES CORP ]]>
        </entity>
        <accessionID>146420</accessionID>
        <filingAccession>0000051143-15-000005</filingAccession>
        <filingDate>2015-07-28</filingDate>
        <elementName>EarningsPerShareDilutedAbstract</elementName>
        <namespace>http://fasb.org/us-gaap/2014-01-31</namespace>
        <treeDepth>2</treeDepth>
        <treeSequence>25</treeSequence>
        <order>1</order>
        <calculationWeight/>
        <calculationEffectiveWeight/>
        <leafNode>1</leafNode>
        <networkName>
          000010 - Statement - CONSOLIDATED STATEMENT OF EARNINGS
        </networkName>
        <preferredLabel>http://www.xbrl.org/2003/role/terseLabel</preferredLabel>
        <networkID>21030812</networkID>
        <networkType>presentationLink</networkType>
        <networkLink>parent-child</networkLink>
        <groupURI>
          http://www.ibm.com/role/StatementCONSOLIDATEDSTATEMENTOFEARNINGS
        </groupURI>
        </fact>
      <count>1</count>
    </dataRequest>
```
    `dataRequest - date` - The data request date attribute is the date that the data was generated. It is not the date of the query.  Data is cached once it is requested and is returned from cache if available. The data remains in cache for a day from the request. This means that data could be up to a day old if it has been previously requested.

    `calculationEffectiveWeight` - This is the weight relationship between the element in the request and the element returned in this record. This differs from the calculationWeight which is the weight to the parent element in the calculation tree. Whereas as the calculationEffectiveWeight is the weight relative to the requested element. They will often be the same but will vary as the tree depth increases.

    `leafNode` - This indicates if the element is a leaf on the tree, or a branch. If the value is 0 the element is the last node on the tree (It has no children). If the value is 1 then the element is a branch element that will have children elements.




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
    An error is provided if a filing number or CIK is not provided.

```xml
    <error>
      <date>Tue, 06 Oct 2015 19:43:06</date>
      <status>Error - Insufficient Parameters</status>
      <message>
        <![CDATA[
          'This call returns too much data. Please revise the attributes to include at least a network id or accession. Number.
        ]]>
      </message>
    </error>
```



* **Notes:**

  Any parameters defined that are not in the list above will result in an error.
