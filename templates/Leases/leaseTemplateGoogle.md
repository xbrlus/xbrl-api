
Lease Template Example
--
The following is the link to a google doc that uses the xbrlValues api to build a lease worksheet that calculates the adjustments to account for an operating lease in the same manner as a capitalized lease.  The template shows how the lease payments and discount rates can be extracted from XBRL data.

This template uses custom functions to pull the values from the API.  To get a copy of these functions take a copy of the spreadsheet using File>Make a Copy. This will duplicate the spreadsheets with  the custom functions.  These functions allow you to make up to 20,000 calls to the API.  In addition the function caches the results to conserve the number of calls made. The cache is flushed after 6 hours.


* Lease Template ([Google doc](https://docs.google.com/a/xbrl.us/spreadsheets/d/1JA_Gx_Wu0FwNdKatRg-8Ru3gyW36eOr3o7OuUv_QQR4/edit?usp=sharing))


Google Sheets - Custom functions
--
These functions allow the user to access the API without the need to use the XMLIMPORT function in Google docs which is limited and requires a knowledge of XPATH.  The following functions are included in the sheet.

 **xbrlValues**

This function is used to get xbrl fact values. To use the function you need to pass a number of parameters. The function supports four parameters. Each of these is defined below:

*url*

The url of the data you want.  This is defined in the api and maybe something like the following:

`http://csuite.xbrl.us/php/dispatch.php?Task=xbrlValues&Element=OperatingLeasesFutureMinimumPaymentsDueCurrent&Period=Y&Year=2014&CIK=0000732717&Ultimus=true&NoYears=1&DimReqd=false&API_Key=EnterKeyHere`

This will return the value of operating lease payments in the next year for 2014 year for a specific company.

*returnProperty*

This is the data that you want to actually put in the cell. This could be the amount, the elementName, the units, decimals etc.  All the allowable values are defined in the API documentation. The allowable values are as follows:

* entity
* entityCode
* accessionID
* filingAccession
* elementName
* namespace
* extensionflag
* axis
* member
* units
* amount
* decimals
* fact
* period
* year
* filingDate
* aligned
* factID
* axisLocalName
* memberLocalName
* dimensionCount
* url

*arrayPosition*
The values returned by this function may be many and could populate many cells. To limit the number of records this parametr allows you to limit it to the first record, the last record or all records. If left blank the function defaults to `All`. The allowable values are as follows:
* First
* last
* All

When the records are returned tha latest value reported will always be last. To get the latest value this parameter can be set to `last`.

*dimensionCount*
This parameter allows you to limit the records returned to those records that have a matching dimension count. This value takes an integer value. SO if you want those values that have 0 dimensions or are defined as the default value you would enter 0.

 **xbrlCIKLookup**

 This function allows you to lookup a CIK number by providing a ticker symbol. The function has two parameters which are defined below:

 *url*

 The url of the data you want.  This is defined in the api and maybe something like the following:

 `http://csuite.xbrl.us/php/dispatch.php?Task=xbrlCIKLookup&Ticker=aapl`

 This will return the CIK for Apple.

 *returnProperty*

 This is the data that you want to actually put in the cell. This could be the CIK, the name of the company or the sic code.  All the allowable values are defined in the API documentation. The allowable values are as follows:

 * cik
 * ticker
 * sic

 **xbrlSchema**

 This function is used to get xbrl schema values from the USGAAP taxonomy. To use the function you need to pass a number of parameters. The function supports two parameters. Each of these is defined below:

 *url*

 The url of the data you want.  This is defined in the api and maybe something like the following:

 `http://csuite.xbrl.us/php/dispatch.php?Task=xbrlBaseElement&Element=Assets&Namespace=http://fasb.org/us-gaap/2015-01-31&API_Key=EnterKeyHere`

 *returnProperty*

 This is the data that you want to actually put in the cell. This could be details about the element.  All the allowable values are defined in the API documentation. The allowable values are as follows:

 * elementName
 * namespace
 * abstract
 * type
 * substitutionGroup
 * id
 * periodType
 * balance
 * nillable
 * standard
 * documentation
