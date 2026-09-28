---
title: "🚀 Tự động chấm điểm bài tập PDF bằng Google Gemini AI và lưu báo cáo lên Google Drive"
description: "Hướng dẫn xây dựng hệ thống tự động hóa chấm bài tập PDF, phân tích nội dung chi tiết bằng AI Google Gemini và lưu trữ báo cáo đánh giá lên Google Drive với n8n."
slug: "tu-dong-cham-diem-bai-tap-pdf-google-gemini-google-drive"
tags: [n8n, automation, google-gemini, google-drive, ai-agents, document-extraction]
keywords: [n8n workflow, chấm bài tập tự động, google gemini ai, google drive automation, ai summarization]
---

# 🚀 Tự động chấm điểm bài tập PDF bằng Google Gemini AI và lưu báo cáo lên Google Drive

Các sếp trong lĩnh vực giáo dục, đào tạo hay nhân sự có đang cảm thấy quá tải mỗi khi phải đọc, đánh giá và chấm hàng chục, hàng trăm bài tập PDF thủ công? Việc này không chỉ ngốn vô số thời gian mà đôi khi còn gặp vấn đề về tính khách quan và nhất quán trong tiêu chí chấm điểm.

Được phát triển bởi **Pixcels Themes** — agency hàng đầu về tự động hóa tích hợp AI, giải pháp workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động trích xuất nội dung file PDF, tận dụng sức mạnh thông minh của **Google Gemini AI** để phân tích, cho điểm, đưa ra nhận xét chi tiết, sau đó tự động tổng hợp và lưu trữ báo cáo kết quả lên **Google Drive**. Toàn bộ quy trình diễn ra hoàn toàn tự động, nhanh chóng và chính xác 100% không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Bỏ qua hoàn toàn công đoạn đọc và chấm bài thủ công hàng loạt.
- **Đánh giá chuẩn xác & Khách quan:** Google Gemini AI áp dụng đúng rubric (tiêu chí) chấm điểm đã được định nghĩa sẵn cho từng bài.
- **Báo cáo chuyên nghiệp:** Tự động tạo file báo cáo chi tiết cho từng học viên/nhân sự và lưu trữ ngăn nắp trên Google Drive.
- **Hoạt động 24/7:** Hệ thống tiếp nhận và xử lý bài nộp liên tục, không mệt mỏi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Gemini API Key** (dùng cho mô hình AI phân tích).
- **Tài khoản Google Drive** (để lưu trữ file PDF bài tập đầu vào và file báo cáo đầu ra).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chủ n8n (Template ID: 13806) hoặc copy đoạn mã JSON, sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình chính xác các thành phần cốt lõi sau trong workflow:
- **Webhook Node (`webhook`):** Điểm tiếp nhận dữ liệu bài tập PDF gửi lên từ hệ thống LMS, Form hoặc API ngoài. Hãy cấu hình đúng Method (POST) và đường dẫn endpoint.
- **Extract From File Node (`extractFromFile`):** Đảm bảo node này được cấu hình đúng để đọc dữ liệu văn bản từ tệp PDF đầu vào.
- **Google Gemini LM Node (`lmChatGoogleGemini`):** Nhập Google Gemini API Key và chọn model AI phù hợp (ví dụ: `gemini-1.5-pro` hoặc `gemini-1.5-flash`) để xử lý ngữ cảnh dài của tài liệu PDF.
- **AI Agent & Structured Output Parser (`agent`, `outputParserStructured`):** Thiết lập prompt hệ thống (System Prompt) yêu cầu AI đóng vai trò giám khảo/giảng viên, đồng thời định dạng cấu trúc đầu ra mong muốn (Điểm số, Nhận xét điểm mạnh, Điểm cần cải thiện, Gợi ý...).
- **Convert to File & Google Drive Nodes (`convertToFile`, `googleDrive`):** Cấu hình định dạng file báo cáo (JSON/TXT/PDF) và trỏ đến thư mục đích trên Google Drive để lưu trữ tự động.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một file PDF mẫu để test thử nghiệm xem AI chấm điểm có đúng ý không.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình hơn nữa, các sếp có thể mở rộng workflow bằng cách:
- **Tích hợp Slack/Telegram:** Gửi thông báo ngay lập tức về kênh chat của giảng viên hoặc học viên khi có kết quả chấm bài.
- **Lưu trữ Google Sheets:** Ghi nhận điểm số và tên học viên vào một bảng tính chung để tiện theo dõi tiến độ tổng quan.
- **Gửi Email tự động:** Dùng node Gmail để tự động gửi phiếu điểm chi tiết tới email cá nhân của từng học viên ngay sau khi AI chấm xong.

### 📌 Kết luận
Việc tự động hóa chấm bài tập PDF với Google Gemini AI không chỉ giúp giải phóng sức lao động mà còn nâng cao chất lượng phản hồi cho người học. Hãy triển khai ngay workflow này để tối ưu hóa quy trình làm việc của doanh nghiệp hoặc tổ chức giáo dục của các sếp ngay hôm nay!