# Tổng quát về Prometheus

> Prometheus là một dịch vụ theo dõi và cảnh báo về hệ thống. Đây là một dịch vụ mã nguồn mở (Open source)


## 1. Time Series Database (TSDB)
> Là cơ sở dữ liệu tối ưu hoá cho dữ liệu chuỗi thời gian. Chuỗi thời gian là dữ liệu được thu thập và ghi lại theo thời gian, thường được sắp xếp theo thứ tự thời gian.

- TSDB rất hữu ích trong các trường hợp mà dữ liệu được thu thập liên tục và cần phân tích theo thời gian, ví dụ như giám sát hệ thống, phân tích xu hướng, dự báo, v.v.

- TSDB cung cấp một số tính năng đặc biệt để xử lý dữ liệu chuỗi thời gian, bao gồm:

    - Hiệu suất cao khi ghi và truy vấn dữ liệu: TSDB được tối ưu hóa để ghi và truy vấn dữ liệu theo thời gian, điều này giúp nó hoạt động nhanh hơn so với các loại cơ sở dữ liệu truyền thống khi làm việc với dữ liệu chuỗi thời gian.

    - Tính năng nén dữ liệu: TSDB thường có khả năng nén dữ liệu chuỗi thời gian mà không làm mất thông tin, giúp tiết kiệm không gian lưu trữ.

    - Hỗ trợ truy vấn dựa trên thời gian: TSDB cho phép bạn truy vấn dữ liệu dựa trên khoảng thời gian, điều này rất hữu ích khi bạn muốn phân tích xu hướng hoặc mô hình dữ liệu theo thời gian

- Prometheus, mà bạn đang tìm hiểu, sử dụng một TSDB nội bộ để lưu trữ các metrics mà nó thu thập.

## 2. Metrics trong prometheus

> Metrics là những dữ liệu số đo lường mà Prometheus thu thập từ các hệ thống và ứng dụng mà nó giám sát. Các metrics này cung cấp thông tin chi tiết về hoạt động và hiệu suất của hệ thống và ứng dụng.

- Metrics là số liệu được đo tại một thời điểm của hệ thống
- Đơn vị đo có thể là giá trị, mốc thời gian và định danh về một cái gì đó

### 2.1 - Các loại metrics

- Counter: Là một số liệu đại diện cho một bộ đếm có giá trị chỉ có thể tăng hoặc trở về 0 khi được khởi động lại. Không sử dụng để đếm các giá trị có thể giảm.
- Gauge: Là số liệu đại diện cho một giá trị số duy nhất, có thể tăng hoặc giảm.
- Histogram: Đếm các giá trị thường xảy ra theo các tiêu chí mà ta cấu hình, nó cung cấp một cơ chế giúp ta có thể tính tổng các giá trị của các tiêu chí đó.
- Summary: Tương tự Histogram. Nhưng là lựa chọn tốt hơn cho việc tính toán chính xác hơn.

**Hai loại metrics khác là Histogram và Summary, nhưng chúng phức tạp hơn và không được sử dụng nhiều như Counter và Gauge.**