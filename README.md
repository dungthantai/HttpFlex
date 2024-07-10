# HttpFlex - Java HTTP Client


## Introduce - *Giới thiệu*

|English|Tiếng Việt|
|-|-|
|HttpFlex is a Java library that makes sending and receiving HTTP requests simpler and easier. This library supports many HTTP methods and allows easy configuration of headers, request body, and proxy. | *HttpFlex là một thư viện Java giúp việc gửi và nhận các yêu cầu HTTP trở nên đơn giản và dễ dàng hơn. Thư viện này hỗ trợ nhiều phương thức HTTP và cho phép cấu hình* |

## Setting - *Cài đặt*

|English|Tiếng Việt|
|-|-|
|To use HttpFlex in your project, you need to add this library to your dependencies or directly copy it into your package. | *Để sử dụng HttpFlex trong dự án của bạn, bạn cần thêm thư viện này vào dependencies hoặc trực tiếp copy vào package.* |



## Use - *Sử dụng*

### Initialize HttpFlex - *Khởi tạo HttpFlex*

|English|Tiếng Việt|
|-|-|
|You can initialize an `HttpFlex` object with a URL or URI as follows: | *Bạn có thể khởi tạo một đối tượng `HttpFlex` với URL hoặc URI như sau:* |

```java
HttpFlex httpFlex = new HttpFlex("https://example.com");
HttpFlex httpFlex = new HttpFlex(URI.create("https://example.com"));
``` 

```java
HttpFlex httpFlex = HttpFlex.instance("https://example.com");
HttpFlex httpFlex = HttpFlex.instance(URI.create("https://example.com"));
``` 


### Send GET request - *Gửi yêu cầu GET*

|English|Tiếng Việt|
|-|-|
|To send a GET request, you can use the `get()` method:<br />In the case of converting the returned result to MyObject, the program will automatically use Gson to convert json String into Object. | *Để gửi một yêu cầu GET, bạn có thể sử dụng phương thức `get()`:<br />Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để convert json String thành Object* |

```java
String response = httpFlex.get();
InputStream is = httpFlex.get(InputStream.class);
byte[] bytes = httpFlex.get(byte[].class);
MyObject responseObject = httpFlex.get(MyObject.class);
```


### Send POST request - *Gửi yêu cầu POST*

|English|Tiếng Việt|
|-|-|
|With the data sent, the program supports the following Types<br />InputStream Path byte[] String (Primitive)<br />Object (Automatically converted to json String using Gson)<br />Multipart, UrlEncoded (Located in the library)<br /><br />To send a POST request with a request body, you can use the `post()` method:<br />In the case of converting the returned result to MyObject, the program will automatically use Gson to convert json String into Object|Với dữ liệu gửi đi, chương trình hỗ trợ các Type sau<br />InputStream Path byte[] String (Nguyên thủy)<br />Object (Tự động convert thành json String bằng Gson)<br />Multipart, UrlEncoded (Nằm trong thư viện)*<br /><br />*Để gửi một yêu cầu POST với thân yêu cầu, bạn có thể sử dụng phương thức `post()`:<br />Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để convert json String thành Object|


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
myRequestBody = null;
```


```java
String response = httpFlex.post(myRequestBody);
InputStream is = httpFlex.post(myRequestBody, InputStream.class);
byte[] bytes = httpFlex.post(myRequestBody, byte[].class);
MyObject responseObject = httpFlex.post(myRequestBody, MyObject.class);
```

### Multipart processing - *Xử lý đa phần (Multipart)*

|English|Tiếng Việt|
|-|-|
|HttpFlex supports sending requests with multipart content:|*HttpFlex hỗ trợ gửi yêu cầu với nội dung dạng multipart:*|

```java
HttpFlex.Multipart multipart = HttpFlex.Multipart.instance().put("field1", "value1").put("file1", new FileInputStream("path/to/file1")).put("file2", Paths.get("path/to/file2"));
String response = httpFlex.post(multipart);
```

### Url encoding - *Xử lý mã hóa Url (application/x-www-form-urlencoded)*

|English|Tiếng Việt|
|-|-|
|HttpFlex supports sending requests with urlencoded content:|*HttpFlex hỗ trợ gửi yêu cầu với nội dung dạng urlencoded:*|

```java
HttpFlex.UrlEncoded urlEncoded = HttpFlex.UrlEncoded.instance().put("field1", "value1").put("field2", "Value2");
String response = httpFlex.post(urlEncoded);
```

### Send custom method request - *Gửi yêu cầu tùy chỉnh*

|English|Tiếng Việt|
|-|-|
|Similar to sending POST data, you just need to use method in addition to the name of the type of method you want to send|*Tương tự như việc gửi dữ liệu POST, bạn chỉ cần sử dụng method thêm vào tên của loại method muốn gửi*|

```java
String response = httpFlex.method("PUT", myRequestBody);
```


### Use Proxy - *Sử dụng Proxy*

```java
httpFlex.proxy("proxy.example.com", 8080);
```

### Login and configure proxy - *Đăng nhập và cấu hình proxy*

```java
httpFlex.proxyAuth("username", "password");
```

### Add HTTP headers - *Thêm tiêu đề HTTP*

|English|Tiếng Việt|
|-|-|
|To enable debug mode for HttpFlex, you can configure as follows:|*Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:*| 

```java
httpFlex.header("Content-Type", "application/json");
httpFlex.header("Authorization", "Bearer my-token");
httpFlex.header("Content-Type", HttpFlex.ContentType.JSON);
httpFlex.header("Content-Type", HttpFlex.ContentType.custom("audio/aac");
```


### Debug mode - *Chế độ Debug*

|English|Tiếng Việt|
|-|-|-|
|To enable debug mode for HttpFlex, you can configure as follows:|*Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:*| 

```java
httpFlex.debug(true);
```

### Debug Mode Default for all queries - *Chế độ Debug Mặc định cho mọi truy vấn*

|English|Tiếng Việt|
|-|-|
|To enable debug mode for HttpFlex, you can configure as follows:|*Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:*|

```java
httpFlex.defaultDebug(true);
```



#### I will write more instructions for some static functions when I have time. You can try using them to download files - *Một số hàm static tôi sẽ viết thêm hướng dẫn khi có thời gian, các bạn có thể thử sử dụng chúng để download file*
