---
title: "🚀 Tự động trích xuất lệnh giao dịch chứng khoán Indonesia (IDX) từ Telegram bằng Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc hóa đơn/xác nhận giao dịch chứng khoán IDX từ Telegram, phân tích bằng Gemini AI qua OpenRouter và gửi xác nhận tương tác."
slug: "trich-xuat-chung-khoan-indonesia-telegram-gemini-ai"
tags: [n8n, automation, telegram, ai, openrouter, gemini]
keywords: [n8n workflow, trích xuất hóa đơn, chứng khoán indonesia, idx telegram, ai extraction, openrouter gemini]
---

# 🚀 Tự động trích xuất lệnh giao dịch chứng khoán Indonesia (IDX) từ Telegram bằng Gemini AI

Các nhà đầu tư và nhà quản lý quỹ thường xuyên đối mặt với việc xử lý hàng loạt các file PDF hoặc hình ảnh xác nhận giao dịch (trade confirmation) từ các công ty chứng khoán Indonesia (IDX). Việc nhập liệu thủ công các thông tin như mã cổ phiếu, khối lượng, giá mua/bán vừa mất thời gian, dễ sai sót lại vừa làm giảm năng suất.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code. Chỉ cần gửi file xác nhận vào bot Telegram, hệ thống sẽ tự động tải xuống, gọi AI (Gemini qua OpenRouter) để cấu trúc hóa dữ liệu giao dịch và gửi lại bảng xác nhận trực quan cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Biến file PDF/Ảnh xác nhận giao dịch thành dữ liệu JSON sạch chỉ trong tích tắc.
- **AI thông minh**: Sử dụng mô hình Gemini (qua OpenRouter) để bóc tách chính xác các thông tin phức tạp từ hóa đơn chứng khoán.
- **Tương tác trực quan**: Gửi thông báo kèm nút bấm xác nhận trực tiếp trên Telegram trước khi lưu trữ vào hệ thống.
- **Linh hoạt mở rộng**: Dễ dàng kết nối dữ liệu đã trích xuất tới Google Sheets, Airtable, Notion hoặc cơ sở dữ liệu riêng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted bản mới nhất).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Tài khoản OpenRouter & API Key** để sử dụng mô hình Gemini (Google Gemini Flash/Pro).
- **Môi trường n8n hỗ trợ HTTPS** (Webhook của Telegram yêu cầu URL công khai qua Cloudflare Tunnel, ngrok hoặc VPS có domain chuẩn SSL).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON workflow được cung cấp, copy toàn bộ nội dung và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, hãy cấu hình kỹ các node trọng điểm sau:
- **Telegram Trigger**: Thêm credential tài khoản Telegram Bot của các sếp để nhận tin nhắn và file từ người dùng.
- **Download File**: Node này sử dụng resource `file` để tải tài liệu từ Telegram servers về xử lý.
- **OpenRouter Extract (HTTP Request)**: Cấu hình Header Auth credential mang tên **OpenRouter API** với giá trị `Authorization: Bearer sk-or-...`. Kiểm tra payload trong node **Build Request** (mặc định sử dụng model `google/gemini-2.5-flash-lite`).
- **Send Confirmation & Reply Invoice Error**: Các node Telegram chịu trách nhiệm gửi bảng tổng hợp giao dịch kèm nút bấm (✅ / ❌) hoặc phản hồi lỗi khi đọc file.

#### 3. Kích hoạt ⚡️
- Gửi thử một file PDF hoặc hình ảnh xác nhận giao dịch mẫu đến Telegram Bot để kiểm tra (`Test workflow`).
- Nếu dữ liệu trả về chính xác, hãy gạt công tắc sang **Active** để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động**: Kết nối đầu ra của node **Format Confirmation** tới Google Sheets hoặc Airtable để lưu lại toàn bộ lịch sử giao dịch.
- **Cảnh báo qua Slack/Telegram**: Thêm nhánh thông báo riêng nếu phát hiện lỗi đọc hóa đơn (`Invoice Error?`) để bộ phận kế toán xử lý kịp thời.
- **Đổi AI Model**: Các sếp có thể tinh chỉnh prompt trong node **Build Request** hoặc đổi sang các model LLM mạnh mẽ hơn trên OpenRouter tùy theo độ phức tạp của hóa đơn.

### 📌 Kết luận
Workflow xử lý hóa đơn chứng khoán IDX này là một ví dụ tuyệt vời cho việc ứng dụng AI Agent và No-code vào nghiệp vụ tài chính thực tế. Hãy "lên đồ" ngay hôm nay để tối ưu hóa quy trình làm việc của các sếp!