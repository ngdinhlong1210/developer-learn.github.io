# Bind Mounts

- Khi bạn sử dụng bind mount, file hoặc thư mục trong `host machine` sẽ được gắn liền với container. Tệp hoặc thư mục được tham chiếu bằng đường dẫn tuyệt đối. Vậy nên trong trường hợp file hoặc folder này không tồn tại trên docker host thì quá trình mount sẽ bị lỗi
- Khi sử dụng `volume`, thư mục mới được tạo trong thư mục lưu trữ của docker trên máy chủ docker và docker quản lý nội dung của thư mục đó

## Chọn flag `-v` hay `--mount`

- Chạy 1 container với bind mount theo 2 cách

  - Sử dụng flag -v: khi sử dụng flag `v` nếu source folder trên docker host chưa tồn tại, Docker sẽ tự động tạo mới folder
  - Sử dụng flag -mount: khi sử dụng flag `mount` phải đảm bảo folder trên docker host đã tồn tại nếu không sẽ bị lỗi
- Nhìn chung thì --mount rõ ràng & cụ thể hơn. Sự khác biệt lớn nhất giữa `-v` và `--mount` là trong khi cú pháp của -v gộp tất cả option vào 1 trường còn --mount lại TÁCH chúng ra riêng:

  - `v` hoặc `--volume`: chứa 3 trường, được phân tách bởi dấu `(:)`. Thứ tự các trường phải đúng thứ tự và ý nghĩa của các trường cũng không rõ ràng:

    - Trường đầu tiên là đường dẫn tới file hoặc thư mục trong host machine
    - Trường thứ hai là đường dẫn nơi file hoặc thư mục được mount tới container
    - Trường thứ 3 là 'optional', các tùy chọn cách nhau bởi dấu phẩy (,)
  - `--mount`: bao gồm nhiều cặp `key-value`, ngăn cách bởi dấu `(,)`, thứ tự của các cặp key không quan trọng:

    - `type`: có thể là `bind`, `volume`, `tmpfs`
    - `source`: với `bind mount`, đây là đường dẫn tới file hoặc thư mục trong docker daemon host
    - `destination` (dst hoặc target): là đường dẫn nơi chứa tập tin hoặc thư mục sẽ được mount vào trong container
    - `readonly`: option, làm cho liên kết gắn kết được gắn vào container dưới dạng chỉ đọc.

Một số chú ý với binds mount:

- Khi sử dụng bind mounts và flag –mount thì phải đảm bảo file hoặc folder từ docker host đã được tồn tại.
- Không giống như volume, nếu folder trong Container “không trống” và được mount với folder của docker host thì tất cả các file trong folder của container sẽ bị ẩn đi. Điều này giống với khi bạn save dữ liệu của mình trong /mnt, sau đó cắm USB và mount USB với thư mục /mnt thì những file dữ liệu có từ trước sẽ bị ẩn đi đến khi USB được umount. Để test trường hợp này mình có một ví dụ sau:
