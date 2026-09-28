---
title: "🚀 Tự động hóa sàng lọc và Matching Hồ sơ ứng viên với Gemini AI và Decodo Scraping"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích CV, quét dữ liệu LinkedIn, matching công việc bằng Gemini AI và gửi báo cáo HTML qua Gmail."
slug: "tu-dong-hoa-matching-ho-so-ung-vien-gemini-decodo"
tags: [n8n, automation, no-code, hr-automation, google-gemini, ai-scraping]
keywords: [n8n workflow, tuyển dụng tự động, gemini ai, decodo scraping, matching cv, hr tech]
---

# 🚀 Tự động hóa sàng lọc và Matching Hồ sơ ứng viên với Gemini AI và Decodo Scraping

Các sếp làm trong ngành nhân sự (HR), tuyển dụng hay Headhunter chắc hẳn đều thấm thía cảnh ngập lụt trong hàng đống CV mỗi khi mở một vị trí tuyển dụng. Việc đọc thủ công từng CV, đối chiếu kỹ năng, tra cứu profile LinkedIn rồi tìm kiếm các công việc phù hợp tốn vô số thời gian và dễ bỏ lỡ nhân tài.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động tiếp nhận hồ sơ từ biểu mẫu ứng tuyển, phân tích CV bằng **Gemini AI**, quét thông tin mạng xã hội qua **Decodo**, tiến hành đối chiếu (matching) với các cơ hội việc làm và tự động gửi một báo cáo HTML cực kỳ chuyên nghiệp qua **Gmail** cho các sếp. Tất cả diễn ra hoàn toàn tự động mà không cần tốn một phút thao tác tay nào!

:::info[Gợi ý hạ tầng cho n8n]
Vì workflow này sử dụng **community node (Decodo)**, các sếp bắt buộc phải cài đặt n8n trên môi trường tự host (Self-hosted) để hệ thống hoạt động ổn định 24/7.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải đọc thủ công từng CV hay tra cứu LinkedIn từng ứng viên.
- **Sàng lọc chính xác:** Gemini AI phân tích sâu kỹ năng, kinh nghiệm và độ phù hợp (matching score) với thị trường việc làm.
- **Báo cáo chuyên nghiệp:** Nhận ngay bản tóm tắt hồ sơ và danh sách công việc phù hợp định dạng HTML trực quan ngay trong hộp thư Gmail.
- **Quy trình liền mạch:** Tự động hóa toàn bộ từ bước ứng viên nộp form cho đến khi kết quả được gửi đi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted instance** (Do workflow sử dụng cộng đồng node Decodo).
- **Tài khoản & API Key Google Gemini (Google Palm API)**: Dành cho các node phân tích CV và AI Agent matching.
- **Tài khoản Decodo**: Đăng ký [tại đây](https://visit.decodo.com/discount) để lấy API Key phục vụ việc cào dữ liệu LinkedIn và Job Boards.
- **Tài khoản Gmail**: Kết nối qua OAuth2 để gửi báo cáo tự động.
- **Biểu mẫu thu thập (Form)**: Ví dụ như Tally, Google Forms hoặc Typeform để nhận dữ liệu đầu vào đẩy qua Webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn.
- Mở n8n Editor của các sếp, chọn **Add workflow** -> Dán JSON vào giao diện.
- Cài đặt thêm **Decodo community node** từ thư viện cộng đồng của n8n (Community Nodes).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Webhook: Receive Intake Form (POST)**: Lấy Webhook URL cấu hình vào form ứng tuyển của các sếp (Ví dụ: Tally, Google Form) để nhận dữ liệu POST lên.
- **Set: Capture Form Fields**: Kiểm tra lại các trường dữ liệu thu thập từ form (summary, resume link, LinkedIn URL) để khớp với đầu vào.
- **Switch: Has LinkedIn URL?**: Nhánh phân loại ứng viên có hoặc không có link LinkedIn để tối ưu hóa quá trình xử lý.
- **Decodo: Scrape LinkedIn Profile & Decodo Tool: Scrape Job Boards**: Nhập thông tin **Decodo API Credentials** đã chuẩn bị.
- **Gemini: Parse Resume & Gemini Model: Profile Extraction / Job Matching**: Kết nối tài khoản `googlePalmApi` và tinh chỉnh prompt nếu muốn AI đánh giá theo tiêu chí riêng của công ty.
- **Gmail: Send Resume Summary and Top Matches Job**: Kết nối tài khoản Gmail OAuth2, nhớ bật tính năng **Send as HTML** để báo cáo hiển thị đẹp mắt.

#### 3. Kích hoạt ⚡️
- Gửi thử một bản ghi mẫu qua form ứng tuyển để test luồng chạy (Test run).
- Kiểm tra xem email đã đổ về hộp thư với định dạng HTML chuẩn chưa.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatbot thông báo**: Kết nối thêm node Telegram hoặc Slack để bắn thông báo nhanh cho HR ngay khi có ứng viên tiềm năng đạt điểm match cao.
- **Lưu trữ dữ liệu ứng viên**: Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử ứng tuyển và điểm số matching phục vụ việc tra cứu sau này.
- **Tự động gửi email phản hồi**: Mở rộng workflow bằng cách tự động gửi email cảm ơn hoặc lịch phỏng vấn dựa trên kết quả điểm số từ Gemini AI.

### 📌 Kết luận
Việc tự động hóa quy trình tuyển dụng chưa bao giờ dễ dàng và chuyên nghiệp đến thế. Với sự kết hợp hoàn hảo giữa Gemini AI và Decodo Scraping trên n8n, các sếp sẽ giải phóng toàn bộ thời gian xử lý thủ công, nhanh chóng nắm bắt và kết nối với những nhân tài xuất sắc nhất. Chúc các sếp cài đặt thành công và xây dựng được đội ngũ nhân sự vững mạnh!