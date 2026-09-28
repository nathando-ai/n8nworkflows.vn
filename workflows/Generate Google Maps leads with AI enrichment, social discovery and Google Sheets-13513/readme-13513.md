---
title: "🚀 Tự động quét Lead từ Google Maps, làm giàu dữ liệu bằng AI & Lưu Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm khách hàng tiềm năng toàn diện từ Google Maps, quét thông tin mạng xã hội, kiểm tra email, phân tích bằng AI và lưu vào Google Sheets."
slug: "tu-dong-quet-lead-google-maps-ai-google-sheets"
tags: [n8n, automation, lead-generation, google-maps, ai, google-sheets]
keywords: [n8n workflow, tạo lead google maps, ai enrichment, quét email tự động, serp api, n8n viet nam]
---

# 🚀 Tự động quét Lead từ Google Maps, làm giàu dữ liệu bằng AI & Lưu Google Sheets

Thay vì mất hàng giờ nghiên cứu doanh nghiệp thủ công bằng tay, workflow này sẽ lo thay các sếp từ A-Z! Chỉ cần cung cấp từ khóa tìm kiếm, hệ thống sẽ tự động tìm kiếm các doanh nghiệp trên Google Maps, thu thập website, số điện thoại, mạng xã hội, xác thực email, chạy qua AI để phân tích và viết tin nhắn tiếp cận (outreach) cá nhân hóa, tính điểm chất lượng (Lead Score) rồi tự động lưu gọn gàng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét dữ liệu hàng loạt từ Google Maps mà không cần copy/paste thủ công.
- **Làm giàu dữ liệu thông minh (AI Enrichment):** AI tự động đọc hiểu website doanh nghiệp, tóm tắt dịch vụ và viết sẵn nội dung chăm sóc khách hàng (outreach message) cực kỳ sát thực tế.
- **Lọc sạch data rác:** Tự động kiểm tra độ sống của email (Email Validation) và loại bỏ các bản ghi trùng lặp (Duplicate Removal).
- **Chấm điểm tiềm năng (Lead Scoring):** Đánh giá điểm số từng lead từ 0 đến 10 dựa trên độ hoàn thiện của hiện diện số.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Serper API Key** (Dùng để tìm kiếm thông tin mạng xã hội bổ sung).
- **Google Sheets Credentials (OAuth)** để lưu dữ liệu.
- **Email Validation API Key** (Dùng cho node `Validate Email Address`).
- **AI Model Endpoint** (Có thể dùng Ollama chạy local, hoặc OpenAI, Groq, Mistral, Anthropic...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste toàn bộ khối JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 35 nodes hoạt động nhịp nhàng, các sếp chú ý cấu hình kỹ các điểm sau:
- **`Start Lead Generation` & `Split Search Queries`**: Điền các từ khóa tìm kiếm mục tiêu của các sếp (Ví dụ: *"dentists in Pune"*, *"gyms in Hanoi"*,...).
- **`Save Leads to Google Sheets`**: Chọn credential Google Sheets OAuth, điền chính xác **Spreadsheet ID** và Sheet Name vào node này (đảm bảo cấu trúc cột sẵn sàng nhận dữ liệu).
- **Các node gọi API (Serper, Email Validation)**: Kết nối API Key tương ứng vào phần Credentials của các HTTP Request nodes.
- **Phần AI Nodes (`Analyze Business (AI)`, `Create Outreach Message`)**:
  - Nếu dùng **Ollama**: Thay đổi endpoint URL phù hợp với môi trường chạy (Docker Mac, Windows/Linux Docker, Local, hoặc Remote server).
  - Nếu dùng **OpenAI / Groq / Mistral**: Thay thế URL endpoint tương ứng và cấu hình Header `Authorization` với API Key của nhà cung cấp đó.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** chạy thử thủ công với một từ khóa mẫu để kiểm tra dòng chảy dữ liệu qua từng node (`Maps section` -> `Scraping` -> `Social` -> `Email Validation` -> `AI` -> `Export`).
- Kiểm tra kết quả hiển thị trên Google Sheets xem đã đổ về mượt mà chưa.
- Bật công tắc **Active** để hệ thống sẵn sàng hoạt động tự động bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay lập tức mỗi khi quét xong một mảng lead chất lượng cao.
- **Lưu lịch sử chạy:** Kết hợp thêm Google Drive node để lưu báo cáo tổng kết theo tuần/tháng.
- **Tối ưu tốc độ:** Điều chỉnh thông số thời gian ở các node `Rate Limit Protection` và `AI Rate Limit Buffer` để cân đối giữa tốc độ quét và giới hạn gọi API (Rate Limit) của các bên thứ ba.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp đội ngũ Sales và Marketing tiết kiệm hàng chục giờ đồng hồ mỗi tuần. Hãy trang bị ngay cho hệ thống n8n của các sếp để tối ưu hóa quy trình tìm kiếm khách hàng tiềm năng ngay hôm nay!