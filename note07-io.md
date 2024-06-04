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
