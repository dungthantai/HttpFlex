# HttpFlex - Java HTTP Client

## Introduce

HttpFlex is a Java library that makes sending and receiving HTTP requests simpler and easier. This library supports many HTTP methods and allows easy configuration of headers, request body, and proxy.

## Setting

To use HttpFlex in your project, you need to add this library to your dependencies or directly copy it into your package.

## Use

### Initialize HttpFlex

You can initialize an `HttpFlex` object with a URL or URI as follows:

```java
HttpFlex httpFlex = new HttpFlex("https://example.com");
HttpFlex httpFlex = new HttpFlex(URI.create("https://example.com"));
``` 

```java
HttpFlex httpFlex = HttpFlex.instance("https://example.com");
HttpFlex httpFlex = HttpFlex.instance(URI.create("https://example.com"));
``` 

### Send GET request

To send a GET request, you can use the `get()` method:
In the case of converting the returned result to MyObject, the program will automatically use Gson to convert json String into Object.

```java
String response = httpFlex.get();
InputStream is = httpFlex.get(InputStream.class);
byte[] bytes = httpFlex.get(byte[].class);
MyObject responseObject = httpFlex.get(MyObject.class);
```

### Send POST request

With the data sent, the program supports the following Types:
InputStream, Path, byte[], String (Primitive), Object (Automatically converted to json String using Gson), Multipart, UrlEncoded (Located in the library).

To send a POST request with a request body, you can use the `post()` method:
In the case of converting the returned result to MyObject, the program will automatically use Gson to convert json String into Object.

```java
InputStream myRequestBody = Files.newInputStream("path/to/file");
```

```java
Path myRequestBody = Paths.get("path/to/file");
```

```java
byte[] myRequestBody = Files.readAllBytes(Paths.get("path/to/file"));
```

```java
String myRequestBody = "dataIsSomeString";
```

```java
MyObject myRequestBody = new MyObject();
```

```java
String response = httpFlex.post(myRequestBody);
InputStream is = httpFlex.post(myRequestBody, InputStream.class);
byte[] bytes = httpFlex.post(myRequestBody, byte[].class);
MyObject responseObject = httpFlex.post(myRequestBody, MyObject.class);
```

### Multipart processing

HttpFlex supports sending requests with multipart content:

```java
HttpFlex.Multipart multipart = HttpFlex.Multipart.instance()
.put("field1", "value1")
.put("file1", new FileInputStream("path/to/file1"))
.put("file2", Paths.get("path/to/file2"));
String response = httpFlex.post(multipart);
```

### Url encoding

HttpFlex supports sending requests with urlencoded content:

```java
HttpFlex.UrlEncoded urlEncoded = HttpFlex.UrlEncoded.instance()
.put("field1", "value1")
.put("field2", "Value2");
String response = httpFlex.post(urlEncoded);
```

### Send custom method request

Similar to sending POST data, you just need to use method in addition to the name of the type of method you want to send.

```java
String response = httpFlex.method("PUT", myRequestBody);
```

### Use Proxy

```java
httpFlex.proxy("proxy.example.com", 8080);
```

### Login and configure proxy

```java
httpFlex.proxyAuth("username", "password");
```

### Add HTTP headers

To enable debug mode for HttpFlex, you can configure as follows:

```java
httpFlex.header("Content-Type", "application/json");
httpFlex.header("Authorization", "Bearer my-token");
httpFlex.header("Content-Type", HttpFlex.ContentType.JSON);
httpFlex.header("Content-Type", HttpFlex.ContentType.custom("audio/aac"));
```

### Debug mode

To enable debug mode for HttpFlex, you can configure as follows:

```java
httpFlex.debug(true);
```

### Debug Mode Default for all queries

To enable debug mode for HttpFlex, you can configure as follows:

```java
httpFlex.defaultDebug(true);
```

#### I will write more instructions for some static functions when I have time. You can try using them to download files.
