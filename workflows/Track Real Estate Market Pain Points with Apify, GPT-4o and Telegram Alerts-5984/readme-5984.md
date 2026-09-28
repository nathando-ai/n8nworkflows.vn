---
title: "🏡 Tự động hóa theo dõi thị trường bất động sản với Apify, GPT-4o và cảnh báo Telegram"
description: "Hướng dẫn tự động hóa theo dõi thị trường bất động sản hàng ngày, phát hiện điểm đau và nhận cảnh báo qua Telegram - giải pháp toàn diện cho các chuyên gia bất động sản"
slug: "tu-dong-hoa-theo-doi-thi-truong-bat-dong-san"
tags: [n8n, automation, no-code, real estate, market research]
keywords: [n8n workflow, tự động hóa bất động sản, AI thị trường, cảnh báo Telegram, Apify]
---

# 🏡 Tự động hóa theo dõi thị trường bất động sản với Apify, GPT-4o và cảnh báo Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các chuyên gia bất động sản khi phải theo dõi thị trường thủ công hàng ngày. Giới thiệu workflow như giải pháp tự động hóa toàn diện 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quá trình theo dõi thị trường hàng ngày
- **Phát hiện điểm đau sớm**: AI tự động nhận diện 3 điểm đau thị trường hàng ngày
- **Phát hiện xu hướng**: So sánh với dữ liệu ngày hôm trước để nhận diện xu hướng mới
- **Thông báo tức thì**: Nhận cảnh báo qua Telegram ngay khi có điểm đau mới xuất hiện
- **Lưu trữ dữ liệu**: Tích lũy dữ liệu lịch sử trong Airtable cho phân tích dài hạn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify (để scrape dữ liệu từ Google)
- API Key OpenAI (để sử dụng GPT-4o)
- Bot Telegram và Chat ID (để nhận cảnh báo)
- Tài khoản Airtable (để lưu trữ dữ liệu)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5984)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình thời gian chạy hàng ngày (ví dụ: 8:00 AM mỗi ngày)

2. **Apify Scraper**:
   - Cần cấu hình credentials cho Apify
   - Thay đổi query tìm kiếm nếu cần theo dõi chủ đề khác

3. **OpenAI Chat Model**:
   - Cấu hình credentials cho OpenAI
   - Đảm bảo chọn model "gpt-4o-mini" hoặc cao hơn

4. **Read Yesterday Pain Points**:
   - Cấu hình credentials cho Airtable
   - Đảm bảo bảng Airtable đã được tạo với cấu trúc phù hợp

5. **Telegram Notifier**:
   - Cấu hình credentials cho Telegram
   - Điền đúng Chat ID để nhận cảnh báo

6. **Store to Airtable**:
   - Cấu hình credentials cho Airtable
   - Đảm bảo bảng Airtable đã được tạo với cấu trúc phù hợp

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với workflow gửi email tự động để thông báo cho đội ngũ
- Thêm node để lưu trữ dữ liệu vào Google Sheets thay vì Airtable
- Tích hợp với CRM để tự động tạo lead từ các điểm đau mới phát hiện
- Thêm node để gửi báo cáo hàng tuần qua email
- Kết nối với Slack để nhận cảnh báo thay vì Telegram

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho các chuyên gia bất động sản để theo dõi thị trường một cách hiệu quả. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào các chiến lược quan trọng hơn thay vì phải theo dõi thị trường thủ công hàng ngày. Hãy triển khai ngay để nhận được thông tin thị trường mới nhất một cách nhanh chóng và chính xác!