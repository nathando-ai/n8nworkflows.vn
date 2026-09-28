---
title: "📈 Phân tích kỹ thuật chứng khoán với Telegram, Airtable và AI Agent - Workflow n8n hoàn chỉnh"
description: "Tự động hóa phân tích kỹ thuật chứng khoán 100% không cần code. Nhận phân tích từ AI qua Telegram, lưu dữ liệu vào Airtable và tạo biểu đồ kỹ thuật tự động."
slug: "phan-tich-ky-thuat-chung-khoan-voi-telegram-airtable-ai-agent"
tags: [n8n, automation, no-code, finance, ai]
keywords: [n8n workflow, tự động hóa chứng khoán, phân tích kỹ thuật, AI trading, Telegram bot]
---

# 📈 Phân tích kỹ thuật chứng khoán với Telegram, Airtable và AI Agent - Workflow n8n hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà đầu tư khi phải tự phân tích chứng khoán thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận phân tích kỹ thuật từ AI qua Telegram ngay lập tức
- Lưu trữ dữ liệu phân tích vào Airtable để theo dõi dài hạn
- Tạo biểu đồ kỹ thuật tự động với các tham số tùy chỉnh
- Tiết kiệm thời gian và công sức cho việc phân tích thủ công
- Nhận cảnh báo và thông báo tự động từ hệ thống
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot API key
- Tài khoản Airtable với bảng dữ liệu đã tạo
- Tài khoản OpenAI với API key
- URL dịch vụ tạo biểu đồ (cần API key)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3053](https://n8n.io/workflows/3053)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger** và **Send Analysis**:
   - Cần cấu hình credentials cho Telegram API
   - Thay đổi Chat ID trong các node Telegram để tương ứng với kênh chat của bạn

2. **OpenAI Chat Model**:
   - Cấu hình credentials cho OpenAI API
   - Chọn model phù hợp (gpt-4o được đề xuất)

3. **Get Chart URL**:
   - Cấu hình credentials cho HTTP Header Auth
   - Thay đổi API key trong header (x-api-key)
   - Cập nhật URL dịch vụ tạo biểu đồ

4. **Airtable**:
   - Cấu hình credentials cho Airtable Token API
   - Đảm bảo bảng dữ liệu đã được tạo trong Airtable

5. **Download Chart**:
   - Cập nhật URL dịch vụ tạo biểu đồ

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu bằng cách gửi tin nhắn đến Telegram bot
- Kiểm tra kết quả phân tích được gửi về
- Bật Active workflow sau khi đã kiểm tra đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo phân tích
- Thêm node lưu log các giao dịch phân tích
- Tạo báo cáo định kỳ từ dữ liệu trong Airtable
- Kết nối với các dịch vụ khác như TradingView để tích hợp thêm dữ liệu
- Tùy chỉnh prompt cho AI để phù hợp với chiến lược giao dịch của bạn

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc phân tích kỹ thuật chứng khoán thông qua Telegram và AI. Với việc tự động hóa toàn bộ quy trình, các nhà đầu tư có thể tập trung vào việc ra quyết định thay vì phải tốn thời gian cho việc phân tích dữ liệu. Hãy thử ngay và tối ưu hóa chiến lược giao dịch của bạn!