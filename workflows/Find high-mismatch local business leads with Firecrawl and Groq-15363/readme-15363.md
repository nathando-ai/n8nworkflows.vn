---
title: "🚀 Tự động tìm kiếm Lead doanh nghiệp tiềm năng bằng Firecrawl và Groq AI"
description: "Hướng dẫn cấu hình workflow n8n tự động phát hiện các doanh nghiệp địa phương có độ vênh số hóa (High-mismatch) bằng AI và Firecrawl, hỗ trợ chốt sales hiệu quả."
slug: "tu-dong-tim-kiem-lead-doanh-nghiep-voi-firecrawl-va-groq"
tags: [n8n, automation, no-code, firecrawl, groq, lead-generation, ai]
keywords: [n8n workflow, tìm kiếm lead tự động, firecrawl n8n, groq ai, sales automation, local business leads]
---

# 🚀 Tự động tìm kiếm Lead doanh nghiệp tiềm năng bằng Firecrawl và Groq AI

Việc tìm kiếm và lọc ra các khách hàng tiềm năng (leads) chất lượng cao cho dịch vụ Agency hoặc Sales thủ công đang ngốn quá nhiều thời gian của các sếp. Thường thì chúng ta phải tự lên Google Maps, kiểm tra từng trang web kém chất lượng, phân tích đối thủ cạnh tranh rồi mới viết kịch bản tiếp cận. Quá oải và tốn kém!

Giải pháp ư? Workflow n8n siêu việt này sẽ thay các sếp làm toàn bộ quy trình từ A-Z: tự động quét, phân tích độ vênh số hóa (reputation vs. digital capability), tìm kiếm điểm mù của doanh nghiệp địa phương và gửi thẳng báo cáo chi tiết kèm kịch bản sales về Slack mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Hàng tuần hệ thống tự quét tìm các doanh nghiệp có uy tín thực tế cao nhưng website/digital marketing quá tệ (High-mismatch).
- **Lọc trùng thông minh:** Tự động đối chiếu với Database hiện có để không bao giờ xử lý hoặc mất phí quét trùng lặp một lead hai lần.
- **Phân tích sâu bằng AI:** Sử dụng mô hình `llama-3.3-70b-versatile` qua Groq để phân tích đánh giá của khách hàng, đối thủ cạnh tranh và viết sẵn kịch bản pitch sales cực bén.
- **Báo cáo trực quan:** Tổng hợp danh sách, chấm điểm cơ hội và gửi báo cáo HTML thẳng vào Slack hoặc n8n Table.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Firecrawl API Key** (Dùng để tìm kiếm map và cào dữ liệu web/review).
- **Groq API Key** (Dùng cho các node LLM chạy mô hình Llama 3.3).
- **Slack App / Bot** (Tùy chọn, nếu muốn nhận báo cáo qua Slack).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ JSON), sau đó paste trực tiếp vào giao diện n8n Editor của các sếp bằng cách chọn **New workflow** -> Dán (Ctrl+V).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:

- **Node `Configuration` (Set):** Cấu hình khu vực (`location`) và ngành nghề (`category`) mà các sếp muốn quét lead (ví dụ: *Dental clinic in Helsinki*).
- **Các node liên quan đến Groq (`Groq Chat Model`, `Groq Chat Model1`, `Groq Chat Model2`):** Chọn credentials `groqApi` đã chuẩn bị và đảm bảo model được trỏ tới `llama-3.3-70b-versatile`.
- **Các node liên quan đến Firecrawl (`Discovery Search`, `Scrape Business Profile`, `Scrape Website`, `Find Competitors`, `Scrape Competitor`, `Search Reviews`):** Thiết lập credentials `firecrawlApi` để cấp quyền cào dữ liệu bản đồ và website.
- **Node `Fetch Existing Leads` & `Save to n8n Table` (DataTable):** Tạo sẵn một bảng (n8n Table) tương ứng trên hệ thống n8n để lưu trữ cơ sở dữ liệu lead, tránh việc quét trùng lặp ở những lần chạy sau.
- **Node `Send Slack` (Slack):** Kết nối tài khoản Slack và chọn channel nhận thông báo báo cáo HTML hàng tuần.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử lần đầu (Test run) với một vài dữ liệu mẫu để kiểm tra kết nối API.
- Nếu mọi thứ xanh mướt, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch hẹn (Mặc định: Thứ Hai hàng tuần lúc 9 giờ sáng).

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Ngoài Slack, các sếp có thể nối thêm node Telegram, Email (Gmail/SMTP) hoặc đẩy dữ liệu trực tiếp lên Google Sheets, Airtable, HubSpot CRM.
- **Tùy biến Mismatch Prompt:** Tinh chỉnh lại code trong node `The Mismatch Engine` để AI tập trung vào các điểm yếu cụ thể mà dịch vụ của các sếp đang cung cấp (ví dụ: SEO yếu, thiếu booking online, giao diện mobile lỗi...).
- **Tăng tốc độ quét:** Điều chỉnh thời gian ở node `Rate Limit Delay` nếu muốn đẩy nhanh tốc độ cào dữ liệu (nhưng cần lưu ý giới hạn Rate Limit của Firecrawl API).

### 📌 Kết luận
Workflow "Find high-mismatch local business leads with Firecrawl and Groq" là một "vũ khí bí mật" thực thụ cho các Agency, Freelancer hoặc đội ngũ Sales B2B. Thay vì mò kim đáy bể, giờ đây hệ thống AI sẽ tự động tìm ra những doanh nghiệp đang "đau đầu" vì digital kém và dâng tận miệng danh sách khách hàng kèm kịch bản tiếp cận. Lên đồ ngay thôi các sếp!