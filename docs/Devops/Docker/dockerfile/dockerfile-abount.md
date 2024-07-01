# Dockerfile

## Câu lệnh Dockerfile

- FROM: định nghĩa base image (có thể là ubuntu, maven, ...)
- RUN: chạy một lệnh trong quá trình build
- WORKDIR: Thiết lập đường dẫn mặc định của container
- COPY: Sao chép file hoặc thư mục vào từ HOST IMAGE
- ADD: Sao chép file hoặc thư mục vào từ HOST IMAGE
- CMD: Chỉ định lệnh nào sẽ chạy khi container khởi động
- ENTRYPOINT: Chỉ định lệnh nào sẽ chạy khi container khởi động. Lệnh này giống `CMD` nhưng không bị ghi đè bởi người dùng khi họ sử dụng docker run
- ENV: định nghĩa biến môi trường
- EXPOSE: khai báo port hoạt động