---
title: "🚀 Tự động chấm điểm và phân tích độ khớp giữa CV và Job Description với Google Gemini & n8n"
description: "Hướng dẫn xây dựng hệ thống AI tự động phân tích CV ứng viên dựa trên Mô tả công việc (JD), đánh giá độ phù hợp và gửi báo cáo chi tiết qua Gmail."
slug: "tu-dong-phan-tich-cv-va-jd-voi-gemini-n8n"
tags: [n8n, automation, ai, google-gemini, gmail, recruitment]
keywords: [n8n workflow, AI CV analyzer, tự động hóa tuyển dụng, Gemini AI, chấm điểm CV bằng AI]
---

# 🚀 Tự động chấm điểm và phân tích độ khớp giữa CV và Job Description với Google Gemini & n8n

Trong quy trình tuyển dụng hoặc khi ứng tuyển công việc, việc đọc hàng loạt CV và so sánh thủ công với yêu cầu công việc (Job Description - JD) ngốn rất nhiều thời gian. Chưa kể, ứng viên cũng rất khó biết CV của mình thiếu sót những gì để cải thiện. 

Giải pháp? Một hệ thống tự động hóa 100% không cần code sử dụng sức mạnh của **Google Gemini AI** và **n8n**. Workflow này sẽ tiếp nhận file CV (PDF) và đường dẫn JD, phân tích chiều sâu, tìm ra các điểm khớp, điểm yếu, đưa ra lời khuyên tối ưu và gửi báo cáo trực quan qua email cho người dùng chỉ trong vài phút.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Nhận file CV và link JD qua Webhook/Form, xử lý và trả kết quả tự động mà không cần can thiệp thủ công.
- **Phân tích thông minh bằng AI**: Sử dụng Google Gemini để trích xuất kỹ năng, đánh giá mức độ phù hợp (Fit Score) và tìm ra khoảng trống (gaps) giữa CV và JD.
- **Báo cáo chuẩn hóa**: Trả về dữ liệu cấu trúc rõ ràng (JSON) và gửi email báo cáo chi tiết, chuyên nghiệp cho ứng viên hoặc nhà tuyển dụng.
- **Tiết kiệm 90% thời gian**: Giảm tải công sức sàng lọc hồ sơ ban đầu, giúp đưa ra quyết định nhanh chóng và chính xác hơn.
:::

### 📦 Các thành phần chính trong Workflow (12 Nodes)
- **Webhook (`Webhook - CV Optimizer Form`)**: Điểm tiếp nhận request chứa thông tin form (Upload CV, Job Link, Email).
- **Respond to Webhook (`Webhook Response - HTML Form`)**: Phản hồi giao diện form nộp hồ sơ.
- **Extract from File (`Extract CV Text (PDF)`)**: Trích xuất toàn bộ văn bản từ file PDF CV của ứng viên.
- **HTTP Request (`Fetch Job Posting`)**: Tải nội dung văn bản từ đường dẫn Job Description được cung cấp.
- **Code (`Job Text Cleaner`)**: Làm sạch và chuẩn hóa định dạng văn bản JD.
- **Set & Merge (`Prepare CV Text`, `Merge CV + Job Data`)**: Gom nhóm và kết hợp dữ liệu CV và JD thành một payload thống nhất.
- **AI Agent & LangChain Nodes (`AI CV Analyzer`, `Gemini Model - Primary`, `Gemini Model`, `Parse AI JSON Output`)**: Sử dụng mô hình Google Gemini để phân tích, đối chiếu và ép kiểu dữ liệu trả về theo cấu trúc JSON định sẵn.
- **Gmail (`Send report`)**: Tự động soạn và gửi email báo cáo kết quả chi tiết đến người nhận.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Gemini API Key**: Tài khoản Google AI Studio/PaLM để cấu hình cho các node AI.
- **Gmail Account (OAuth2)**: Tài khoản Gmail để cấp quyền cho n8n gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n, sao chép toàn bộ mã JSON của workflow này (hoặc import file JSON) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node Webhook (`Webhook - CV Optimizer Form`)**: Kiểm tra đường dẫn endpoint (path: `cv-optimizer`) và đảm bảo phương thức là **POST** với các trường dữ liệu đầu vào: `Upload CV`, `Job Link`, `email`.
- **Nodes Google Gemini (`Gemini Model - Primary` & `Gemini Model`)**: 
  - Chọn hoặc tạo mới Credentials loại **Google Gemini / PaLM API**.
  - Dán API Key của các sếp vào đây để AI có thể hoạt động.
- **Node AI Agent (`AI CV Analyzer`)**: Các sếp có thể tinh chỉnh System Prompt bên trong agent để thay đổi tiêu chí chấm điểm, ngôn ngữ báo cáo (tiếng Việt/tiếng Anh) hoặc cấu trúc output JSON theo nhu cầu thực tế.
- **Node Gmail (`Send report`)**: 
  - Cấu hình **Gmail OAuth2 Credentials**.
  - Thiết lập địa chỉ người nhận động (`{{ $json.email }}`) lấy từ thông tin form gửi lên, kèm tiêu đề và nội dung HTML báo cáo từ kết quả của AI Agent.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một request mẫu chứa file PDF CV và link tuyển dụng để kiểm tra luồng chạy.
- Sau khi kiểm tra mọi thứ trơn tru, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ Log vào Google Sheets**: Thêm một node Google Sheets sau bước phân tích của AI để lưu lại lịch sử các CV đã chấm điểm, email ứng viên và điểm số tương ứng để tiện theo dõi, thống kê.
- **Tích hợp Slack / Telegram**: Thêm node thông báo về kênh chat nội bộ của công ty mỗi khi có một ứng viên mới nộp hồ sơ tối ưu CV qua hệ thống.
- **Tạo Custom Webhook Form đẹp mắt**: Thay vì dùng form mặc định của webhook, các sếp có thể dựng một trang landing page nhỏ (hoặc dùng Typeform/Tally) rồi bắn dữ liệu về Webhook của n8n để trải nghiệm người dùng mượt mà hơn.

### 📌 Kết luận
Với workflow **AI CV Analyzer & Matcher**, quy trình đánh giá sự phù hợp giữa ứng viên và công việc không còn là nỗi ám ảnh thủ công nữa. Hãy thiết lập ngay hôm nay để tối ưu hóa thời gian và mang lại trải nghiệm chuyên nghiệp cho ứng viên của các sếp!