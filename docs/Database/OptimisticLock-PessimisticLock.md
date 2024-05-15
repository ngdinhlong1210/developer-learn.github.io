# Optimistic lock và Pessimistic lock

- Với việc read/write data với multi-thread có thể dẫn đến data race, vấn đề nhỏ nhưng hậu quả lớn. khiến chương trình sai lệch nghiêm trọng

=> sử dụng các cơ chế mutual exclusion là giải quyết được vấn đề này.


> Optimistic concurrency control và Pessimistic concurrency control là hai khái niệm trong database nói đến cách xử lý write data với multi-session/multi-transaction

## 1. Pessimistic lock

> **Pessimistic concurrency** control hay **pessimistic lock** đều diễn tả về cơ chế giải quyết xung đột khi có nhiều transaction cùng thay đổi dữ liệu trên một hoặc một tập các records.

Ví dụ: 
Giả dụ có 2 dữ liệu được gửi insert vào chung 1 table cùng lúc. Lúc này, dữ liệu nào được gửi vào table trước sẽ được xử lý trước, và dữ liệu sau sẽ phải chờ cho đến khi dữ liệu đầu hoàn thành xử lý. Nếu có nhiều dữ liệu được gửi cùng lúc thì nó sẽ chờ lần lượt cho các dữ liệu hoàn thành xong lần lượt


* Có thể hiểu pessmistic lock hoạt động như sau: 
  - Khi transaction T1 start và modify data, nó sẽ thực hiện lock row, set of row hoặc table tùy thuộc vào điều kiện query. Các transaction Tx sau không thể modify data trên row đó mà bắt buộc phải chờ cho đến khi T1 hoàn thành.
  - Nhược điểm của pessimistic lock là toàn bộ các transaction sau phải chờ cho đến khi transaction trước đó hoàn thành. Nếu chưa hoàn thành thì… tiếp tục chờ đợi.
  - Tuy nhiên, nhược điểm trên cũng chính là ưu điểm của pessimistic lock. Do chỉ có duy nhất một transaction thực hiện write nên sẽ tránh conflict data với các transaction còn lại.

* Cơ chế sử dụng pessimistic lock bao gồm 3 phase:

  - Xác định loại lock cần sử dụng: exclusive lock, shared lock…
  - Xây dựng cơ chế quản lý lock.
  - Xác định quy trình sử dụng lock cho các transaction.

* Với pessimistic lock, về cơ bản toàn bộ quá trình update diễn ra như sau:
  - Acquire lock.
  - Update data.
  - Release lock.


* Hãy tưởng tượng quá trình update data diễn ra rất lâu, hoặc trước khi release lock lại thực hiện một load read data khác lâu không kém thì các transaction khác nếu update cùng data phải chờ mốc mỏ mới được thực thi. Thậm chí còn dẫn đến deadlock nếu transaction update data không release lock.


## 2. Optimistic lock

* Ta thấy nhược điểm rất lớn của pessimistic lock liên quan đến vấn đề chờ đợi… một khi đã chờ đợt thì rất bực mình. Thà là cho vào… ngắm cái rồi đuổi về cũng được, đằng này cứ bắt chờ.
* Optimistic lock linh hoạt hơn pessimistic lock, cho phép tất cả được vào nhưng… chỉ có một con duy nhất chui vào trứng thành công

Ví dụ:
Vẫn là cuộc đua giữa Rùa và Thỏ và bác Gấu là người canh giữ ngôi đền bí mật. Thỏ nhanh chân hơn đến trước, bác Gấu phát cho Thỏ tấm thẻ chữ X để vào ngôi đền. Rùa chậm hơn đến sau nhưng cũng được phát cho tấm thẻ tương tự vào trong. Do Thỏ mải chơi ngắm nghía nên quên nhiệm vụ chính. Rùa mặc dù đến sau nhưng tập trung tìm kim cương nên lấy được trước. Rùa ra khỏi cửa trả cho bác Gấu tấm thẻ X, bác Gấu kiểm tra với tủ khóa hiện tại và chưa có ai trả khóa X cả. Bác gấu sau đó cập nhật khóa X lên Y và cho phép Rùa ra khỏi ngôi đền. Thỏ mải chơi ra sau trả thẻ cho bác Gấu. Lúc này khóa mới là Y, không khớp với thẻ của Thỏ. Bác Gấu phát mới cho Thỏ thẻ Y để làm lại nhiệm vụ nếu muốn tiếp tục cuộc chơi.

Lúc này, người đến ngôi đền trước chưa chắc đã là người chiến thắng. Kẻ chiến thắng là người lấy được viên kim cương và ra khỏi ngôi đền đầu tiên.



* Cách hoạt động của optimistic lock tương tự với ví dụ trên. Thay vì lock row trong quá trình update như pessimistic lock, optimistic lock chỉ lock khi commit việc update.

* Cơ chế update data với optimistic lock diễn ra như sau:

  - Fetch data kèm theo version hiện tại. Tất cả các transaction đều có thể fetch data mà không lo ngại vấn đề blocking.
  - Update data, đồng thời thêm một version mới.
  - Commit transaction. Bây giờ mới là lúc acquire lock. Bác Gấu kiểm tra version cũ của record đó có trùng với version hiện tại mà bác Gấu biết không. Nếu đúng thì cho phép update, đồng thời cập nhật version mới của data. Sau đó release lock. Nếu sai version thì… tất nhiên rồi, lệnh update không thành công.

* Hóa ra vẫn là lock, chỉ là chuyển từ vị trí này sang vị trí khác mà thôi. Tuy nhiên việc chuyển dịch đó cũng là ưu điểm to lớn mà optimistic lock đem lại. At least, cost cho blocking đã giảm kha khá. Optimisic lock sẽ block để compare version nên diễn ra rất nhanh, thay vì block toàn bộ row/table để chờ quá trình update hoàn thành.

* Nhanh chưa hẳn đã tốt, đặc biệt là các anh có vợ nhanh quá còn bị ăn… chửi. Nhược điểm chết người của optimistic lock nằm ở việc update data fail do sai version:

  - Retry, retry và retry ở application level. Thỏ phải request bác Gấu cấp một thẻ bài mới ứng với version mới, sau đó tiếp tục công cuộc tìm kiếm kim cương nếu vẫn muốn về đích.
  - Với bài toán UPDATE đi kèm WHERE condition. Nó là cả một sự phức tạp vì ban đầu việc UPDATE đó được phép và lỡ trigger một function nào đó. Tuy nhiên đến lúc COMMIT thì mới phát hiện ra sai version.
  - Ngoài ra, optimistic lock chỉ verify trên các update operation nên việc read vẫn có thể dẫn đến inconsistence data. Cụ tỉ thế nào chờ bài sau nhé.

* Pessimistic lock khá đơn giản để implement, chỉ cần thực hiện lock row/set of row/table là ok. Tuy nhiên với optimistic lock sẽ phức tạp hơn, không hẳn là phức tạp mà là có nhiều cách để implement dựa trên việc quản lý version của record:

  - Time-based update detection: dựa trên giá trị time update của column để xác định version của data.
  - Implicit hidden column: tạo một column mới do database quản lý để lưu version.

## 3. OPTIMISTIC LOCK HAY PESSIMISTIC LOCK

- Optimistic lock: áp dụng với case có xác suất conflict transaction thấp, cực cực thấp để giảm việc retry.
- Pessimistic lock: áp dụng với case có xác suất conflict transaction cao để đảm bảo data consistence và cũng giảm thiểu retry.