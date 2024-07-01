# Các lệnh linux

# Cài đặt user
adduser <nameuser>  # thêm user 
-----------------
useradd <nameuser>  # thêm user nhưng được chọn nh chức năng hơn, có thể dùng để đăng nhập 
-----------------
vi /etc/passws      # xem thông tin các user
-----------------
deluser <nameuser>  # xoá user
-----------------
groupadd <namegroup>    # thêm group
-----------------
delgroup <namegroup>    # xoá group
-----------------
usermod -aG [groupname] [nameuser] # thêm người dùng vào group
-----------------
deluser [groupname] [nameuser]      # xoá user khỏi group


# Phân quyền