---
title: "🚀 Tự động hóa tạo báo cáo marketing từ Google Sheets với GPT-4 và PDF.co"
description: "Hướng dẫn xây dựng workflow n8n trích xuất dữ liệu marketing từ Google Sheets, sử dụng GPT-4 phân tích thông minh và xuất file PDF chuyên nghiệp qua PDF.co."
slug: "tao-bao-cao-marketing-google-sheets-gpt-4-pdf-co"
tags: [n8n, automation, google-sheets, gpt-4, pdf-co, ai]
keywords: [n8n workflow, tao bao cao marketing, google sheets automation, gpt-4 ai insights, pdf.co n8n]
---

# 🚀 Tự động hóa tạo báo cáo marketing từ Google Sheets với GPT-4 và PDF.co

Các sếp có đang cảm thấy mệt mỏi mỗi khi cuối tháng hay cuối tuần phải hì hục mở Google Sheets, copy số liệu chi tiêu quảng cáo, tự tính toán từng kênh, rồi lại vắt óc viết nhận xét và căn chỉnh file PDF để gửi sếp lớn hoặc khách hàng? Công việc thủ công lặp đi lặp lại này không chỉ ngốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia **Robert Breen** sẽ giúp các sếp giải quyết triệt để vấn đề này. Workflow này sẽ tự động hóa từ A-Z: lấy dữ liệu từ Google Sheets, tổng hợp chi tiêu theo từng kênh, nhờ AI (GPT-4) phân tích và viết tóm tắt chiến lược, sau đó xuất ra một bản báo cáo PDF cực kỳ chuyên nghiệp thông qua PDF.co!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh tổng hợp số liệu và viết báo cáo thủ công mỗi kỳ.
- **Phân tích thông minh:** GPT-4 tự động đưa ra các nhận xét, insight đắt giá về hiệu suất chiến dịch marketing.
- **Báo cáo chuyên nghiệp:** Biểu mẫu PDF đẹp mắt, chuẩn brand identity được tạo tự động qua PDF.co.
- **Hoạt động liền mạch:** Dễ dàng kích hoạt thủ công hoặc tích hợp lịch trình chạy định kỳ (Cron).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Google Account** (để kết nối Google Sheets).
- **OpenAI API Key** (Sử dụng mô hình `gpt-4.1-mini` hoặc tương đương).
- **Tài khoản PDF.co** (Miễn phí để lấy API Key và tạo Template HTML).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã JSON của workflow từ nguồn gốc (ID: 7861) hoặc copy đoạn JSON tương ứng dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Node `Get Marketing Data` (Google Sheets):**
  - Cần tạo Credential loại `Google Sheets OAuth2 Api`.
  - Copy [File Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1UDWt0-Z9fHqwnSNfU3vvhSoYCFG6EG3E-ZewJC_CLq4/edit?gid=365710158#gid=365710158) vào Google Drive cá nhân của các sếp.
  - Chọn đúng **Spreadsheet ID** và **Worksheet** tương ứng trong node.

- **Node `OpenAI Chat Model`:**
  - Chọn credential OpenAI đã chuẩn bị.
  - Đảm bảo model được chọn là `gpt-4.1-mini` (hoặc các biến thể GPT-4 phù hợp).

- **Node `Create PDF` (PDF.co Api):**
  - Tạo tài khoản miễn phí tại [PDF.co](https://pdf.co/), lấy API Key và cấu hình Credential `PDF.co API` trong n8n.
  - Vào **PDF.co Dashboard → HTML to PDF Templates**, tạo một **Mustache template** mới sử dụng mã HTML báo cáo.
  - Lấy **Template ID** dán vào tham số tương ứng trong node `Create PDF` (với thao tác `URL/HTML to PDF`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node `When clicking ‘Execute workflow’` để test chạy thử dữ liệu mẫu.
- Kiểm tra kết quả đầu ra tại node `Create PDF` để đảm bảo file PDF được tạo thành công.
- Bật công tắc **Active** để lưu lượng công việc sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node `manualTrigger` bằng node `Schedule Trigger` để n8n tự động tạo báo cáo vào thứ Hai hàng tuần hoặc ngày 1 hàng tháng.
- **Gửi báo cáo qua Email/Slack:** Nối thêm node Gmail, Microsoft Outlook hoặc Slack ở cuối workflow để tự động gửi file PDF báo cáo trực tiếp đến ban quản lý hoặc nhóm marketing.
- **Lưu trữ file:** Thêm node Google Drive hoặc Dropbox để lưu trữ tự động các file báo cáo PDF phục vụ việc tra cứu lịch sử.

### 📌 Kết luận
Workflow tạo báo cáo marketing tự động kết hợp Google Sheets, GPT-4 và PDF.co là một "vũ khí" cực mạnh giúp tối ưu hóa hiệu suất làm việc cho các marketer và agency. Hãy triển khai ngay hôm nay để giải phóng bản thân khỏi các tác vụ thủ công!