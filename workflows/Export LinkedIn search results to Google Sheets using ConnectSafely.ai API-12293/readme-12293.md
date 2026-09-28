---
title: "🚀 Tự Động Xuất Kết Quả Tìm Kiếm LinkedIn Sang Google Sheets Với ConnectSafely.ai API"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động tìm kiếm profile LinkedIn không cần cookie và lưu trữ trực tiếp vào Google Sheets hoặc JSON."
slug: "xuat-tim-kiem-linkedin-ra-google-sheets-n8n"
tags: [n8n, automation, no-code, linkedin, lead-generation, google-sheets, api]
keywords: [n8n workflow, tự động hóa linkedin, connectsafely api, xuất dữ liệu linkedin, google sheets automation]
---

# 🚀 Tự Động Xuất Kết Quả Tìm Kiếm LinkedIn Sang Google Sheets Với ConnectSafely.ai API

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) trên LinkedIn theo cách thủ công cực kỳ tốn thời gian: phải copy từng profile, dán vào file Excel, chưa kể rủi ro bị LinkedIn quét tài khoản nếu dùng các công cụ auto dạng extension rườm rà. 

Giải pháp ư? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: gọi API tìm kiếm profile chuyên nghiệp, làm sạch dữ liệu và đổ thẳng vào Google Sheets hoặc file JSON một cách an toàn, không cần lo về cookie hay rủi ro block tài khoản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Tìm kiếm profile theo từ khóa, địa điểm, chức danh mà không cần thao tác tay.
- **An toàn tuyệt đối:** Sử dụng ConnectSafely.ai API chuẩn chỉnh, tuân thủ nền tảng, không sợ khóa tài khoản LinkedIn.
- **Dữ liệu sẵn sàng:** Thu về hơn 100+ kết quả mỗi lần quét và đồng bộ ngay vào Google Sheets để đội sales chăm sóc.
- **Linh hoạt đầu ra:** Hỗ trợ xuất dữ liệu song song dạng Google Sheets và file JSON để dùng cho các mục đích khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản và API Key tại [ConnectSafely.ai](https://connectsafely.ai/dashboard) (Vào Settings → API Keys).
- Tài khoản Google có quyền tạo và chỉnh sửa Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n hoặc copy đoạn mã JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

- **Node `Search LinkedIn People` (HTTP Request):** 
  - Cần thiết lập Credentials dạng **HTTP Bearer Auth** hoặc **HTTP Header Auth** với API Key lấy từ ConnectSafely.ai.
- **Node `Set Search Parameters` (Set):** 
  - Cấu hình các tham số tìm kiếm mong muốn như từ khóa (keywords), địa điểm (location), chức danh (job title).
- **Node `Export to Google Sheets` (Google Sheets):** 
  - Chọn Credentials là **Google Sheets OAuth2 API**.
  - Cập nhật đúng **Spreadsheet ID** và tên Sheet của các sếp vào ô cấu hình. Đảm bảo thao tác (operation) được đặt là `append` (thêm dòng mới).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử công cụ thủ công từ node `Manual Trigger` để kiểm tra kết quả trả về từ API và dữ liệu đã vào Google Sheets chưa.
- Khi mọi thứ mượt mà, gạt công tắc sang **Active** để bật chế độ tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước `Export to Google Sheets` để bắn tin nhắn báo cáo ngay khi quét xong danh sách khách hàng mới.
- **Lên lịch chạy định kỳ:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để n8n tự động quét LinkedIn hàng tuần/hàng tháng mà không cần động tay.
- **Kết hợp AI làm giàu dữ liệu:** Đưa danh sách kết quả qua node OpenAI/Claude để phân loại mức độ tiềm năng trước khi đẩy vào Google Sheets.

### 📌 Kết luận
Workflow này là "vũ khí" cực mạnh cho các đội ngũ Sales và Marketing muốn xây dựng hệ thống inbound lead từ LinkedIn một cách tự động và chuyên nghiệp. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian prospecting cho team!