# So sánh Reverse proxy và Forward proxy

[1.Forward proxy là gì?](#whatisforwardproxy)

[2.Reverse proxy là gì?](#whatisreveseproxy)

[3.Reverse proxy và Forward proxy](#reveseproxy&forwardproxy)

# <a name="whatisforwardproxy">1.Forward proxy là gì?</a>

- Forward Proxy thường được gọi tắt luôn là **proxy**. Chúng là loại proxy server được dùng phía client

- Khi sử dụng forward proxy, các requests phía client sẽ tới proxy server và proxy server sẽ chuyển tiếp các requests này tới Internet (đại khái là khi gửi request tới server, ta phải chuyển trước qua proxy để ẩn đi IP, thông tin, .. trước khi gửi tới server). Tác dụng của Forward proxy:
    - Ẩn địa chỉ IP của client khi truy cập tới các website trên internet do phía các website chỉ có thể biết được địa chỉ của forward proxy server.
    - Bypass firewall restriction để truy cập các website bị chặn bởi công ty, chính phủ, bla bla.
    - Dùng trong công ty, tổ chức để chặn các website không mong muốn, quản lý truy cập và chặn các content độc hại.
    - Sử dụng làm caching server để tăng tốc độ.

Ví dụ: Giả dụ 1 website từ nước ngoài chặn các IP tới từ Việt Nam, ta sẽ sử dụng Proxy như 1 nơi để ẩn thông tin IP, quốc gia, thông tin, ... 

# <a name="whatisreveseproxy">2.Reverse proxy là gì?</a>

- Thay vì dùng ở phía client như là Forward Proxy thì Reverse Proxy sẽ được dùng ở phía server.

- Requests sẽ đi từ client tới proxy server và sau đó proxy server sẽ chuyển tiếp các requests này tới server backend. Tác dụng của Reverse Proxy bao gồm:

    - Load balancing: giúp điều phối requests tới các servers backend để cân bằng tải, ngoài ra nó còn giúp hệ thống đạt tính sẵn sàng cao khi lỡ không may có server bị ngỏm thì nó sẽ chuyển request tới một server còn sống để thực thi.
    - Increased Security: Reverse Proxy còn đóng vai trò là một lớp bảo vệ cho các servers backend. Nó giúp cho chúng ta có thể ẩn đi địa chỉ và cấu trúc thực của server backend.
    - Logging: Tất cả các requests tới các servers backend đều phải đi qua reverse proxy nên việc quản lý log của access tới từng server và endpoint sẽ dễ dàng hơn rất nhiều so với việc kiểm tra trên từng server một.
    - Encrypted Connection: Bằng việc mã hóa kết nối giữa client và reverse proxy với TLS, users sẽ được hưởng lợi từ việc mã hóa dữ liệu và bảo mật với HTTPS.

# <a name="reveseproxy&forwardproxy">3.Reverse proxy và Forward proxy</a>

- Khác biệt lớn nhất giữa hai loại proxy này là forward proxy được sử dụng bởi client (ví dụ như trình duyệt). Trong khi đó, reverse proxy được sử dụng bởi server (ví dụ như web server). Forward proxy có thể nằm trong một mạng nội bộ cùng với client hoặc cũng có thể công khai trên Internet.

- Hay nói một cách dễ hiểu hơn, forward proxy đại diện cho client, còn reverse proxy đại diện cho server.