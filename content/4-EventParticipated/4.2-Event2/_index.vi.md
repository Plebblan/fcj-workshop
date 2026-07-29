---
title: "Event 2"
date: 2025-07-11
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Báo cáo tổng kết: “AWS Community Sharing – Monitoring, Security và AWS Cloud Practitioner”

### Mục tiêu sự kiện

- Chia sẻ kiến thức thực tiễn về giám sát hệ thống và quản lý SLA trên nền tảng AWS.
- Giới thiệu giải pháp ứng dụng Agentic AI trong bảo mật ứng dụng web.
- Hướng dẫn lộ trình ôn tập và kinh nghiệm thi chứng chỉ **AWS Certified Cloud Practitioner (CLF-C02)**.
- Giúp người tham dự hiểu rõ hơn về các dịch vụ AWS cũng như cách áp dụng vào học tập và phát triển nghề nghiệp.

### Diễn giả

- **Nguyễn Huỳnh Sơn** – *SLA and Monitoring: From SLA to Monitoring What Really Matters*
- **Nguyễn Tuấn Thịnh** – *Securing Your Web Apps With AWS Security Agent*
- **Ngô Lê Tấn Huy** – *Inside the Exam: AWS Cloud Practitioner*

### Nội dung nổi bật

#### SLA và Monitoring

- **Khái niệm SLA**: Hiểu Service Level Agreement là cam kết về mức độ dịch vụ giữa nhà cung cấp và khách hàng.
- **Monitoring theo góc nhìn người dùng**: Không chỉ theo dõi CPU, Memory mà cần đo lường trải nghiệm thực tế như tỷ lệ đăng nhập thành công hoặc khả năng hoàn thành giao dịch.
- **Monitoring Pyramid**: Bao gồm các tầng Cloud Provider, Infrastructure, Application, Business Metrics và Customer Experience.
- **Alerting Workflow**: Xây dựng quy trình cảnh báo với CloudWatch Alarm và Amazon SNS nhằm phát hiện sự cố trước khi khách hàng phản ánh.

#### AWS Security Agent

- **Agentic AI trong bảo mật**: Ứng dụng Amazon Bedrock để tự động thực hiện các tác vụ đánh giá bảo mật.
- **Ba giai đoạn bảo mật**: Design Review, Code Security Review và Automated Penetration Testing.
- **Tự động phát hiện lỗ hổng**: Phân tích tài liệu thiết kế, kiểm tra Pull Request và mô phỏng các chuỗi tấn công thực tế.
- **Giới hạn của AI Security Agent**: Khó xử lý các bài toán liên quan đến Business Logic, MFA và các cơ chế xác thực phức tạp.

#### AWS Cloud Practitioner

- **Cấu trúc kỳ thi**: Gồm 65 câu hỏi trong 90 phút, tập trung vào kiến thức nền tảng về AWS Cloud.
- **Bốn nhóm kiến thức chính**:
  - Cloud Concepts
  - Security and Compliance
  - Cloud Technology and Services
  - Billing, Pricing and Support
- **Kiến thức trọng tâm**: Shared Responsibility Model, IAM, các dịch vụ AWS phổ biến và mô hình định giá.
- **Kinh nghiệm ôn thi**: Học theo từ khóa, thực hành trên AWS Free Tier, luyện đề và phân tích kỹ các câu trả lời sai.

### Bài học rút ra

#### Giám sát hệ thống

- **Monitoring hướng đến người dùng**: Chỉ số hạ tầng không phản ánh đầy đủ chất lượng dịch vụ.
- **Business Metrics**: Theo dõi Login Success Rate, Checkout Success hay các chỉ số nghiệp vụ quan trọng.
- **Quản lý rủi ro**: Monitoring là một phần của quy trình phát hiện, phản ứng và cải tiến liên tục.

#### Bảo mật ứng dụng

- **Shift Left Security**: Đưa hoạt động kiểm tra bảo mật vào sớm trong vòng đời phát triển phần mềm.
- **AI hỗ trợ DevSecOps**: Agentic AI giúp tự động hóa nhiều tác vụ kiểm thử và đánh giá bảo mật.
- **Kết hợp con người và AI**: AI hỗ trợ tăng hiệu quả nhưng vẫn cần chuyên gia xác minh các vấn đề liên quan đến nghiệp vụ.

#### Chuẩn bị chứng chỉ AWS

- **Nắm vững kiến thức nền tảng**: Hiểu mục đích và trường hợp sử dụng của từng dịch vụ AWS.
- **Thực hành thực tế**: Trải nghiệm trực tiếp trên AWS giúp ghi nhớ kiến thức hiệu quả hơn.
- **Chiến lược làm bài**: Áp dụng phương pháp loại trừ đáp án và đọc kỹ từ khóa trong đề thi.

### Áp dụng vào công việc

- **Thiết kế hệ thống Monitoring** theo hướng theo dõi trải nghiệm người dùng thay vì chỉ quan tâm đến tài nguyên hệ thống.
- **Ứng dụng CloudWatch và Amazon SNS** để xây dựng hệ thống cảnh báo chủ động.
- **Tích hợp bảo mật sớm** vào quy trình phát triển phần mềm bằng các công cụ AI hỗ trợ kiểm tra bảo mật.
- **Thực hành các dịch vụ AWS** để nâng cao kỹ năng sử dụng Cloud và chuẩn bị cho các chứng chỉ AWS.
- **Áp dụng tư duy quản lý rủi ro** trong quá trình vận hành và phát triển hệ thống.

### Trải nghiệm tham gia sự kiện

Tham dự buổi chia sẻ về **Monitoring, AWS Security Agent và AWS Cloud Practitioner** giúp em có cái nhìn toàn diện hơn về việc xây dựng, vận hành và bảo vệ các hệ thống trên nền tảng AWS. Nội dung của ba bài trình bày vừa mang tính thực tiễn, vừa cung cấp nhiều kinh nghiệm hữu ích cho việc học tập cũng như định hướng nghề nghiệp trong lĩnh vực Cloud Computing.

#### Học hỏi từ các chuyên gia

- Các diễn giả chia sẻ kinh nghiệm thực tế trong quá trình triển khai và vận hành hệ thống trên AWS.
- Những ví dụ minh họa giúp em hiểu rõ hơn cách áp dụng các dịch vụ AWS vào các tình huống thực tế.

#### Tiếp cận các kiến thức thực tiễn

- Hiểu được tầm quan trọng của việc giám sát trải nghiệm người dùng thay vì chỉ theo dõi các chỉ số hạ tầng.
- Tìm hiểu cách xây dựng hệ thống cảnh báo bằng CloudWatch và Amazon SNS để phát hiện sự cố sớm.
- Quan sát cách Agentic AI hỗ trợ tự động hóa các quy trình đánh giá bảo mật ứng dụng.

#### Chuẩn bị cho chứng chỉ AWS

- Nắm được cấu trúc và phạm vi kiến thức của kỳ thi AWS Certified Cloud Practitioner.
- Học được phương pháp ôn tập hiệu quả thông qua việc luyện đề, thực hành AWS Free Tier và ghi nhớ các từ khóa quan trọng.
- Hiểu rõ hơn về Shared Responsibility Model cũng như các dịch vụ cốt lõi của AWS.

#### Mở rộng tư duy về Cloud và Security

- Buổi chia sẻ giúp em nhận ra rằng việc xây dựng một hệ thống tốt không chỉ dừng ở triển khai hạ tầng mà còn phải đảm bảo khả năng giám sát, bảo mật và quản lý rủi ro.
- Việc kết hợp AI với các quy trình DevSecOps mở ra nhiều cơ hội để nâng cao hiệu quả phát triển và vận hành hệ thống.

#### Bài học thu được

- Monitoring cần phản ánh đúng trải nghiệm của người dùng cuối thay vì chỉ dựa trên trạng thái của máy chủ.
- AI có thể hỗ trợ mạnh mẽ trong các quy trình bảo mật nhưng vẫn cần sự giám sát của con người.
- Việc học AWS nên kết hợp giữa lý thuyết, thực hành và chuẩn bị chứng chỉ để xây dựng nền tảng kiến thức vững chắc.

#### Một số hình ảnh tại sự kiện

*Thêm hình ảnh của bạn tại đây.*

> Nhìn chung, buổi chia sẻ đã giúp em hiểu rõ hơn về các khía cạnh quan trọng trong vận hành hệ thống trên AWS, từ monitoring, bảo mật đến lộ trình học tập và đạt chứng chỉ AWS Cloud Practitioner. Những kiến thức và kinh nghiệm được chia sẻ sẽ là nền tảng hữu ích để em tiếp tục phát triển kỹ năng về Cloud Computing và ứng dụng vào các dự án trong tương lai.