# Well Ops Public API Documentation
Welcome to the Well Ops public API documentation.

<!--TODO: What can it be used for?-->

The base of the URL for this API is https://wellopsdev.azurewebsites.net. The URI for any HTTP request sent 
to the API should be this address followed by the path for a specific endpoint.

Use the links below to get started using the API.
* For an introduction to using the API and the documentation, view the [Quick Start](#quick-start) portion 
  of this documentation.

* For a list of all endpoints, visit the [API Overview](#overview).

* For information on authentication and API keys, read the [Authentication](#authentication) portion of 
  this documentation.
  
* For information on how to interpret JSON response bodies, read [JSON Data Object Structure](#json-data-object-structure).

Last updated: 11/03/2023

## Table of Contents
* [Introduction](#well-ops-public-api-documentation)
* [Quick Start](#quick-start)
* [Overview](#overview)
* [Versioning](#versioning)
* [Authentication](#authentication)
* [JSON Data Object Structure](#json-data-object-structure)
* [Lookup Values](#lookup-values)
* [Endpoints](#endpoints)

## Quick Start
In this section, we will cover all the basics you need to get started using the Well Ops public API.
First, read about how to generate and use an API key. Then cover how to find the values you need to
make your HTTP request. Finally, we'll show an example call to the API and provide links to further 
documentation.

---

### Generate or Retrieve an API Key
If you have not used the Well Ops public API before, you may need to generate an API key. If you have, you
will need to retrieve it. 

For now, please contact Mi4 Support at support@mi4.com to receive an API key.

<!--TODO: describe getting api key, log in, navigate to key, etc.-->

<!--If you already have an API key, you can copy it here. If you do not already have an API key, select 'Generate
API Key' and one will be generated for you. Once your API key appears, you can copy it.-->

Find more information about API key generation and retrieval here: [Authentication](#authentication).

---
### Build Your HTTP Request
Once you have an API key, you can begin constructing your HTTP request. 

First, you must determine what action you wish to take. A full list of all endpoints can be found at the
[API Overview](#overview).

Once you have decided on an endpoint, find the values you will need for your request. Start by visiting 
your endpoint's portion of this documentation. Either look for your endpoint in [Endpoints](#endpoints) or 
use the [API Overview](#overview) to link you to the correct section. Once there, locate the following:

1. Request Method and Path
    * Always required.
    * May include route or query paramters, explained below.
    * The root URI for the API is **wellopsdev.azurewebsites.net**
        * The URI you should use in your request is the root URI followed by the path specified for the endpoint
        you wish to hit.
2. Route and Query Parameters
    * These parameters are required for some endpoints but not needed for others. 
    * More information about accepted parameter values can be found at [Lookup Values](#lookup-values)
    or by using the [Lookups Endpoints](#lookups).
3. Body
    * Some endpoints require a body, some do not accept requests with a body, and some have an optional body.
    * If your request will include a body, ensure it is in the format specified by the endpoint's documentation.
4. Headers
    * All endpoints require the request to have an authentication header, usually the X-Api-Key header.
        * This header's value should be the API key from the first portion of this quick start guide.
        * If you are unable to set custom HTTP headers, read [Using an API Key](#using-an-api-key) for other options. 
        * For more information about API keys, visit the [Authentication](#authentication) portion of this
        documentation.
    * Check that your endpoint does not require any other headers.

With all of these values, we can now craft and send an HTTP request and receive a response. Visit the section
of this documentation covering your endpoint for information about server responses.

---

### Example
Let's consider an example. For this quick start example, we will retrieve a list of companies we have access
to through the public API. We do this by using the [Get Companies](#get-companies) endpoint. 

Using the [Get Companies](#get-companies) endpoint documentation, we can quickly determine our needed values.

1. Request Method and Path
    * GET
    * /Company
    * URI: **wellopsdev.azurewebsites.net/Company**
2. Route and Query Parameters
    * No parameters
3. Body
    * No body
4. Headers
    * X-Api-Key
        * We'll use the following sample key: Mi4-TN7puOjkqVLcUxn4k98VPEoC62kXKo4Bj7IILL
    * No other headers

Using these values, we construct our HTTP request:

> GET&emsp;&emsp;wellopsdev.azurewebsites.net/Company  
> X-Api-Key: "Mi4-TN7puOjkqVLcUxn4k98VPEoC62kXKo4Bj7IILL"


The response from this request is a status code of 200 and a JSON list of companies we have access to, as shown
below:   
<!--TODO: Update returned values-->

> 200&emsp;&emsp; OK                                     
[   
            &emsp;{   
            &emsp;&emsp;"companyID": 123,   
            &emsp;&emsp;"companyName": "Example Drilling Co.",   
            &emsp;&emsp;"role": "ApiReadUsers"      
            &emsp;},    
            &emsp;{   
            &emsp;&emsp;"companyID": 321,   
            &emsp;&emsp;"companyName": "Notreal Drilling",   
            &emsp;&emsp;"role": "ApiFullAccessUsers"      
            &emsp;}                                                 
 ]

Where to go from here:

* For more information about the endpoint used in this example, read [Get Companies](#get-companies).

* For a list of all endpoints, visit the [Overview](#overview) portion of this documentation.

* For information on authentication and API keys, read the [Authentication](#authentication) portion of 
  this documentation.

* [Return to Table of Contents](#table-of-contents)

---

## Overview
The following is a list of all endpoints. Click each endpoint to find more information about it.

### Companies
[**Get Companies**](#get-companies) -
Returns all companies the user has access to.

### Fields
[**Get Fields**](#get-fields) - 
Returns all fields from the specified company that the user has access to. 

### Wells
[**Get Wells**](#get-wells) - 
Returns all wells from the specified company that the user has access to.

[**Get Well Daily Production**](#get-well-daily-production) - 
Retrieves all well daily production data the user has access to. Use optional parameters to filter by field, well, 
or date.

### Lookups
[**Get Well Status Options**](#get-well-status-options) - 
Returns all valid well status values.

Where to go from here:

* For help getting started sending HTTP requests, read the [Quick Start](#quick-start) section.

* For an overview of API keys and authentication, visit the [Authentication](#authentication) portion of this documentation.

* For information on how to interpret JSON response bodies, read [JSON Data Object Structure](#json-data-object-structure).

* [Return to Table of Contents](#table-of-contents)
---

## Versioning
The current version of the Well Ops Public API is version 1. 

When requests are sent to the API without any version information, it is assumed the request means to access the 
most current version. 

In order to use an older, not current version of the API, include the version number in your HTTP requests. This can be
done in two main ways, through the query string or through the X-Version header.

### Query String Parameter
One way to specify the API version you intend to use is to include the version as a query string parameter. When making
your request, include a **version** parameter in the query string.

For example, take the HTTP call shown in the quick start [Example](#example) portion of this guide. This is a call to 
the [Get Wells](#get-wells) endpoint made with the following URI:

&emsp;&emsp; **wellopsdev.azurewebsites.net/Company/\{companyID}/Well?fieldID=\{fieldID}&date=\{date}**

If I wanted to make the same call but to a specific version of the API, I would simply add a version parameter:

&emsp;&emsp; **wellopsdev.azurewebsites.net/Company/\{companyID}/Well?fieldID=\{fieldID}&date=\{date}&version=\{versionNumber}**

### X-Api-Version Header
Another way to specify the version is to provide the x-api-version header on your request.

For this method, simply provide the version as the value for the x-api-version header on your HTTP request.

Where to go from here:

* For help getting started sending HTTP requests, read the [Quick Start](#quick-start) section.

* [Return to Table of Contents](#table-of-contents)
---

## Authentication
API keys are the authentication and authorization scheme used for the Well Ops public API. When a user
wants to use the public API, they first must generate or retrieve an API key using the web portal. Then they can 
make calls to the public API with their API key value in the X-Api-Key header for the request. This key will be 
used to authenticate the user making the request and then to authorize any action taken as a result of the 
endpoint being called. 

In the sections below, learn more about API key generation and use.

---

### API Key Generation
For now, please contact Mi4 Support at support@mi4.com to receive an API key.

<!--Once you have confirmed you are logged in to the Well Ops portal TODO: Portal?, do the following to generate
or retrieve an API key. TODO: edit navigation/generation

1. From the Well Ops portal, navigate to the API Keys page.
    * Click on the admin link in the menu on the left hand side of the screen
    * Then click API Keys
2. Generate an API key. Skip this step if you have already generated one.
    * On the API Keys page, click 'Generate API Key'
    * If you have already generated an API key, the generate button will not appear and you can move to the 
    next step
3. Copy the API key.
    * Once your API key has been generated, you can copy it from the API Keys page

The API key you have generated and copied can now be used to access the public API. -->

**Note:** This API key will give any
request made with it the same permissions as your account. Be sure to treat this key with the 
same level of security as your username and password. 

---

### Using an API Key
After generating and retrieving an API key, it can be used to access the Well Ops public API. There are two ways
to use your API key: by providing the API key as the value for a X-Api-Key header or by using basic authentication
and providing the API key as either the username or password. In this section, we will detail both methods.

---

**X-Api-Key Header**   
The easiest way to use the API key is by including a X-Api-Key header on any HTTP requests to the API. For the 
value of the header, provide your API key. 

For example, if our API key is **Mi4-TN7puOjkqVLcUxn4k98VPEoC62kXKo4Bj7IILL**, our HTTP request should have a X-Api-Key
header value as follows:   
&emsp;&emsp;**X-Api-Key: 'Mi4-TN7puOjkqVLcUxn4k98VPEoC62kXKo4Bj7IILL'**

---

**Authentication Header**   
Though the X-Api-Key header is very straightforward, you may not be able to include it if you are using a tool 
that does not allow you to add custom headers. In this case, you can use basic authentication with the Authorization
header to submit your API key.

When using the Authorization header, some changes must be made to your API key before it can be submitted with your 
request.
1. Start by creating a credentials token
    1. For cases with a username and password, the token starts with a string as follows:   
&emsp;&emsp;**'username:password'** 
    2. Since we are submitting just one value, the API key will take the place of the username and the password will
    be left blank:   
&emsp;&emsp;**'apiKey:'**
    3. Then, the string is encoded with Base64. The result is the credentials token.
2. Next, the keyword 'Basic ' is prepended to the string:    
&emsp;&emsp;**'Basic \<credentials token\>'**
2. Finally, The whole string can be submitted as the value for the Authorization header   
&emsp;&emsp;**Authorization: 'Basic \<credentials token\>'**

For example, suppose our API key is **Mi4-TN7puOjkqVLcUxn4k98VPEoC62kXKo4Bj7IILL**. To use it in the Authorization header
we would follow the steps:
1. Create credentials token   
    1. Construct the string    
&emsp;&emsp;**'Mi4-TN7puOjkqVLcUxn4k98VPEoC62kXKo4Bj7IILL:'**
    2. Encode with Base64   
&emsp;&emsp;**'TWk0LVRON3B1T2prcVZMY1V4bjRrOThWUEVvQzYya1hLbzRCajdJSUxMOg=='**
2. Prepend the Basic keyword   
&emsp;&emsp;**'Basic TWk0LVRON3B1T2prcVZMY1V4bjRrOThWUEVvQzYya1hLbzRCajdJSUxMOg=='**
3. Use as the value for the Authorization header   
&emsp;&emsp;**Authorization: 'Basic TWk0LVRON3B1T2prcVZMY1V4bjRrOThWUEVvQzYya1hLbzRCajdJSUxMOg=='**

---

**API Key Processing**   
When you make a request, the API first checks for a X-Api-Key header. If your request does not have one, then the 
API will look at the Authentication header and try to retrieve your API key. 

Once your API key has been retrieved, it will be used to authenticate your identity. This is similar to using a
username and password to log in to the web portal. Keep in mind that the account used to generate the API key 
is the identity that will be recognized.

Once authenticated, your identity will be used to authorize access to certain companies and reports. 

Where to go from here:

* For a list of all endpoints, visit the [Overview](#overview) portion of this documentation.

* For help getting started sending HTTP requests, read the [Quick Start](#quick-start) section.

* [Return to Table of Contents](#table-of-contents)
---

## JSON Data Object Structure 
In the API, JSON is used to transmit data in the bodies of requests and responses. 

When using the API, a user may need to submit data in the body of their HTTP request. To be understood by the API,
this data must be a JSON object with the expected attributes or keys. A user also needs to understand any JSON 
objects they may receive in the body of a HTTP response. 

In this portion of the documentation, we cover the expected JSON structure of data objects within the API. 

**Requests**    
Before submitting a request with a JSON object in the body, be sure to read the documentation for the endpoint you 
are calling. This way, you will ensure your object is properly formatted and contains only attributes that the endpoint
is expecting. 

**Responses**  
Some endpoints return JSON objects in the body of the reponse. Read the endpoint's documentation and the following
documentation on different object types for help understnading your response.

<!--TODO: Overall view?-->

&emsp;[Return to Table of Contents](#table-of-contents)   

---

### Well
The well object consists of the fields that record all of the information pertaining to a well. This includes the
wellID, the fieldID, latitude and longitude, and more.

Some of the information presented in the well object may change over time. For example, the wellStatus value may change
from active to shut-in. For this reason, the well object also has effectiveFromDate and effectiveToDate attributes. These
attributes describe the period of time for which the information given in the well object is correct. 

<!--TODO: Example?-->

**Fields/Attributes:**
* wellID - ID of the well.
* wellName - Name of the well.
* fieldID - ID of the field that the well belongs to.
* fieldName - Name of the field.
* wellStatus - Representation of the status of the well. Find out more at [Lookup-Values](#lookup-values).
* apiNumber - API number of the well.
* latitude - Latitude of the well.
* longitude - longitude of the well.
* leaseNumber - TODO
* countyOrParish - The county or parish the well is located in.
* state - The state the well is located in.
* district - The district the well is located in.
* effectiveFromDate and effectiveToDate - Respresent the period of time for which the other attributes 
correcty described the well.

**JSON:**                                               
 &emsp;&emsp;{                                                 
 &emsp;&emsp;&emsp;"wellID": 46,                               
 &emsp;&emsp;&emsp;"wellName": "Well 3 #46",                   
 &emsp;&emsp;&emsp;"fieldID": 1,                               
 &emsp;&emsp;&emsp;"fieldName": "TX 3, 1",                     
 &emsp;&emsp;&emsp;"wellStatus": 1,                            
 &emsp;&emsp;&emsp;"apiNumber": "42-355-06002",                
 &emsp;&emsp;&emsp;"latitude": null,                           
 &emsp;&emsp;&emsp;"longitude": null,                          
 &emsp;&emsp;&emsp;"leaseNumber": "13485",                     
 &emsp;&emsp;&emsp;"countyOrParish": "Nueces",                 
 &emsp;&emsp;&emsp;"state": "TX",                              
 &emsp;&emsp;&emsp;"district": "04",                           
 &emsp;&emsp;&emsp;"effectiveFromDate": null,                  
 &emsp;&emsp;&emsp;"effectiveToDate": null                     
 &emsp;&emsp;} 

&emsp;[Return to Table of Contents](#table-of-contents)   
<!--&emsp;[Return to Overall Object Structure](#json-data-object-structure)-->

---
### Well Daily Production

<!--TODO: Example?-->

**Fields/Attributes:**

**JSON:**            

&emsp;[Return to Table of Contents](#table-of-contents)   
<!--&emsp;[Return to Overall Object Structure](#json-data-object-structure)-->

---

## Lookup Values
This section will cover lookup values. Some values used in the Well Ops platform are given ID values that make
them easier to store. For example, the possible well status values all have an accompanying wellStatusID.

A user may need to look up the options for a particular attribute and their corresponding IDs in order to submit a 
request to the API. A user may also need to decipher the IDs returned to them from a request. This section of 
the Well Ops API documentation lists and details the attributes and options where IDs are used to represent longer
values.

### Well Statuses
At any point in time, each well can be described by a well status. These statuses include values such as active, 
shut-in, etc. Each of these statuses is represented by a wellStatusID.

A full list of possible well statuses and their wellStatusIDs can be retrieved by using the 
[**Get Well Status Options**](#get-well-status-options) endpoint. 

A call to this endpoint returns a list of well statuses, each with an ID, name, shortName and sortOrder.

Where to go from here:

* For help getting started sending HTTP requests, read the [Quick Start](#quick-start) section.

* For an overview of API keys and authentication, visit the [Authentication](#authentication) portion of this documentation.

* For a list of all endpoints, visit the [Overview](#overview) portion of this documentation.

* [Return to Table of Contents](#table-of-contents)
---

## Endpoints
### Company
#### Get Companies
Returns all companies the user has access to.

**Method and Path** - GET /Company

**URL** - **wellopsdev.azurewebsites.net/Company**

**Route Parameters** - None

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**

* 200: Ok
    * Body: JSON array of companies
        * Each object in the array represents a company
        * Each company has:
            * companyID - ID of the company
            * companyName - Name of the company
            * role - role or access level for the user
    * Example response body:   
        [   
            &emsp;{   
            &emsp;&emsp;"companyID": 123,   
            &emsp;&emsp;"companyName": "Example Drilling Co.",   
            &emsp;&emsp;"role": "ApiReadUsers"      
            &emsp;},    
            &emsp;{   
            &emsp;&emsp;"companyID": 321,   
            &emsp;&emsp;"companyName": "Notreal Drilling",   
            &emsp;&emsp;"role": "ApiFullAccessUsers"      
            &emsp;}    
        ] 

* 400: Bad Request - Missing/invalid values
    * Failed to retrieve participant company access list.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.
    
&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
### Field
#### Get Fields
Returns all fields from the specified company that the user has access to. 

**Method and Path** - GET /Company/{companyID}/Field

**URL** - **wellopsdev.azurewebsites.net/Company/{companyID}/Field**

**Route Parameters** - 
* *companyID* - ID of the company you want to retrieve wells for
    * Use [Get Companies](#get-companies) to retrieve a list of companies you have access to via the public API

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**

* 200: Ok
    * Body: JSON array of fields
        * Each object in the array represents a field
        * Each company has:
            * fieldID - ID of the field
            * fieldName - Name of the field
    * Example response body:   
        [   
            &emsp;{   
            &emsp;&emsp;"fieldID": 123,   
            &emsp;&emsp;"fieldName": "Example Field"        
            &emsp;},    
            &emsp;{   
            &emsp;&emsp;"fieldID": 321,   
            &emsp;&emsp;"fieldName": "Another Example Field"          
            &emsp;}    
        ] 

* 400: Bad Request - Missing/invalid values
    * Failed to retrieve field list.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---

### Well
#### Get Wells
Returns all wells from the specified company that the user has access to. Can retrieve wells for the whole company or
a single, specified field. If a date is provided, will retrieve data for that date. Otherwise, will retrieve data for
the current date.

**Method and Path** - GET /Company/{companyID}/Well?fieldID={fieldID}&date={date}

**URL** - **wellopsdev.azurewebsites.net/Company/{companyID}/Well?fieldID={fieldID}&date={date}**

**Route Parameters** - 
* *companyID* - ID of the company you want to retrieve wells for

**Query Parameters** -
* *fieldID* - ID of the field you want to retrieve wells for.
    * Optional
    * If not provided, will retrieve all wells for the given company 
* *date* - Date you want to retrieve wells for.
    * Will retrieve all wells and well values for the given date
    * Optional
    * If not provided, will retrieve wells and values for the current date

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**

* 200: Ok
    * Body: JSON array of wells
        * Each object in the array represents a well
        * Read [Well](#well) for more information about JSON formatted wells.

* 400: Bad Request - Missing/invalid values
    * Failed to retrieve well list.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
#### Get Well Daily Production
Retrieves all well daily production data the user has access to.

Use optional parameters to filter by field, well, or date.

**Method and Path** - GET /Company/{companyID}/WellDailyProduction?fieldID={fieldID}&wellID={wellID}&
startDate={startDate}&endDate={endDate}

**URL** - **wellopsdev.azurewebsites.net/Company/{companyID}/WellDailyProduction?fieldID={fieldID}&wellID={wellID}&
startDate={startDate}&endDate={endDate}**

**Route Parameters** - 
* *companyID* - ID of the company you want to retrieve well daily production for.

**Query Parameters** -
* *fieldID* - ID of the field you want to retrieve well daily production for.
    * Optional
    * If not provided, will retrieve well daily production for all fields
* *wellID* - ID of the well you want to retrieve well daily production for.
    * Optional
    * If not provided, will retrieve all well daily production for all wells
* *startDate* and *endDate* - Range of dates you want to retrieve well daily production for.
    * Optional
    * If neither provided, will retrieve all well daily production 
    * If only start date provided, will retrieve all well daily production from after provided start date
    * If only end date provided, will retrieve all well daily production from before provided end date

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**

* 200: Ok
    * Body: JSON array of well daily production objcts
 <!--   TODO-->
        * Each object in the array represents the daily production for a well
        * Read [Well Daily Production](#well-daily-production) for more information.

* 400: Bad Request - Missing/invalid values
    * Failed to retrieve well list.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
### Lookups
#### Get Well Status Options
Returns all valid well status values.

**Method and Path** - GET /Company/{companyID}/WellStatus

**URL** - **wellopsdev.azurewebsites.net/Company/{companyID}/WellStatus**

**Route Parameters** - 
* *companyID* - ID of the company you want to retrieve possible well statuses for

**Query Parameters** - None

**Body** - None

**Headers**   
* **X-Api-Key**    
    * Include **X-Api-Key** header with your API key as the value.  
    * This header is used to authenticate and authorize your request.
    * For information on generating, retrieving, and using an API key, read the [Authentication](#authentication)
    portion of this documentation.

**Responses**

* 200: Ok
    * Body: List of possible well status values, each with an ID and a name.
        * Find more information at [Well Statuses](#well-statuses)
    * Example response body:
 
&emsp;[                                                           
&emsp;&emsp;{                                                     
&emsp;&emsp;&emsp;"id": 1,                     
&emsp;&emsp;&emsp;"name": "Active",
&emsp;&emsp;&emsp;"shortName": "ACT.",                               
&emsp;&emsp;&emsp;"sortOrder": 1                               
&emsp;&emsp;},                                            
&emsp;&emsp;{                                                                      
&emsp;&emsp;&emsp;"id": 2,                     
&emsp;&emsp;&emsp;"name": "Shut-In",
&emsp;&emsp;&emsp;"shortName": "S.I.",                               
&emsp;&emsp;&emsp;"sortOrder": 2                                         
&emsp;&emsp;},                                                
&emsp;&emsp;{                                                                          
&emsp;&emsp;&emsp;"id": 3,                     
&emsp;&emsp;&emsp;"name": "Plugged and Abandoned",
&emsp;&emsp;&emsp;"shortName": "P&A",                               
&emsp;&emsp;&emsp;"sortOrder": 3                                         
&emsp;&emsp;}                                                     
&emsp;]    


* 400: Bad Request - Missing/invalid values
    * Failed to retrieve well status options.

* 401: Unauthorized - Missing/invalid API key
    * API key is missing, not a valid value, or associated with an account that does not have access to any
    active companies.

&emsp;[Return to Table of Contents](#table-of-contents)   
&emsp;[Return to Overview of Endpoints](#overview)

---
Last updated: 11/03/2023
