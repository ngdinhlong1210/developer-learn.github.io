# Thuộc tính ACID trong Hệ thống cơ sở dữ liệu

> ACID là tính chất bao gồm 4 đặc tính khác nhau áp dụng cho một database transaction

- 4 tính chất đó là:
  - Atomicity (tính nguyên tử)
  - Isolation (độc lập)
  - Durability (bền vững)
  - consistency (nhất quán)

## 1. Tính nguyên tử

- Có nghĩa là tất cả hoặc không có, ví dụ:
  > Một ứng dụng sẽ chèn 30 bản ghi trong một giao dịch. Trong quá trình chèn này, bất kỳ sự cố nào xảy ra và tại thời điểm này, chỉ có 12 bản ghi được xử lý. Trong giao dịch trạng thái này sẽ không chỉ chèn 12 bản ghi mà nó sẽ khôi phục toàn bộ giao dịch này, vì vậy điều này sẽ xử lý tất cả hoặc không.
  >

## 2. Tính nhất quán:

- Nghĩa là đưa cơ sở dữ liệu từ trạng thái hợp lệ này sang trạng thái hợp lệ khác.

> Luôn luôn phải xác định một số quy tắc dữ liệu, ràng buộc, kích hoạt ở cuối cơ sở dữ liệu cũng như cuối ứng dụng.
>
> Bất kỳ dữ liệu nào sẽ được chèn vào, tất cả chúng phải được xác thực bằng cách thiết lập các quy tắc và đảm bảo rằng không có dữ liệu không hợp lệ nào sẽ được chèn vào cơ sở dữ liệu, do đó, bằng cách này nó sẽ quản lý tính nhất quán của cơ sở dữ liệu..
> Trong mọi trường hợp giao dịch đang chạy vi phạm quy tắc đồng thời toàn bộ giao dịch sẽ bị khôi phục.

## 3. Tính độc lập

- Có nghĩa là mỗi giao dịch không biết về một giao dịch khác.

> Một người bán tại cửa hàng đang bán rất nhanh các mặt hàng và lượng hàng cũng đang giảm dần. Đồng thời, một người khác cũng đang thêm một mặt hàng mới trong kho.
>
> Ở đây, cả hai giao dịch này là khác nhau và không biết về nhau.
>
> Sự cách ly level ensures that one transaction is not interrupted by another transaction.
>
> For database transaction, this one of the important properties because any database system is going with lots of concurrent and parallel transactions where Sự cách ly property is very much required and ensure that all transactions are defined under proper isolation level.
>
> A different database technology has different type of default Sự cách ly level like,
>
> Oracle có READ_COMMITTED
>
> MySQL có REPETABLE_READ
>
> MSSQL có READ_COMMITTED
>
> PostgreSQL có READ_COMMITTED
>
> DB2 có READ_COMMITTED
>
> Read_committed Sự cách ly level is most preferable, but many times it’s also required to show READ_UNCOMMITTED data in a data history kind of pages.

## 4. Độ bền: 
- Có nghĩa là giữ cho dữ liệu đã cam kết mãi mãi.

> Ứng dụng đã chèn 30 bản ghi trong một giao dịch và giao dịch này được hoàn tất và cam kết thành công trong cơ sở dữ liệu có nghĩa là các bản ghi sẽ tồn tại mãi mãi trong cơ sở dữ liệu cho đến khi và trừ khi nó không bị xóa bởi bất kỳ người dùng ứng dụng hoặc người dùng cơ sở dữ liệu nào.