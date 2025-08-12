# 3. Employees

## 3.1 List Employees

### 3.1.1 HTTP Request

`GET https://api.joinupbackend/api/company/employees/`

This endpoint lists employees in a paginated format.

This endpoint can be called 1 time per second.

### 3.1.2 Case Company Group

```shell
curl "https://localhost:8000/api/company/employees/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json"
```

```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
    'Content-Type': 'application/json',
}

response = requests.get('https://localhost:8000/api/company/employees/', headers=headers)
```

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://localhost:8000/api/company/employees/"))
    .GET()
    .setHeader("Authorization", "JWT beep-beep-beep-beep-beep")
    .setHeader("Content-Type", "application/json")
    .build();

HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
```

> The above command returns JSON structured like this:

```json
{
    "count": 4062,
    "next": "https://api.joinupbackend/api/company/employees/?page=4",
    "previous": "https://api.joinupbackend/api/company/employees/?page=2",
    "results": [
        {
            "id": 14518,
            "name": "Test",
            "base_email": "test@example.com",
            "enabled": false,
            "enabled_date": "2020-10-05T08:19:32.312058Z",
            "disabled_date": null,
            "employee_id": "1234",
            "cost_center": "foo",
            "service_reason": "27: bar",
            "dni": "",
            "supervisor_email": "",
            "extra_text_1": "",
            "extra_text_2": "",
            "extra_text_3": "",
            "management": "",
            "section": "",
            "pep_code": "",
            "layer": "",
            "extra_field_1": "",
            "extra_field_2": "",
            "extra_field_3": "",
            "company_cif": "AXXYYZZUU",
            "company_name": "Test company"
        },

    ]
}
```

<aside class="notice">
Use this section if Joinup system has configured a Company group for your mobility platform
</aside>

#### 3.1.2.1 Query Parameters

Parameter   |  Type       | Required    | Description
----------- | ----------- | ---------   | ------------
page_size   |  Integer    |  No         | Default: 10. The number of employees returned per page. Maximun value: 100
page        |  Integer    |  No         | Default: 1. The page number to retrieve
ordering    |  String     |  No         | Default id. Specifies the sorting order of the returned results, by one or more fields. Possible values: id, enabled, enabled_date,  disabled_date, company_name, company_cif (prefix with - for descending order)
id          |  Integer    |  No         | Filters the results by the specified employee ID
enabled     |  Boolean    |  No         | Filters employees by their enabled status. Accepts true or false
enabled_date__gte |  String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees enabled on or after the specified datetime
enabled_date__lt | String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees enabled before the specified datetime
disabled_date__gte |  String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees disabled on or after the specified datetime
enabled_date__lt | String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees disabled before the specified datetime
company_name | String     | No          | Filters employees whose company name contains the specified value
company_cif  | String     | No          | Filters employees whose company CIF contains the specified value

#### 3.1.2.2 Attributes response


Attribute        | Type    | Description
---------------- | ------- | ------------
id               | Integer | Unique identifier of the employee
name             | String  | Full name of the employee
base_email       | String  | Primary email address of the employee
enabled          | Boolean | Boolean indicating if the employee is currently enabled (true or false)
enabled_date     | String  (datetime in ISO 8601 format, UTC timezone) | Date and time when the employee was enabled (ISO 8601 UTC)
disabled_date    | String  (datetime in ISO 8601 format, UTC timezone) | Date and time when the employee was disabled (ISO 8601 UTC)
employee_id      | String  | Internal identification code or number used by the company to identify the employee
cost_center      | String  | Default cost center associated with the employee
service_reason   | String  | Default service reason associated with the employee. Format: <<ID: TEXT>>
dni              | String  | National identification number
supervisor_email | String  | Email address of the employee’s supervisor
extra_text_1     | String  | Default additional text field 1 for custom use
extra_text_2     | String  | Default additional text field 2 for custom use
extra_text_3     | String  | Default additional text field 3 for custom use
management       | String  | Management unit or department to which the employee belongs
section          | String  | Section or subdivision within the management unit
pep_code         | String  | Pep code or officine code
layer            | String  | Organizational layer or level of the employee
extra_field_1    | String  | Additional custom field 1
extra_field_2    | String  | Additional custom field 2
extra_field_3    | String  | Additional custom field 3
company_name     | String  | Name of the company employing the employee
company_cif      | String  | Company tax identification code (CIF)

### 3.1.3 Case Single Company

```shell
curl "https://localhost:8000/api/company/employees/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json"
```

```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
    'Content-Type': 'application/json',
}

response = requests.get('https://localhost:8000/api/company/employees/', headers=headers)
```

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://localhost:8000/api/company/employees/"))
    .GET()
    .setHeader("Authorization", "JWT beep-beep-beep-beep-beep")
    .setHeader("Content-Type", "application/json")
    .build();

HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
```


> The above command returns JSON structured like this:

```json
{
    "count": 4062,
    "next": "https://api.joinupbackend/api/company/employees/?page=4",
    "previous": "https://api.joinupbackend/api/company/employees/?page=2",
    "results": [
        {
            "id": 14518,
            "name": "Test",
            "base_email": "test@example.com",
            "enabled": false,
            "enabled_date": "2020-10-05T08:19:32.312058Z",
            "disabled_date": null,
            "employee_id": "1234",
            "cost_center": "foo",
            "service_reason": "27: bar",
            "dni": "",
            "supervisor_email": "",
            "extra_text_1": "",
            "extra_text_2": "",
            "extra_text_3": "",
            "management": "",
            "section": "",
            "pep_code": "",
            "layer": "",
            "extra_field_1": "",
            "extra_field_2": "",
            "extra_field_3": ""
        },
        ...

    ]
}
```

<aside class="notice">
Use this section if Joinup system has configured a single company for your mobility platform
</aside>

#### 3.1.3.1 Query Parameters

Parameter   |  Type       | Required    | Description
----------- | ----------- | ---------   | ------------
page_size   |  Integer    |  No         | Default: 10. The number of employees returned per page. Maximun value: 100
page        |  Integer    |  No         | Default: 1. The page number to retrieve
ordering    |  String     |  No         | Default id. Specifies the sorting order of the returned results, by one or more fields. Possible values: id, enabled, enabled_date,  disabled_date, company_name, company_cif (prefix with - for descending order)
id          |  Integer    |  No         | Filters the results by the specified employee ID
enabled     |  Boolean    |  No         | Filters employees by their enabled status. Accepts true or false
enabled_date__gte |  String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees enabled on or after the specified datetime
enabled_date__lt | String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees enabled before the specified datetime
disabled_date__gte |  String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees disabled on or after the specified datetime
enabled_date__lt | String  (datetime in ISO 8601 format, UTC timezone) | No | Filters employees disabled before the specified datetime

#### 3.1.3.2 Attributes response


Attribute        | Type    | Description
---------------- | ------- | ------------
id               | Integer | Unique identifier of the employee
name             | String  | Full name of the employee
base_email       | String  | Primary email address of the employee
enabled          | Boolean | Boolean indicating if the employee is currently enabled (true or false)
enabled_date     | String  (datetime in ISO 8601 format, UTC timezone) | Date and time when the employee was enabled (ISO 8601 UTC)
disabled_date    | String  (datetime in ISO 8601 format, UTC timezone) | Date and time when the employee was disabled (ISO 8601 UTC)
employee_id      | String  | Internal identification code or number used by the company to identify the employee
cost_center      | String  | Default cost center associated with the employee
service_reason   | String  | Default service reason associated with the employee. Format: <<ID: TEXT>>
dni              | String  | National identification number
supervisor_email | String  | Email address of the employee’s supervisor
extra_text_1     | String  | Default additional text field 1 for custom use
extra_text_2     | String  | Default additional text field 2 for custom use
extra_text_3     | String  | Default additional text field 3 for custom use
management       | String  | Management unit or department to which the employee belongs
section          | String  | Section or subdivision within the management unit
pep_code         | String  | Pep code or officine code
layer            | String  | Organizational layer or level of the employee
extra_field_1    | String  | Additional custom field 1
extra_field_2    | String  | Additional custom field 2
extra_field_3    | String  | Additional custom field 3


### 3.1.4 Status codes

Status Code | Meaning
---------- | -------
200 | OK. The results are returned
400 | Bad Request indicates that the server would not process the request due to something the server considered to be a client error. The errors are indicated in the response.
401 | Unauthorized indicates the client must authenticate to access the resource.
403 | Forbidden means the client is authenticated but does not have permission to access the resource.
429 | Too Many Requests indicates the client has sent another request in less than 1 second ago.

## 3.2 Manage Employees

### 3.2.1 HTTP Request

`POST https://api.joinupbackend/api/company/employees/`

This endpoint creates, updates or disables employees. 

This endpoint supports a maximum of 50 employees.

This endpoint can be called 1 time per minute.

This endpoint (in production environment) can send a report with the result. It is possible add a customer email. This report can be accessed via API.

### 3.2.2 Case Company Group

```shell
curl "https://api.joinupbackend/api/company/employees/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '[
        {
          "base_email":"test@example.com",
          "name": "Test",
          "operation": "onboarding",
          "company_name": "Company 1",
          "flexible": true,
          ...
        },
        {
          "base_email":"test2@example.com", 
          "name": "Test 2",
          "operation": "offboarding",
          "company_name": "Company 1",
          ...
        },
        {
          "base_email":"test3@example.com", 
          "name": "Test 3",
          "operation": "updated",
          "company_name": "New company",
          "flexible": true,
          ...
        },
        ...
  ]'
```
```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
    'Content-Type': 'application/json',
}

json_data = [
    {
      "base_email":"test@example.com", 
      "name": "Test",
      "operation": "onboarding",
      "company_name": "Company 1",
      "flexible": True,
      ...
    },
    {
      "base_email":"test2@example.com", 
      "name": "Test 2",
      "operation": "offboarding",
      "company_name": "Company 1",
      ...
    },
    {
      "base_email":"test3@example.com", 
      "name": "Test 3",
      "operation": "updated",
      "company_name": "New company",
      "flexible": True,
      ...
    },
    ...
  ]

response = requests.post(
  'https://api.joinupbackend/api/company/employees/',
  headers=headers, json=json_data)
```

```java

import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;
import java.util.List;
import java.util.Map;
import com.fasterxml.jackson.databind.ObjectMapper;

public class Main {
    public static void main(String[] args) throws Exception {
        String url = "https://api.joinupbackend/api/company/employees/";
        String token = "JWT beep-beep-beep-beep-beep";
        List<Map<String, Object>> data = List.of(
            Map.of(
                "base_email", "test@example.com",
                "name", "Test",
                "operation", "onboarding",
                "company_name", "Company 1",
                "flexible", true,
                ...
            ),
            Map.of(
                "base_email", "test2@example.com",
                "name", "Test 2",
                "operation", "offboarding",
                "company_name", "Company 1",
                ...
            ),
            Map.of(
                "base_email", "test3@example.com",
                "name", "Test 3",
                "operation", "updated",
                "company_name", "New company",
                "flexible", true,
                ...
            ),
            ...
        );

        ObjectMapper mapper = new ObjectMapper();
        String requestBody = mapper.writeValueAsString(data);

        HttpClient client = HttpClient.newHttpClient();

        HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create(url))
            .header("Authorization", token)
            .header("Content-Type", "application/json")
            .POST(HttpRequest.BodyPublishers.ofString(requestBody))
            .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
    }
}

```

> The above command returns JSON structured like this:

```json
    {
      "message": "Bulk task started!",
      "request_id": "6899d4573a7e8f5ac4bc3ad3"
    }
```
<aside class="notice">
Use this section if Joinup system has configured a Company group for your mobility platform
</aside>

Attribute |  Required | Description
--------- | ----------- | ----------
operation |  Yes | It can be onboarding (to create), offboarding (to disable) or updated (to update).
flexible | No. Default is false |Used when operation is onboarding or offboarding. It works like a create or update
base_email | Yes | Employee email. Used to search for an employee when operation is updated or offboarding. This field can not be updated (via API)
name | Yes |Employee Name
company_name | company_name or company_cif are required | Name of company. If there is not any company with this name our system will create a company with this name belonging to your Company Group
company_cif | company_name or company_cif are required | Spanish Tax Identification Number (CIF). If there is not any company with this CIF our system will create a company with this CIF belonging to your Company Group
other fields | No | cost_center, service_reason, management, section etc. Employees have various fields available according to each client’s needs. It is not necessary to use all of them. Only the fields strictly required to provide the service should be used. Please if you need to save more info contact the Joinup team. We will indicate what is the best field for your case.

<aside class="notice">
  It is possible to send company_name and company_cif. In this case, firstly will search an existing company for CIF, secondly will search an existing company for name. And if there is not any company, our system will create a company with this name and with this CIF belong to your company group
</aside>



### 3.2.3 Case Single Company

```shell
curl "https://api.joinupbackend/api/company/employees/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '[
        {
          "base_email":"test@example.com",
          "name": "Test",
          "operation": "onboarding",
          "flexible": true,
          ...
        },
        {
          "base_email":"test2@example.com", 
          "name": "Test 2",
          "operation": "offboarding"
        },
        {
          "base_email":"test3@example.com", 
          "name": "Test 3",
          "operation": "updated",
          "flexible": true,
          ...
        },
        ...
  ]'
```
```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
    'Content-Type': 'application/json',
}

json_data = [
    {
      "base_email":"test@example.com", 
      "name": "Test",
      "operation": "onboarding",
      "flexible": True,
      ...
    },
    {
      "base_email":"test2@example.com", 
      "name": "Test 2",
      "operation": "offboarding"
    },
    {
      "base_email":"test3@example.com", 
      "name": "Test 3",
      "operation": "updated",
      "flexible": True,
      ...
    },
    ...
  ]

response = requests.post(
  'https://api.joinupbackend/api/company/employees/',
  headers=headers, json=json_data)
```

```java

import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;
import java.util.List;
import java.util.Map;
import com.fasterxml.jackson.databind.ObjectMapper;

public class Main {
    public static void main(String[] args) throws Exception {
        String url = "https://api.joinupbackend/api/company/employees/";
        String token = "JWT beep-beep-beep-beep-beep";
        List<Map<String, Object>> data = List.of(
            Map.of(
                "base_email", "test@example.com",
                "name", "Test",
                "operation", "onboarding",
                "flexible", true,
                ...
            ),
            Map.of(
                "base_email", "test2@example.com",
                "name", "Test 2",
                "operation", "offboarding"
            ),
            Map.of(
                "base_email", "test3@example.com",
                "name", "Test 3",
                "operation", "updated",
                "flexible", true,
                ...
            ),
            ...
        );

        ObjectMapper mapper = new ObjectMapper();
        String requestBody = mapper.writeValueAsString(data);

        HttpClient client = HttpClient.newHttpClient();

        HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create(url))
            .header("Authorization", token)
            .header("Content-Type", "application/json")
            .POST(HttpRequest.BodyPublishers.ofString(requestBody))
            .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
    }
}

```

> The above command returns JSON structured like this:

```json
    {
      "message": "Bulk task started!",
      "request_id": "6899d4573a7e8f5ac4bc3ad3"
    }
```

<aside class="notice">
Use this section if Joinup system has configured a single company for your mobility platform
</aside>

Attribute |  Required | Description
--------- | ----------- | ----------
operation |  Yes | It can be onboarding (to create), offboarding (to disable) or updated (to update).
flexible | No. Default is false |Used when operation is onboarding or offboarding. It works like a create or update
base_email | Yes | Employee email. Used to search for an employee when operation is updated or offboarding. This field can not be updated (via API)
name | Yes |Employee Name
other fields | No | cost_center, service_reason, management, section etc. Employees have various fields available according to each client’s needs. It is not necessary to use all of them. Only the fields strictly required to provide the service should be used. If you need to save more info, please contact the Joinup team. We will indicate what is the best field for your case.

### 3.2.4 Status codes

Status Code | Meaning
---------- | -------
202 | Accepted indicates that a request has been accepted for processing, but processing has not been completed or may not have started. The request will be proccess in background.
400 | Bad Request indicates that the server would not process the request due to something the server considered to be a client error. The errors are indicated in the response.
401 | Unauthorized indicates the client must authenticate to access the resource.
403 | Forbidden means the client is authenticated but does not have permission to access the resource.
413 | Content Too Large indicates that the request entity was larger than limits defined by server: 50 employees.
429 | Too Many Requests indicates the client has sent another request in less than 1 minute ago.

## 3.3 Get report

```shell
curl "https://api.joinupbackend/api/company/employees/check-request/6899d4573a7e8f5ac4bc3ad3/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json"
```

```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
    'Content-Type': 'application/json',
}

response = requests.get(
    'https://api.joinupbackend/api/company/employees/check-request/6899d4573a7e8f5ac4bc3ad3/',
    headers=headers,
)
```

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.joinupbackend/api/company/employees/check-request/6899d4573a7e8f5ac4bc3ad3/"))
    .GET()
    .setHeader("Authorization", "JWT beep-beep-beep-beep-beep")
    .setHeader("Content-Type", "application/json")
    .build();

HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

```

> The above command returns JSON structured like this:

```json
{
    "status": "pending",
    "created": "2025-08-11T11:30:31.627000",
    "id": "6899d4573a7e8f5ac4bc3ad3"
}
```

> Or when the task is finished:

```json
{
    "status": "finished",
    "created": "2025-08-11T11:30:31.627000",
    "company_created": [
        "NAME_OR_CIF1",
        "NAME_OR_CIF2",
        "NAME_OR_CIF3"
    ],
    "offboarding": {
        "success": [
          "test1@example.com"
        ],
        "error": {
          "test6@example.com": "ERROR MESSAGE"
        }
    },
    "onboarding": {
        "success": [
            "test2@example.com",
            "test3@example.com",
            "test4@example.com",
            "test5@example.com",
        ],
        "error": {}
    },
    "updated": {
        "success": [
          "test6@example.com",
        ],
        "error": {}
    },
    "id": "6899d4573a7e8f5ac4bc3ad3"
}
```


### 3.3.1 HTTP Request

`GET https://api.joinupbackend/api/company/employees/check-request/<ID>/`

This endpoint retrieves the report created after run manage employees. 

This endpoint can be called 1 time per minute.

The id used will be the request_id returned in the request to manage employees


Attribute |  Type | Description
--------- | -----  | -----------
status    | String | pending: Request is still being processed, finished: request has been completed
created   | String  (datetime in ISO 8601 format, UTC timezone) | Date when the request was made
id        | String | Identifier of the request
company_created | List[str] | Only for company group administrators. company names (or CIFs) list created in the request
offboarding | Object | Report of offboarding employees
onboarding | Object | Report of onboarding employees
updated | Object | Report of updated employees


## 3.4 Hook during signup process

<aside class="notice">
To use this hook it is necessary that the client API meets all the requirements
</aside>

Due to internal security policies, it may not be desirable to provide employee information until they actually start using our App. For this purpose, the Joinup API has a hook to get employee info during signup process.

In other words, due to company or group security policies, we might avoid using the “Manage Employees” endpoint with the operation field set to onboarding.

We have an alternative: provide this information at the moment the employee is signed.

Our system will be configured so that when a user registers in the Joinup App, if their email domain matches one of the domains already registered for that company or group, the system will make a request to a client API to retrieve the employee information.


### 3.4.1 Case Company Group:

<aside class="notice">
Use this section if Joinup system has configured a Company group for your mobility platform
</aside>

```shell
curl "https://api.clientbackend/api/company/employees/" \
  -H "Authorization: buzz-buzz-buzz-buzz-buzz" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{"email": "test1@example.com"}'
```

```python
import requests

headers = {
    'Authorization': 'buzz-buzz-buzz-buzz-buzz',
    'Content-Type': 'application/json',
}

json_data = {
    'email': 'test1@example.com',
}

response = requests.post('https://api.clientbackend/api/company/employees/', headers=headers, json=json_data)
```

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpRequest.BodyPublishers;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.clientbackend/api/company/employees/"))
    .POST(BodyPublishers.ofString("{\"email\": \"test1@example.com\"}"))
    .setHeader("Authorization", "buzz-buzz-buzz-buzz-buzz")
    .setHeader("Content-Type", "application/json")
    .build();

HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

```
> The above command returns JSON structured like this:

```json
{
  "name": "FULL NAME",
  "email": "test1@example.com",
  "company_name": "Example 1",
  "company_cif": "AZZYYZZUU",
  "cost_center": "CC1",
  "extra_text_1": "Project",
  ...
}
```
 Definition | Description
---------- | -------------
URL | It is defined by the client
Authentication | This will be done exclusively with the Authorization header. Using a token without refresh. If necessary, it can be changed as many times as necessary throughout the year.
Content Type | application/json
Method | POST
Payload | {"email": "test1@example.com"}
Status code | 400, 401, 403, 404 or 200
Body for 400, 401, 403 and 404 status | {}
Body for 200 status | Complete list of all attributes that the response can contain: name, email, employee_id, cost_center, service_reason, dni, supervisor_email, extra_text_1, extra_text_2, extra_text_3, management, section, pep_code, layer, extra_field_1, extra_field_2, extra_field_3, company_name, company_cif

<aside class="notice">
  It is possible to receive company_name and company_cif. In this case, firstly will search an existing company for CIF, secondly will search an existing company for name. And if there is not any company, our system will create a company with this name and with this CIF belong to your company group
</aside>


### 3.4.2 Case Single Company:

<aside class="notice">
Use this section if Joinup system has configured a single company for your mobility platform
</aside>

```shell
curl "https://api.clientbackend/api/company/employees/" \
  -H "Authorization: buzz-buzz-buzz-buzz-buzz" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{"email": "test1@example.com"}'
```

```python
import requests

headers = {
    'Authorization': 'buzz-buzz-buzz-buzz-buzz',
    'Content-Type': 'application/json',
}

json_data = {
    'email': 'test1@example.com',
}

response = requests.post('https://api.clientbackend/api/company/employees/', headers=headers, json=json_data)
```

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpRequest.BodyPublishers;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.clientbackend/api/company/employees/"))
    .POST(BodyPublishers.ofString("{\"email\": \"test1@example.com\"}"))
    .setHeader("Authorization", "buzz-buzz-buzz-buzz-buzz")
    .setHeader("Content-Type", "application/json")
    .build();

HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

```


> The above command returns JSON structured like this:

```json
{
  "name": "FULL NAME",
  "email": "test1@example.com",
  "cost_center": "CC1",
  "extra_text_1": "Project",
  ...
}
```
 Definition | Description
---------- | -------------
URL | It is defined by the client
Authentication | This will be done exclusively with the Authorization header. Using a token without refresh. If necessary, it can be changed as many times as necessary throughout the year.
Content Type | application/json
Method | POST
Payload | {"email": "test1@example.com"}
Status code | 400, 401, 403, 404, or 200
Body for 401 and 403 status | {}
Body for 200 status | Complete list of all attributes that the response can contain: name, email, employee_id, cost_center, service_reason, dni, supervisor_email, extra_text_1, extra_text_2, extra_text_3, management, section, pep_code, layer, extra_field_1, extra_field_2, extra_field_3

### 3.4.3 Status codes

Status Code | Meaning
---------- | -------
200 | Ok returns the employee information
400 | Bad Request indicates that the server would not process the request due to something the server considered to be a client error. E.g.: Payload without email
401 | Unauthorized indicates the client must authenticate to access the resource.
403 | Forbidden means the client is authenticated but does not have permission to access the resource.
404 | Not Found employee not found
