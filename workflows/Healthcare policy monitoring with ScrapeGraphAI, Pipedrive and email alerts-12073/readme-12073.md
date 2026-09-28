---
title: "🚀 Giám sát chính sách y tế tự động với ScrapeGraphAI, Pipedrive và Email"
description: "Tự động quét, phân tích và cảnh báo các đề xuất chính sách y tế mới nhất bằng AI ScrapeGraphAI, lưu vào Pipedrive CRM và gửi email thông báo."
slug: "giam-sat-chinh-sach-y-te-tu-dong-scrapegraphai-pipedrive"
tags: [n8n, automation, ai, scrapegraphai, pipedrive, healthcare, email-alerts]
keywords: [n8n workflow, tự động hóa n8n, giám sát chính sách, ScrapeGraphAI, Pipedrive CRM, AI summarization]
---

# 🚀 Giám sát chính sách y tế tự động với ScrapeGraphAI, Pipedrive và Email

Việc theo dõi thủ công các trang web của chính phủ hoặc cơ quan y tế để cập nhật văn bản và chính sách mới là một "cực hình" mất rất nhiều thời gian, dễ bỏ lỡ thông tin quan trọng. Các quản trị viên y tế và nhà nghiên cứu thị trường thường xuyên phải đối mặt với việc kiểm tra hàng loạt trang web mỗi ngày.

Workflow n8n này sẽ giải quyết hoàn toàn bài toán đó bằng cách tự động hóa 100% quy trình: Quét trang web bằng AI (ScrapeGraphAI), làm giàu dữ liệu, lọc chính sách mới trong 30 ngày, lưu trữ vào Pipedrive CRM và gửi cảnh báo qua Email ngay lập tức mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công kiểm tra các trang web chính sách y tế mỗi ngày.
- **Không bỏ lỡ thông tin:** Phát hiện và cảnh báo ngay lập tức các chính sách mới xuất bản trong vòng 30 ngày.
- **Đồng bộ CRM thông minh:** Tự động tạo deal và hoạt động trong Pipedrive để đội ngũ dễ dàng theo dõi, phân tích.
- **Cá nhân hóa cảnh báo:** Nhận tóm tắt chi tiết qua email với định dạng rõ ràng, dễ đọc ngay trên hộp thư đến.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản và API Key của **ScrapeGraphAI**.
- API Key cho dịch vụ phân tích/làm giàu dữ liệu bên ngoài (hoặc LLM tương đương).
- Tài khoản **Pipedrive** (đã thiết lập các trường tùy chỉnh: `Policy Date` và `Reference Number`).
- Thông tin cấu hình SMTP (để gửi email).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node trọng yếu sau đây trước khi vận hành:
- **Define Target URLs (`code`):** Thay thế danh sách URL mẫu bằng các trang web chính sách y tế thực tế mà các sếp muốn theo dõi.
- **Scrape Policy Page (`n8n-nodes-scrapegraphai.scrapegraphAi`):** Kết nối tài khoản ScrapeGraphAI và thiết lập prompt tự nhiên để trích xuất tiêu đề, tóm tắt, ngày tháng và mã số văn bản.
- **Enrich with Metadata (`httpRequest`):** Nhập API Key cho dịch vụ phân tích mở rộng để gắn nhãn chủ đề và mức độ cảm xúc (sentiment).
- **Create an activity (`pipedrive`):** Chọn credentials của Pipedrive, đảm bảo các trường tùy chỉnh `Policy Date` và `Reference Number` đã được tạo trên hệ thống CRM.
- **Send Policy Alert (`emailSend`):** Cấu hình thông tin máy chủ SMTP cá nhân hoặc doanh nghiệp để gửi email cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Run Workflow** (thông qua node `manualTrigger`) để kiểm tra dữ liệu chạy thử mẫu.
- Kiểm tra kết quả trả về trong Pipedrive và hộp thư Email.
- Bật công tắc **Active** để workflow tự động hoạt động theo lịch trình hoặc nhu cầu thủ công.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Dễ dàng kết nối thêm node Telegram hoặc Slack ngay sau bước lọc dữ liệu để nhóm nhận tin tức nhanh hơn trên chat.
- **Lưu trữ mở rộng:** Ngoài Pipedrive, các sếp có thể đồng thời đẩy dữ liệu về Google Sheets hoặc Notion để làm kho lưu trữ báo cáo dài hạn.
- **Tùy chỉnh khoảng thời gian lọc:** Chỉnh sửa logic trong node code `Generate Unique ID` hoặc `Is Recent Policy?` nếu muốn thay đổi mốc thời gian lọc (ví dụ: trong vòng 7 ngày thay vì 30 ngày).

### 📌 Kết luận
Workflow tự động hóa giám sát chính sách y tế này là công cụ đắc lực giúp các tổ chức y tế, doanh nghiệp dược phẩm và nhà nghiên cứu luôn đi trước một bước trong việc cập nhật quy định pháp lý. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc!