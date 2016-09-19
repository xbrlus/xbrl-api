---
title: xbrlParts REST API
keywords: api
summary: "This API allows the user to get all the calculation parts comprising an element across all networks in the filing."
sidebar: api_sidebar
permalink: xbrlParts.html
folder: api
---
The API requires the element name and the filing number. The API will return all calculation children of the specified element plus attributes such as weight, the effective weight, the leaf node, balance type and associated network.

### **URL**

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlParts&AccessionID=135173&Element=ProfitLoss&API_Key=EnterKeyHere>

### **Method:**

  The API supports the following

  `GET` | `POST`

### **URL Params**

   **Required:**

  `TASK=xbrlParts`

  `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

  `AccessionID=[int] OR Accession=[alpha]` - AccessionID: Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one company will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

  - Accession: SEC Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter allows a comma separated list.

  `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.


   **Optional:**

  `AccessionID=[int]` - Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one company will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

  `Accession=[alpha]` - Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter allows a comma separated list.


   **Minimum:**

   All calls to the API must include the `Element` parameter name and at least an `AccessionID` or an `Accession` number. In addition the extended link role should not be used. To get the calculation children of an element in a network use the API xbrlChildren. xbrlParts is only for calculation relationships and gives a comprehensive relationship tree across all linkbases in the filing.


### **Data Params**

    The API supports the same params as the URL.

### **Success Response (Normal):**

```xml
    <dataRequest date="2015-10-06T19:34:20-0400">
      <fact>
        <entity>
        <![CDATA[ EXXON MOBIL CORP ]]>
        </entity>
        <accessionID>157992</accessionID>
        <filingAccession>0000034088-16-000065</filingAccession>
        <filingDate>2016-02-24</filingDate>
        <elementName>AssetsCurrent</elementName>
        <namespace>http://fasb.org/us-gaap/2015-01-31</namespace>
        <abstract>f</abstract>
        <balance>Debit</balance>
        <periodType>Instant</periodType>
        <monetary>true</monetary>
        <parentElementName>Assets</parentElementName>
        <parentNamespace>http://fasb.org/us-gaap/2015-01-31</parentNamespace>
        <treeDepth>1</treeDepth>
        <treeSequence>1</treeSequence>
        <calculationWeight>1</calculationWeight>
        <calculationEffectiveWeight>1</calculationEffectiveWeight>
        <leafNode>1</leafNode>
        <rootNode>1</rootNode>
        <networkName>000200 - Statement - Consolidated Balance Sheet</networkName>
        <groupURI>
        http://www.exxonmobil.com/role/StatementConsolidatedBalanceSheet
        </groupURI>
    </dataRequest>
```
  `dataRequest - date` - The data request date attribute is the date that the data was generated. It is not the date of the query.  Data is cached once it is requested and is returned from cache if available. The data remains in cache for a day from the request. This means that data could be up to a day old if it has been previously requested.

  `calculationEffectiveWeight` - This is the weight relationship between the element in the request and the element returned in this record. This differs from the calculationWeight which is the weight to the parent element in the calculation tree. Whereas as the calculationEffectiveWeight is the weight relative to the requested element. They will often be the same but will vary as the tree depth increases.

  `leafNode` - This indicates if the element is a leaf on the tree, or a branch. If the value is 0 the element is the last node on the tree (It has no children). If the value is 1 then the element is a branch element that will have children elements.

  `rootNode` - This indicates if the element is a root of the tree, or a branch. If the value is 0 the element is the first node on the tree (The element requested). If the value is 1 then the element is a branch element that will have a parent elements.




### **Error Response:**

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



### **Notes:**

  Any parameters defined that are not in the list above will result in an error.
  
### **XBRL Database:**

  The API calls the XBRL database using a recursive query. An example of the query is shown below. If you take a copy of the XBRL database or use the public database you can build the same API in your system using this query. Replace the $ variables with the appropriate parameters.

  Example query

  ```sql
  WITH RECURSIVE rels(
      relationship_id
      , network_id
      , from_element_id
      , to_element_id
      , tree_sequence
      , tree_depth
      , accession_id
      , extended_link_qname_id
      , extended_link_role_uri_id
      , description
      , weight
      , calculation_weight)
      AS (
      WITH ar AS
      (SELECT
        relationship_id
        , n.network_id
        , from_element_id
        , to_element_id
        , tree_sequence
        , tree_depth
        , n.accession_id
        , n.extended_link_qname_id
        , n.extended_link_role_uri_id
        , n.description
        , calculation_weight
        , calculation_weight
      FROM relationship
      JOIN network n
        ON n.network_id = relationship.network_id
      WHERE n.accession_id in ($AccessionValues)
      AND n.extended_link_qname_id = (SELECT qname_id FROM qname WHERE local_name = 'calculationLink')
      )
      SELECT
      ar.*
      FROM ar
      JOIN accession_element ae
        ON ar.accession_id = ae.accession_id AND ar.from_element_id = ae.element_id
      JOIN element e_from
        ON e_from.element_id = ae.element_id
      JOIN qname q_from
        ON q_from.qname_id = e_from.qname_id  
      WHERE  
        ae.accession_id in ($AccessionValues)  
        AND q_from.local_name = '$ElementName'
      UNION
      SELECT
        r.relationship_id
        , r.network_id
        , r.from_element_id
        , r.to_element_id
        , r.tree_sequence
        , r.tree_depth
        , n.accession_id
        , n.extended_link_qname_id
        , n.extended_link_role_uri_id
        , n.description
        , r.calculation_weight * rels.weight AS weight
        , r.calculation_weight
      FROM  rels
      JOIN relationship r
        ON r.from_element_id = rels.to_element_id
      JOIN network n
        ON r.network_id = n.network_id AND rels.accession_id = n.accession_id AND n.extended_link_qname_id = rels.extended_link_qname_id
      JOIN accession_element ae
        ON n.accession_id = ae.accession_id AND r.from_element_id = ae.element_id
      )
      SELECT
        local_name_from
        , namespace_from
        , local_name
        , namespace
        , entity_name
        , filing_date
        , accession_id
        , filing_accession_number
        , calculation_weight
        , calculation_effective_weight
        , child_balance
        , child_period_type
        , child_is_abstract
        , child_is_monetary
        , parent_balance
        , parent_period_type
        , parent_is_abstract
        , parent_is_monetary
        , MAX (CASE WHEN local_name_from = ANY (child) THEN 1 ELSE 0 END) AS root_node_flag
        , MAX (CASE WHEN local_name = ANY (parent) THEN 1 ELSE 0 END) AS leaf_node_flag
        , string_agg(tree_depth::text,', ')  AS tree_depth
        , string_agg(tree_sequence::text,', ') AS tree_sequence
        , string_agg(uri,', ') AS group_uri
        , string_agg(description,', ') AS description
      FROM
          (SELECT
            qfrm.local_name as local_name_from
            , qfrm.namespace as namespace_from
            , qto.local_name
            , qto.namespace
            , ac.entity_name
            , ac.filing_date
            , ac.accession_id
            , filing_accession_number
            , rl.calculation_weight
            , rl.weight as calculation_effective_weight
            , CASE
                  WHEN elto.balance_id = 1 THEN 'Debit'::text
                  WHEN elto.balance_id = 2 THEN 'Credit'::text
                  ELSE NULL::text
                END AS child_balance
            , CASE
                  WHEN elto.period_type_id = 1 THEN 'Instant'::text
                  WHEN elto.period_type_id = 2 THEN 'Duration'::text
                  WHEN elto.period_type_id = 3 THEN 'Forever'::text
                  ELSE NULL::text
                END AS child_period_type
            , elto.abstract as child_is_abstract
            , CASE
                  WHEN elto.is_monetary = 't' THEN 'true'::text
                  WHEN elto.is_monetary = 'f' THEN 'false'::text
                  ELSE NULL::text
                END as child_is_monetary
            , CASE
                  WHEN elfrom.balance_id = 1 THEN 'Debit'::text
                  WHEN elfrom.balance_id = 2 THEN 'Credit'::text
                  ELSE NULL::text
                END AS parent_balance
            , CASE
                  WHEN elfrom.period_type_id = 1 THEN 'Instant'::text
                  WHEN elfrom.period_type_id = 2 THEN 'Duration'::text
                  WHEN elfrom.period_type_id = 3 THEN 'Forever'::text
                  ELSE NULL::text
                END AS parent_period_type
            , elfrom.abstract as parent_is_abstract
            , CASE
                  WHEN elfrom.is_monetary = 't' THEN 'true'::text
                  WHEN elfrom.is_monetary = 'f' THEN 'false'::text
                  ELSE NULL::text
                END as parent_is_monetary
            , tree_depth
            , tree_sequence
            , elruri.uri
            , rl.description
            , array_agg(qto.local_name) OVER (Partition BY ac.accession_id) as child
            , array_agg(qfrm.local_name) OVER (Partition BY ac.accession_id) as parent
          FROM rels rl
            JOIN element elfrom
              ON elfrom.element_id = rl.from_element_id
            JOIN qname qfrm
              ON qfrm.qname_id = elfrom.qname_id
            JOIN element elto
              ON elto.element_id = rl.to_element_id
            JOIN qname qto
              ON qto.qname_id = elto.qname_id
            JOIN accession ac
              ON ac.accession_id = rl.accession_id
            JOIN uri elruri
              ON rl.extended_link_role_uri_id = elruri.uri_id
            ORDER BY description, tree_sequence
            )  AS all_links
      GROUP by 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18
      ORDER BY
          accession_id
          , root_node_flag
          , min(description)
          , min(tree_sequence)
          , min(tree_depth)

  ```
