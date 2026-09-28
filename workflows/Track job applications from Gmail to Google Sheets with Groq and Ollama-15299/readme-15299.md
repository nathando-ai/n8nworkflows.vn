---
title: "🚀 Tự động theo dõi đơn ứng tuyển từ Gmail đến Google Sheets với Groq và Ollama"
description: "Hướng dẫn tự động hóa quá trình theo dõi đơn ứng tuyển từ Gmail đến Google Sheets với AI Groq và Ollama, tiết kiệm thời gian và nâng cao hiệu quả tìm việc"
slug: "tu-dong-theo-doi-don-ung-tuyen-gmail-google-sheets-groq-ollama"
tags: [n8n, automation, no-code, gmail, google-sheets, ai, llm]
keywords: [n8n workflow, tự động hóa, theo dõi đơn ứng tuyển, groq, ollama, google sheets]
---

# 🚀 Tự động theo dõi đơn ứng tuyển từ Gmail đến Google Sheets với Groq và Ollama

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công hàng chục đơn ứng tuyển qua email. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi hàng trăm email ứng tuyển mỗi ngày
- Phân loại tự động đơn ứng tuyển thành 4 trạng thái: Đã ứng tuyển, Phỏng vấn, Từ chối, Nhận offer
- Tiết kiệm thời gian lên tới 80% so với phương pháp thủ công
- Dữ liệu được lưu trữ và quản lý tập trung trên Google Sheets
- Tự động tổng hợp báo cáo hàng ngày về tình hình ứng tuyển
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail đã kích hoạt API
- Tài khoản Google Workspace (để sử dụng Google Sheets API)
- API key từ Groq (hoặc cài đặt Ollama local)
- Google Sheet đã chuẩn bị với các cột: `company`, `role`, `status`, `Application Link`, `Last Update Date`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15299](https://n8n.io/workflows/15299)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, chọn "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Gmail Trigger & Gmail Backfill**:
   - Cấu hình credentials Gmail OAuth2
   - Đảm bảo tài khoản Gmail đã bật IMAP và API

2. **Node Google Sheets**:
   - Cấu hình credentials Google Sheets OAuth2
   - Điền URL Google Sheet vào trường "URL"
   - Điền Sheet ID vào trường "ID" (phần `<Google-sheet-ID>` trong URL)

3. **Node AI Classification**:
   - Đối với Groq: Thêm API key vào credentials
   - Đối với Ollama: Đảm bảo đã cài đặt Ollama local và chạy dịch vụ

4. **Node Schedule Trigger**:
   - Thiết lập thời gian chạy hàng ngày (mặc định là 8:00 AM)

#### 3. Kích hoạt ⚡️
1. Chạy test với 1 email mẫu để kiểm tra toàn bộ luồng
2. Kích hoạt workflow bằng cách bật nút "Active"

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh mô hình AI**:
   - Thay đổi mô hình Groq từ `llama-3.3-70b-versatile` sang các mô hình khác như `mixtral-8x7b-32768`
   - Đối với Ollama, có thể thử các mô hình khác như `llama3.1:8b`

2. **Kết nối thêm dịch vụ**:
   - Thêm node Slack để nhận thông báo khi có đơn ứng tuyển mới
   - Kết nối với Notion thay vì Google Sheets để lưu trữ dữ liệu

3. **Tối ưu hiệu suất**:
   - Thiết lập bộ lọc email trong Gmail để giảm số lượng email xử lý
   - Sử dụng mô hình local (Ollama) để tránh giới hạn API của Groq

4. **Báo cáo nâng cao**:
   - Thêm node để gửi báo cáo hàng tuần qua email
   - Tạo biểu đồ trực quan hóa dữ liệu trên Google Sheets

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi đơn ứng tuyển, giảm thiểu công việc thủ công và tập trung vào những cơ hội việc làm quan trọng. Với khả năng tích hợp AI tiên tiến, workflow này không chỉ tiết kiệm thời gian mà còn nâng cao độ chính xác trong việc phân loại và quản lý đơn ứng tuyển. Hãy thử ngay và bắt đầu cuộc hành trình tìm việc hiệu quả hơn!