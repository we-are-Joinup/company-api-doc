# 3. Employees

## 3.1 HTTP Request

`POST https://api.joinupbackend/api/company/employees/`

This endpoint creates, updates or disables employees. 

This endpoint supports a maximum of 50 employees.

This endpoint can be called 1 time per minute.

This endpoint (in production environment) sends a report with the result. It is possible add a customer email.

## 3.2 Configuration Company Group

```shell
curl "https://api.joinupbackend/api/company/employees/" \
  -H "Authorization: beep-beep-beep-beep-beep" \
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
    'Authorization': 'beep-beep-beep-beep-beep',
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
        String token = "beep-beep-beep-beep-beep";
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
      "message": "Bulk task started!"
    }
```

Use this section if Joinup system has configured a Company group for your mobility platform

Attribute |  Required | Description
--------- | ----------- | ----------
operation |  Yes | It can be onboarding (to create), offboarding (to disable) or updated (to update).
flexible | No. Default is false |Used when operation is onboarding or offboarding. It works like a create or update
base_email | Yes | Employee email. Used to search for an employee when operation is updated or offboarding. This field can not be updated (via API)
name | Yes |Employee Name
company_name | company_name or company_cif are required | Name of company. If there is not any company with this name our system will create a company with this name belonging to your Company Group
company_cif | company_name or company_cif are required | Spanish Tax Identification Number (CIF). If there is not any company with this CIF our system will create a company with this CIF belonging to your Company Group
other fields | No |cost_center, service_reason, management, section etc. There are a lot of employee fields. Please if you need to save more info contact the Joinup team. We will indicate what is the best field for your case.

<aside class="notice">
  It is possible to send company_name and company_cif. In this case, firstly will search an existing company for CIF, secondly will search an existing company for name. And if there is not any company, our system will create a company with this name and with this CIF belong to your company group
</aside>



## 3.3 Configuration Company

```shell
curl "https://api.joinupbackend/api/company/employees/" \
  -H "Authorization: beep-beep-beep-beep-beep" \
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
    'Authorization': 'beep-beep-beep-beep-beep',
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
        String token = "beep-beep-beep-beep-beep";
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
      "message": "Bulk task started!"
    }
```

Use this section if Joinup system has configured a single company for your mobility platform

Attribute |  Required | Description
--------- | ----------- | ----------
operation |  Yes | It can be onboarding (to create), offboarding (to disable) or updated (to update).
flexible | No. Default is false |Used when operation is onboarding or offboarding. It works like a create or update
base_email | Yes | Employee email. Used to search for an employee when operation is updated or offboarding. This field can not be updated (via API)
name | Yes |Employee Name
other fields | No |cost_center, service_reason, management, section etc. There are a lot of employee fields. Please if you need save more info contact with Joinup team. We will indicate what is the best field for your case.


## 3.4 Status codes

Status Code | Meaning
---------- | -------
202 | Accepted indicates that a request has been accepted for processing, but processing has not been completed or may not have started. The request will be proccess in background.
400 | Bad Request indicates that the server would not process the request due to something the server considered to be a client error. The errors are indicated in the response.
413 | Content Too Large indicates that the request entity was larger than limits defined by server: 50 employees.
429 | Too Many Requests indicates the client has sent another request in less than 1 minute ago.