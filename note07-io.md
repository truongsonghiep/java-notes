# IO VS NIO


# IO
Java cung cấp một bộ các lớp và giao diện trong package **java.io** và **java.nio** để thao tác với các file và thư mục nằm bên ngoài phạm vi chương trình.
## File Và Thư Mục
Lớp `java.io.File` đại diện cho một file hoặc một thư mục. Một số thao tác với lớp File:
```java
// tạo file
File parent = new File("/home/smith");
File child = new File(parent,"data/zoo.txt");

//kiểm tra file có tồn tại không?
file.exists(); //trả về true/false

//
listFiles();//trả về một danh sách các file và thư mục con trực tiếp của nó.
```
## Đọc Và Ghi Dữ Liệu Trong File
Khi một chương trình Java đọc một file, nó không lưu trữ toàn bộ nội dung của file trong bộ nhớ, mà chỉ đọc từng "đoạn" (chunk) dữ liệu một lần. Điều này giúp Java có thể đọc một file lớn khoảng vài GB mà chỉ với bộ nhớ nhỏ.

![image](https://github.com/truongsonghiep/java-notes/assets/57567162/bdf390ae-50ca-4481-b10a-0a81fb2951d9)

Java cung cấp rất nhiều lớp khác nhau để đọc và ghi file, mỗi lớp có một cách tiếp cận khác nhau ví dụ: Đọc/ghi theo byte, Đọc/ghi theo ký tự, Đọc/ghi theo dòng, Đọc/ghi theo nhóm byte.

Thực tế là tuy có những cách tiếp cận khác nhau nhưng bản chất của các lớp vẫn là đọc ghi các byte.

Có thể bạn không nhận ra nhưng chúng ta đã sử dụng các stream io rồi, đó là các hàm System.in, System.err, and System.out

## The FileInputStream and FileOutputStream Classes

##  The ObjectInputStream and ObjectOutputStream Classes

### The FileReader and FileWriter classes
FileReader và FileWriter cùng với các lớp buffer của nó được sử dụng để đọc và ghi dữ liệu văn bản (text). Chúng có các hàm `read()` và `write()` tương ứng để đọc và ghi các giá trị char thay vì byte.


### The BufferedReader and BufferedWriter Classes



## Interacting with Users

# NIO
## Introducing NIO.2
Trong Java file I/O đã trải qua vô số lần biến đổi, ban đầu là các java.io API, nó sử dụng byte stream để tương tác với file data, mặc dù có phát triển trong nhiều năm nhưng cơ bản là vẩn dự trên khái niệm byte stream. Từ Java 4 trở đi java.nio xuất hiện để thay thế java.io truyền thống, nó cung cáp cách tiếp cận hiệu quả hơn là sử dụng buffer thay vì luồng byte điều này giúp io không bị chặn khi thực thi.

### Path
interface `java.nio.file.Path` đại diện cho một đường dẫn đến file hoặc thư mục. Nó giống như lớp `File` mà chúng ta đã biết. Nó tham chiếu đến file hoặc thư mục gốc trong hệ thống lưu trữ. không giống file, path sử dụng một liên kết tượng trưng, liên kết tượng trưng là một con trỏ, khi thao tác với dữ liệu, hệ điều hành sẽ thao tác trực tiếp còn ta là người ra lệnh.

### Creating Instances with Factory and Helper Classes

Lý do Path là một interface thay vì một lớp là vì việc tạo ra một tập tin hoặc thư mục được coi là một nhiệm vụ phụ thuộc vào hệ thống tập tin trong NIO.2. Khi bạn nhận được một đối tượng Path từ hệ thống tệp mặc định trong NIO.2, JVM trả về một đối tượng khác với java.io.File mà xử lý các chi tiết cụ thể của hệ thống cho nền tảng hiện tại một cách trong suốt.

Nếu bạn không sử dụng mẫu nhà máy để tạo một đối tượng Path, bạn sẽ phải biết hệ thống tệp dưới đây là gì và sử dụng điều này trong mỗi phương thức tạo. Điều này sẽ làm cho mã của bạn phức tạp và khó di chuyển sang các hệ thống tệp khác nhau. Trong thực tế, lúc này bạn chỉ bao giờ triển khai hoặc khởi tạo một đối tượng Path trực tiếp nếu bạn viết mã để tương tác với loại hệ thống tệp của riêng bạn.

Lợi ích của việc sử dụng mẫu nhà máy ở đây là bạn có thể viết cùng một mã sẽ chạy trên nhiều nền tảng khác nhau. Như bạn sẽ thấy trong chương này, không phải tất cả các hệ thống tệp đều giống nhau; do đó, cùng một mã có thể có kết quả khác nhau khi chạy trên các hệ thống tệp khác nhau. Bằng cách cung cấp một triển khai Path khác nhau cho mỗi nền tảng, Java có thể xử lý những khác biệt này một cách hiệu quả.

![image](https://github.com/truongsonghiep/java-notes/assets/57567162/e3709dd4-09ef-48cd-a6c2-2da3e7d49acf)

Bởi vì Path là một interface nên không thể tạo trực tiếp từ nó mà sẽ có một lớp factory giúp ta đó là lớp `Paths`.
```java
Path path1 = Paths.get("pandas/cuddly.png");
Path path2 = Paths.get("c:\\zooinfo\\November\\employees.txt");
Path path3 = Paths.get("/home/zoodirector");
```

đường dẫn tuyệt đối bắt đầu bằng `/` hoặc ký tự ổ đĩa `C:/abc/def` còn lại là tương đối `.../abc/def`

Bạn có thể dử dụng
```java
Path path1 = Paths.get("pandas","cuddly.png");
Path path2 = Paths.get("c:","zooinfo","November","employees.txt");
Path path3 = Paths.get("/","home","zoodirector");
```
Hãy chú ý Path và Paths nếu không muốn mất điểm trong kỳ thi.

```java
Path path1 = Paths.get(new URI("file://pandas/cuddly.png")); // THROWS EXCEPTION
// AT RUNTIME
Path path2 = Paths.get(new URI("file:///c:/zoo-info/November/employees.txt"));
Path path3 = Paths.get(new URI("file:///home/zoodirectory"));
```

NIO bao gồm các lớp và giao diện nằm trong package `java.nio`, nó cung cấp một cách tiếp cận hiệu quả hơn cho việc xử lý IO so với truyền thống của Java IO.



## Interacting with Paths and Files
Lưu ý: đối tượng `Path` đại diện cho vị trí của file chứ không đại diện cho file. 




Metadata (siêu dữ liệu) là "dữ liệu của dữ liệu", nó mô tả về thông tin của dữ liệu, ví dụ: người tạo ra nó, người thay đổi, ngày thay đổi, tiêu đề, mô tả, loại, kích thước...

Lớp `Files` trong Java cung cấp một số hàm để cật nhật các metadata của file được gọi là các attribute, các hàm này thay đổi dựa vào hệ điều hành.
