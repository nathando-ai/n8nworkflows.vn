---
title: "💰 Tự Động Xử Lý Hóa Đơn & Trích Lợi Tiền Trả Lại (Cashback) với JotForm + Gemini AI & Notion"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp xử lý hóa đơn, trích xuất thông tin chi tiết, tính toán cashback và gửi thông báo tự động đến khách hàng và team marketing. Tiết kiệm thời gian lên đến 90% so với cách làm thủ công!"
slug: "tu-dong-hoa-xu-ly-hoa-don-cashback-jotform-gemini-notion"
tags: [n8n, automation, no-code, jotform, gemini-ai, notion, cashback, ai-agent, receipt-processing]
keywords: [n8n workflow cashback, tự động hóa hóa đơn, gemini ai n8n, trích xuất hóa đơn tự động, cashback automation, jotform n8n, notion database integration]
---

# 🚀 **Tự Động Xử Lý Hóa Đơn & Trích Lợi Tiền Trả Lại (Cashback) với JotForm + Gemini AI & Notion**

### **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Quét và nhập thủ công** hàng trăm hóa đơn từ khách hàng qua JotForm.
- **Tìm kiếm sản phẩm** trong danh sách để tính toán cashback.
- **Gửi thông báo cá nhân hóa** cho từng khách hàng về số tiền được trả lại.
- **Lưu trữ dữ liệu** một cách rối loạn, khó theo dõi.

**Kết quả?** Thời gian làm việc tăng gấp 10 lần, dễ mắc lỗi, và trải nghiệm khách hàng không được tối ưu.

**Workflow này giải quyết tất cả!** Sử dụng **Gemini AI** để tự động trích xuất thông tin hóa đơn, tính toán cashback, và gửi thông báo tự động đến khách hàng **và** team marketing.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Tính toán cashback chính xác** với Gemini AI.
- **Gửi thông báo tự động** đến khách hàng (email) và team marketing (email nội bộ).
- **Lưu trữ dữ liệu** trong Notion, dễ theo dõi và phân tích.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản JotForm** (đã tạo form nhận hóa đơn).
2. **API Key JotForm** (phải cấp quyền **"Full Access"** để tải file).
3. **Tài khoản Gmail** (để gửi email xác nhận và thông báo marketing).
4. **Tài khoản Notion** (đã tạo database để lưu trữ thông tin cashback).
5. **API Key Gemini AI** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
6. **VPS n8n** (để workflow chạy 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9417](https://n8n.io/workflows/9417) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted** (nếu chạy trên VPS).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình JotForm Trigger**
- **Thiết lập Webhook** theo hướng dẫn dưới đây:
  ```markdown
  1. Mở JotForm → Chọn form → **Settings** → **Integrations**.
  2. Tìm **Webhooks** → Dán URL Webhook từ node **JotForm Trigger** trong workflow.
  3. Lưu và kích hoạt.
  ```
- **Điền API Key JotForm** vào:
  - Node **JotForm Trigger** (Credentials).
  - Node **Fetch All Receipts** (Query Parameters).

##### **B. Cấu Hình Gemini AI**
- **Đăng ký API Key Gemini** tại [Google AI Studio](https://makersuite.google.com/).
- **Điền vào node "Google Gemini Chat Model"** (Prompt đã được tối ưu sẵn):
  ```json
  "prompt": "Analyze this receipt text and extract structured data including:
  - Product names
  - Prices
  - Cashback eligible products
  - Total cashback amount"
  ```

##### **C. Cấu Hình Notion Database**
- **Tạo một database mới** trong Notion với các trường:
  - `Customer Name` (Text)
  - `Email` (Email)
  - `Cashback Amount` (Number)
  - `Transaction Date` (Date)
- **Điền Database ID** vào node **Add info to Database**.

##### **D. Cấu Hình Email (Gmail)**
- **Thiết lập SMTP Gmail** trong node **Customer Email** và **Marketing Email**:
  ```markdown
  - **Username**: Email của bạn (ví dụ: `tendangky@gmail.com`)
  - **Password**: App Password (nếu sử dụng 2FA)
  - **Host**: `smtp.gmail.com`
  - **Port**: `465` (SSL)
  ```

##### **E. Cấu Hình OCR.Space (Nếu cần)**
- **Đăng ký API Key** tại [OCR.Space](https://ocr.space/).
- **Điền vào node "OCR.Space"** (nếu muốn sử dụng OCR thay vì Gemini).

#### **3. Kích Hoạt ⚡️**
- **Test Run** với một hóa đơn mẫu để kiểm tra workflow.
- **Bật Active** và **đợi phản hồi tự động** từ n8n.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
- **Kết hợp với Slack/Telegram**: Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo lỗi hoặc thành công.
- **Lưu Log**: Thêm node **StickyNote** để ghi lại lịch sử xử lý.
- **Báo Cáo Định Kỳ**: Sử dụng node **Gmail** hoặc **Notion** để gửi báo cáo tổng hợp hàng tháng cho team.
- **Cải Tiến Gemini Prompt**: Nếu cashback tính sai, điều chỉnh prompt để Gemini hiểu rõ hơn về sản phẩm của bạn.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng trải nghiệm khách hàng** với thông báo cá nhân hóa, và **tối ưu hóa team marketing** với dữ liệu chi tiết.

**🚀 Hãy áp dụng ngay!**
- **Nếu chưa có VPS**, đăng ký ngay [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N** (giảm tới 39%).
- **Hoặc chọn VPS Xeon 4GB chỉ 50k/tháng** tại [BNIX](https://my.bnix.one/aff.php?aff=172).

**Chúc các sếp thành công!** 💪