# HttpFlex - Java HTTP Client

## Introduce - *Giới thiệu*

HttpFlex is a Java library that makes sending and receiving HTTP requests simpler and easier. This library supports many HTTP methods and allows easy configuration of headers, request body, and proxy.
*HttpFlex là một thư viện Java giúp việc gửi và nhận các yêu cầu HTTP trở nên đơn giản và dễ dàng hơn. Thư viện này hỗ trợ nhiều phương thức HTTP và cho phép cấu hình dễ dàng các tiêu đề, thân yêu cầu, và proxy.*

## Setting - *Cài đặt*

To use HttpFlex in your project, you need to add this library to your dependencies or directly copy it into your package.
*Để sử dụng HttpFlex trong dự án của bạn, bạn cần thêm thư viện này vào dependencies hoặc trực tiếp copy vào package.*

## Use - *Sử dụng*

### Initialize HttpFlex - *Khởi tạo HttpFlex*

You can initialize an `HttpFlex` object with a URL or URI as follows:
*Bạn có thể khởi tạo một đối tượng `HttpFlex` với URL hoặc URI như sau:*

```java
HttpFlex httpFlex = new HttpFlex("https://example.com");
HttpFlex httpFlex = HttpFlex.instance("https://example.com");
```

### Send GET request - *Gửi yêu cầu GET*

To send a GET request, you can use the `get()` method:
In the case of converting the returned result to MyObject, the program will automatically use Gson to convert json String into Object.
*Để gửi một yêu cầu GET, bạn có thể sử dụng phương thức `get()`:
Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để convert json String thành Object*

```java
String response = httpFlex.get();
InputStream is = httpFlex.get(InputStream.class);
byte[] bytes = httpFlex.get(byte[].class);
MyObject responseObject = httpFlex.get(MyObject.class);
```

### Send POST request - *Gửi yêu cầu POST*

To send a POST request with a request body, you can use the `post()` method:
In the case of converting the returned result to MyObject, the program will automatically use Gson to convert json String into Object.
With the information sent, the program supports the following Types
InputStream Path byte[] String (Primitive)
Object (Automatically converted to json String using Gson)
Multipart, UrlEncoded (Located in the library)
*Để gửi một yêu cầu POST với thân yêu cầu, bạn có thể sử dụng phương thức `post()`:
Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để convert json String thành Object
Với thông tin gửi đi, chương trình hỗ trợ các Type sau
InputStream Path byte[] String (Nguyên thủy)
Object (Tự động convert thành json String bằng Gson)
Multipart, UrlEncoded (Nằm trong thư viện)*

```java
String response = httpFlex.post(myRequestBody);
InputStream is =httpFlex.post(myRequestBody, InputStream.class);
byte[] bytes = httpFlex.post(myRequestBody, byte[].class);
MyObject responseObject = httpFlex.post(myRequestBody, MyObject.class);
```

### Use Proxy - *Sử dụng Proxy*

You can configure the proxy for HTTP requests as follows:
*Bạn có thể cấu hình proxy cho các yêu cầu HTTP như sau:*

```java
httpFlex.proxy("proxy.example.com", 8080);
```

### Login and configure proxy - *Đăng nhập và cấu hình proxy*

```java
httpFlex.proxyAuth("username", "password");
```

### Add HTTP headers - *Thêm tiêu đề HTTP*

To add headers to HTTP requests, you can use the `header()` method:
*Để thêm tiêu đề cho yêu cầu HTTP, bạn có thể sử dụng phương thức `header()`:*

```java
httpFlex.header("Content-Type", "application/json");
httpFlex.header("Authorization", "Bearer my-token");
httpFlex.header("Content-Type", HttpFlex.ContentType.JSON);
httpFlex.header("Content-Type", HttpFlex.ContentType.custom("audio/aac");
```

### Multipart processing (Multipart) - *Xử lý đa phần (Multipart)*

HttpFlex supports sending requests with multipart content:
*HttpFlex hỗ trợ gửi yêu cầu với nội dung dạng multipart:*

```java
HttpFlex.Multipart multipart = HttpFlex.Multipart.instance()
    .put("field1", "value1")
    .put("file1", new FileInputStream("path/to/file1"))
    .put("file2", Paths.get("path/to/file2"));

String response = httpFlex.post(multipart);
```

### Handle Url encoding (application/x-www-form-urlencoded) - *Xử lý mã hóa Url (application/x-www-form-urlencoded)*

HttpFlex supports sending requests with urlencoded content:
*HttpFlex hỗ trợ gửi yêu cầu với nội dung dạng urlencoded:*

```java
HttpFlex.UrlEncoded urlEncoded = HttpFlex.UrlEncoded.instance()
    .put("field1", "value1")
    .put("field2", "Value2");

String response = httpFlex.post(urlEncoded);
```

### Debug mode - *Chế độ Debug*

To enable debug mode for HttpFlex, you can configure as follows:
*Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:*

```java
httpFlex.debug(true);
```

### Debug Mode Default for all queries - *Chế độ Debug Mặc định cho mọi truy vấn*

To enable debug mode for HttpFlex, you can configure as follows:
*Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:*

```java
httpFlex.defaultDebug(true);
```
