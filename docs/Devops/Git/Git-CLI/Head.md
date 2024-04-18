# HEAD

## 1. HEAD là gì 
- Thể hiện cho vị trí commit hiện tại (hoặc branch hiện tại) đang làm việc
- Bình thường `HEAD` trỏ tới tên nhánh. Khi bạn commit, trạng thái của branch được thay đổi này được thấy thông qua `HEAD`
- Có thể check hiện tại HEAD đang ở đâu bằng lệnh `cat .git/HEAD`
- Nếu đang ở nhánh `main` hiện tại, `HEAD` sẽ luôn ẩn mình dưới nhanh `main`


https://github.com/ngdinhlong1210/docs-devops/assets/146752374/b3839de6-9808-424a-a241-3b94e99efe05

- Trong thực tế, việc dùng HEAD với mã băm (hash) không hề thuận tiện nên ta thường sử dụng 1 số chữ cái đầu hash commit 
- Sử dụng tham chiếu tương đối cũng là một cách thay thế cho việc sử dụng hash
    - Dịch chuyển lên 1 commit với `^`. Ví dụ: `main^` là commit trước của `main`, `main^^` là 2 commit trước của main
    - Dịch chuyển lên nhiều commit với `~(number)`. Ví dụ `~3` là 3 commit trước commit (hoặc nhánh) hiện tại
    
- Ngoài ra, ta có thể trực tiếp gán lại nhánh cho commit với cú pháp `-f`(force)

    `git branch -f main HEAD~2`: dịch chuyển ép buộc nhánh main lên 3 commit phía trên `HEAD`
