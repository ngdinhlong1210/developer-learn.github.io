# Exclusive lock và Shared lock

Phía client, hay nói cách khác là application, chúng ta tương tác với database thông qua các câu lệnh DML (INSERT/UPDATE/DELETE)… và bản chất tất cả đều được thực thi như một transaction nếu không explicit khai báo và không auto commit.

Nếu execute single query:

> UPDATE TABLE X SET COLUMN = 'Y' WHERE ID = 1;

Nó được thực thi giống như:

> **START** TRANSACTION;
> **UPDATE** **TABLE** X **SET** **COLUMN** **=** **'Y'** **WHERE** ID **=** **1**;
> **COMMIT**;

* Phía dưới database level, nó nhận các transaction và thực hiện xử lý với multi-thread. Ta biết rằng nếu xử lý multi-thread không tốt sẽ dẫn đến nhiều rủi ro không lường trước. Cách đơn giản để handle issue này là sync/lock.
* Lock cũng có nhiều loại, với bài trước ta biết một vài level locking là row-level lock, page-level lock và table-level lock. Cụ thể hơn với các concurrent read/write còn sử dụng 2 lock mode là exclusive lock và shared lock.
* Cùng đi tìm hiểu về exclusive lock và shared lock trong bài viết này nhé. Lưu ý rằng 2 loại lock này chỉ đảm bảo data integriry - tức là tính toàn vẹn dữ liệu.

## 1. SHARED LOCK

Shared lock hay còn gọi là read lock, điểm qua một vài tính chất của nó đã:

> * Được sử dụng khi một transaction muốn read data.
> * Vì chỉ cho phép read nên mọi transaction khác muốn write trong khoảng thời gian read đều không được phép.
> * Ngoài ra, shared lock cho phép nhiều transaction cùng read data.

Nhờ các tính chất trên, nó đảm bảo tính toàn vẹn dữ liệu - data integrity. Quá trình đọc diễn ra trọn vẹn, không bị cắt ngang bởi quá trình write.

## 2. EXCLUSIVE LOCK

Với exclusive lock, hay còn gọi là read-write lock, chúng có những tính chất sau:

> * Được sử dụng khi transaction muốn read và write data.
> * Chỉ duy nhất một transaction có quyền chiếm exclusive lock trên data đó.
> * Ngoài ra không có transaction nào khác có thể apply shared lock.
> * Do đó, nó ngăn chặn các transaction khác chiếm quyền trong khoảng thời gian thực thi.

![](assets/1.png)

Chỉ duy nhất shared lock có khả năng share chung với multi-transaction. Ngoài ra tất cả các kết hợp còn lại đều không thể. Đã có shared lock thì không có exclusive lock và ngược lại.

## 3. Example

Chắc hẳn với mớ lý thuyết trên, ta vẫn chưa nắm được cách thức hoạt động và trường hợp sử dụng của shared lock/exclusive lock. Phải có ví dụ mới dễ hình dung.

Table Account bao gồm rất nhiều columns, nhưng chỉ cần quan tâm đến:

> * Tên tài khoản
> * Số dư


| Name | Balance | … | … | … | … | … | … | … | … | … |
| ------ | --------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Gấu | $1000   | … | … | … | … | … | … | … | … | … |
| Thỏ | $200    | … | … | … | … | … | … | … | … | … |
| Rùa | $500    | … | … | … | … | … | … | … | … | … |

![](assets/2.png)


* Thời điểm T1, Gấu muốn nạp thêm $100 vào tài khoản. Để làm được điều đó, ta cần thực hiện query UPDATE - write data. Do vậy cần acquire exclusive lock. Việc acquire thành công vì chưa có lock nào trên data của Gấu. Nếu một transaction khác muốn acquire shared lock để read data thì sao? Data đó có thể không chính xác vì lý do half-written. Muốn read không được, write thì càng không được. Vậy nên không cho phép bất kì exclusive lock hay shared lock nào khác được apply trên data đã có exclusive lock.
* Đến thời điểm T2, transaction xử lý thành công. Lúc này tài khoản của Gấu tổng cộng là $1100. Không có vấn đề gì xảy ra.
* T3, Gấu tiếp tục thực hiện một longgg transaction để… read data thôi. Hơi lâu, chắc smell code, nhưng kệ nó đi. Do chỉ read data nên acquire shared lock, chưa có lock nào nên acquire thành công. Với shared lock, Gấu ngầm nói rằng đứa nào muốn đọc thì đọc, nhưng đừng có write data nhé. Tao đang đọc $1100, đứa nào modify làm tao đọc lỗi (half written) thì cứ cẩn thận. Đó là lý do đã shared lock thì không thể exclusive lock.
* Đến T4, Thỏ kiểm tra số dư tài khoản để tối nay đi chơi với Sói - đôi bạn thân mến thân. Lúc này Thỏ acquire shared lock trên account của nó và acquire thành công vì chưa có lock nào, mà cũng không liên quan gì đến account của Gấu.
* T5, bạn Rùa hay tin tối nay Thỏ đi chơi với Sói nên hào hiệp chuyển ít tiền cho Thỏ… Chắc chắn là phải thực hiện query UPDATE - write data, acquire exclusive lock trên account của Thỏ nhưng tất nhiên sẽ faillllll… vì đã tồn tại shared lock zoài. Muốn làm người tốt cũng không dễ ::joy::. Thỏ đang read data và không muốn ai modify data đó cả, đọc nhầm thì… bỏ m.
* Đúng là Rùa, luôn kiên trì và nỗ lực. Rùa không bỏ cuộc, chờ đến thời điểm T6 khi Thỏ đã check xong account, Rùa acquire exclusive lock, chuyển cho Thỏ $200. Lần này chắc chắn là thành công rồi.

Clear hơn về cách sử dụng của shared lock và exclusive lock rồi đúng không. Cơ bản, các loại lock đều hướng đến mục đích đảm bảo tính data integrity, các dữ liệu cần được nguyên vẹn.

> * Với shared lock: khi read data, ta muốn data đó nguyên vẹn không bị thay đổi từ lúc bắt đầu đọc cho đến khi kết thúc.
> * Với exclusive lock: khi write data, ta không muốn bất kì một ai có thể xen vào giữa quá trình này kể cả là read data.

Lưu ý lại lần nữa, 2 loại lock trên chỉ đảm bảo data integrity, không đảm bảo data consistency. Vậy làm thế nào để đảm bảo data consistency, đón chờ phần sau nhé.
