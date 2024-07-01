# Cài đặt Kong API Gateway

## I. Cài đặt với docker

- Trước hết, ta nên khởi tạo một network riêng cho kong vì khi cài đặt kong phải sử dụng `kong database` và `kong gateway`

> docker network create kong-api


Sau đó sử dụng như file Docker-compose hoặc cài đặt như link dưới đây [Kong API Documentation](https://docs.konghq.com/gateway/latest/)