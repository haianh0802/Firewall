### Iptables là gì?

Trong hệ điều hành Linux, tường lửa được thực thi tốt nhất bằng cách sử dụng netfilter. Đây là một kernel module quyết định packet nào được phép đi vào (input) hoặc đi ra bên ngoài (output).

iptables chỉ là interface cho netfilter và cả hai thường được coi là tương tự nhau. Một cách nhìn dễ hiểu hơn là nghĩ về nó như một backend và một frontend.

### Lý do bạn nên sử dụng iptables

- Đây là một công cụ đầy đủ tính năng cung cấp cho bạn mọi thứ bạn cần

- Bạn có thể xử lý các packet linh hoạt hơn.

- iptables cực kỳ thú vị và có thể sẽ khiến bạn cảm thấy cực kỳ tuyệt vời khi làm việc với chúng.

- Bạn sẽ cảm thấy mình giống như một hacker hoặc một kẻ lập dị phi thường khi tự mình viết được những rule tuyệt vời chống lại các cuộc tấn công.

### Cấu trúc iptables là gì?

Để hiểu rõ iptables một cách cụ thể, ta hãy đi tìm hiểu chi tiết hơn về nó. Iptables bao gồm các thành phần khác nhau:

**- Chain**: Có 5 chain trong iptables và mỗi chain chịu trách nhiệm cho một nhiệm vụ cụ thể. Các chain này là: PREROUTING, INPUT, FORWARD, OUTPUT và POSTROUTING. Giống như tên gọi của chúng, chúng chịu trách nhiệm về các packet ngay khi nhận được, hoặc ngay trước khi định tuyến ra bên ngoài.

**- Table**: các table khác nhau chịu trách nhiệm cho các nhiệm vụ khác nhau. Danh sách table bao gồm:  filter, nat, mangle, raw và security. Hai table đầu được sử dụng nhiều nhất. Table filter chịu trách nhiệm lọc (filter) và hạn chế các packet đến máy chủ. Table nat chịu trách nhiệm về chuyển đổi địa chỉ mạng (NAT – Network Address Translation).

**- target**: Các target chỉ định nơi packet sẽ đi. Điều này được quyết định bằng cách sử dụng các target của chính iptables:

**- ACCEPT**(chấp nhận)
 
 **- DROP** (gỡ bỏ)
 
**- RETURN** (quay trở lại)

Hoặc target của các extension module, phổ biến nhất là DNAT, LOG, MASQUERADE, REJECT, SNAT, TRACE và TTL.

Các target được chia thành có kết thúc và không kết thúc. Các target có kết thúc chấm dứt rule và các packet sẽ bị ngừng ở đó. Nhưng các target không kết thúc sẽ xử lý packet theo một cách nào đó và rule sẽ  được thực hiện tiếp tục sau đó.

### Chain iptables là gì?

**PREROUTING:** chain này quyết định điều gì sẽ xảy ra với một packet ngay khi nó tới Network Interface. Chúng ta có các tùy chọn khác nhau như thay đổi packet (có thể là NAT), bỏ packet hoặc không làm gì cả và để nó tiếp tục di chuyển và được xử lý ở nơi khác trên đường đi.

**INPUT:** Đây là một trong những chain phổ biến vì nó hầu như luôn chứa các rule nghiêm ngặt để kiểm soát truy cập từ internet gây hại cho máy tính của chúng ta. Nếu bạn muốn mở hay chặn một port thì đây là nơi bạn sẽ làm điều đó.

**FORWARD:** chain này chịu trách nhiệm forward packet. Chúng ta có thể coi máy tính như một bộ định tuyến (router) và đây là nơi mà một số quy tắc (rule) có thể áp dụng để thực hiện công việc.

**OUTPUT:** chịu trách nhiệm cho tất cả quá trình truy cập ra bên ngoài. Bạn không thể gửi một packet mà không được sự cho phép. Đó là nơi tốt nhất để hạn chế lưu lượng outgoing của bạn nếu bạn không chắc chắn mỗi ứng dụng đang giao tiếp qua cổng nào.

**POSTROUTING:** chain này là nơi các packet để lại dấu vết cuối cùng, trước khi rời khỏi máy tính của chúng ta. Điều này được sử dụng để định tuyến (routing) trong số nhiều tác vụ khác để đảm bảo các packet được xử lý theo cách chúng ta muốn.

Hầu hết các trường hợp, bạn sẽ sử dụng thường xuyên chain INPUT & OUTPUT.

### Các table iptables

- filter: là table được sử dụng nhiều nhất hàng ngày. Đó là lý do tại sao nó là table mặc định. Trong table này, bạn sẽ quyết định xem packet có được phép vào (input) hoặc ra (output) khỏi máy tính của bạn hay không. Nếu bạn muốn chặn một port để ngừng nhận bất cứ thứ gì, đây là điểm table bạn cần.

- nat: Table này là table phổ biến thứ hai và chịu trách nhiệm tạo kết nối mới. Đó là cách viết tắt của Network Address Translation.

- mangle: table này dùng để thay đổi dữ liệu bên trong các packet trước khi chúng đến hoặc ra khỏi máy tính.

- raw: table này xử lý packet raw chưa qua xử lý như tên gọi của nó. Chủ yếu là để theo dõi trạng thái kết nối. Chúng ta sẽ thấy các ví dụ về điều này bên dưới khi muốn cho các packet thành công từ kết nối SSH.

- security: có nhiệm vụ đánh dấu những gói tin có liên quan đến context của SELinux, nó giúp cho SELinux hoặc các thành phần khác hiểu được context SELinux và xử lý gói tin.

### Các tùy chọn để chỉ định thông số IPtables

- Chỉ định tên table: -t ,

- Chỉ định loại giao thức: -p ,

- Chỉ định card mạng vào: -i ,

- Chỉ định card mạng ra: -o ,

- Chỉ định địa chỉ IP nguồn: -s <địa_chỉ_ip_nguồn>,

- Chỉ định địa chỉ IP đích: -d <địa_chỉ_ip_đích>, tương tự như –s.
 
 - Chỉ định cổng nguồn: –sport ,

- Chỉ định cổng đích: –dport , tương tự như –sport

### Các tùy chọn để thao tác với chain trong IPtables 

- Tạo chain mới: IPtables -N

- Xóa hết các rule đã tạo trong chain: IPtables -X

- Đặt chính sách cho các chain `built-in` (INPUT, OUTPUT & FORWARD): IPtables -P , ví dụ: IPtables -P INPUT ACCEPT để chấp nhận các packet vào chain INPUT

- Liệt kê các rule có trong chain: IPtables -L

- Xóa các rule có trong chain (flush chain): IPtables -F

- Reset bộ đếm packet về 0: IPtables -Z

### Các tùy chọn để thao tác với rule trong IPtables 

- Thêm rule: -A (append)

- Xóa rule: -D (delete)

- Thay thế rule: -R (replace)

- Chèn thêm rule: -I (insert)

## Cài đặt Iptables trên Centos 7

– Iptables thường được cài đặt mặc định trong hệ thống. Nếu chưa được cài đặt:

`yum install iptables`

CentOS 7 sử dụng FirewallD làm tường lửa mặc định thay vì Iptables. Nếu bạn muốn sử dụng Iptables thực hiện:

 `systemctl mask firewalld`
 
`systemctl enable iptables`

`systemctl enable ip6tables`

`systemctl stop firewalld`

`systemctl start iptables`

`systemctl start ip6tables` 

![image](https://user-images.githubusercontent.com/101684058/167084184-dcc719ef-3f1a-4c14-beae-95f4629318ad.png)

– Kiểm tra Iptables đã được cài đặt trong hệ thống:

 `rpm -q iptables`

`iptables --version`

![image](https://user-images.githubusercontent.com/101684058/167084509-8eb3001c-cbcb-4506-9c2d-8664cad04cf4.png)

– Check tình trạng của Iptables, cũng như cách bật tắt services trên CentOS

`service iptables status`

![image](https://user-images.githubusercontent.com/101684058/167084682-4d846d65-bbd8-4515-ab24-b799702df2a6.png)

`service iptables start`

`service iptables stop`

`service iptables restart`

![image](https://user-images.githubusercontent.com/101684058/167084824-654db9f1-5685-45a2-9a28-3a4307ac76f0.png)

– Khởi động Iptables cùng hệ thống

`chkconfig iptables on`

##  Các nguyên tắc áp dụng trong Iptables

Để bắt đầu, bạn cần xác định các services muốn đóng/mở và các port tương ứng.

Liệt kê các quy tắc hiện tại:

`iptables -L`

![image](https://user-images.githubusercontent.com/101684058/167085762-388b8bd3-2f21-43cf-8ea4-2be6687b732e.png)

Cột 1: TARGET hành động sẽ được áp dụng cho mỗi quy tắc

Accept: gói dữ liệu được chuyển tiếp để xử lý tại ứng dụng cuối hoặc hệ điều hành

Drop: gói dữ liệu bị chặn, loại bỏ

Reject: gói dữ liệu bị chặn, loại bỏ đồng thời gửi một thông báo lỗi tới người gửi

Cột 2: PROT (protocol – giao thức) quy định các giao thức sẽ được áp dụng để thực thi quy tắc, bao gồm all, TCP hay UDP. Các ứng dụng SSH, FTP, sFTP… đều sử dụng giao thức TCP.

Cột 4, 5: SOURCE và DESTINATION địa chỉ của lượt truy cập được phép áp dụng quy tắc.

## Cách sử dụng Iptables để mở port VPS
1. Mở port SSH
2. 
Để truy cập VPS qua SSH, bạn cần mở port SSH 22. Bạn có thể cho phép kết nối SSH ở bất cứ thiết bị nào, bởi bất cứ ai và bất cứ dâu.

`iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT`

![image](https://user-images.githubusercontent.com/101684058/167090087-4db2514b-1ad0-4a6a-929c-e79a9c1855ee.png)

2. Mở port Web Server

Để cho phép truy cập vào webserver qua port mặc định 80 và 443:

`iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT`

`iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT`

3. Mở port Mail

– Để cho phép user sử dụng SMTP servers qua port mặc định 25 và 465:

`iptables -I INPUT -p tcp -m tcp --dport 25 -j ACCEPT`

`iptables -I INPUT -p tcp -m tcp --dport 465 -j ACCEPT`

– Để user đọc email trên server, bạn cần mở port POP3 (port mặc định 110 và 995)

`iptables -A INPUT -p tcp -m tcp --dport 110 -j ACCEPT`

`iptables -A INPUT -p tcp -m tcp --dport 995 -j ACCEPT`

4. Chặn 1 IP truy cập

`iptables -A INPUT -s IP_ADDRESS -j DROP`

Cuối cùng, bạn cần lưu lại các thiết lập tường lửa Iptables nếu không các thiết lập sẽ mất khi bạn reboot hệ thống. 

`service iptables save`

![image](https://user-images.githubusercontent.com/101684058/167090976-019e214a-7669-4d8f-b4f4-83954e7ebe89.png)
