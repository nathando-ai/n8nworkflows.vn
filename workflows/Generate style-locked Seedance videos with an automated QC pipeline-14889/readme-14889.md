---
title: "🚀 Tự động hóa tạo video Seedance khóa phong cách và Kiểm định chất lượng (QC) bằng n8n"
description: "Xây dựng pipeline tự động hóa quy trình chuyển đổi phong cách điện ảnh, tạo video AI qua Seedance và kiểm định QC tự động trước khi gửi bản dựng."
slug: "tu-dong-hoa-tao-video-seedance-qc-pipeline-n8n"
tags: [n8n, automation, no-code, ai-video, seedance, content-creation]
keywords: [n8n workflow, seedance ai, style transfer, qc pipeline, tự động hóa video, ai workflow]
---

# 🚀 Tự động hóa tạo video Seedance khóa phong cách và Kiểm định chất lượng (QC)

Trong các quy trình sản xuất hậu kỳ VFX và dựng phim, việc giữ vững phong cách hình ảnh (style-locked) qua từng khung hình là một thử thách lớn. Làm thủ công thường mất rất nhiều thời gian để render, đối chiếu màu sắc, độ tương phản và gửi duyệt qua nhiều kênh. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò do **Rahul Joshi** thiết kế: tự động nhận yêu cầu, gọi model AI Seedance để tạo video khóa phong cách dựa trên ảnh tham chiếu (hero reference image), chạy hệ thống QC (Quality Control) tự động chấm điểm, và tự động phân phối kết quả qua Slack, Gmail, Jira hoặc Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Khóa phong cách chuẩn điện ảnh 100%**: Mọi video biến đổi đều neo vào một khung hình tham chiếu đã được đạo diễn phê duyệt, không còn tình trạng lệch tông màu hay ánh sáng.
- **QC tự động hóa thông minh**: Hệ thống tự động chấm điểm độ tương phản, khớp màu, độ sáng dựa trên thông số chuẩn thay vì dựa vào cảm tính.
- **Đa kênh thông báo & phân phối**: Kết quả được gửi đồng thời lên Slack, tạo task trên Jira cho đội review, gửi email HTML chuyên nghiệp qua Gmail cho biên tập viên, và cảnh báo Telegram nếu bị từ chối.
- **Tiết kiệm 90% thời gian duyệt**: Chỉ những variant đạt chuẩn mới được đẩy tiếp vào chuỗi biên tập, giảm thiểu thao tác thủ công lặp đi lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (bản self-hosted hoặc cloud).
- **Seedance API Key**: Tài khoản và API key của dịch vụ AI Seedance.
- **Slack Workspace**: OAuth2 credentials và Channel ID để nhận báo cáo QC.
- **Gmail Account**: OAuth2 credentials để gửi email báo cáo cho ban biên tập.
- **Jira Cloud**: Credentials và Project ID/Issue Type để tự động tạo task review.
- **Telegram Bot** (Tùy chọn): Token và Chat ID để nhận thông báo từ chối QC.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n templates (link gốc: `https://n8n.io/workflows/14889`) hoặc copy toàn bộ JSON và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau trước khi kích hoạt:

- **Webhook: Style Look Transfer2**: Đóng vai trò là điểm tiếp nhận dữ liệu đầu vào. Payload gửi lên qua phương thức `POST` cần chứa các trường: `shotCode`, `newShotDescription`, và `heroReferenceUrl`.
- **Seedance: Generate Style-Locked Variant2** & **Poll: Check Variant Generation Status1**: Thay thế token `Authorization` mặc định bằng Seedance API Key của các sếp thông qua n8n Credentials (HTTP Header Auth).
- **Slack: Post Style QC Report1** & **Slack: Error Alert**: Kết nối tài khoản Slack OAuth2 và cập nhật lại `channelId` chính xác để nhận thông báo.
- **Gmail: Send QC Report to Editorial1**: Cấu hình tài khoản Gmail OAuth2. Địa chỉ người nhận sẽ được điều khiển động qua trường `deliveryEmail` trong payload gửi đến.
- **Jira: Create Style Review Task1**: Kết nối Jira Cloud credential, sau đó cập nhật thông số `project` và `issueType` tương ứng với bảng quản lý công việc của đội ngũ.
- **Telegram: Notify on QC Rejection1** (Tùy chọn): Điền thông tin Bot Token và `chatId` nếu muốn nhận thông báo khi có variant bị rớt QC.

#### 3. Kích hoạt ⚡️
- Gửi một request mẫu (sample payload) đến Webhook endpoint để test thử luồng chạy của toàn bộ 18 nodes.
- Kiểm tra kết quả trên Slack, Gmail, Jira xem dữ liệu đã đổ về chính xác chưa.
- Bật công tắc **Active workflow** để đưa hệ thống vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Các sếp có thể kết nối thêm node Microsoft Teams hoặc Discord nếu đội ngũ không dùng Slack.
- **Lưu trữ Log QC**: Thêm một node Google Sheets hoặc Airtable để lưu lại lịch sử chấm điểm QC của từng shot, phục vụ việc phân tích hiệu suất model AI theo thời gian.
- **Báo cáo định kỳ**: Kết hợp node Cron (Schedule Trigger) để tổng hợp số liệu video đạt/trượt QC gửi về email quản lý vào cuối mỗi ngày.

### 📌 Kết luận
Workflow tích hợp AI Seedance và QC Pipeline này là một giải pháp toàn diện giúp các đội ngũ sản xuất nội dung, VFX tự động hóa hoàn toàn khâu tạo và kiểm định video. Hãy cài đặt ngay để tối ưu hóa năng suất và đảm bảo chất lượng hình ảnh luôn đạt chuẩn điện ảnh!