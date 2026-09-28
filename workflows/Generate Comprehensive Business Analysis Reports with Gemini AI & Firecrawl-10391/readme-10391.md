---
title: "🚀 Tự động hóa tạo báo cáo phân tích kinh doanh chuyên sâu với Gemini AI & Firecrawl trong n8n"
description: "Hướng dẫn chi tiết xây dựng hệ thống n8n workflow tự động phân tích doanh nghiệp, nghiên cứu thị trường, tạo Google Docs/PDF và gửi email báo cáo chuyên nghiệp."
slug: "tao-bao-cao-phan-tich-kinh-doanh-gemini-ai-firecrawl"
tags: [n8n, automation, ai-summarization, market-research, google-docs, gemini, firecrawl]
keywords: [n8n workflow, phan tich kinh doanh, gemini ai, firecrawl, tu dong hoa bao cao, ai agents]
---

# 🚀 Tự động hóa tạo báo cáo phân tích kinh doanh chuyên sâu với Gemini AI & Firecrawl

Các sếp có bao giờ mất hàng giờ đồng hồ (hoặc thậm chí vài ngày) để nghiên cứu đối thủ, thu thập dữ liệu thị trường, tổng hợp thông tin và viết một bản báo cáo phân tích kinh doanh (Business Analysis Report) hoàn chỉnh? Công việc thủ công này cực kỳ ngốn thời gian, dễ thiếu sót và khó duy trì sự nhất quán.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một siêu phẩm n8n workflow do chuyên gia **Daniel Agrici** xây dựng. Hệ thống này sẽ tự động hóa từ A-Z: nhận yêu cầu từ Form, dùng AI (Gemini) kết hợp các công cụ tìm kiếm thông minh (Perplexity, Firecrawl, SERP) để thu thập dữ liệu chiều sâu, tự động điền vào Google Docs, xuất file PDF và gửi thẳng vào email của khách hàng hoặc đối tác!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ việc nhận yêu cầu qua Form đến khi hoàn thiện và gửi báo cáo PDF qua email mà không cần chạm tay vào.
- **Dữ liệu cực kỳ chất lượng:** Kết hợp sức mạnh của Gemini AI, Perplexity (tìm kiếm thông minh) và Firecrawl (quét website) để phân tích đối thủ và thị trường cực kỳ sắc bén.
- **Chuyên nghiệp hóa tài liệu:** Tự động tạo bản sao từ template Google Docs chuẩn, điền dữ liệu động và chuyển đổi thành PDF đẹp mắt.
- **Tiết kiệm thời gian tối đa:** Thay vì mất 3-5 ngày làm báo cáo, hệ thống chỉ mất vài phút để hoàn thành một bản Business Analysis Report chi tiết.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Cloud Account** (Google Drive, Google Docs, Gmail APIs).
- **Google AI Studio API Key** (cho Gemini).
- **Perplexity API Key** (cho node tìm kiếm `online_search` và `deep_research`).
- **Firecrawl API Key** (cho node quét website `URL_search`).
- **DataforSEO API** (nếu sử dụng các tool SERP liên quan).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã JSON gốc từ nguồn cung cấp, sau đó vào n8n Editor chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp JSON vào workspace).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hệ thống gồm 23 nodes được sắp xếp logic. Các sếp chú ý cấu hình kỹ các điểm sau:

- **Thiết lập Data Table:** Tạo một Data Table trong n8n với tên tương ứng và các cột dữ liệu theo mẫu: `session_id`, `client_name`, `client_country`, `client_language`, `client_website`, `client_description`, `target_audience_personas`, v.v.
- **Node `Business Analyst` (Google Gemini):** 
  - Chọn model **Gemini 2.5 Pro**.
  - Kết nối các tool phụ trợ như `online_search`, `deep_research` (Perplexity), `URL_search` (Firecrawl), và các tool nội bộ khác.
  - Đảm bảo trỏ đúng vào **Data Table** để lưu trữ kết quả phân tích theo từng `session_id`.
- **Nhóm Google Nodes (`Make Copy of Template`, `Change Variables in Doc`, `Send email`):**
  - Cấu hình **Google Drive OAuth2** và **Google Docs OAuth2**.
  - Lấy template chuẩn tại [Link Template Google Docs](https://docs.google.com/document/d/1Q6LvBw6cSGdcNbsEd0Tjo-pVfQsXI1_jUpeUaBsRDdg/edit?usp=sharing) hoặc bản backup `.docx`, sau đó đưa ID vào node `Make Copy of Template`.
  - Tại node **`Send email`** (Gmail API), điền địa chỉ email nhận báo cáo hoàn chỉnh.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách điền thông tin vào `Submit Form` (Form Trigger).
- Kiểm tra từng node xem dữ liệu trả về có chính xác không (Sử dụng tính năng click Play từng node).
- Sau khi mọi thứ chạy trơn tru, bật công tắc **Active workflow** lên xanh để hệ thống tự động hoạt động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau bước `Send email` để đội ngũ sales hoặc quản lý nhận được thông báo ngay khi có bản phân tích mới hoàn thành.
- **Lưu trữ backup:** Tự động tạo một thư mục riêng trên Google Drive để lưu trữ toàn bộ các file PDF báo cáo phân tích theo tên khách hàng.
- **Mở rộng nguồn dữ liệu:** Tích hợp thêm các công cụ Social Listening hoặc CRM (như HubSpot, Notion) để làm giàu dữ liệu đầu vào cho AI phân tích sâu hơn.

---

### 📌 Kết luận
Workflow tạo báo cáo phân tích kinh doanh tự động với Gemini AI & Firecrawl là một "vũ khí hạng nặng" giúp tối ưu hóa quy trình nghiên cứu thị trường và chăm sóc khách hàng. Hãy triển khai ngay hôm nay để nâng cấp hệ thống tự động hóa của doanh nghiệp các sếp lên một tầm cao mới!