# Cài đặt IP tĩnh của ubuntu

- Khi cài đặt máy ảo vmware, ta sẽ được cấp DHCP IP => khi tắt máy bật lại sẽ bị thay đổi địa chỉ IP => cần cài đặt lại địa chỉ IP tĩnh

- Các bước
```
sudo -i  #vao root

vi /etc/netplan/00-installer-config.yaml  ## cai dat dia chi ip tinh cho server

# Chỉnh dcpp4 về false cho việc cấp IP động k được thực hiện

# Thêm 1 đoạn ngay dưới dòng dhcp4

addresses: [<IP mong muốn>]
gateway4: 192.168.1.1    # chú ý thêm nếu sử dụng là mạng NAT thì ta vào Edit -> Virtual Machine network của vmware lấy giá trị gateway và IP cũng vậy
nameservers:
    addresses: [8.8.8.8, 8.8.4.4]

```