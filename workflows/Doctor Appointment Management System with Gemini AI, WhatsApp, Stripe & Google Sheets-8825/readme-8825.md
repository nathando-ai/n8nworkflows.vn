---
title: "🚀 Xây dựng Hệ thống Quản lý Lịch hẹn Y tế thông minh tích hợp Gemini AI, WhatsApp & Stripe trên n8n"
description: "Tự động hóa toàn diện quy trình đặt lịch khám, dời lịch, hủy lịch và thanh toán trực tuyến qua WhatsApp, Google Sheets và Stripe sử dụng AI Agent."
slug: "he-thong-quan-ly-lich-hen-y-te-whatsapp-gemini-stripe"
tags: [n8n, automation, ai-agent, whatsapp, stripe, google-sheets, gemini]
keywords: [n8n workflow, đặt lịch khám tự động, whatsapp chatbot ai, thanh toán stripe n8n, quản lý lịch hẹn google sheets]
---

# 🚀 Xây dựng Hệ thống Quản lý Lịch hẹn Y tế thông minh với n8n, Gemini AI và WhatsApp

Các sếp đang gặp khó khăn trong việc quản lý lịch hẹn khám bệnh? Nhân viên tốn quá nhiều thời gian để nhắn tin tư vấn, xác nhận lịch, xử lý hủy lịch và nhắc nhở bệnh nhân qua lại? 

Hãy tưởng tượng một hệ thống trợ lý ảo hoạt động 24/7 trên WhatsApp, tự động trò chuyện với bệnh nhân, tra cứu lịch trống, đặt lịch, dời lịch, hủy lịch, thậm chí tự động tạo link thanh toán qua Stripe và gửi tin nhắn nhắc nhở mỗi sáng. Tất cả đều được tự động hóa 100% không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow phức tạp với AI Agent và các Webhook hoạt động ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chatbot AI xử lý từ khâu đặt lịch mới, xem lịch hẹn, dời lịch cho đến hủy lịch qua WhatsApp.
- **Thanh toán mượt mà:** Tự động tạo Link thanh toán Stripe khi có lịch hẹn mới chọn hình thức thanh toán online, tự động hoàn tiền (Refund) khi hủy lịch đã thanh toán.
- **Đồng bộ hóa dữ liệu:** Mọi thông tin đều được cập nhật thời gian thực vào Google Sheets.
- **Chăm sóc khách hàng chủ động:** Tự động gửi tin nhắn nhắc nhở lịch hẹn vào 8:00 sáng hàng ngày nhờ AI Agent quét danh sách.
:::

### 📦 Các phân hệ chính trong Workflow
Workflow này bao gồm 35 nodes tích hợp chặt chẽ với nhau để vận hành 4 luồng nghiệp vụ chính:
1. **AI Booking Assistant:** Xử lý tin nhắn đến từ WhatsApp, sử dụng **Google Gemini Chat Model**, **Simple Memory** và các **Google Sheets Tool** để tra cứu/thêm/sửa/xóa lịch hẹn.
2. **Payment Link Generation:** Lắng nghe sự kiện thêm lịch mới từ Google Sheets, tự động tạo Stripe Session Checkout và gửi link thanh toán qua WhatsApp.
3. **Payment Verification:** Lắng nghe webhook từ Stripe khi thanh toán thành công, cập nhật trạng thái đơn hàng trong Google Sheets và gửi thông báo xác nhận.
4. **Appointment Reminder & Cancellation:** 
   - Hàng ngày lúc 8:00 sáng (**Schedule Trigger1**), AI Agent quét lịch và gửi tin nhắn nhắc nhở.
   - Khi có thao tác hủy lịch trên Sheet, tự động gửi thông báo hủy và kích hoạt hoàn tiền qua **Stripe Refund API1** nếu đã thanh toán.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã bật tính năng LangChain / AI Agents.
- **WhatsApp Business Cloud API:** Tài khoản Meta Developer kết nối với WhatsApp Business.
- **Google Gemini API Key:** Để vận hành các node `Google Gemini Chat Model`.
- **Google Sheets:** File Google Sheet mẫu chứa các tab cấu hình bệnh nhân và lịch hẹn.
- **Stripe Account:** Lấy Stripe Secret Key và cấu hình Webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow (hoặc copy từ nguồn cấp) và import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Cấu hình Google Sheets (`Get Appointment sheet1`, `Add Patient`, `Add Appointment`, v.v.):** 
  - Thay thế `YOUR_SPREADSHEET_ID_HERE` và `YOUR_SHEET_TAB_ID_HERE` bằng ID Google Sheet thực tế của các sếp.
- **Cấu hình WhatsApp (`Send message`, `Send message in WhatsApp Business Cloud`, v.v.):**
  - Kết nối Credentials tài khoản WhatsApp Business Cloud.
  - Điền số điện thoại thử nghiệm tại các node gửi tin nhắn.
- **Cấu hình AI Agent:**
  - Kiểm tra kết nối tới `Google Gemini Chat Model` và `Google Gemini Chat Model3`.
  - Tùy chỉnh **System Message** trong AI Agent để điều chỉnh tính cách, giọng điệu và hành vi của trợ lý ảo (hỗ trợ tiếng Việt linh hoạt).
- **Cấu hình Thanh toán (`Stripe Trigger1`, `Generate Stripe Payment Link1`, `Stripe Refund API1`):**
  - Thêm Stripe Secret Key vào Credentials.
  - Trỏ Webhook URL của Stripe về n8n Trigger node tương ứng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với tin nhắn mẫu trên WhatsApp hoặc giả lập một dòng dữ liệu trên Google Sheets.
- Kiểm tra các nhánh If (`Check Appointment Payment Mode1`, `Check Is Amount Paid1`, `Check status "Cancelled"1`).
- Bật công tắc **Active** để đưa hệ thống vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Thêm node gửi thông báo về kênh nội bộ mỗi khi có khách hàng đặt lịch hoặc thanh toán thành công để đội ngũ y bác sĩ nắm bắt kịp thời.
- **Log lỗi tự động:** Bắt sự kiện lỗi bằng node `Error Trigger` để gửi cảnh báo về nhóm chat riêng nếu API Stripe hoặc WhatsApp gặp sự cố.
- **Cá nhân hóa tin nhắn:** Tinh chỉnh prompt của AI Agent để tự động thêm tên bác sĩ, phòng khám hoặc các lưu ý đặc biệt trước khi khám.

### 📌 Kết luận
Hệ thống quản lý lịch hẹn y tế kết hợp AI và WhatsApp này là giải pháp chuyển đổi số cực kỳ mạnh mẽ cho các phòng khám, spa hoặc dịch vụ tư vấn cá nhân. Triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!