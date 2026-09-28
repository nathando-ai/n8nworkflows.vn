---
title: "🚀 Tự động hóa chẩn đoán HVAC với AI Gemini, GoHighLevel và WhatsApp"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp quản lý yêu cầu HVAC, phân tích ảnh bằng AI và thông báo kỹ thuật viên qua WhatsApp"
slug: "tu-dong-hoa-chan-doan-hvac-voi-ai-gemini-gohighlevel-whatsapp"
tags: [n8n, automation, no-code, ai, crm]
keywords: [n8n workflow, tự động hóa, ai chẩn đoán, gohighlevel, whatsapp]
---

# 🚀 Tự động hóa chẩn đoán HVAC với AI Gemini, GoHighLevel và WhatsApp

[Các sếp đang gặp khó khăn khi xử lý hàng nghìn yêu cầu HVAC hàng ngày. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhận yêu cầu đến thông báo kỹ thuật viên - hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân tích ảnh HVAC bằng AI Gemini Vision (đánh giá tình trạng sửa chữa)
- Tự động tạo lead trong GoHighLevel CRM
- Tự động thông báo kỹ thuật viên qua WhatsApp (bao gồm ảnh và kết quả phân tích)
- Tiết kiệm 80% thời gian xử lý yêu cầu HVAC hàng ngày
- Tăng độ chính xác chẩn đoán nhờ AI
- Hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Gemini Vision (để phân tích ảnh)
- Tài khoản GoHighLevel CRM (để lưu lead)
- Tài khoản WhatsApp Business API (để gửi thông báo)
- Form nhận yêu cầu HVAC (có trường upload ảnh)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15104](https://n8n.io/workflows/15104)
2. Click "Import" và chọn "Import from URL"
3. Dán link workflow vào và nhấn "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "When Form Submitted"**: Cấu hình form trigger để nhận trường upload ảnh
- **Node "Post to Gemini API"**: Cấu hình credentials Google Palm API
- **Node "Create Lead in GoHighLevel"**: Cấu hình credentials GoHighLevel OAuth2 API
- **Node "Send WhatsApp to Technician"**: Cấu hình credentials WhatsApp API và số điện thoại kỹ thuật viên

#### 3. Kích hoạt ⚡️
1. Test workflow với dữ liệu mẫu
2. Kiểm tra kết quả ở cả 3 hệ thống (Gemini, GoHighLevel, WhatsApp)
3. Bật Active workflow khi đã kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo cho quản lý khi có yêu cầu mới
- Tích hợp với hệ thống quản lý công việc (Jira, Trello)
- Thêm chức năng nhận phản hồi từ kỹ thuật viên qua WhatsApp
- Tự động hóa báo cáo hàng tuần về tình trạng HVAC
- Kết nối với hệ thống quản lý tài liệu (Google Drive, Dropbox)

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc xử lý yêu cầu HVAC. Bằng cách kết hợp AI Gemini Vision, GoHighLevel CRM và WhatsApp, các sếp có thể tự động hóa toàn bộ quy trình từ nhận yêu cầu đến thông báo kỹ thuật viên - hoàn toàn không cần code. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ kỹ thuật HVAC!