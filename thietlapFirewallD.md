## Cài đặt FirewallD

– FirewallD được cài đặt mặc định trên CentOS 7. Cài đặt nếu chưa có:

` yum install firewalld`

– Khởi động FirewallD:

`systemctl start firewalld`

– Kiểm tra tình trạng hoạt động

`systemctl status firewalld`

![image](https://user-images.githubusercontent.com/101684058/166649603-085f4764-76ea-4a79-9af1-c04b55bd7586.png)

`systemctl is-active firewalld`

 `firewall-cmd --state`

– Thiết lập FirewallD khởi động cùng hệ thống

`systemctl enable firewalld`

Kiểm tra lại :

`systemctl is-enabled firewalld`

![image](https://user-images.githubusercontent.com/101684058/166649880-686ccc91-5383-48bf-9328-740ce8a90017.png)

Ban đầu, bạn không nên cho phép FirewallD khởi động cùng hệ thống cũng như thiết lập Permanent, tránh bị khóa khỏi hệ thống nếu thiết lập sai. Chỉ thiết lập như vậy khi bạn đã hoàn thành các quy tắc tường lửa cũng như test cẩn thận.

– Khởi động lại

`systemctl restart firewalld`

` firewall-cmd --reload`

![image](https://user-images.githubusercontent.com/101684058/166650060-d67a185e-65aa-4691-9499-2dfc488e7fb6.png)

– Dừng và vô hiệu hóa FirewallD

`systemctl stop firewalld`

`systemctl disable firewalld`

 ## Cấu hình FirewallD
 
1. Thiết lập các Zone

– Liệt kê tất cả các zone trong hệ thống

`firewall-cmd --get-zones`

![image](https://user-images.githubusercontent.com/101684058/166655591-50e5e38a-7a8e-410a-baff-d41ff116ce1f.png)

– Kiểm tra zone mặc định

`firewall-cmd --get-default-zone`

![image](https://user-images.githubusercontent.com/101684058/166655658-df2f5ea6-51a9-4c6f-9867-e06d6872f373.png)

– Kiểm tra zone active (được sử dụng bởi giao diện mạng)

Vì FirewallD chưa được thiết lập bất kỳ quy tắc nào nên zone mặc định cũng đồng thời là zone duy nhất được kích hoạt, điều khiển mọi luồng dữ liệu.

`firewall-cmd --get-active-zones`


![image](https://user-images.githubusercontent.com/101684058/166655700-9b629640-4caf-4ca3-aeb7-8a8bb97b6c4f.png)

– Thay đổi zone mặc định, ví dụ thành home:

 ` firewall-cmd --set-default-zone=home`
 
 2. Thiết lập các quy tắc

Trước khi thiết lập các quy tắc mới, hãy cùng HocVPS kiểm tra các quy tắc hiện tại:

– Liệt kê toàn bộ các quy tắc của các zones:

`firewall-cmd --list-all-zones`

– Liệt kê toàn bộ các quy tắc trong zone mặc định và zone active

`firewall-cmd --list-all`

![image](https://user-images.githubusercontent.com/101684058/166655912-6ea48fef-6d61-4c7f-89de-06abdb5c09c8.png)

Kết quả cho thấy public là zone mặc định đang được kích hoạt, liên kết với card mạng eth0 và cho phép DHCP cùng SSH.

– Liệt kê toàn bộ các quy tắc trong một zone cụ thể, ví dụ home

`firewall-cmd --zone=home --list-all`

![image](https://user-images.githubusercontent.com/101684058/166655983-1f8f8671-5b28-49cc-ada3-5a3bb32cbdc8.png)

– Liệt kê danh sách services/port được cho phép trong zone cụ thể:

`firewall-cmd --zone=public --list-services`

`firewall-cmd --zone=public --list-ports`

![image](https://user-images.githubusercontent.com/101684058/166656040-6c2bc27a-ebf8-41ec-b654-8986ab3ea3b5.png)

a. Thiết lập cho Service

Đây chính là điểm khác biệt của FirewallD so với Iptables – quản lý thông qua các services. Việc thiết lập tường lửa đã trở nên dễ dàng hơn bao giờ hết – chỉ việc thêm các services vào zone đang sử dụng.

– Đầu tiên, xác định các services trên hệ thống:

`firewall-cmd --get-services`

![image](https://user-images.githubusercontent.com/101684058/166656107-0eb62ae7-7d57-4d5c-b137-feea02cd0a07.png)

– Thiết lập cho phép services trên FirewallD, sử dụng --add-service:

` firewall-cmd --zone=public --add-service=http`

`firewall-cmd --zone=public --add-service=http --permanent`

![image](https://user-images.githubusercontent.com/101684058/166656246-f523f4f5-2227-4ae7-87cb-85a3a17079d1.png)

Ngay lập tức, zone “public” cho phép kết nối HTTP trên cổng 80. Kiểm tra lại

`firewall-cmd --zone=public --list-services`

![image](https://user-images.githubusercontent.com/101684058/166656290-35fcabbf-2218-473e-ba0c-16465b8d119b.png)

– Vô hiệu hóa services trên FirewallD, sử dụng --remove-service:

`firewall-cmd --zone=public --remove-service=http`

`firewall-cmd --zone=public --remove-service=http --permanent`

![image](https://user-images.githubusercontent.com/101684058/166656351-86821855-23ee-41b8-a544-027037c3b641.png)

b. Thiết lập cho Port

Trong trường hợp bạn thích quản lý theo cách truyền thống qua Port, FirewallD cũng hỗ trợ bạn điều đó.

– Mở Port với tham số --add-port:

`firewall-cmd --zone=public --add-port=9999/tcp`

`firewall-cmd --zone=public --add-port=9999/tcp --permanent`

![image](https://user-images.githubusercontent.com/101684058/166656463-0b0d108c-eda7-4cac-a72e-d1fccf479b56.png)

Mở 1 dải port

`firewall-cmd --zone=public --add-port=4990-5000/tcp`

`firewall-cmd --zone=public --add-port=4990-5000/tcp --permanent`

![image](https://user-images.githubusercontent.com/101684058/166656566-3cbf2d08-4ce7-4ca4-a919-c007f580a30d.png)

Kiểm tra lại

`firewall-cmd --zone=public --list-ports`

![image](https://user-images.githubusercontent.com/101684058/166656719-b47059ab-4204-4b4c-8a95-a5d96670765c.png)

– Đóng Port với tham số --remove-port:

`firewall-cmd --zone=public --remove-port=9999/tcp`

`firewall-cmd --zone=public --remove-port=9999/tcp --permanent`

### Cấu hình nâng cao

1. Tạo Zone riêng

Mặc dù, các zone có sẵn là quá đủ với nhu cầu sử dụng, bạn vẫn có thể tạo lập zone của riêng mình để mô tả rõ ràng hơn về các chức năng của chúng. Ví dụ, bạn có thể tạo riêng một zone cho webserver publicweb hay một zone cấu hình riêng cho DNS trong mạng nội bộ privateDNS. Bạn cần thiết lập Permanent khi thêm một zone.

`firewall-cmd --permanent --new-zone=publicweb`

`firewall-cmd --permanent --new-zone=privateDNS`

`firewall-cmd --reload`

![image](https://user-images.githubusercontent.com/101684058/166656873-d5eb07aa-df0e-42d0-b786-4d6f300537fe.png)

Kiểm tra lại

`firewall-cmd --get-zones`

![image](https://user-images.githubusercontent.com/101684058/166656936-c85649a4-982f-486a-b224-1d656279aecc.png)

Khi đã có zone thiết lập riêng, bạn có thể cấu hình như các zone thông thường: thiết lập mặc định, thêm quy tắc… Ví dụ:

`firewall-cmd --zone=publicweb --add-service=ssh --permanent`

`firewall-cmd --zone=publicweb --add-service=http --permanent`

` firewall-cmd --zone=publicweb --add-service=https --permanent`

![image](https://user-images.githubusercontent.com/101684058/166657014-5e121f36-6bb6-432b-a0f5-d760c7d9fb25.png)

2. Định nghĩa services riêng trên FirewallD

Việc mở port trên tường lửa rất dễ dàng nhưng lại khiến bạn gặp khó khăn khi ghi nhớ các port và các services tương ứng. Vì vậy, khi có một services mới thêm vào hệ thống, bạn sẽ có 2 phương án:

Mở Port của services đó trên FirewallD

Tự định nghĩa services đó trên FirewallD

– Tạo file định nghĩa riêng từ file chuẩn ban đầu

`cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/hocvps-admin.xml`

– Chỉnh sửa để định nghĩa servies trên FirewallD

`nano /etc/firewalld/services/hocvps-admin.xml`

![image](https://user-images.githubusercontent.com/101684058/166658315-380c4d1b-7cc7-48e4-8794-555727d45d10.png)

– Lưu lại và khởi động lại FirewallD

`firewall-cmd --reload`

– Kiểm tra lại danh sách services:

`firewall-cmd --get-services`

![image](https://user-images.githubusercontent.com/101684058/166658397-e9147636-d930-4c04-8206-a5b5bd752bd2.png)

