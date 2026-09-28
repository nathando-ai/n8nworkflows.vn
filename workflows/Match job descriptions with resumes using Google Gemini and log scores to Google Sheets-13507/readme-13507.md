---
title: "🚀 Tự động chấm điểm CV ứng viên với Google Gemini và Google Sheets bằng n8n"
description: "Xây dựng hệ thống lọc hồ sơ tự động từ Form, sử dụng AI Gemini để đánh giá độ phù hợp (0-10), phân tích điểm mạnh/yếu và tự động lưu kết quả vào Google Sheets."
slug: "tu-dong-cham-diem-cv-ung-vien-google-gemini-google-sheets-n8n"
tags: [n8n, automation, ai, google-gemini, google-sheets, hr-automation]
keywords: [n8n workflow, loc cv tu dong, google gemini ai, cham diem cv n8n, google sheets hr automation]
---

# 🚀 Tự động chấm điểm và đánh giá CV ứng viên bằng AI & n8n

Trong quy trình tuyển dụng hiện đại, việc phải đọc hàng trăm bộ hồ sơ (CV) thủ công cho mỗi vị trí tuyển dụng ngốn rất nhiều thời gian và công sức của đội ngũ HR. Đôi khi, những chi tiết quan trọng có thể bị bỏ sót do mỏi mắt hoặc quá tải công việc.

Giải pháp? Một trợ lý AI thông minh chạy 24/7 trên n8n! Workflow này sẽ tự động nhận hồ sơ từ ứng viên qua biểu mẫu, trích xuất nội dung, đối chiếu với mô tả công việc (JD), nhờ **Google Gemini** đánh giá chi tiết (điểm số, điểm mạnh, điểm yếu, rủi ro) và tự động ghi log toàn bộ vào Google Sheets để các sếp dễ dàng theo dõi, lọc ứng viên tiềm năng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian sàng lọc:** AI đọc và đánh giá hồ sơ chỉ trong vài giây.
- **Đánh giá khách quan & đồng nhất:** Sử dụng tiêu chí chuẩn hóa thông qua Gemini LLM Agent.
- **Lưu trữ tự động thông minh:** Mọi thông tin liên hệ, điểm số (0-10), và phân tích chi tiết được đẩy thẳng lên Google Sheets.
- **Trải nghiệm mượt mà:** Ứng viên nộp qua form, HR chỉ việc mở bảng tính ra xem người nào điểm cao để gọi phỏng vấn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản Google** (để cấu hình Google Sheets OAuth2 và Form Trigger).
- **Google Gemini API Key** (Google Palm/Gemini Chat Model credentials).
- Chuẩn bị sẵn một Google Sheet theo template mẫu để lưu dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste node trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình kỹ các node trọng điểm sau đây:
- **On form submission (`formTrigger`):** Cấu hình form nhận thông tin ứng viên (Họ tên, Email, Link/File CV, Link hoặc nội dung JD).
- **Extract from File2 (`extractFromFile`):** Thiết lập trích xuất định dạng PDF từ file CV mà ứng viên tải lên.
- **Google Gemini Chat Model (`lmChatGoogleGemini`):** Kết nối API Key của Google AI Studio vào credentials.
- **Recruiter Agent & Information Extractor (`agent`, `informationExtractor`, `outputParserStructured`):** Tinh chỉnh các prompt hướng dẫn AI đóng vai trò một chuyên gia nhân sự (Recruiter) để chấm điểm từ 0-10, phân tích điểm mạnh, điểm yếu và cấu trúc hóa dữ liệu đầu ra.
- **Append Data (`googleSheets`):** Kết nối tài khoản Google Sheets, chọn đúng file Sheet template và map các trường dữ liệu (Tên, Email, Điểm số, Đánh giá) tương ứng với các cột trong bảng tính.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một bộ dữ liệu mẫu (1 CV và 1 JD giả định) để kiểm tra xem dữ liệu có đẩy lên Google Sheets chính xác không.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước `Append Data` để bắn tin nhắn thông báo ngay lập tức cho trưởng bộ phận tuyển dụng khi có ứng viên xuất sắc đạt điểm trên 8/10.
- **Tự động gửi email phản hồi:** Thêm nhánh điều kiện (If node), nếu điểm số đạt yêu cầu thì tự động gửi email mời phỏng vấn, ngược lại gửi email cảm ơn lịch sự.
- **Lưu trữ file:** Tự động lưu file CV gốc của ứng viên lên Google Drive thay vì chỉ trích xuất text.

### 📌 Kết luận
Workflow "Smart Resume Screener" là một ứng dụng AI thực chiến cực kỳ mạnh mẽ giúp tối ưu hóa khâu tuyển dụng đầu vào cho các doanh nghiệp, Agency hoặc bộ phận HR nội bộ. Hãy triển khai ngay hôm nay để tự động hóa quy trình tuyển dụng của các sếp!