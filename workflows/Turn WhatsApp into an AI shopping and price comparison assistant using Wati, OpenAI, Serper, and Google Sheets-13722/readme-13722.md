```yaml
---
title: "🛍️ Tự động hóa mua sắm thông minh với WhatsApp + AI: So sánh giá & chatbot"
description: "Hướng dẫn tạo chatbot WhatsApp tự động so sánh giá sản phẩm từ nhiều nguồn, lưu vào Google Sheets và trả lời khách hàng bằng AI - hoàn toàn không cần code"
slug: "tao-chatbot-whatsapp-so-sanh-gia-ai"
tags: [n8n, automation, no-code, whatsapp, ai, google-sheets]
keywords: [n8n workflow, tự động hóa mua sắm, chatbot whatsapp, so sánh giá, ai chatbot]
---
```

# 🛍️ Tự động hóa mua sắm thông minh với WhatsApp + AI: So sánh giá & chatbot

[Các sếp đang gặp khó khăn khi phải trả lời hàng trăm tin nhắn WhatsApp mỗi ngày về giá sản phẩm, so sánh từ nhiều nguồn khác nhau. Với workflow này, các sếp có thể tạo ngay một chatbot thông minh hoàn toàn tự động hóa mà không cần lập trình.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động so sánh giá từ nhiều nguồn (Amazon, Shopee, Tiki...) chỉ với 1 tin nhắn
- Lưu dữ liệu giao dịch vào Google Sheets để phân tích sau
- Trả lời khách hàng ngay lập tức bằng AI (OpenAI) với thông tin chính xác
- Giảm tới 90% thời gian trả lời tin nhắn thủ công
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business (hoặc số điện thoại cá nhân)
- API Key từ OpenAI (GPT-3.5 hoặc GPT-4)
- API Key từ Serper (dịch vụ tìm kiếm thông minh)
- Tài khoản Google Cloud với Google Sheets API đã kích hoạt
- Tài khoản Wati (dịch vụ kết nối WhatsApp với API)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13722](https://n8n.io/workflows/13722)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Wati Trigger**:
   - Chọn credentials đã tạo cho Wati
   - Điền số điện thoại WhatsApp của bạn vào trường "Phone Number"

2. **Node Google Sheets**:
   - Chọn credentials Google Cloud của bạn
   - Điền ID của Google Sheet nơi lưu dữ liệu
   - Đảm bảo Sheet có các cột: "Tên sản phẩm", "Giá", "Nguồn", "Thời gian"

3. **Node HTTP Request (Serper)**:
   - Điền API Key của Serper vào header Authorization
   - Đảm bảo endpoint là `https://google.serper.dev/search`

4. **Node Code (JavaScript)**:
   - Kiểm tra hàm xử lý dữ liệu trả về từ Serper
   - Đảm bảo logic so sánh giá hoạt động đúng

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra Google Sheet để xác nhận dữ liệu được lưu đúng
3. Kiểm tra WhatsApp để xác nhận chatbot trả lời đúng
4. Nếu mọi thứ ổn, click vào nút "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết nối Slack/Telegram**: Thêm node để nhận thông báo khi có giao dịch lớn
2. **Lịch gửi báo cáo**: Thêm node Schedule Trigger để gửi báo cáo hàng ngày
3. **Quản lý kho**: Kết nối với hệ thống quản lý kho để cập nhật tồn kho
4. **Phân tích dữ liệu**: Sử dụng Google Data Studio để tạo dashboard từ dữ liệu

### 📌 Kết luận
Với workflow này, các sếp có thể biến WhatsApp thành một công cụ bán hàng thông minh hoàn toàn tự động. Không cần lập trình, không cần nhân viên bán hàng 24/7 - chỉ cần một lần cài đặt và workflow sẽ làm việc cho bạn. Hãy thử ngay và tiết kiệm thời gian quý giá của các sếp!