# Giới thiệu về SSL

## Mục lục

[1. SSL là gì](#item-one)

[2. SSL hoạt động](#item-two)

<a id="item-one"></a>
### 1. SSL là gì

> SSL (Secure sockets layer) là một giao thức bảo mật dùng để mã hoá dữ liệu được truyền đi giữa hai hệ thống

- Một ví dụ phổ biến nhất về hai hệ thống giao tiếp với nhau mà có sử dụng SSL là giao tiếp giữa trình duyệt và máy chủ web. Nếu ta truy cập một trang web mà ta thấy giao thức của nó là HTTP, thì giao tiếp giữa trình duyệt và máy chủ đang không được bảo mật, dữ liệu đang được truyền đi theo dạng văn bản thô. Còn nếu ta truy cập một trang web mà thấy giao thức của nó là HTTPS, có nghĩa là nó đang có xài SSL và dữ liệu truyền đi giữa trình duyệt và máy chủ đã được mã hóa.


    ![SSL](assets/SSL-about.png)

- TLS (Transport Layer Security) là phiên bản mới hơn của SSL, và hiện nay thì hầu hết mọi giao thức HTTPS đều thực hiện thông qua TLS, nhưng vì thói quen nên mọi người vẫn gọi là SSL.

<a id="item-two"></a>
### 2. SSL hoạt động

- Trước khi tìm hiểu về cách SSL hoạt động, ta cần tìm hiểu trước về hai khái niệm sau: Asymmetric Cryptography và Symmetric Cryptography. Đây là hai cách mã hóa dữ liệu mà SSL sử dụng:

    - **Asymmetric Cryptography**
        - Asymmetric Cryptography hay còn gọi Public Key Cryptography là cách mã hóa dữ liệu sử dụng một cặp khóa (key) Public Key và Private Key.

        - Với Public Key là key sẽ được chia sẻ ra bên ngoài cho ai muốn giao tiếp, còn Private Key là key bảo mật được giữ ở máy chủ và không được chia sẻ.

        - Khi giao tiếp thì bên gửi sẽ dùng Public Key để mã hóa dữ liệu, và khi dữ liệu được gửi tới thì bên nhận sẽ dùng Private Key để giải mã dữ liệu.

    Asymmetric Cryptography
    ![Asymmetric Cryptography](assets/asymmetric-cryptography.png)


    - **Symmetric Cryptography**
        - Symmetric Cryptography cũng là cách mã hóa dữ liệu giống Asymmetric Cryptography, chỉ khác ở điểm là thay vì sử dụng một cặp khóa thì nó chỉ sử dụng duy nhất một khóa cho cả việc mã hóa và giải mã dữ liệu.

    ![Symmetric Cryptography](assets/symmetric-cryptography.png)

- SSL xử lý dữ liệu
    - SSL sử dụng cả Asymmetric và Symmetric cho việc mã hóa dữ liệu, việc giao tiếp giữa hai hệ thống sử dụng SSL sẽ có hai bước như sau: SSL handshake và Data Transfer.

    - Asymmetric Cryptography được sử dụng trong bước SSL handshake. Symmetric Cryptography được sử dụng cho việc truyền dữ liệu sau bước SSL handshake.

![SSL data](assets/SSL-data.png)


- SSL Handshake
    - Ta sẽ lấy ví dụ giao tiếp giữa trình duyệt và máy chủ web.

    - Kết nối SSL giữa hai hệ thống sẽ bắt đầu với SSL handshake sử dụng Asymmetric Cryptography. Bước SSL handshake này là để trình duyệt xác thực SSL với máy chủ. Quá trình như sau, khi ta nhâp địa chỉ HTTPS vào trình duyệt:

        - Trình duyệt gửi một thông điệp với nội dung là “client hello” tới máy chủ
        - Máy chủ sẽ trả lời với nội dung là “server hello”, trong đó chứa thông tin chứng thực SSL và Public Key của SSL đó
        - Trình duyệt sẽ xác nhận thông tin chứng thực SSL có đúng là hàng thật hay không, nếu xác nhận thành công thì trình duyệt sẽ tạo ra một Session Key
        - Session Key này sẽ được mã hóa bằng Public Key và được gửi tới máy chủ
        - Máy chủ sẽ nhận Session Key đã được mã hóa này, và dùng Private Key để giải mã nó và lưu Session Key này lại, sau đó nó sẽ trả về tín hiệu cho trình duyệt là đã nhận được Session Key

    ![SSL handshake](assets/ssl-handshake.png)
    - Kết thúc quá trình SSL handshake thì cả trình duyệt và máy chủ đều có Session Key, đây là Key mà sẽ được sử dụng để mã hóa và giải mã dữ liệu trong quá trình giao tiếp của hai hệ thống về sau.

- Data Transfer
    - Đây là quá trình truyền dữ liệu giữa hai hệ thống, Symmetric Cryptography sẽ được sử dụng ở bước này, cả hai đều sử dụng Session Key để mã hóa và giải mã dữ liệu.

    ![data transfer](assets/data-transfer.png)