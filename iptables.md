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
