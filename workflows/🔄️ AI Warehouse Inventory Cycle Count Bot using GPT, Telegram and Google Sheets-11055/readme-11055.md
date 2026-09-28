---
title: "🚀 AI Warehouse Inventory Cycle Count Bot: Tự động hóa kiểm kê kho bằng Telegram và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa kiểm kê kho bằng AI, Telegram và Google Sheets với n8n. Tiết kiệm thời gian, giảm sai sót và tối ưu hóa quy trình kiểm kê."
slug: "ai-warehouse-inventory-cycle-count-bot-telegram-google-sheets"
tags: [n8n, automation, no-code, inventory, warehouse]
keywords: [n8n workflow, tự động hóa kiểm kê kho, AI inventory, Telegram bot, Google Sheets]
---

# 🚀 AI Warehouse Inventory Cycle Count Bot: Tự động hóa kiểm kê kho bằng Telegram và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Kiểm kê kho hàng là một công việc quan trọng nhưng tốn thời gian và dễ xảy ra sai sót. Các sếp thường phải:
- Ghi chép thủ công số lượng hàng hóa tại từng vị trí
- So sánh với dữ liệu hệ thống
- Cập nhật kết quả vào hệ thống quản lý kho
- Xử lý các trường hợp ngoại lệ

Quy trình này dễ gây lỗi, tốn thời gian và không hiệu quả. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình kiểm kê bằng công nghệ AI, Telegram và Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian kiểm kê: Từ 30-50% thời gian thủ công
- Giảm sai sót: Hệ thống AI tự động trích xuất dữ liệu chính xác
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công
- Theo dõi tiến độ: Nhận thông báo Telegram về tiến độ kiểm kê
- Tích hợp với hệ thống hiện tại: Dễ dàng kết nối với Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã tạo sẵn (cấu trúc: location_id, system_quantity, actual_quantity, checked)
- Tài khoản Telegram và API token của bot Telegram
- Tài khoản OpenAI với API key (để sử dụng các tính năng AI)
- Google Sheets credentials cho n8n
- Telegram credentials cho n8n
- OpenAI credentials cho n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11055](https://n8n.io/workflows/11055)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

Hoặc copy/paste JSON vào n8n Editor:
```json
{
  "nodes": [...],
  "connections": [...],
  "settings": {...}
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger** node:
   - Chọn credentials của Telegram bot
   - Đảm bảo bot đã được thêm vào nhóm chat hoặc kênh kiểm kê

2. **Transcribe Operator Command** node:
   - Chọn credentials của OpenAI
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng API

3. **Model: Information Extraction** node:
   - Chọn model "gpt-4.1-mini" hoặc model phù hợp khác
   - Cấu hình prompt để trích xuất chính xác location_id và quantity

4. **Update Inventory Quantity** node:
   - Chọn credentials của Google Sheets
   - Điền ID của Google Sheet chứa dữ liệu kiểm kê
   - Đảm bảo Sheet có cấu trúc đúng (location_id, system_quantity, actual_quantity, checked)

5. **Collect Remaining Locations** node:
   - Cấu hình truy vấn để lấy các vị trí chưa được kiểm kê
   - Đảm bảo truy vấn chỉ lấy các bản ghi có checked = FALSE

6. **Get Locations to Check** node:
   - Cấu hình truy vấn tương tự như node Collect Remaining Locations

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một tin nhắn thử nghiệm đến bot Telegram
   - Kiểm tra xem hệ thống có nhận và xử lý tin nhắn đúng cách không
   - Xác minh dữ liệu đã được cập nhật trong Google Sheets

2. Bật Active workflow:
   - Sau khi test thành công, nhấn nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Teams:
   - Thêm node gửi thông báo đến các kênh cộng tác khác
   - Tạo báo cáo tổng hợp hàng ngày về tiến độ kiểm kê

2. Lưu log hoạt động:
   - Thêm node ghi log các hoạt động quan trọng
   - Dễ dàng theo dõi và audit các thay đổi

3. Gửi báo cáo định kỳ:
   - Thêm node tạo báo cáo tổng hợp sau khi hoàn thành kiểm kê
   - Gửi báo cáo qua email hoặc lưu vào Google Drive

4. Tích hợp với hệ thống WMS:
   - Thay thế Google Sheets bằng kết nối trực tiếp với hệ thống WMS
   - Đồng bộ dữ liệu kiểm kê với hệ thống chính

### 📌 Kết luận
Workflow AI Warehouse Inventory Cycle Count Bot giúp các sếp tự động hóa hoàn toàn quy trình kiểm kê kho hàng. Với sự kết hợp của AI, Telegram và Google Sheets, các sếp có thể tiết kiệm thời gian, giảm sai sót và tối ưu hóa quy trình kiểm kê một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất hoạt động của kho hàng!