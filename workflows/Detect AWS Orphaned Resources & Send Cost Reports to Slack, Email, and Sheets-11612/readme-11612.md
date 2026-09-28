---
title: "🚀 Tự động phát hiện tài nguyên AWS mồ côi và gửi báo cáo chi phí qua Slack, Email, Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động quét AWS để tìm EBS volumes bỏ quên, snapshot cũ và Elastic IPs chưa dùng, giúp tiết kiệm hàng ngàn đô la chi phí cloud mỗi tháng."
slug: "tu-dong-phat-hien-tai-nguyen-aws-mo-coi-n8n"
tags: [n8n, automation, aws, devops, cost-optimization, slack, google-sheets]
keywords: [n8n workflow, aws orphaned resources, tối ưu chi phí aws, ebs volumes, elastic ips, devops automation]
---

# 🚀 Tự động phát hiện tài nguyên AWS mồ côi và gửi báo cáo chi phí qua Slack, Email, Google Sheets

Các sếp làm DevOps hoặc quản lý hạ tầng Cloud chắc hẳn đã quá quen thuộc với cơn đau đầu mang tên "hóa đơn AWS tăng vọt cuối tháng". Nguyên nhân lớn nhất thường đến từ các tài nguyên "mồ côi" (orphaned resources) bị bỏ quên như: ổ đĩa EBS không gắn vào đâu, các snapshot cũ mèm từ năm ngoái, hay Elastic IP để không tốn phí duy trì. Làm thủ công bằng cách kiểm tra từng Region thì tốn thời gian và rất dễ bỏ sót.

Workflow n8n này (được thiết kế bởi chuyên gia DevOps Chad M. Crowell) sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: tự động quét định kỳ, tính toán chi phí lãng phí, tổng hợp dữ liệu và bắn cảnh báo đa kênh (Slack, Gmail, Google Sheets).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí thực tế:** Trung bình tiết kiệm từ $50 đến $10,000/tháng nhờ dọn dẹp kịp thời tài nguyên thừa.
- **Báo cáo đa kênh tức thì:** Gửi thông báo chi tiết qua Slack, báo cáo HTML chuyên nghiệp qua Gmail, và lưu trữ log chi tiết vào Google Sheets.
- **Hoạt động hoàn toàn tự động:** Lịch trình chạy tự động hàng tuần (hoặc theo cấu hình tùy chỉnh) mà không cần can thiệp thủ công.
- **Quản trị minh bạch:** Phân tích, xếp hạng 5 tài nguyên ngốn tiền nhiều nhất và kiểm tra thẻ (Tags) thiếu sót.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản AWS & Lambda Function:** Đã triển khai AWS Lambda script để quét tài nguyên và IAM User (`n8n-resource-scanner`) có quyền EC2 read + Lambda invoke.
- **Tài khoản n8n:** Đã cấu hình các Credentials:
  - AWS IAM Credentials
  - Slack OAuth hoặc Webhook
  - Gmail OAuth2
  - Google Sheets OAuth2
- **Google Sheet:** Một bảng tính sẵn sàng với các cột tiêu đề (headers) để lưu audit log.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow, sau đó vào giao diện n8n, chọn **Add workflow** -> bấm vào dấu ba chấm (...) ở góc trên bên phải -> chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Weekly Scan Trigger1:** Cài đặt lịch chạy tự động (mặc định là Thứ Hai hàng tuần lúc 8 giờ sáng UTC).
- **Initialize Config:** Cấu hình các thông số cốt lõi như giới hạn thời gian snapshot (>90 ngày), định dạng tag bắt buộc (*Environment, Owner, CostCenter*).
- **Set Region Variables:** Điền danh sách các Region AWS cần quét (ví dụ: `us-east-1`, `ap-southeast-1`...).
- **Scan Elastic IPs, Scan EBS Snapshots, Scan unattached EBS Volumes:** Kết nối với credentials **AWS** đã chuẩn bị sẵn để gọi Lambda function.
- **Send Email Report:** Chọn credentials **Gmail OAuth2** để gửi báo cáo HTML chi tiết.
- **Send Slack Alert / None Found Slack Message:** Kết nối tài khoản Slack và chọn channel nhận tin (ví dụ: `#cloud-ops`).
- **Append or update row in sheet & Log to Google Sheets (Found):** Kết nối credentials **Google Sheets OAuth2**, trỏ tới file Google Sheet và đảm bảo tên Sheet khớp chính xác.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu thực tế từ AWS.
- Kiểm tra kết quả trên Slack, Email và Google Sheets xem dữ liệu đã đổ về chuẩn chỉnh chưa.
- Sau khi test OK, gạt công tắc sang **Active** để bật chế độ tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Webhook khác:** Ngoài Slack và Gmail, các sếp có thể clone nhánh thông báo để đẩy cảnh báo về nhóm Telegram của công ty.
- **Tự động hóa hành động (Auto-Remediation):** Nâng cấp workflow bằng cách thêm bước tự động xóa (hoặc gửi ticket Jira yêu cầu chủ sở hữu xóa) các tài nguyên mồ côi thay vì chỉ cảnh báo.
- **Báo cáo định kỳ hàng tháng:** Tạo thêm một nhánh chạy vào ngày đầu tiên của tháng để tổng hợp số tiền tiết kiệm được nhờ dọn dẹp tài nguyên gửi cho ban giám đốc.

### 📌 Kết luận
Việc quản lý chi phí AWS không còn là ác mộng nếu các sếp áp dụng tự động hóa. Hãy triển khai ngay workflow này để tối ưu hóa ngân sách Cloud cho doanh nghiệp ngay hôm nay!