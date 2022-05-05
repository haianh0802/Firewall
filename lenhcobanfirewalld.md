##### Mở TCP/ UDP port :

Để add thêm 1 port, ví dụ như port 443 HTTPS, sử dụng cú pháp dòng lệnh như bên dưới. Lưu ý rằng ta cần phải xác định rõ là port UDP hay TCP đằng sau port number :

 `sudo firewall-cmd --add-port=443/tcp --permanent`
 
Tương tự, để chỉ định 1 port UDP, ta sẽ điền ngay sau port number

`sudo firewall-cmd --add-port=53/tcp -- permanent`

“–permanent “ đây là cú pháp thông báo rằng các rule vẫn tồn tại ngay cả sau khi khởi động lại.

##### Block 1 port TCP/ UDP : 

Để chặn một TCP port, như là port 22, ta chạy dòng lệnh sau :

`sudo firewall-cmd --remove-port=22/tcp –permanent`

Tương tự, ta block UDP port bằng dòng lệnh :

`sudo firewall-cmd --remove-port=53/udp -- permanent`

##### Mở một service :

Service network được xác định trong file /etc/services. Để mở một service như https, ta thực hiện command :

 `sudo firewall-cmd --add-service=https`
 
##### Block 1 service :

Để block 1 service, ví dụ FTP, ta chạy lệnh :

`sudo firewall-cmd --remove-service=https`

##### Tạo Whitelist 1 địa chỉ IP :

Để cho phép 1 địa chỉ IP thông qua firewall, ta thực hiện dòng lệnh sau :

`sudo firewall-cmd --permanent --add-source=192.168.2.50`

Bạn cũng có thể cho phép 1 dãy địa chỉ IP trong một subnet bằng dòng lệnh :

`sudo firewall-cmd --permanent --add-source=192.168.2.0/24`

##### Xóa 1 địa chỉ IP whitelist :

Nếu muốn remove 1 IP whitelist trên Firewall, sử dụng cú pháp –remove-source :

`sudo firewall-cmd --permanent --remove-source=192.168.2.50`

Đối với cả một hệ thống subnet,ta chạy lệnh :

`sudo firewall-cmd --permanent --remove-source=192.168.2.50/24`

##### Block 1 địa chỉ IP :

Ví dụ để block 1 địa chỉ IP 192.168.2.50 ta chạy command :

`sudo firewall-cmd --permanent --add-rich-rule="rule family='ipv4' source address='192.168.2.50' reject"`

##### Để block subnet :

`sudo firewall-cmd --permanent --add-rich-rule="rule family='ipv4' source address='192.168.2.0/24' reject"`

##### Save firewall rules :

Nếu đã thực hiện bất kì thay đổi nào trên firewall, bạn cần chạy dòng lệnh sau để thay đổi có hiệu lực :

`sudo firewall-cmd –reload`

Xem lại Firewall rule :

Để xem lại tất cả rule trên firewall, ta chạy dòng lệnh :

`sudo firewall-cmd --list-all`
