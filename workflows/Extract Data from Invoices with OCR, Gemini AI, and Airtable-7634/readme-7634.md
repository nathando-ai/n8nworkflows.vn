---
title: "🚀 Tự động trích xuất dữ liệu hóa đơn bằng OCR, Gemini AI và Airtable"
description: "Giải pháp tự động 100% trích xuất thông tin từ hóa đơn (JPG/PNG/PDF) và lưu vào Airtable, gửi thông báo qua Telegram."
slug: "tang-dong-trich-xuat-hoa-don-o-ocr-gemini-airtable"
tags: [n8n, automation, no-code, ai-summarization, multimodal-ai, airtable, telegram, ocr, gemini]
keywords: [n8n workflow, tự động hóa, trích xuất dữ liệu, OCR, Gemini AI, Airtable, Telegram, invoice extraction, PDF extraction, AI summarization]
---

# 🚀 Tự động trích xuất dữ liệu hóa đơn bằng OCR, Gemini AI và Airtable

Bạn đang phải xử lý hàng trăm hóa đơn mỗi ngày?  
Mỗi lần mở file, đọc dữ liệu, nhập vào bảng tính hay hệ thống ERP là một công việc tốn thời gian, dễ sai sót và chi phí cao.  
Workflow này sẽ **đánh dấu** một bước ngoặt: **tự động 100%** nhận diện, trích xuất và lưu trữ dữ liệu từ hình ảnh hoặc PDF của hóa đơn, đồng thời gửi thông báo qua Telegram khi hoàn thành—**không cần viết một dòng code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xử lý thủ công xuống vài giây tự động.  
- **Độ chính xác cao**: OCR + Gemini AI giảm thiểu lỗi nhập liệu.  
- **Tích hợp liền mạch**: Dữ liệu ngay vào Airtable, dễ dàng báo cáo, phân tích.  
- **Thông báo tức thời**: Telegram gửi tin nhắn khi hoàn thành, giúp sếp luôn cập nhật.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **VPS hoặc máy chủ** có cài n8n (Self-hosted).  
- **Google Gemini API key** (đăng ký tại Google Cloud).  
- **Telegram Bot token** và **Chat ID** (để gửi tin nhắn).  
- **Airtable API token** và **Base ID** (để lưu dữ liệu).  
- **Thư mục** `/image-output/ocr` được mount vào n8n (để trigger nhận file).  
- **Node community**: `n8n-nodes-pdf-page-extract` và `n8n-nodes-tesseractjs`.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ [link workflow](https://n8n.io/workflows/7634).  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** → chọn file.  
3. Hoặc copy toàn bộ JSON và dán vào tab **Raw** → **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên trong workflow | Cần cấu hình gì? |
|------|---------------------|------------------|
| **Local File Trigger** | `Local File Trigger` | Đường dẫn `/image-output/ocr` (đảm bảo thư mục tồn tại). |
| **Check File Type** | `Check File Type` | Định nghĩa các file hợp lệ: `jpg`, `png`, `pdf`. |
| **Switch** | `Switch` | Chọn nhánh dựa trên loại file: `PDF` → `PDF Page Extract`, `Image` → `Tesseract`. |
| **PDF Page Extract** | `PDF Page Extract` | Đặt `Page range` (thường là `1-1` nếu