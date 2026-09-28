---
title: "🚀 Tự động Giám sát SLA Thời gian Phản hồi Lead với Google Sheets và Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động kiểm tra, phát hiện và cảnh báo qua Telegram khi thời gian phản hồi lead (SLA) vượt quá giới hạn 15 phút."
slug: "giam-sat-sla-phản-hoi-lead-google-sheets-telegram"
tags: [n8n, automation, no-code, crm, google-sheets, telegram, sla-monitoring]
keywords: [n8n workflow, giám sát sla, phản hồi lead, google sheets telegram, tự động hóa crm]
---

# 🚀 Tự động Giám sát SLA Thời gian Phản hồi Lead với Google Sheets và Telegram

Trong bán hàng và chăm sóc khách hàng, thời gian phản hồi (Speed-to-Lead) đóng vai trò quyết định tỷ lệ chốt đơn. Tuy nhiên, việc kiểm tra thủ công xem đội ngũ sales đã phản hồi các lead mới hay chưa thường xuyên bị bỏ sót, dẫn đến việc khách hàng tiềm năng nguội lạnh và chuyển sang đối thủ.

Workflow này giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: liên tục quét danh sách lead, phát hiện các trường hợp vi phạm cam kết chất lượng dịch vụ (SLA) quá 15 phút chưa được phản hồi, và ngay lập tức gửi cảnh báo chi tiết kèm link trực tiếp đến Google Sheet qua Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt nhịp khách hàng kịp thời:** Cảnh báo ngay lập tức qua Telegram khi một lead bị bỏ quên quá 15 phút.
- **Tăng tỷ lệ chuyển đổi:** Đảm bảo không có khách hàng tiềm năng nào bị "bỏ quên" trong CRM hoặc Google Sheets.
- **Tối ưu hiệu suất đội ngũ:** Giám sát thời gian phản hồi (SLA) một cách minh bạch, tự động hóa hoàn toàn không tốn nhân lực kiểm tra thủ công.
- **Thao tác 1 chạm:** Tin nhắn cảnh báo kèm theo đường link trực tiếp đến dòng dữ liệu trong Google Sheet giúp sales xử lý cực kỳ nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- Một hệ thống n8n (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** chứa danh sách lead (bao gồm thông tin trạng thái, thời gian tạo, thông tin liên hệ).
- Một **Telegram Bot** đã được tạo sẵn qua `@BotFather` và đã lấy được Token cùng Chat ID để gửi tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/8293](https://n8n.io/workflows/8293)) hoặc copy/paste trực tiếp đoạn JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Every 5 Minutes (Cron):** Node này định thời gian chạy workflow đều đặn mỗi 5 phút để rà soát lead. Các sếp có thể điều chỉnh lại thời gian nếu muốn (ví dụ: mỗi 10 phút hoặc 15 phút).
- **Get row(s) in sheet (Google Sheets):** 
  - Kết nối tài khoản Google Sheets của các sếp bằng `Google Sheets OAuth2 API`.
  - Chọn đúng File (Spreadsheet) và Sheet chứa dữ liệu lead cần theo dõi.
- **Code1 (Code):** Node này thực hiện việc làm sạch dữ liệu, tính toán thời gian và gắn thêm đường link trực tiếp đến từng dòng (row) cụ thể trong Google Sheet giúp người nhận dễ dàng click xem chi tiết.
- **SLA Breach Check (If):** Node này áp dụng điều kiện lọc ra các lead có trạng thái "Unreplied" (Chưa phản hồi) và thời gian chờ đợi vượt quá giới hạn 15 phút. 
- **Send a text message (Telegram):**
  - Kết nối `Telegram API` bằng Bot Token của các sếp.
  - Điền Chat ID của nhóm chat hoặc cá nhân nhận thông báo.
  - Nội dung tin nhắn sẽ tự động lấy thông tin chi tiết của lead và link Google Sheet từ các bước trước đó để gửi đi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử dữ liệu mẫu và kiểm tra xem Telegram đã nhận được thông báo hay chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tự động hóa chăm sóc khách hàng tối ưu hơn, các sếp có thể mở rộng workflow này bằng cách:
1. **Tích hợp thêm kênh cảnh báo:** Ngoài Telegram, có thể kết nối thêm node Slack hoặc gửi Email nhắc nhở trực tiếp cho quản lý nếu lead quá hạn 30 phút.
2. **Tự động cập nhật trạng thái:** Thêm bước tự động chuyển trạng thái "Escalated" trong Google Sheets sau khi tin nhắn cảnh báo được gửi đi.
3. **Ghi log báo cáo:** Lưu lịch sử các lần vi phạm SLA vào một sheet riêng để tổng kết hiệu suất làm việc của đội ngũ sales cuối tuần/cuối tháng.

### 📌 Kết luận
Việc kiểm soát SLA phản hồi lead chưa bao giờ dễ dàng đến thế với workflow tự động hóa n8n này. Hãy cài đặt ngay để không bỏ lỡ bất kỳ cơ hội kinh doanh nào từ khách hàng tiềm năng nhé các sếp!