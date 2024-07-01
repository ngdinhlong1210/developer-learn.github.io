# Giới thiệu về Vagrant

## 1. Vấn đề
- Giả sử khi vào một dự án, ta cần cài đặt máy ảo và rất nhiều phần mềm để sử dụng. Nhưng với dự án khoảng 100 người, và 100 người đều phải bắt đầu cài từ đầu: cài ubuntu, docker, jdk, maven,..... => Việc này sẽ làm việc cài đặt dự án bị chậm đi, phức tạp. Vì vậy ta cần phải có 1 file cấu hình những thứ cần cài đặt và sau đó ta chỉ việc chạy file là máy ảo và các phần mềm sẽ được cài đặt (nghe khá giống docker nhưng sử dụng trên máy ảo)

=> Chính vì sự phức tạp đó, vagrant ra đời làm giảm đi sự phức tạp đó. vagrant có thể chia sẻ file đến cho mọi người và các dev khác chỉ việc bung file đó ra là sẽ có đầy đủ máy ảo và các phần mềm cần thiết


## 2. Vagrant là gì

> Là một công cụ xây dựng và quản lý môi trường máy ảo chạy trên Linux, Windows và MacOS

