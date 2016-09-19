---
title: xbrlTaxChildren REST API
keywords: api
summary: "This API allows the user to fetch the relationships in a base taxonomy by passing the extended link role (GroupURI), an element name and the namespace of a given taxonomy."
sidebar: api_sidebar
permalink: xbrlTaxChildren.html
folder: api
---
The API will return all children of the specified element plus attributes such as weight, order and preferred labels. It will return multiple results. The API also allows the user to specify the different linkbases and relationship types associated with a report or network. For example a user can request the calculation children of Assets in the balance sheet defined in the base taxonomy.

* **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlTaxChildren&Taxonomy=http://fasb.org/us-gaap/2015-01-31&Element=InterestExpenseBorrowings&GroupURI=http://fasb.org/us-gaap/role/statement/StatementOfIncome&Linkbase=Calculation&ResetCache=False&API_Key=EnterKeyHere>

* **Method:**

  The API supports the following

   `GET` | `POST`

*  **URL Params**

   **Required:**

   `TASK=xbrlTaxChildren`

   `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

   `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.

   `Taxonomy=[uri]` - The namespace of the taxonomy the element is in. The parameter allows you to get details from specific taxonomies.

   `GroupURI=[uri]`  - The extended link role defined in the taxonomy url referenced in the taxonomy parameter For example http://fasb.org/us-gaap/role/statement/StatementOfIncome		

   **Optional:**

   `Linkbase=[Calculation|Definition|Presentation]` - The type of network relationship. This could be a Presentation, Calculation or Definition. If this is not entered then the relationship type found first will be returned.

   `ResetCache=[boolean]` - If set to True the query will pull the data from the database and will not use a cached file if it is available. Setting the parameter to False will utilize cache and will be faster.



   **Minimum:**

   All calls to the API must include the `Element` parameter name and at least an `AccessionID` or an `Accession` number. In addition the extended link role must be reported.


* **Data Params**

    The API supports the same params as the URL.

* **Success Response (Normal):**

```xml
    <dataRequest date="2016-06-15T00:04:58-0400">
      <fact>
        <elementName>InterestExpenseBorrowings</elementName>
        <namespace>http://fasb.org/us-gaap/2015-01-31</namespace>
        <treeDepth>0</treeDepth>
        <treeSequence>0</treeSequence>
        <order>0</order>
        <calculationWeight/>
        <calculationEffectiveWeight/>
        <leafNode>1</leafNode>
        <networkName>
        124000 - Statement - Statement of Income (Including Gross Margin)
        </networkName>
        <preferredLabel/>
        <networkType>calculationLink</networkType>
        <networkLink/>
        <groupURI>
        http://fasb.org/us-gaap/role/statement/StatementOfIncome
        </groupURI>
      </fact>
      <fact>
        <elementName>InterestExpenseShortTermBorrowings</elementName>
        <namespace>http://fasb.org/us-gaap/2015-01-31</namespace>
        <treeDepth>1</treeDepth>
        <treeSequence>10</treeSequence>
        <order>10</order>
        <calculationWeight>1</calculationWeight>
        <calculationEffectiveWeight>1</calculationEffectiveWeight>
        <leafNode>1</leafNode>
        <networkName>
        124000 - Statement - Statement of Income (Including Gross Margin)
        </networkName>
        <preferredLabel/>
        <networkType>calculationLink</networkType>
        <networkLink>summation-item</networkLink>
        <groupURI>
        http://fasb.org/us-gaap/role/statement/StatementOfIncome
        </groupURI>
      </fact>
      <count>2</count>
    </dataRequest>
```
   `dataRequest - date` - The data request date attribute is the date that the data was generated. It is not the date of the query.  Data is cached once it is requested and is returned from cache if available. The data remains in cache for a day from the request. This means that data could be up to a day old if it has been previously requested.

   `treeDepth` - This is depth of the element in the tree relative to the element name requested. For example children of the element selected will have a value of 1. Grandchildren will have a value of 2.

   `treeSequence` - This is a derived sequence which allows a user to order all the elements in a sequence that matches that defined in the taxonomy. The number has no meaning itself. Its meaning is relative to the other nodes in a tree. If the nodes are sorted by this number the entire tree will be shown in the same sequence as that shown in the taxonomy.

   `calculationWeight` - This is the weight value for the relationship between two elements defined in the taxonomy.

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
        The parameter of with with a value of 2 is not valid.
        ]]>
      </message>
    </error>
```

* **Notes:**

  Any parameters defined that are not in the list above will result in an error.
