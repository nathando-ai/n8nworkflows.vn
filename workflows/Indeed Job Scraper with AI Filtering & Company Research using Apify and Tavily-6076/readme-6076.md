---
title: "🚀 Tự động quét việc làm trên Indeed với AI & Tavily Research trong n8n"
description: "Xây dựng hệ thống tự động hóa tìm kiếm việc làm trên Indeed, lọc bằng AI OpenAI, nghiên cứu công ty qua Tavily và lưu trữ gọn gàng vào Google Sheets."
slug: "indeed-job-scraper-ai-filtering-tavily-n8n"
tags: [n8n, automation, no-code, apify, openai, tavily, google-sheets, lead-generation]
keywords: [n8n workflow, indeed job scraper, apify n8n, tavily ai research, openai job filter, tự động hóa tìm việc]
---

# 🚀 Tự động quét việc làm trên Indeed với AI & Tavily Research trong n8n

Các sếp đang làm dịch vụ tuyển dụng, săn đầu người (Headhunter) hay tìm kiếm khách hàng tiềm năng qua tin tuyển dụng (B2B Lead Gen) chắc chắn hiểu rõ cảm giác mệt mỏi khi phải lướt Indeed mỗi ngày, thủ công lọc từng tin tuyển dụng, sau đó tra cứu thông tin công ty để gửi email chào hàng. Việc này ngốn rất nhiều thời gian và dễ bỏ sót cơ hội vàng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh mang tên **Indeed Job Scraper with AI Filtering & Company Research** do tác giả Adrian Bent xây dựng. Workflow này tự động hóa 100% quy trình từ quét dữ liệu, lọc trùng lặp, dùng AI đánh giá độ phù hợp, tìm kiếm thông tin người ra quyết định (Decision Maker) qua Tavily và lưu kết quả vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công search, copy/paste thông tin việc làm và công ty lên Excel nữa.
- **Lọc thông minh bằng AI:** Node OpenAI sẽ tự động đọc mô tả công việc và chọn ra những job thực sự phù hợp với tiêu chí của các sếp.
- **Nghiên cứu chuyên sâu:** Tự động dùng Tavily để tìm kiếm thông tin về công ty và người ra quyết định (DM), giúp cá nhân hóa nội dung tiếp cận.
- **Tránh trùng lặp dữ liệu:** Hệ thống kiểm tra kỹ lưỡng danh sách có sẵn trong Google Sheets để không bao giờ xử lý lại các job cũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Apify Account:** Để chạy Actor cào dữ liệu từ Indeed.
- **OpenAI API Key:** Cho node AI phân tích và lọc job.
- **Tavily API Key:** Dành cho việc tìm kiếm thông tin người ra quyết định và công ty (`Find DM`).
- **Google Sheets:** Tạo sẵn một bảng tính để lưu trữ danh sách việc làm và thông tin nghiên cứu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này hoặc tải file từ kho lưu trữ n8n, sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đã đưa workflow lên sàn, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Webhook:** Nhận tín hiệu kích hoạt khi Apify Actor quét xong dữ liệu. Cần copy URL webhook này cấu hình ngược lại vào Apify.
- **Get dataset items (Apify):** Kết nối tài khoản Apify (`apifyApi`), trỏ tới Actor cào Indeed để lấy danh sách kết quả thô (`Datasets` -> `Get items`).
- **Get row(s) in sheet & Append row in sheet (Google Sheets):** Kết nối tài khoản Google Sheets (`googleSheetsOAuth2Api`), chọn đúng file Spreadsheet và Sheet Name để lưu thông tin tuyển dụng và đọc dữ liệu kiểm tra trùng lặp.
- **Job Filter (OpenAI):** Cấu hình Credentials OpenAI (`openAiApi`). Viết Prompt phù hợp để AI đánh giá xem tin tuyển dụng có đáp ứng đúng tiêu chí dịch vụ của các sếp hay không (`Relevant Job posting?`).
- **Find DM (Tavily):** Cấu hình Credentials Tavily (`tavilyApi`) để hệ thống tự động tìm kiếm thông tin về công ty tuyển dụng và người ra quyết định.
- Các node logic như **Remove Duplicates**, **Filter 1**, **Loop Over Items1 (splitInBatches)** và **Wait** giúp dòng chảy dữ liệu mượt mà, không bị lỗi Rate Limit khi gọi API liên tục.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test step / Test workflow**) với một lượng dữ liệu nhỏ để kiểm tra luồng chạy qua các điều kiện IF, Merge.
- Sau khi mọi thứ xanh mướt, hãy bật công tắc **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ngay sau bước **Append row in sheet** để nhận thông báo tức thì ngay khi có một job tiềm năng được tìm thấy và lưu lại.
- **Cá nhân hóa Email:** Sử dụng kết quả nghiên cứu từ Tavily kết hợp thêm một bước gọi OpenAI nữa để viết sẵn nội dung email icebreaker (mở đầu) cực kỳ thuyết phục để gửi cho Decision Maker.
- **Mở rộng nguồn dữ liệu:** Không chỉ Indeed, các sếp có thể kết hợp thêm Apify Actor cào LinkedIn Jobs hoặc Google Jobs vào cùng một luồng xử lý.

### 📌 Kết luận
Workflow Indeed Job Scraper kết hợp AI và Tavily Research là một "vũ khí tối thượng" cho các đội ngũ Sales B2B và Headhunter thời đại số. Hãy cài đặt ngay hôm nay để tự động hóa toàn bộ quy trình tìm kiếm khách hàng tiềm năng và tối ưu hóa hiệu suất công việc của các sếp!