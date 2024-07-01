# Cài đặt vagrant

## Các lệnh vagrant cơ bản

> vagrant init  # tạo VagrantFile mới

> vagrant up    # thực hiện tạo máy ảo

> vagrant ssh   # truy cập vào máy ảo

> vagrant halt  # dừng máy ảo (shutdown)

> vagrant relad # chạy lại máy ảo có cập nhật lại cấu hình từ Vagrantfile

> vagrant destroy # xoá máy ảo

## 1. Cài đặt với windows

- Tải file ở trang https://www.vagrantup.com/


- Cài đặt máy ảo (có thể là virtual box hoặc vmware)
    - Với vmware ta phải cài thêm phần mềm Vagrant Vmware Utility
    - Mặc định khi chạy nó sẽ chạy với virtual box

- Sau đó ta thêm file như sau

```
Vagrant.configure("2") do |config| 				#Khai báo máy ảo
  config.vm.box = "ubuntu/trusty64"			# Tạo máy ảo ubuntu-20.04 lts
  config.vm.provider "virtualbox" do |vb|		# Máy ảo dùng virtualbox và cấu hình tài nguyên
	vb.name = "server-ubuntu"				# Tên máy ảo
	vb.cpus = 1									# Cấp máy ảo 1 core CPU
	vb.memory = "2048"							# Cấp máy ảo 2GB ram
  end											# Kết thúc cấu hình tài nguyên
end												# Kết thúc cấu hình tạo máy ảo
```

**Đọc thêm về nhiều cấu hình file Vagrant tại đây: https://devhints.io/vagrantfile** 

- Cuối cùng ta sử dụng `vagrant up`

- Cuối cùng ta dùng lệnh `vagrant ssh` truy cập thông qua ssh, pass mặc định sẽ là `vagrant`

## 2. Cài đặt với linux

- Cài đặt vagrant
> sudo apt update && sudo apt upgrade

> sudo apt-get -y install vagrant

> vagrant --version

- Cài đặt virtual box
> sudo apt update && sudo apt upgrade

> sudo apt install virtualbox

> vboxmanage --version

- Ta tạo file config máy ảo vagrant

```
Vagrant.configure("2") do |config| 				#Khai báo máy ảo
  config.vm.box = "ubuntu/trusty64"			# Tạo máy ảo ubuntu-20.04 lts
  config.vm.provider "virtualbox" do |vb|		# Máy ảo dùng virtualbox và cấu hình tài nguyên
	vb.name = "server-ubuntu"				# Tên máy ảo
	vb.cpus = 1									# Cấp máy ảo 1 core CPU
	vb.memory = "2048"							# Cấp máy ảo 2GB ram
  end											# Kết thúc cấu hình tài nguyên
end												# Kết thúc cấu hình tạo máy ảo
```

- Sau đó mở terminal chạy

> vagrant up

- Cuối cùng ta truy cập thông qua ssh, pass mặc định sẽ là `vagrant`

> vagrant ssh