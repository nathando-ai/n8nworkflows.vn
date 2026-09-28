---
title: "🚀 Tự động hóa trích xuất & tổng hợp thông tin công ty từ Glassdoor với Google Gemini và Decodo"
description: "Hướng dẫn chi tiết cách tự động hóa việc trích xuất và tổng hợp thông tin công ty từ Glassdoor thành dữ liệu cấu trúc và bản tóm tắt bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả nghiên cứu thị trường."
slug: "tu-dong-hoa-trich-xuat-tong-hop-thong-tin-cong-ty-glassdoor"
tags: [n8n, automation, no-code, glassdoor, ai, market-research]
keywords: [n8n workflow, tự động hóa, glassdoor, ai summarization, market research]
---

# 🚀 Tự động hóa trích xuất & tổng hợp thông tin công ty từ Glassdoor với Google Gemini và Decodo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ trích xuất đến tổng hợp dữ liệu
- Chính xác: Sử dụng công nghệ AI tiên tiến của Google Gemini để phân tích và tổng hợp thông tin
- Cá nhân hóa: Tạo ra báo cáo chi tiết về từng công ty với các thông tin cụ thể như đánh giá, nhận xét, câu hỏi thường gặp
- Hoạt động liên tục: Workflow có thể chạy tự động theo lịch trình hoặc theo yêu cầu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Decodo với API key
- URL công ty trên Glassdoor
- Thiết lập n8n trên VPS (tự host) hoặc sử dụng dịch vụ cloud của n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link: https://n8n.io/workflows/9924
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When clicking ‘Execute workflow’" (manualTrigger)**:
   - Không cần cấu hình gì, chỉ cần nhấn "Execute Workflow" để bắt đầu quá trình

2. **Node "Set the Input Fields" (set)**:
   - Cấu hình các trường đầu vào:
     - `company_url`: URL công ty trên Glassdoor
     - `geo`: Vị trí địa lý (ví dụ: "US", "IN"...)
     - `output_file_path`: Đường dẫn lưu file kết quả (ví dụ: "C:\{{CompanyName}}.json")

3. **Node "Decodo" (@decodo/n8n-nodes-decodo.decodo)**:
   - Cấu hình credentials "decodoApi" với API key của bạn
   - Đảm bảo tài khoản Decodo có quyền truy cập vào Glassdoor

4. **Node "Google Gemini Chat Model for Summarization" (lmChatGoogleGemini)**:
   - Cấu hình credentials "googlePalmApi" với API key của bạn
   - Đảm bảo tài khoản Google Cloud có quyền truy cập vào Google Gemini

5. **Node "Google Gemini Chat Model for Structured Data Extract" (lmChatGoogleGemini)**:
   - Cấu hình credentials "googlePalmApi" với API key của bạn
   - Đảm bảo tài khoản Google Cloud có quyền truy cập vào Google Gemini

6. **Node "Read/Write Files from Disk" (readWriteFile)**:
   - Đảm bảo n8n có quyền ghi file vào đường dẫn đã cấu hình
   - Kiểm tra định dạng file đầu ra (JSON)

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu trước khi kích hoạt workflow chính thức
- Sau khi cấu hình xong, nhấn "Activate" để workflow chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tạo báo cáo định kỳ bằng cách kết hợp với node "Schedule Trigger"
- Tích hợp với các công cụ phân tích dữ liệu khác như Google Sheets, Airtable...

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình nghiên cứu thị trường bằng cách trích xuất và tổng hợp thông tin công ty từ Glassdoor một cách nhanh chóng và chính xác. Với công nghệ AI tiên tiến của Google Gemini và Decodo, bạn có thể nhận được những thông tin chi tiết và bản tóm tắt hữu ích để đưa ra quyết định kinh doanh sáng suốt. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả công việc!