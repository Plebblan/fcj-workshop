---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Tổng quan

## Giới thiệu

Cloud Converting Media là quy trình chuyển đổi, mã hóa và tối ưu hóa nội dung đa phương tiện (video, audio, hình ảnh) bằng các dịch vụ đám mây. Trong workshop này, chúng ta sẽ tìm hiểu cách xây dựng pipeline chuyển đổi media an toàn, tự động và có thể mở rộng bằng cách sử dụng storage, compute, event trigger và phân phối nội dung.

## Mục tiêu workshop

* Hiểu kiến trúc chuyển đổi media trên nền tảng cloud.
* Triển khai workflow upload, chuyển đổi và lưu trữ đầu ra.
* Tối ưu chất lượng và định dạng media cho nhiều nền tảng.
* Bảo vệ nội dung bằng IAM, VPC Endpoint và chính sách truy cập.

## Lợi ích chính

* **Mở rộng linh hoạt:** Xử lý nhiều file media đồng thời mà không cần đầu tư hạ tầng tại chỗ.
* **Tự động hóa:** Kích hoạt chuyển đổi media bằng sự kiện upload hoặc lịch trình.
* **Phân phối nhanh:** Sử dụng CDN để phục vụ nội dung đã chuyển đổi với độ trễ thấp.
* **Tiết kiệm chi phí:** Chỉ trả tiền cho tài nguyên sử dụng thực tế và xóa file tạm khi không cần thiết.

## Kiến trúc cơ bản

Một hệ thống Cloud Converting Media thường gồm các thành phần:

1. **Media source:** File media upload vào storage như Amazon S3.
2. **Event trigger:** Sự kiện upload hoặc API call kích hoạt workflow.
3. **Media conversion:** Dịch vụ chuyển mã hoặc compute instance thực hiện mã hóa và tạo các định dạng đầu ra.
4. **Output storage:** Lưu trữ file đã chuyển đổi theo nhiều định dạng và độ phân giải.
5. **Distribution:** CDN hoặc endpoint riêng tư để phân phối nội dung.
6. **Monitoring:** Giám sát tiến trình, thời gian xử lý và lỗi.

## Nội dung

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Truy cập đến S3 từ VPC](5.3-S3-vpc/)
4. [Truy cập đến S3 từ TTDL On-premises](5.4-S3-onprem/)
5. [VPC Endpoint Policies (làm thêm)](5.5-Policy/)
6. [Dọn dẹp tài nguyên](5.6-Cleanup/)