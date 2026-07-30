---
title: "Worklog Tuần 5"
date: 2026-07-12
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Thiết kế giao diện người dùng (UI) cho ứng dụng web Cloud Media Converter and Storage.
* Xây dựng phần frontend dựa trên thiết kế UI và các yêu cầu chức năng của dự án.
* Thiết lập cấu trúc frontend và xây dựng các component có khả năng tái sử dụng.
* Xác định và triển khai các API call cần thiết để các thành viên khác có thể phát triển và tích hợp phần backend.
* Đảm bảo sự thống nhất và phối hợp hiệu quả giữa phần frontend và backend trong quá trình phát triển.

### Các công việc cần triển khai trong tuần này:
| Thứ | Ngày | Công việc | Nguồn tài liệu |
| --- | ---- | --------- | -------------- |
| 2 | 06/07/2026 | **Thiết kế Giao diện (UI):**<br>&emsp;+ Phân tích các yêu cầu chức năng của dự án và xác định những màn hình chính cần thiết cho ứng dụng web.<br>&emsp;+ Thiết kế bố cục và luồng sử dụng cho các chức năng upload file, chuyển đổi media, quản lý file và tương tác với người dùng.<br>&emsp;+ Trao đổi thiết kế với các thành viên trong nhóm và điều chỉnh dựa trên ý kiến đóng góp. |
| 3 | 07/07/2026 | **Phát triển Frontend:**<br>&emsp;+ Thiết lập và tổ chức cấu trúc của frontend project.<br>&emsp;+ Xây dựng layout chính và các component điều hướng của ứng dụng.<br>&emsp;+ Phát triển các UI component có khả năng tái sử dụng cho quy trình chuyển đổi media.<br>&emsp;+ Xây dựng giao diện upload file và hiển thị thông tin cơ bản của file. | 
| 4 | 08/07/2026 | **Phát triển Frontend và Chuẩn bị Tích hợp:**<br>&emsp;+ Tiếp tục xây dựng các trang và UI component chính.<br>&emsp;+ Xây dựng giao diện hiển thị các file đã upload và kết quả sau khi chuyển đổi.<br>&emsp;+ Bổ sung các trạng thái loading, success và error để cải thiện trải nghiệm người dùng.<br>&emsp;+ Kiểm tra lại cấu trúc frontend để chuẩn bị tích hợp với backend API. |
| 5 | 09/07/2026 | **Thiết kế API và Chuẩn bị Giao tiếp với Backend:**<br>&emsp;+ Xác định các API endpoint cần thiết cho frontend.<br>&emsp;+ Xây dựng cấu trúc request và response cho các chức năng upload file, chuyển đổi, liệt kê file và lấy file.<br>&emsp;+ Xây dựng các API call cần thiết và cung cấp đặc tả để các thành viên phụ trách backend triển khai.<br>&emsp;+ Trao đổi với thành viên backend về yêu cầu API và dữ liệu trả về. |
| 6 | 10/07/2026 | **Kiểm tra và Hoàn thiện Frontend:**<br>&emsp;+ Rà soát giao diện và phần frontend đã triển khai.<br>&emsp;+ Kiểm tra các luồng sử dụng chính và xác định các vấn đề liên quan đến giao diện.<br>&emsp;+ Điều chỉnh UI dựa trên phản hồi từ các thành viên trong nhóm.<br>&emsp;+ Kiểm tra lại API specification và đảm bảo các yêu cầu từ frontend được truyền đạt rõ ràng đến nhóm backend.<br>&emsp;+ Cập nhật worklog và tài liệu dự án. |

### Kết quả đạt được tuần 5:

* **Thiết kế Giao diện:**
  * Thiết kế giao diện người dùng chính cho ứng dụng web Cloud Media Converter and Storage.
  * Xác định luồng sử dụng chính cho việc upload media, lựa chọn định dạng chuyển đổi, theo dõi trạng thái chuyển đổi và truy cập các file đã chuyển đổi.
  * Xây dựng layout thống nhất và cấu trúc component cho phần frontend.

* **Phát triển Frontend:**
  * Thiết lập và tổ chức cấu trúc của frontend project.
  * Xây dựng layout chính và hệ thống navigation của ứng dụng.
  * Phát triển các UI component có khả năng tái sử dụng để phục vụ quy trình chuyển đổi media.
  * Xây dựng giao diện upload và quản lý các file media.
  * Bổ sung các trạng thái loading, success và error nhằm cung cấp phản hồi rõ ràng hơn cho người dùng.

* **Chuẩn bị API và Tích hợp Backend:**
  * Xác định các API operation cần thiết cho frontend.
  * Xây dựng cấu trúc request và response dự kiến cho quá trình giao tiếp giữa frontend và backend.
  * Xây dựng các API call cần thiết và mô tả cách hoạt động để các thành viên khác có thể triển khai phần backend tương ứng.
  * Trao đổi với nhóm backend để đảm bảo yêu cầu giữa frontend và backend được thống nhất.

* **Làm việc Nhóm:**
  * Phối hợp với các thành viên để đảm bảo thiết kế frontend phù hợp với kiến trúc tổng thể của hệ thống.
  * Trao đổi các yêu cầu API của frontend với các thành viên phụ trách backend.
  * Phân tách rõ hơn trách nhiệm giữa frontend và backend, giúp các thành viên có thể phát triển phần việc của mình hiệu quả hơn.

* **Tiến độ Dự án:**
  * Hoàn thành phiên bản frontend ban đầu và xây dựng nền tảng cho việc tích hợp các dịch vụ backend.
  * Chuẩn bị codebase frontend cho quá trình tích hợp API và kiểm thử chức năng trong các tuần tiếp theo.
  * Cải thiện sự thống nhất giữa thiết kế UI, phần frontend và kiến trúc backend dự kiến.

* ...