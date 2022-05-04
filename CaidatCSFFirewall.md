# Cài đặt CSF Firewall trên CentOS 7

1. Bước 1: Dừng và vô hiệu hóa tường lửa.

Để dừng và vô hiệu hoá Firewalld trên centos các bạn sử dụng 2 lệnh sau

`systemctl disable firewalld `

`systemctl stop firewalld` 

![image](https://user-images.githubusercontent.com/101684058/166621367-be81483f-ae9b-4a3c-bc61-faed9e849fab.png)

2. Bước 2: Cài đặt iptables.

Sau khi đã dừng và vô hiệu hoá Firewalld chúng ta tiến hành cài đặt ibtables

`yum -y install iptables-services`

Tạo tập tin cần thiết bởi iptables.

`touch /etc/sysconfig/iptables `

`touch /etc/sysconfig/iptables6`

Khởi động iptables.

`systemctl start iptables `

`systemctl start ip6tables`

Kích hoạt iptables mỗi khi khởi động lại VPS/Server.

`systemctl enable iptables `

`systemctl enable ip6tables`

![image](https://user-images.githubusercontent.com/101684058/166621475-aa623fdb-20cb-4624-a89d-9be1e59aea58.png)

3. Bước 3: Cài đặt các thư viện cần thiết.

Tiếp theo các bạn tiến hành cài đặt các thư viện cần thiết cho việc hoạt động của CSF

`yum -y install wget perl unzip net-tools perl-libwww-perl perl-LWP-Protocol-https perl-GDGraph`

4. Bước 4:  cài đặt CSF.

Sau khi đã cài đặt đầy đủ các thư viện chúng ta tiến hành cài đặt CSF. Việc cài đặt diễn ra hết sức đơn giản với các lệnh dưới đây

`cd /opt`

`wget https://download.configserver.com/csf.tgz `

`tar -xzf csf.tgz `

`cd csf `

`sh install.sh`

Loại bỏ các tập tin cài đặt.

`cd /`

`rm -rf /opt/csf /opt/csf.tgz`

Bây giờ chúng ta sẽ kiểm tra xem CSF có thực sự hoạt động trên máy chủ không. Chúng tôi sẽ làm một bài kiểm tra để xác minh.

`cd /usr/local/csf/bin/`

`perl csftest.pl`

Nếu bạn thấy kết quả như hiển thị như bên dưới thì CSF sẽ hoạt động mà không gặp sự cố nào trên máy chủ của bạn.

![image](https://user-images.githubusercontent.com/101684058/166636025-a146e179-c7a0-465a-8b8a-387faf7febc2.png)


5. Bước 5: Cấu hình CSF

Tiếp theo, chúng ta sẽ cần cấu hình CSF bằng cách chỉnh sửa file /etc/csf/csf.confcsf.conf. Trong bài viết này HOSTVN sẽ sử dụng nano editor để chỉnh sửa, các bạn có thể sử dụng VIM nếu muốn.

`nano /etc/csf/csf.conf`

bạn sẽ cần sửa một số thông số dưới đây

TESTING = "0"

RESTRICT_SYSLOG = "3"

TCP_OUT = "20,21,22,25,53,80,110,113,443,587,465,993,995"

Sau khi đã chỉnh sửa các bạn tiến hành khởi động csf

`systemctl enable csf`

`systemctl enable lfd`

`systemctl start csf`

Để kiểm tra xem csf đã hoạt động hay chưa các bạn có thể sử dụng lệnh dưới đây

`systemctl status csf`

![image](https://user-images.githubusercontent.com/101684058/166636722-d73ec33e-b90e-4b13-b320-326defd4a1c7.png)

