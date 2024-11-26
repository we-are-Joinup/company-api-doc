# 2. Authentication & Authorization

> To authorization, use this code when we are creating an user:


```shell
curl "api_endpoint_here" \
  -H "Authorization: JWT beep-beep-beep-beep-beep"
```

```python
import requests

headers = {
    'Authorization': 'JWT beep-beep-beep-beep-beep',
}

response = requests.get('http://api_endpoint_here', headers=headers)
```

```java
import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;

class Main {

	public static void main(String[] args) throws IOException {
		URL url = new URL("api_endpoint_here");
		HttpURLConnection httpConn = (HttpURLConnection) url.openConnection();
		httpConn.setRequestMethod("GET");

		httpConn.setRequestProperty("Authorization", "JWT beep-beep-beep-beep-beep");

		InputStream responseStream = httpConn.getResponseCode() / 100 == 2
				? httpConn.getInputStream()
				: httpConn.getErrorStream();
		Scanner s = new Scanner(responseStream).useDelimiter("\\A");
		String response = s.hasNext() ? s.next() : "";
		System.out.println(response);
	}
}
```

> Make sure to replace `beep-beep-beep-beep-beep` with your private token.

Joinup API expects for the token to be included in all API requests to the server in a header that looks like the following:

`Authorization: beep-beep-beep-beep-beep`

<aside class="notice">
You must replace <code>beep-beep-beep-beep-beep</code> with your token.
</aside>
