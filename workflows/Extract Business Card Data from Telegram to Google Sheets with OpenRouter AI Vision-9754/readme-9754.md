---
title: "🚀 Tự động trích xuất danh thiếp (Business Card) từ Telegram qua OpenRouter AI Vision vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc ảnh danh thiếp gửi qua Telegram, dùng AI Vision trích xuất thông tin và lưu thẳng vào Google Sheets."
slug: "trich-xuat-danh-thiep-telegram-google-sheets-ai-vision"
tags: [n8n, automation, telegram, google-sheets, ai-vision, openrouter]
keywords: [n8n workflow, tự động hóa danh thiếp, telegram to google sheets, openrouter ai vision, ocr danh thiếp]
---

# 🚀 Tự động trích xuất danh thiếp (Business Card) từ Telegram qua Google Sheets với AI Vision

Các sếp đi sự kiện, hội thảo về mang theo cả đống danh thiếp (namecard) rồi tối về ngồi gõ mỏi tay vào file Excel hoặc CRM? Việc nhập liệu thủ công này cực kỳ mất thời gian, dễ sai sót và làm giảm hiệu suất làm việc của đội ngũ Sales.

Giải pháp ở đây là gì? Hãy để **n8n** lo! Workflow này sẽ giúp các sếp tự động hóa 100% quy trình: chỉ cần chụp ảnh danh thiếp ném vào **Telegram Bot**, AI sẽ tự động đọc, bóc tách thông tin (tên, chức vụ, công ty, email, số điện thoại,...) và lưu ngay vào **Google Sheets**. Không cần code một dòng nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải gõ thủ công từng chiếc namecard sau mỗi buổi networking.
- **Độ chính xác cao:** Ứng dụng sức mạnh của AI Vision (qua OpenRouter) nhận diện cực tốt các trường thông tin phức tạp.
- **Đồng bộ thời gian thực:** Dữ liệu có mặt ngay trên Google Sheets ngay khi vừa gửi ảnh lên Telegram.
- **Hoạt động 24/7:** Bot Telegram luôn sẵn sàng nhận ảnh bất cứ lúc nào các sếp đang di chuyển.
:::

### 📦 Các Nodes chính trong Workflow
Workflow này gồm 6 nodes chính hoạt động mượt mà với nhau:
1. **Telegram Trigger**: Nhận tin nhắn (hình ảnh danh thiếp) gửi tới Bot.
2. **Check Input Type (IF Node)**: Kiểm tra xem tin nhắn gửi vào có chứa hình ảnh hay không.
3. **AI Vision Agent**: Tác nhân AI xử lý hình ảnh, phân tích các trường thông tin.
4. **OpenAI Vision Model (OpenRouter)**: Mô hình AI thị giác máy tính nhận diện nội dung trên danh thiếp.
5. **Ingredient Parser (Output Parser Structured)**: Định dạng kết quả trả về chuẩn JSON sạch sẽ.
6. **Add to Google Sheet**: Tự động thêm mới hoặc cập nhật thông tin liên hệ vào file Google Sheets (`appendOrUpdate`).

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot**: Tạo một bot thông qua [@BotFather](https://t.me/BotFather) để lấy API Token.
- **Tài khoản OpenRouter**: Cần có API Key của OpenRouter để sử dụng các mô hình AI Vision mạnh mẽ.
- **Google Sheets**: Chuẩn bị sẵn một file Google Sheets chứa các cột thông tin cần lưu (Tên, Công ty, Chức vụ, Email, Số điện thoại, Địa chỉ...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Telegram Trigger`**: Kết nối với tài khoản Telegram của các sếp bằng cách điền **Telegram API Token** từ BotFather. Đảm bảo bot đã được kích hoạt và khởi chạy (Start).
- **Node `OpenAI Vision Model`**: Điền **OpenRouter API Key** và chọn mô hình Vision phù hợp (ví dụ: Claude 3.5 Sonnet hoặc GPT-4o qua OpenRouter để đạt độ chính xác OCR tốt nhất).
- **Node `Ingredient Parser`**: Kiểm tra cấu trúc JSON schema để đảm bảo AI trả về đúng các trường dữ liệu mà các sếp muốn lưu (Company, Name, Department, Job Title, Phone, Email, Address,...).
- **Node `Add to Google Sheet`**: Kết nối tài khoản Google qua OAuth2, sau đó chọn đúng file Spreadsheet và Sheet Name đã chuẩn bị. Map các trường dữ liệu từ AI Parser vào đúng các cột tương ứng trong Google Sheets (sử dụng chế độ `appendOrUpdate`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** ở Telegram Trigger và gửi thử một bức ảnh danh thiếp vào bot của bạn để test.
- Kiểm tra xem dữ liệu có đổ về Google Sheets chuẩn xác không.
- Gạt công tắc sang **Active** để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram**: Thêm một node Telegram ở cuối workflow để bot gửi tin nhắn phản hồi lại *"✅ Đã lưu danh thiếp của [Tên] vào Google Sheets thành công!"* cho các sếp yên tâm.
- **Gửi email chào mừng tự động**: Nếu danh thiếp có email, có thể tích hợp thêm node Gmail để tự động gửi email giới thiệu bản thân/doanh nghiệp ngay lập tức sau khi quét xong.
- **Tích hợp CRM**: Thay vì chỉ lưu Google Sheets, các sếp có thể đẩy thẳng dữ liệu vào Hubspot, Salesforce hoặc Notion CRM.

### 📌 Kết luận
Chỉ với vài phút thiết lập workflow n8n này, các sếp đã sở hữu ngay một trợ lý AI thông minh chuyên xử lý danh thiếp cực kỳ chuyên nghiệp. Bắt tay vào làm ngay thôi nào!