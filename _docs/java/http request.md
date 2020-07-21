---
order: 17
title: (JAVA) http request
category: Java
---

```
import java.net.http.*; >> must
import java.io.IOException; 
import java.net.URI; >> must
import java.util.ArrayList;
  
public String get_html_body(String url) throws IOException, InterruptedException {
		HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
	.uri(URI.create(url))
	.build();

HttpResponse<String> response = client.send(request,
	HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
	
return response.body();
}

```