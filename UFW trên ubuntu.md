### UFW là gì?

UFW là một công cụ cho phép chúng tôi quản lý Tường lửa của mình bằng cách sử dụng dòng lệnh mà chúng tôi sẽ quản lý cấu hình Tường lửa. Nhờ có UFW, chúng tôi có thể làm việc với các chính sách bảo mật khác nhau tùy thuộc vào các tham số bảo mật.

### Vai trò của tường lửa trong Hệ điều hành

- Bảo vệ mạng.

- Duy trì tính toàn vẹn của thông tin được lưu trữ trong thiết bị.

- Tránh từ chối các cuộc tấn công dịch vụ.

- Giữ gìn sự riêng tư của tổ chức và của chính nó.

- Tránh sự xâm nhập của người dùng trái phép vào hệ thống.

### Các loại quy tắc trong Tường lửa

Khi chúng tôi quản lý tường lửa, chúng tôi có thể quản lý các loại quy tắc khác nhau cho nó, một số trong số đó là:

- Kiểm soát số lượng kết nối.

- Đăng nhập và ra khỏi các sự kiện kết nối.

- Quản lý và quản lý quyền truy cập của người dùng.

- Kiểm soát những ứng dụng và chương trình nào có thể truy cập Internet.

- Phát hiện cổng

## Cách cài đặt UFW trên Ubuntu Linux

**Bước 1:** SSH vào hệ thống Linux

**Bước 2:** Cập nhật hệ thống kiểm tra cài đặt

Cập nhật hệ thống

`sudo apt update`

![image](https://user-images.githubusercontent.com/101684058/167099571-cf0a4f4c-3e06-42e3-b59b-6284263675f8.png)

`sudo apt upgrade`

![image](https://user-images.githubusercontent.com/101684058/167099649-571eba19-5f55-43a4-857a-1a7c1e764117.png)

Kiểm tra cài đặt ufw

Để kiểm tra ufw đã được cài đặt chưa bạn sử dụng lệnh which để kiểm tra như sau.

`which ufw`

![image](https://user-images.githubusercontent.com/101684058/167108146-6d5b6a20-8e2c-4b1e-8ac8-6c008df0cb96.png)

**Bước 3:** Cài đặt ufw

![image](https://user-images.githubusercontent.com/101684058/167108471-73ad977d-ab13-4060-95a5-4cfb52dcb0ef.png)

`sudo apt-get install ufw`

Sau khi bạn cài đặt ufw hoàn tất, bạn hãy sử dụng lệnh sau để kiểm tra. Và mặc định ban đầu sau khi cài đặt thì UFW sẽ được vô hiệu do chưa kích hoạt. Và bạn phải kích hoạt thủ công.

![image](https://user-images.githubusercontent.com/101684058/167108739-d394ffbb-333b-475c-8d75-04b6488956b2.png)

### sử dụng ufw

1. Một số lệnh quản lý kích hoạt ufw

**Kích hoạt ufw sau khi cài đặt**

`sudo ufw enable`

`sudo ufw status`

![image](https://user-images.githubusercontent.com/101684058/167109059-3a3fa8f7-e49f-4894-a7d6-345844aa6989.png)

**Vô hiệu kích hoạt ufw**

`sudo ufw disable`

![image](https://user-images.githubusercontent.com/101684058/167109200-fcf4a6d4-15f3-44bf-9b32-5a0360b4abec.png)

**Khởi động ufw cùng hệ thống**

`sudo ufw enable`

![image](https://user-images.githubusercontent.com/101684058/167109440-390938d7-5b6a-4a59-a0bb-380a6eb7c507.png)

**Khôi phục ufw về mặc định**

`sudo ufw reset`

![image](https://user-images.githubusercontent.com/101684058/167109627-4ffe0fe9-a8ac-4d29-b2af-6470dcb3e169.png)

**Tải lại các quy tắc**

`sudo ufw reload`

![image](https://user-images.githubusercontent.com/101684058/167109755-2f1b7cc5-7b57-42c0-8c91-f40af20434fa.png)

2. Sử dụng ufw để quản lý quy tắc
**Cho phép, mở port kết nối**

Cú pháp thực hiện

Để thực hiện mở một port (cổng) bất kỳ bạn sử dụng cú pháp như sau.

`sudo ufw allow <port>/<optional: protocol> `

![image](https://user-images.githubusercontent.com/101684058/167110393-29725967-dd7d-43a5-892d-0b8fc5f77b02.png)

**Từ chối, đóng port kết nối**

Để cấm, từ chối bạn sử dụng deny và thực hiện theo cấu trúc cú pháp như sau.

sudo ufw deny <port>/<optional: protocol> 

  ![image](https://user-images.githubusercontent.com/101684058/167110507-0c79d5a4-e325-49a6-ba9f-21a2f0954067.png)

  **Cho phép IP truy cập đến cổng nhất định**
  
  `sudo ufw allow from 192.168.0.1 to any port 22`
  
`sudo ufw allow from 192.168.0.1 to any port 3306`
  
  ![image](https://user-images.githubusercontent.com/101684058/167110859-13315a4d-2fe7-4468-a6b3-048ebe9275c7.png)

**Xoá bỏ các quy tắc**
  
Để quản lý các quy tắc trên UFW của bạn, bạn có thể liệt kê chúng ra theo dạng menu danh sách. Để thực hiện được bạn sử dụng lệnh sau, màn hình hiển thị các quy tắc kèm số thứ tự và bạn sẽ chọn các số thứ tự hoặc tên quy tắc để xoá bỏ.

