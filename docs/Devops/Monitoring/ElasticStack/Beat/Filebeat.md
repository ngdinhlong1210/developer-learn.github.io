# Giới thiệu về FileBeat

## Tổng quan

> Filebeat gửi và quản lý tập trung các log data. Khi cài đặt Filebeat như một người quản lý cho server, Filebeat sẽ giám sát các tệp nhập ký do bạn chỉ định, giám sát các log events và gửi log đó tới `ElasticSearch` hoặc `LogStash`

> Cách hoạt động của Filebeat: Khi chạy Filebeat, nó sẽ bắt đầu giám sát nơi mà bạn đã config để theo dõi log data. Với mỗi file log mà Filebeat định vị, Filebeat sẽ khởi tạo một trình thu thập gửi data tới libbeat - nơi tổng hợp các sự kiện và gửi dữ liệu tổng hợp đến đầu ra mà bạn đã cấu hình cho Filebeat

![Filebeat](../assets/filebeat.png)


- Filebeat bao gồm 2 thành phần chính: `inputs` và `harvesters` (thu thập)
### Harvesters

`Harvesters` chịu trách nhiệm đọc content của file. Việc thu thập này sẽ qua từng file, từng dòng và gửi dữ liệu đến cho `output`
- Một `Harverters` được khởi tạo cho từng file
- Nếu file bị sửa tên hoặc bị xoá đi trong lúc `Beat` đang thu thập, Filebeat sẽ tiếp tục đọc file (điều này có thể sẽ lock lại bộ nhớ đang sử dụng cho tới khi quá trình thu thập được đóng lại)
- Ngược lại, nếu file được xoá hoặc đổi tên khi tiến trình thu thập (harvester) đóng, quá trình thu thập sẽ dừng lại
- Mặc định, Filebeat sẽ giữ file được mở cho tới khi `close_inactive` là true
  

### Input

Input chịu trách nhiệm quản lý các tiến trình and tìm tất cả các nguồn để đọc dữ liệu
- Nếu input type là `log`, input sẽ tìm tất cả các file log trong ổ đĩa khớp với đường dẫn đã cho và khởi động 1 trình thu thập log cho mỗi tệp
- Ví dụ
```
filebeat.inputs:
- type: log
  paths:
    - /var/log/*.log
    - /var/path2/*.log
```

- Các định dạng input type hiện đang được hỗ trợ: [Input type filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-options.html#filebeat-input-types)
- 