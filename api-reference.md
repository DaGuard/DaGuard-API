# API Reference




## API General Info



### Base Url and Message Format
All API requests and responses use application/json content type. Responses	follow HTTP response status codes to indicate
the success and the failure.

#### URL
`http://localhost:8657/api`

#### Message Format
All messages are in json format.



### Message Field Types
Type         | Description
------------ | ------------
Integer      | Integer numbers
Long         | Long numbers
Boolean      | True/False
DoubleString | Decimal numbers are returned as strings to preserve full precision across platforms
Enum         | Enum definition. Passing invalid enum values will result in API_BAD_REQUEST error
String       | Text



### Mandatory Field Indicators
Indicator    | Description
------------ | ----------------------------------------
M            | Mandatory field
(M)          | Mandatory field under certain conditions
O            | Optional field



### Response
Successful http response contains HTTP status code 200 and an optional body. If the response contains the body,
 the fields within the body are documented in each related API sections.  Failed http response contains non 200 HTTP status
code and the body with an errorCode field to indicate the cause of the failures.

#### Error Response Fields
Name         | Type        | Mandatory | Description
------------ | ------------| ----------| -----------------------------------------------------------------------------------------
errorCode    | String      | M         | Error code. e.g.INVALID_PASSWORD
errorData    | String      | O         | Additional information on the user data that may cause the error. Data is provided in json format.



### Pagination
Pagination is supported for all REST calls that return arrays. The newest items are returned by default.

Name	   | Type(value)| Mandatory| Description
-----------| -----------|----------|-------------------
pageNumber | Integer    | O        | Default to 1
pageSize   | Integer    | O	       | Default to 100

Example: GET transfers?pageNumber=1&pageSize=100



### Timestamp
Unless otherwise specified, all timestamps returned from API are milliseconds since UNIX Epoch.





## API Request Headers



### Sending a Request
All API requests must contain the following headers:

* API-KEY
* API-KEY-SECRET
* API-KEY-PASSPHRASE





