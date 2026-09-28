---
title: "🚀 Tự động hóa tìm việc & Đánh giá mức độ phù hợp công việc qua Telegram với AI, Pinecone và Apify"
description: "Hướng dẫn xây dựng trợ lý AI tự động đọc link tuyển dụng từ Telegram, cào dữ liệu bằng Apify, đối chiếu với CV qua Pinecone Vector DB và chuẩn bị trọn bộ hồ sơ ứng tuyển."
slug: "tu-dong-hoa-tim-viec-telegram-openai-pinecone-apify"
tags: [n8n, automation, ai-agent, openai, telegram, google-sheets, apify]
keywords: [n8n workflow, tu dong hoa tim viec, ai agent telegram, apify scraping, pinecone vector db, openai gpt-5]
---

# 🚀 Tự động hóa tìm việc & Đánh giá mức độ phù hợp công việc qua Telegram với AI

Các sếp có đang cảm thấy mệt mỏi mỗi khi lướt thấy một tin tuyển dụng hấp dẫn trên mạng, rồi lại phải tốn hàng giờ đồng hồ để đọc kỹ yêu cầu, viết cover letter, soạn email gửi HR và cập nhật vào bảng Excel theo dõi không? Việc này vừa thủ công, vừa tốn thời gian lại dễ bỏ lỡ cơ hội.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một siêu workflow n8n tự động hóa 100% quy trình trên. Chỉ cần gửi một đường link tuyển dụng qua **Telegram**, trợ lý AI sẽ thay các sếp lo từ A-Z: từ phân tích link, cào dữ liệu, đối chiếu CV cá nhân trong **Pinecone**, đánh giá độ phù hợp, cho đến tự động soạn Cover Letter, tạo bản nháp email trên **Gmail** và lưu log vào **Google Sheets**!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian ứng tuyển:** Không còn phải copy-paste thủ công hay ngồi viết từng chiếc Cover Letter dài dòng.
- **Đánh giá thông minh (AI Fit Score):** Trợ lý AI tự động so sánh JD (Job Description) với CV của các sếp qua Vector Database để biết xem mình có thực sự phù hợp hay không trước khi tốn thời gian apply.
- **Tương tác mượt mà qua Telegram:** Nhận thông báo, xem kết quả phân tích và bấm duyệt (Approve/Reject) trực tiếp ngay trên cửa sổ chat Telegram.
- **Hồ sơ trọn gói:** Tự động tạo file Cover Letter trên Google Drive, tạo bản nháp email gửi HR qua Gmail và ghi nhận toàn bộ vào Google Sheets để theo dõi.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Telegram Bot API:** Tạo bot qua `@BotFather` để lấy Token.
- **OpenAI API Key:** Dùng cho các mô hình AI thông minh (OpenAI URL Parsing Agent, GPT-5 Chat...).
- **Apify Account & API Token:** Dùng để cào nội dung từ các trang tuyển dụng.
- **Pinecone Account:** Vector Database để lưu trữ và truy xuất dữ liệu CV/Resume của các sếp.
- **Google Account:** Kết nối Google Drive, Google Sheets và Gmail để lưu trữ tài liệu và gửi email.
:::

---

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc hoặc sử dụng tính năng import trực tiếp vào n8n Editor của mình.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 34 nodes kết nối chặt chẽ với nhau. Các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **Telegram URL Trigger & Send URL Confirmation on Telegram:** Kết nối với `telegramApi` của các sếp. Node Trigger sẽ lắng nghe tin nhắn chứa link tuyển dụng gửi vào bot.
- **OpenAI URL Parsing Agent & Analyze URL Contents:** Cấu hình OpenAI Credentials và chọn model (ví dụ: `gpt-5-mini`) để AI nhận diện, làm sạch và chuẩn hóa đường dẫn URL từ tin nhắn.
- **Extract Content with Apify & Retrieve Job Content with Apify:** Cấu hình tài khoản Apify để hệ thống tiến hành cào nội dung chi tiết từ trang tuyển dụng.
- **Save Profile Vectors to Pinecone & Generate Resume Embeddings:** Kết nối với Pinecone Vector Store để hệ thống truy vấn dữ liệu CV/Resume đã được nhúng vector trước đó.
- **Assess Job-Fit Suitability & GPT-5 Chat for Compatibility:** AI sẽ tiến hành đối chiếu kỹ năng của các sếp với yêu cầu tuyển dụng để tạo ra bản báo cáo đánh giá mức độ phù hợp (*Fit Analysis Report*).
- **Seek Job Approval via Telegram:** Sử dụng tính năng `sendAndWait` để gửi thông báo kết quả đánh giá kèm nút bấm xin ý kiến quyết định của các sếp (Tiếp tục hay Dừng lại).
- **Prepare Application Kit & GPT-5 Chat for Application Kit:** Sau khi được phê duyệt, AI sẽ tự động biên soạn nội dung hồ sơ (Cover Letter, Email...).
- **Add Entry to Job Tracker Sheets:** Kết nối Google Sheets để ghi log hành trình ứng tuyển (tên công ty, vị trí, trạng thái...).
- **Draft Cover Letter in Google Drive & Compose Email to HR:** Tạo tài liệu Cover Letter trên Google Drive và soạn sẵn bản nháp email trên Gmail để các sếp chỉ cần bấm Gửi.

### 3. Trạng thái hoạt động ⚡️
- Bấm **Execute Workflow** và gửi một link tuyển dụng bất kỳ vào bot Telegram của các sếp để test luồng chạy thực tế.
- Sau khi kiểm tra mọi thứ mượt mà, hãy bật công tắc **Active** để đưa trợ lý AI vào hoạt động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể tích hợp thêm node Slack hoặc Discord để nhận cảnh báo về các job phù hợp ngay trên máy tính làm việc.
- **Lưu trữ nâng cao:** Thêm các bước phân loại mức lương, yêu cầu kinh nghiệm vào Google Sheets để sau này dễ dàng lọc dữ liệu thống kê.
- **Tự động gửi email:** Nếu tự tin tuyệt đối vào AI, các sếp có thể đổi node Gmail từ trạng thái `draft` sang `send` để tự động hóa hoàn toàn khâu gửi email ứng tuyển.

---

### 📌 Kết luận
Với workflow n8n kết hợp AI Agents, Apify và Pinecone này, việc tìm kiếm và ứng tuyển việc làm đã trở thành một trải nghiệm hoàn toàn tự động và cực kỳ chuyên nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất sự nghiệp của các sếp nhé!