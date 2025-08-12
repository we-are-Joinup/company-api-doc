# 4. Cost centers

## 4.1 List Cost centers

### 4.1.1 HTTP Request

`GET https://api.joinupbackend/api/company/cost-centers/`

This endpoint lists cost centers in a paginated format.

This endpoint can be called 1 time per second.

### 4.1.2 Case Company Group

```shell
curl "https://localhost:8000/api/company/cost-centers/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json"
```

```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
    'Content-Type': 'application/json',
}

response = requests.get('https://localhost:8000/api/company/cost-centers/', headers=headers)
```

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://localhost:8000/api/company/cost-centers/"))
    .GET()
    .setHeader("Authorization", "JWT beep-beep-beep-beep-beep")
    .setHeader("Content-Type", "application/json")
    .build();

HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
```

> The above command returns JSON structured like this:

```json
{
    "count": 25,
    "next": "https://api.joinupbackend/api/company/cost-centers/?page=3",
    "previous": "https://api.joinupbackend/api/company/cost-centers/",
    "results": [
        {
            "id": 116220,
            "name": "Test",
            "company_cif": "AXXYYZZUU",
            "company_name": "Test company"
        },
        ...
    ]
}
```

<aside class="notice">
Use this section if Joinup system has configured a Company group for your mobility platform
</aside>

#### 4.1.2.1 Query Parameters

Parameter   |  Type       | Required    | Description
----------- | ----------- | ---------   | ------------
page_size   |  Integer    |  No         | Default: 10. The number of cost centers returned per page. Maximun value: 100
page        |  Integer    |  No         | Default: 1. The page number to retrieve
ordering    |  String     |  No         | Default id. Specifies the sorting order of the returned results, by one or more fields. Possible values: id, name, company_name, company_cif (prefix with - for descending order)
id          |  Integer    |  No         | Filters the results by the specified cost center ID
name        |  String     |  No         | Filters cost centers by their name. Accepts true or false
company_name | String     | No          | Filters cost centers whose company name contains the specified value. Only if your company group does not share the cost centers.
company_cif  | String     | No          | Filters cost centers whose company CIF contains the specified value. Only if your company group does not share the cost centers.


#### 4.1.2.2 Attributes response


Attribute        | Type    | Description
---------------- | ------- | ------------
id               | Integer | Unique identifier of the cost-centers
name             | String  | Name of the cost center


<aside class="notice">
  company_name and company_cif are not returned cost centers are shared by all companies.
</aside>

### 4.1.3 Case Single Company

```shell
curl "https://localhost:8000/api/company/cost-centers/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json"
```

```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
    'Content-Type': 'application/json',
}

response = requests.get('https://localhost:8000/api/company/cost-centers/', headers=headers)
```

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://localhost:8000/api/company/cost-centers/"))
    .GET()
    .setHeader("Authorization", "JWT beep-beep-beep-beep-beep")
    .setHeader("Content-Type", "application/json")
    .build();

HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
```


> The above command returns JSON structured like this:

```json
{
    "count": 25,
    "next": "https://api.joinupbackend/api/company/cost-centers/?page=3",
    "previous": "https://api.joinupbackend/api/company/cost-centers/",
    "results": [
        {
            "id": 116220,
            "name": "Test",
        },
        ...
    ]
}
```

<aside class="notice">
Use this section if Joinup system has configured a single company for your mobility platform
</aside>

#### 4.1.3.1 Query Parameters

Parameter   |  Type       | Required    | Description
----------- | ----------- | ---------   | ------------
page_size   |  Integer    |  No         | Default: 10. The number of cost centers returned per page. Maximun value: 100
page        |  Integer    |  No         | Default: 1. The page number to retrieve
ordering    |  String     |  No         | Default id. Specifies the sorting order of the returned results, by one or more fields. Possible values: id and name (prefix with - for descending order)
id          |  Integer    |  No         | Filters the results by the specified cost center ID
name        |  String     |  No         | Filters cost centers by their name. Accepts true or false

#### 4.1.3.2 Attributes response


Attribute        | Type    | Description
---------------- | ------- | ------------
id               | Integer | Unique identifier of the cost center
name             | String  | Name of the cost center

### 4.1.4 Status codes

Status Code | Meaning
---------- | -------
200 | OK. The results are returned
400 | Bad Request indicates that the server would not process the request due to something the server considered to be a client error. The errors are indicated in the response.
401 | Unauthorized indicates the client must authenticate to access the resource.
403 | Forbidden means the client is authenticated but does not have permission to access the resource.
429 | Too Many Requests indicates the client has sent another request in less than 1 second ago.

## 4.2 Manage Cost centers

### 4.2.1 HTTP Request

`POST https://api.joinupbackend/api/company/cost-centers/`

This endpoint creates, updates or deletes cost centers. 

This endpoint supports a maximum of 50 cost centers.

This endpoint can be called 1 time per minute.

This endpoint (in production environment) can send a report with the result. It is possible add a customer email. This report can be accessed via API.

### 4.2.2 Configuration Company Group

```shell
curl "https://api.joinupbackend/api/company/cost-centers/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '[
        {
          "name": "Test",
          "operation": "onboarding",
          "company_name": "Company 1",
          "flexible": true,
          ...
        },
        {
          "name": "Test 2",
          "operation": "offboarding",
          "company_name": "Company 1",
          ...
        },
        {
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
        "name": "Test",
        "operation": "onboarding",
        "company_name": "Company 1",
        "flexible": True,
        ...
    },
    {
        "name": "Test 2",
        "operation": "offboarding",
        "company_name": "Company 1",
        ...
    },
    {
        "name": "Test 3",
        "operation": "updated",
        "company_name": "New company",
        "flexible": True,
        ...
    },
    ...
  ]

response = requests.post(
  'https://api.joinupbackend/api/company/cost-centers/',
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
        String url = "https://api.joinupbackend/api/company/cost-centers/";
        String token = "JWT beep-beep-beep-beep-beep";
        List<Map<String, Object>> data = List.of(
            Map.of(
                "name", "Test",
                "operation", "onboarding",
                "company_name", "Company 1",
                "flexible", true,
                ...
            ),
            Map.of(
                "name", "Test 2",
                "operation", "offboarding",
                "company_name", "Company 1",
                ...
            ),
            Map.of(
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
      "request_id": "689af497d0d3c748923fcfc3"
    }
```

<aside class="notice">
Use this section if Joinup system has configured a Company group for your mobility platform
</aside>

Attribute |  Required | Description
--------- | ----------- | ----------
operation |  Yes | It can be onboarding (to create), offboarding (to delete) or updated (to update).
flexible | No. Default is false | Used when operation is onboarding or offboarding. It works like a create or update
name | Yes | Cost center. Used to search for an cost center when operation is updated or offboarding. This field can not be updated (via API)
company_name | No | Name of company. If there is not any company with this name our system will create a company with this name belonging to your Company Group
company_cif | No | Spanish Tax Identification Number (CIF). If there is not any company with this CIF our system will create a company with this CIF belonging to your Company Group


<aside class="notice">
  It is possible to send company_name and company_cif. In this case, firstly will search an existing company for CIF, secondly will search an existing company for name. And if there is not any company, our system will create a company with this name and with this CIF belong to your company group
</aside>

<aside class="notice">
  It is possible not to send company_name and company_cif. Use this case only if all cost centers are shared by all companies
</aside>

### 4.2.3 Configuration Single Company

```shell
curl "https://api.joinupbackend/api/company/cost-centers/" \
  -H "Authorization: JWT beep-beep-beep-beep-beep" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '[
        {
          "name": "Test",
          "operation": "onboarding",
          "flexible": true
        },
        {
          "name": "Test 2",
          "operation": "offboarding"
        },
        {
          "name": "Test 3",
          "operation": "updated",
          "flexible": true
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
        "name": "Test",
        "operation": "onboarding",
        "flexible": True
    },
    {
        "name": "Test 2",
        "operation": "offboarding"
    },
    {
        "name": "Test 3",
        "operation": "updated",
        "flexible": True
    },
    ...
  ]

response = requests.post(
  'https://api.joinupbackend/api/company/cost-centers/',
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
        String url = "https://api.joinupbackend/api/company/cost-centers/";
        String token = "JWT beep-beep-beep-beep-beep";
        List<Map<String, Object>> data = List.of(
            Map.of(
                "name", "Test",
                "operation", "onboarding",
                "flexible", true
            ),
            Map.of(
                "name", "Test 2",
                "operation", "offboarding"
            ),
            Map.of(
                "name", "Test 3",
                "operation", "updated",
                "flexible", true
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
      "message": "Bulk task started!"
    }
```

<aside class="notice">
Use this section if Joinup system has configured a single company for your mobility platform
</aside>

Attribute |  Required | Description
--------- | ----------- | ----------
operation |  Yes | It can be onboarding (to create), offboarding (to delete) or updated (to update).
flexible | No. Default is false | Used when operation is onboarding or offboarding. It works like a create or update
name | Yes | Cost center. Used to search for an cost center when operation is updated or offboarding. This field can not be updated (via API)


### 4.2.4 Status codes

Status Code | Meaning
---------- | -------
202 | Accepted indicates that a request has been accepted for processing, but processing has not been completed or may not have started. The request will be proccess in background.
400 | Bad Request indicates that the server would not process the request due to something the server considered to be a client error. The errors are indicated in the response.
401 | Unauthorized indicates the client must authenticate to access the resource.
403 | Forbidden means the client is authenticated but does not have permission to access the resource.
413 | Content Too Large indicates that the request entity was larger than limits defined by server: 50 cost centers.
429 | Too Many Requests indicates the client has sent another request in less than 1 minute ago.

## 4.3 Get report

```shell
curl "https://api.joinupbackend/api/company/cost-centers/check-request/689af497d0d3c748923fcfc3/" \
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
    'https://api.joinupbackend/api/company/cost-centers/check-request/689af497d0d3c748923fcfc3/',
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
    .uri(URI.create("https://api.joinupbackend/api/company/cost-centers/check-request/689af497d0d3c748923fcfc3/"))
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
    "created": "2025-08-12T08:00:23.519000",
    "id": "689af497d0d3c748923fcfc3"
}
```

> Or when the task is finished:

```json
{
    "status": "finished",
    "created": "2025-08-12T08:00:23.519000",
    "company_created": [
        "NAME_OR_CIF1",
    ],
    "offboarding": {
        "success": [
          "COST_CENTER_10"
        ],
        "error": {
          "COST_CENTER_11": "ERROR MESSAGE"
        }
    },
    "onboarding": {
        "success": [
            "COST_CENTER_12",
            "COST_CENTER_13",
            "COST_CENTER_14",
            "COST_CENTER_15",
        ],
        "error": {}
    },
    "updated": {
        "success": [
          "COST_CENTER_5",
        ],
        "error": {}
    },
    "id": "689af497d0d3c748923fcfc3"
}
```


### 4.3.1 HTTP Request

`GET https://api.joinupbackend/api/company/cost-centers/check-request/<ID>/`

This endpoint retrieves the report created after run manage cost centers. 

This endpoint can be called 1 time per minute.

The id used will be the request_id returned in the request to manage cost centers


Attribute |  Type | Description
--------- | -----  | -----------
status    | String | pending: Request is still being processed, finished: request has been completed
created   | String  (datetime in ISO 8601 format, UTC timezone) | Date when the request was made
id        | String | Identifier of the request
company_created | List[str] | Only for company group administrators. company names (or CIFs) list created in the request
offboarding | Object | Report of offboarding cost centers
onboarding | Object | Report of onboarding cost centers
updated | Object | Report of updated cost centers


### 4.3.2 Status codes

Status Code | Meaning
---------- | -------
200 | OK. The report is returned
401 | Unauthorized indicates the client must authenticate to access the resource.
403 | Forbidden means the client is authenticated but does not have permission to access the resource.
404 | Not Found. There is not any request with this ID
