# HttpFlex - Java HTTP Client

## Giới thiệu

HttpFlex là một thư viện Java giúp việc gửi và nhận các yêu cầu HTTP trở nên đơn giản và dễ dàng hơn. Thư viện này hỗ trợ nhiều phương thức HTTP và cho phép cấu hình dễ dàng các header, thân yêu cầu, và proxy.

## Cài đặt

Để sử dụng HttpFlex trong dự án của bạn, bạn cần thêm thư viện này vào dependencies hoặc trực tiếp sao chép vào package.

## Sử dụng

### Khởi tạo HttpFlex

Bạn có thể khởi tạo một đối tượng `HttpFlex` với URL hoặc URI như sau:

```java
HttpFlex httpFlex = new HttpFlex("https://example.com");
HttpFlex httpFlex = new HttpFlex(URI.create("https://example.com"));
``` 

```java
HttpFlex httpFlex = HttpFlex.instance("https://example.com");
HttpFlex httpFlex = HttpFlex.instance(URI.create("https://example.com"));
``` 

### Gửi yêu cầu GET

Để gửi một yêu cầu GET, bạn có thể sử dụng phương thức `get()`:
Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để chuyển đổi chuỗi json thành đối tượng.

```java
String response = httpFlex.get();
InputStream is = httpFlex.get(InputStream.class);
byte[] bytes = httpFlex.get(byte[].class);
MyObject responseObject = httpFlex.get(MyObject.class);
```

### Gửi yêu cầu POST

Với dữ liệu gửi đi, chương trình hỗ trợ các kiểu sau:
InputStream, Path, byte[], String (Nguyên thủy), Object (Tự động chuyển đổi thành chuỗi json bằng Gson), Multipart, UrlEncoded (Có sẵn trong thư viện).

Để gửi một yêu cầu POST với thân yêu cầu, bạn có thể sử dụng phương thức `post()`:
Với trường hợp chuyển đổi kết quả trả về thành MyObject, chương trình sẽ tự động sử dụng Gson để chuyển đổi chuỗi json thành đối tượng.

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

### Gửi yêu cầu tùy chỉnh

Tương tự như việc gửi dữ liệu POST, bạn chỉ cần sử dụng method thêm vào tên của loại method muốn gửi.

```java
String response = httpFlex.method("PUT", myRequestBody);
```

### Sử dụng Proxy

```java
httpFlex.proxy("proxy.example.com", 8080);
```

### Đăng nhập và cấu hình proxy

```java
httpFlex.proxyAuth("username", "password");
```

### Thêm tiêu đề HTTP

Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:

```java
httpFlex.header("Content-Type", "application/json");
httpFlex.header("Authorization", "Bearer my-token");
httpFlex.header("Content-Type", HttpFlex.ContentType.JSON);
httpFlex.header("Content-Type", HttpFlex.ContentType.custom("audio/aac"));
```

### Chế độ Debug

Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:

```java
httpFlex.debug(true);
```

### Chế độ Debug mặc định cho mọi truy vấn

Để bật chế độ debug cho HttpFlex, bạn có thể cấu hình như sau:

```java
httpFlex.defaultDebug(true);
```

#### Một số hàm static tôi sẽ viết thêm hướng dẫn khi có thời gian, các bạn có thể thử sử dụng chúng để download file.
