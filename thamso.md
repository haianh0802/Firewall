# Tham số tường lửa

Các tham số này ảnh hưởng đến hoạt động của S-TAP đối với tường lửa.

Các tham số này được lưu trữ trong phần [TAP] của tệp thuộc tính S-TAP.

|GIM|Guard_tap.ini|Giá trị mặc định|Sự miêu tả|
|--------|-----------|--------------|----------------|
|WINSTAP_FIREWALL_INSTALLED|FIREWALL_INSTALLED|0|Đã bật tính năng tường lửa. Giá trị hợp lệ: 0 : bị vô hiệu hóa. 1 : đã bật.|
|WINSTAP_FIREWALL_TIMEOUT|FIREWALL_TIMEOUT|2|Thời gian, tính bằng giây, chờ phán quyết từ hệ thống Guardium®. Nếu tường lửa hết thời gian chờ, giá trị của tham số firewall_fail_close sẽ xác định xem có chặn hoặc cho phép kết nối hay không. Giá trị hợp lệ: bất kỳ số nguyên nào .|
|WINSTAP_FAIL_CLOSE|FIREWALL_FAIL_CLOSE|0|Giá trị hợp lệ: 0: Tường lửa được kích hoạt mỗi phiên khi được kích hoạt bởi một quy tắc trong chính sách đã cài đặt. 1: Tất cả lưu lượng truy cập được theo dõi để tìm vi phạm chính sách tường lửa|
|WINSTAP_DEFAULT_STATE|FIREWALL_DEFAULT_STATE	|0|Hành động khi phán quyết không thể được đặt theo quy tắc chính sách, ví dụ: firewall_timeout hết hạn. Giá trị hợp lệ: 0 : kết nối đi qua. 1 : kết nối bị chặn. 2: Tất cả lưu lượng được theo dõi để phát hiện vi phạm chính sách tường lửa đối với các gói tin priority_count ban đầu (tham số Guard_tap.ini ). S-TAP® xem phần đầu tiên của mỗi phiên mới vào DB của bạn. Điều này hữu ích khi bạn có các chính sách dựa trên phiên, quy tắc tường lửa dựa trên người dùng hoặc một số thông tin khác được thông qua sớm trong phiên. Nó hạn chế tác động của tường lửa đến hiệu suất. Thay vì xem từng bit của phiên ( firewall_default_state = 1) và chờ kết quả KHÔNG ĐỒNG Ý, S-TAP chỉ đơn giản là tự động mở nếu không có XEM hoặc DROP nào được gửi.|
|WINSTAP_FORCE_WATCH|FIREWALL_FORCE_WATCH|Vô giá trị|Khi firewall_default_state = 0 (tắt), thì firewall_force_watch chỉ định mạng / mặt nạ của các IP mà bạn muốn tường lửa theo dõi, ghi đè mặc định (tắt). Giá trị hợp lệ: danh sách các giá trị IP / mặt nạ được phân tách bằng dấu phẩy.|
|WINSTAP_FORCE_UNWATCH|FIREWALL_FORCE_UNWATCH|Vô giá trị|Khi firewall_default_state = 1 (bật), thì firewall_force_unwatch chỉ định mạng / mặt nạ của các IP mà bạn muốn tường lửa bỏ qua, ghi đè mặc định (bật). Giá trị hợp lệ: danh sách các giá trị IP / mặt nạ được phân tách bằng dấu phẩy.|
