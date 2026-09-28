---
title: "🚀 Tự động gửi gợi ý sách qua Email bằng Ollama AI và OpenLibrary API với n8n"
description: "Xây dựng hệ thống tự động đọc email yêu cầu sách, phân tích ý định bằng Ollama LLM, tìm kiếm thông tin từ OpenLibrary và gửi email gợi ý cá nhân hóa 100% miễn phí."
slug: "tu-dong-goi-y-sach-qua-email-ollama-ai-openlibrary-n8n"
tags: [n8n, automation, no-code, ai, ollama, openlibrary, email-automation]
keywords: [n8n workflow, gợi ý sách tự động, ollama ai, openlibrary api, email automation, tự động hóa n8n]
keywords: [n8n workflow, gợi ý sách tự động, ollama ai, openlibrary api, email automation, tự động hóa n8n]
---

# 🚀 Tự động gửi gợi ý sách qua Email bằng Ollama AI và OpenLibrary API

Các sếp có bao giờ đau đầu khi phải liên tục phản hồi các yêu cầu tìm kiếm tài liệu, gợi ý sách từ khách hàng, thành viên câu lạc bộ đọc sách hay học viên? Việc đọc thủ công từng email, tra cứu thông tin sách trên mạng và soạn email phản hồi tốn rất nhiều thời gian và công sức.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một **n8n workflow** tự động hóa từ A-Z quy trình này. Sử dụng sức mạnh của **Ollama LLM** (chạy cục bộ miễn phí hoặc qua API) kết hợp với **OpenLibrary API**, hệ thống sẽ tự động đọc email, hiểu ý định người dùng, tìm kiếm sách phù hợp và gửi lại một email gợi ý cực kỳ chuyên nghiệp và cá nhân hóa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Hệ thống liên tục lắng nghe hộp thư đến và xử lý yêu cầu ngay lập tức mà không cần con người can thiệp.
- **Trí tuệ nhân tạo Ollama:** Hiểu chính xác thể loại, sở thích và ngữ cảnh mà người dùng yêu cầu qua email (ví dụ: *"Gợi ý cho tôi một cuốn tiểu thuyết khoa học viễn tưởng"*).
- **Dữ liệu phong phú:** Kết nối OpenLibrary API để lấy thông tin sách, tóm tắt và chi tiết chính xác.
- **Cá nhân hóa cao:** Tự động soạn thảo và gửi email phản hồi đẹp mắt, chuyên nghiệp tới đúng người yêu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản Email (IMAP/SMTP):** Hộp thư để nhận yêu cầu sách và gửi email phản hồi.
- **Ollama:** Đã cài đặt và cấu hình model (ví dụ: `llama3.2-16000:latest`) kết nối với n8n qua `lmChatOllama`.
- **OpenLibrary API:** Không cần API Key, hoàn toàn miễn phí để truy xuất dữ liệu sách.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được thiết kế tỉ mỉ. Các sếp cần chú ý cấu hình các điểm sau:
- **Email Trigger – Book Request (`emailReadImap`):** Cấu hình thông tin đăng nhập IMAP của hộp thư dùng để nhận yêu cầu sách từ khách hàng/thành viên.
- **Ollama Model (`lmChatOllama`) & Analyze Email with Ollama (`agent`):** Kết nối với Ollama instance của các sếp và đảm bảo model `llama3.2-16000:latest` (hoặc model tương đương) đã sẵn sàng hoạt động.
- **Call Book Search API (`httpRequest`):** Cấu hình endpoint gọi tới OpenLibrary API để tìm kiếm sách dựa trên truy vấn mà AI đã tạo ra.
- **Check API Response (`if`) & Handle No Book Found (`emailSend`):** Thiết lập logic kiểm tra nếu API không tìm thấy sách, hệ thống sẽ tự động gửi email thông báo lịch sự tới người dùng.
- **Send Recommendation Email (`emailSend`):** Cấu hình thông tin SMTP để gửi email chứa danh sách sách gợi ý và tóm tắt chi tiết về hộp thư của người gửi yêu cầu.

#### 3. Kích hoạt ⚡️
- Nhấn **"Execute Workflow"** và gửi một email test (chẳng hạn với nội dung: *"Gợi ý cho tôi một cuốn sách hay về lập trình"*) để kiểm tra luồng chạy.
- Sau khi test thành công, bật công tắc **Active** để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận yêu cầu:** Thay vì chỉ nhận qua Email, các sếp có thể kết hợp thêm node Telegram hoặc Slack để nhận yêu cầu chat trực tiếp từ team.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable vào luồng để lưu lại lịch sử các yêu cầu và sách đã gợi ý nhằm phục vụ việc phân tích sau này.
- **Tích hợp AI Agent nâng cao:** Tùy chỉnh prompt trong Ollama Agent để AI có thể gợi ý kèm theo bài học rút ra từ cuốn sách hoặc tạo hình ảnh minh họa bằng AI.

### 📌 Kết luận
Workflow tích hợp Ollama LLM và OpenLibrary API là giải pháp tuyệt vời để tự động hóa quy trình chăm sóc khách hàng, xây dựng bản tin (newsletter) hoặc quản lý câu lạc bộ sách một cách thông minh và tiết kiệm thời gian. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!