1. Khởi động “csf” và “lfd” nếu chưa khởi động

`csf -e`

`csf --enable`

![image](https://user-images.githubusercontent.com/101684058/166878513-734860c6-15d5-4372-8d3e-a89880e1912d.png)

2. Tắt “csf” và “lfd”

`csf -x`

![image](https://user-images.githubusercontent.com/101684058/166879086-c0c4b691-bde1-4b38-b523-723fac7f71e8.png)

3. Khởi động lại các rule tường lửa

`csf -r`

`csf --restart`

4. Khởi động rule tường lửa

`csf -s`

`csf --start`

![image](https://user-images.githubusercontent.com/101684058/166884060-07b9225b-e547-47d6-adac-b72bf2f8ca1b.png)
![image](https://user-images.githubusercontent.com/101684058/166884299-84d23e18-7b57-4db7-a3b5-217032a33c6f.png)

5. Xoá toàn bộ rule tường lửa

`csf -f`

`csf --stop`

6. Liệt kê cấu hình rule IPv4 Iptables
`csf -l`

`csf --status`

![image](https://user-images.githubusercontent.com/101684058/166884714-13f22755-fd57-4554-80b4-c06cc445c023.png)

7. Liệt kê cấu hình rule IPv6 Iptables

`csf -l6`

`csf --status6`

![image](https://user-images.githubusercontent.com/101684058/166885255-a632238e-ba3f-4f63-bef0-f4f78f8f0604.png)

8. Cho phép (allow) 1 IP và thêm IP đó vào file /etc/csf/csf.allow

`csf -a ip [nhận xét]

`csf --thêm ip [nhận xét]`

![image](https://user-images.githubusercontent.com/101684058/166890216-fd93da8a-a54f-4e6e-8fa1-0fe8488caebc.png)

![image](https://user-images.githubusercontent.com/101684058/166891076-70d59176-558b-422a-9671-666fe85ba449.png)

9. Gỡ bỏ IP khỏi danh sách cho phép, bỏ IP đó khỏi file /etc/csf/csf.allow

`csf -ar ip`

`csf --addrm ip`

![image](https://user-images.githubusercontent.com/101684058/166891271-e7de245b-f807-4c80-9806-c5c4e361aa11.png)

![image](https://user-images.githubusercontent.com/101684058/166891401-0eddd64d-6492-4da8-80a4-6858efc5a067.png)

10. Chặn (deny) 1 IP và thêm IP đó vào file /etc/csf/csf.deny

`csf -d ip [nhận xét]`

`csf --deny ip [nhận xét]`

![image](https://user-images.githubusercontent.com/101684058/166891734-229a8200-1846-4116-abfa-48d68a53a644.png)

![image](https://user-images.githubusercontent.com/101684058/166891868-562da96a-66c6-4efa-805d-eb1249247fae.png)

11. Chặn 1 IP vĩnh viễn không bị xoá khỏi danh sách IP trong /etc/csf/csf.deny
12. 
– Số lượng IP chặn cũng như số lượng IP entry có thể chứa trong file /etc/csf/csf.deny được quy định bởi cấu hình giá trị “DENY_IP_LIMIT” trong /etc/csf/csf.conf. Nên khi số lượng IP bị deny đạt ngưỡng này thì CSF sẽ tuần tự xoá các IP cũ nhất khỏi danh sách IP bị chặn để thêm 1 IP mới vào danh sách chặn.

– Trong trường hợp đó ta muốn 1 IP đã thêm vào danh sách chặn sẽ không bị CSF gỡ bỏ để phục vụ nhu cầu lấy khoảng trống cho IP mới bị chặn, thì ta sẽ thêm dòng comment “do not delete” khi gõ lệnh chặn IP.

`csf -d ip không xóa`

`csf --deny ip không xóa`

12. Gỡ bỏ IP khỏi danh sách bị chặn, bỏ IP đó khỏi file /etc/csf/csf.deny

`csf -dr ip`

`csf --denyrm ip`

13. Xoá toàn bộ các IP bị chặn cũng như là xoá bộ IP thông tin trong file /etc/csf/csf.deny

`csf -df`

`csf --denyf`

![image](https://user-images.githubusercontent.com/101684058/166892105-3dc29e9d-54db-44d3-8cf6-a4f27b7f1499.png)

14. Tìm thông tin về IP trong danh sách rule tường lửa chặn

– Áp dụng cho cả việc tìm kiếm trong các rule IPv4 và IPv6, giúp xác định IP cần kiểm tra có bị chặn tạm thời, chặn vĩnh viễn hay đang được cho phép như thế nào.

`csf -g ip`

![image](https://user-images.githubusercontent.com/101684058/166892441-e1cf46e5-6afb-402e-bed1-5ffa08526610.png)

15. Thêm IP vào danh sách IP tạm thời được cho phép

`csf -ta ip ttl [-p cổng] [-d hướng] [nhận xét]`

`csf --tempallow ip ttl [-p port] [-d direction] [comment]`

16. Thêm IP vào danh sách IP tạm thời bị chặn

`csf -td ip ttl [-p port] [-d direction] [comment]`

`csf --tempdeny ip ttl [-p port] [-d direction] [comment]`
