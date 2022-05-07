#### 1. Giới thiệu.

Tường lửa là một ý tưởng rất tốt cho một máy chủ. Mặc dù nhiều người nghĩ rằng tường lửa là sự bảo vệ tức thì sẽ làm mọi thứ mà nó thực sự không có. Một tường lửa sẽ giúp ngăn chặn một số thứ nhưng nó sẽ không dừng lại mọi thứ. Nó chỉ là một phần của bảo mật mạng đang được dệt. Tôi khuyên dùng tường lửa bảo vệ nâng cao (APF) bởi rfxnetworks.

APF sẽ chặn các cổng đến và đi không sử dụng. Nó cũng có thể được cấu hình để sử dụng thông tin từ một số danh sách block lists. Danh sách cổng dưới đây sẽ hoạt động cho cPanel. Đối với các bảng điều khiển khác, bạn sẽ cần thêm vào các cổng quản trị.

`cd /root/ `| Truy cập vào thư mục gốc

`wget http://www.rfxnetworks.com/downloads/apf-current.tar.gz`

`tar -xvzf apf-current.tar.gz `| Giải nén file nào!!!!

![image](https://user-images.githubusercontent.com/101684058/167247855-5fb8d95f-a735-4760-9ccd-8595ab390030.png)


![image](https://user-images.githubusercontent.com/101684058/167247898-e73d8c9f-8487-4ff5-a328-5d330224e7fd.png)


Bạn sẽ thấy một danh sách thư mục. Hãy truy cập vào thư mục vừa giải nén sử dụng lệnh:

`cd /tên thư mục/` | Chuyển con trỏ tới thư mục bạn muốn cài đặt

`./install.sh `| Chạy file cài đặt

![image](https://user-images.githubusercontent.com/101684058/167248050-c6563d3a-8823-47f1-acd3-0a32c3352c8e.png)



Chỉnh sửa lại file cấu hình tường lửa có thể khắc phục khá nhiều lỗi

`vi /etc/apf/conf.apf` | Dùng trình soạn thảo VI để sửa file conf.apf

Nếu lỗi xuất phát từ thông báo này: “eth0: error fetching interface information: Device not found“, bạn hãy chỉnh sửa thông số sau:
IFACE_IN=”eth0″
IFACE_OUT=”eth0″
thành
IFACE_IN=”venet0″
IFACE_OUT=”venet0″

![image](https://user-images.githubusercontent.com/101684058/167248359-96955dfe-332b-4921-91d5-1a7f473d12a4.png)

Lưu file vào. Khởi động APF Firewall nhé:

`apf -s` | Command khởi động APF Firewall

![image](https://user-images.githubusercontent.com/101684058/167248511-1e4eb25e-7c8b-46d4-9a6f-066821684e19.png)

![image](https://user-images.githubusercontent.com/101684058/167248523-cc2a08b3-a1d6-4520-bb07-effc2a18c8e0.png)

 thay đổi chế độ chạy thử về chế độ chạy chính thức.

`vi /etc/apf/conf.apf` | Dùng trình soạn thảo VI để sửa file conf.apf
Tìm mục
DEVEL_MODE=”1″
sửa thành
DEVEL_MODE=”0″

![image](https://user-images.githubusercontent.com/101684058/167248584-0d7c4815-0596-4f05-af3d-9e4df183c750.png)

Cuối cùng, phải khởi động lại APF Firewall

`apf -r` | Command khởi động lại APF Firewall

Như vậy, VPS của bạn có một bức tường lửa giúp chặn những truy cập không mong muốn.

![image](https://user-images.githubusercontent.com/101684058/167248652-528eba45-9b30-4136-8b05-b25ec16ad77d.png)

