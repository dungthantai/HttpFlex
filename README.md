# HttpFlex - Java HTTP Client

## Giới thiệu

HttpFlex là một thư viện Java giúp việc gửi và nhận các yêu cầu HTTP trở nên đơn giản và dễ dàng hơn. Thư viện này hỗ trợ nhiều phương thức HTTP và cho phép cấu hình dễ dàng các tiêu đề, thân yêu cầu, và proxy.

## Cài đặt

Để sử dụng HttpFlex trong dự án của bạn, bạn cần thêm thư viện này vào dependencies hoặc trực tiếp copy vào package.

## Sử dụng

### Khởi tạo HttpFlex

Bạn có thể khởi tạo một đối tượng `HttpFlex` với URL hoặc URI như sau:

```java
HttpFlex httpFlex = new HttpFlex("https://example.com");
HttpFlex httpFlex = HttpFlex.instance("https://example.com");
```

### Gửi yêu cầu GET

Để gửi một yêu cầu GET, bạn có thể sử dụng phương thức `get()`:
Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để convert json String thành Object

```java
String response = httpFlex.get();
InputStream is = httpFlex.get(InputStream.class);
byte[] bytes = httpFlex.get(byte[].class);
MyObject responseObject = httpFlex.get(MyObject.class);
```

### Gửi yêu cầu POST

Để gửi một yêu cầu POST với thân yêu cầu, bạn có thể sử dụng phương thức `post()`:
Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để convert json String thành Object
Với thông tin gửi đi, chương trình hỗ trợ các Type sau
InputStream Path byte[] String (Nguyên thủy)
Object (Tự động convert thành json String bằng Gson)
Multipart, UrlEncoded

```java
String response = httpFlex.post(myRequestBody);
InputStream is =httpFlex.post(myRequestBody, InputStream.class);
byte[] bytes = httpFlex.post(myRequestBody, byte[].class);
MyObject responseObject = httpFlex.post(myRequestBody, MyObject.class);
```

### Sử dụng Proxy

Bạn có thể cấu hình proxy cho các yêu cầu HTTP như sau:

```java
httpFlex.proxy("proxy.example.com", 8080);
```

### Đăng nhập và cấu hình proxy

```java
httpFlex.proxyAuth("username", "password");
```

### Thêm tiêu đề HTTP

Để thêm tiêu đề cho yêu cầu HTTP, bạn có thể sử dụng phương thức `header()`:

```java
httpFlex.header("Content-Type", "application/json");
httpFlex.header("Authorization", "Bearer my-token");
httpFlex.header("Content-Type", HttpFlex.ContentType.JSON);
httpFlex.header("Content-Type", HttpFlex.ContentType.custom("audio/aac");
```

### Xử lý đa phần (Multipart)

HttpFlex hỗ trợ gửi yêu cầu với nội dung dạng multipart:

```java
HttpFlex.Multipart multipart = HttpFlex.Multipart.instance()
    .put("field1", "value1")
    .put("file1", new FileInputStream("path/to/file1"))
    .put("file2", Paths.get("path/to/file2"));

String response = httpFlex.post(multipart);
```

### Xử lý mã hóa Url (application/x-www-form-urlencoded)

HttpFlex hỗ trợ gửi yêu cầu với nội dung dạng urlencoded:

```java
HttpFlex.UrlEncoded urlEncoded = HttpFlex.UrlEncoded.instance()
    .put("field1", "value1")
    .put("field2", "Value2");

String response = httpFlex.post(urlEncoded);
```

### Chế độ Debug

Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:

```java
httpFlex.debug(true);
```

### Chế độ Debug Mặc định cho mọi truy vấn

Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:

```java
httpFlex.defaultDebug(true);
```
