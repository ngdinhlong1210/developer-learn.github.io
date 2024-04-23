# DHCP - Dynamic Host Configuration Protocol

> Là giao thức tiêu chuẩn dùng để cấp IP cho thiết bị. Ngoài ra nó đảm bảo không có trường các thiết bị trong cùng một mạng được cấp IP giống nhau


## Phương thức hoạt động của DHCP

- DHCP hoạt động theo cơ chế *Client-Server*. Tức là cần một thiết bị đóng vai trò làm DHCP server (Thiết bị này sẽ quản lý và cung cấp IP cho các thiết bị trong mạng, thường các thiết bị làm DHCP server sẽ là router, switch, máy chủ, ..)

- Khi cấp phát IP thông qua DHCP Server, DHCP Server phải cùng một lớp mạng với client thì client mới có thể gửi gói tin *DHCP DISCOVER* được

![DHCP](assets/DHCP.png)

- Các bước:
    - Đầu tiên khi client (các thiết bị mạng) bắt đầu kết nối, Client sẽ gửi gói tin *DHCP DISCOVER* để kiểm tra xem có DHCP server nào trong mạng hay không
    - Nếu có DHCP server trong mạng, client sẽ xin một địa chỉ IP chưa được sử dụng
    - Tiếp theo, máy chủ DHCP sẽ tìm địa chỉ IP khả dụng rồi cung cấp cho thiết bị. Thông tin IP sẽ được trả về thông qua gói *DHCP OFFER*
    - Sau khi nhận được địa chỉ, client sẽ phản hồi với máy chủ bằng một gói tin *DHCP REQUEST* yêu cầu sử dụng địa chỉ mạng IP này
    - Cuối cùng, máy chủ sẽ gửi tin báo nhận (ACK) xác nhận thiết bị đã được chấp thuận với IP và thời gian sử dụng IP đến khi có địa chỉ mới


