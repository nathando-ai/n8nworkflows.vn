---
title: "🚀 Tự động hóa kết nối và nhắn tin cá nhân hóa trên LinkedIn cho Sales với n8n"
description: "Hướng dẫn xây dựng hệ thống Sales Automation trên LinkedIn bằng n8n, kết hợp Browserflow và OpenAI AI Agent để tìm kiếm, gửi lời mời kết nối và nhắn tin chăm sóc khách hàng tự động."
slug: "tu-dong-hoa-ket-noi-nhan-tin-linkedin-cho-sales-n8n"
tags: [n8n, automation, no-code, linkedin, sales-automation, openai]
keywords: [n8n workflow, linkedin automation, sales b2b n8n, ai agent linkedin, tự động hóa linkedin]
---

# 🚀 Tự động hóa kết nối và nhắn tin cá nhân hóa trên LinkedIn cho Sales

Các sếp làm sales B2B chắc chắn hiểu rõ cảm giác "mỏi tay" khi mỗi ngày phải lục lọi LinkedIn, copy profile từng khách hàng tiềm năng, gửi lời mời kết nối thủ công rồi chờ đợi phản hồi để nhắn tin chăm sóc. Quy trình này cực kỳ tốn thời gian, lặp đi lặp lại và rất dễ bỏ sót khách hàng.

Đừng để thời gian quý báu của đội ngũ sales bị chôn vùi vào những tác vụ thủ công đó! Bài viết này sẽ hướng dẫn các sếp triển khai một **Workflow n8n tự động hóa 100% quy trình kết nối và nhắn tin trên LinkedIn**, có tích hợp trí tuệ nhân tạo (AI) để viết lời nhắn siêu cá nhân hóa dựa trên profile của từng khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Tự động tìm kiếm profile, gửi lời mời kết nối kèm lời nhắn và gửi tin nhắn chăm sóc khi đã kết nối thành công.
- **Cá nhân hóa bằng AI:** Sử dụng OpenAI AI Agent để đọc thông tin profile và viết nội dung nhắn tin cực kỳ tự nhiên, trúng "nỗi đau" của khách hàng.
- **Quản lý tập trung qua Google Sheets:** Mọi dữ liệu về khách hàng, trạng thái kết nối và thống kê đều được đồng bộ thời gian thực.
- **Hoạt động không nghỉ:** Chạy tự động theo lịch trình (Schedule Trigger) hoặc kích hoạt khi có dữ liệu mới, giúp mở rộng mạng lưới khách hàng ngay cả khi ngủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted VPS hoặc n8n Cloud).
- **Tài khoản OpenAI API** (để AI Agent phân tích profile và viết nội dung).
- **Google Sheets API / Credentials** (để lưu trữ danh sách và trạng thái khách hàng).
- **Browserflow** (hoặc công cụ trình duyệt tích hợp tương ứng được cấu hình trong các node Browserflow).
- **Tài khoản Gmail** (tùy chọn, dùng để nhận thông báo hoặc gửi email bổ trợ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ mã JSON).
- Trên giao diện n8n Editor, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà "chạy băng băng", các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Fill Out Keywords (formTrigger)** & **Get Profiles (googleSheets)**: Thiết lập Google Sheet chứa danh sách từ khóa tìm kiếm và bảng dữ liệu chứa thông tin khách hàng tiềm năng (Họ tên, Link Profile LinkedIn, Trạng thái...).
- **AI Agent & OpenAI Chat Model**: Kết nối OpenAI Credentials. Tại đây, các sếp cần viết system prompt hướng dẫn AI cách đọc dữ liệu profile từ bước cào dữ liệu để soạn ra một lời mời kết nối (Invite) hoặc tin nhắn ngắn gọn, lịch sự và đúng trọng tâm.
- **Profile Scraper**, **Connection Checker**, **Invite Sender**, **Send Personalised Message**: Các node Browserflow chịu trách nhiệm tương tác trực tiếp với giao diện LinkedIn. Cần cấu hình đúng tài khoản và đảm bảo phiên đăng nhập LinkedIn trên trình duyệt tự động không bị gián đoạn (tránh bị checkpoint).
- **Loop Over Items / Split In Batches**: Cấu hình số lượng profile xử lý mỗi lần chạy (batch size) nhằm tuân thủ giới hạn an toàn của LinkedIn, tránh việc tài khoản bị quét spam.
- **Stat Update & Update Invite (googleSheets)**: Trỏ đúng các cột trong Google Sheet để hệ thống tự động ghi nhận trạng thái: *Đã gửi lời mời*, *Đã kết nối*, *Đã nhắn tin*.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với 1-2 dòng dữ liệu mẫu trong Google Sheets để kiểm tra luồng chạy của AI và các node Browserflow.
- Sau khi chắc chắn không có lỗi phát sinh, gạt công tắc sang **Active** để hệ thống tự động vận hành theo **Schedule Trigger**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Thêm node gửi thông báo về nhóm chat nội bộ mỗi khi có khách hàng chấp nhận lời mời kết nối hoặc phản hồi tin nhắn.
- **Quản lý hạn mức thông minh:** Tận dụng node **Set Connection Limit** để giới hạn số lượng lời mời gửi đi mỗi ngày (ví dụ: tối đa 20-30 lời mời/ngày), bảo vệ tài khoản LinkedIn khỏi việc bị giới hạn tính năng (restricted).
- **Báo cáo định kỳ:** Kết hợp Google Sheets và Gmail để gửi báo cáo tổng kết số lượng lead đã tiếp cận vào cuối mỗi tuần cho quản lý.

### 📌 Kết luận
Tự động hóa quy trình tìm kiếm khách hàng trên LinkedIn không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn đảm bảo tính nhất quán trong cách tiếp cận khách hàng B2B. Hãy cài đặt ngay workflow này trên hệ thống n8n của các sếp để tối ưu hóa đội ngũ sales ngay hôm nay!