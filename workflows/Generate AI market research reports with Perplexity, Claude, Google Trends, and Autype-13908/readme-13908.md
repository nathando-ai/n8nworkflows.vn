---
title: "🚀 Tự động hóa Nghiên cứu Thị trường & Tạo báo cáo PDF chuyên nghiệp với AI, Perplexity, Claude và Autype"
description: "Hướng dẫn cấu hình workflow n8n tự động hoàn toàn quy trình nghiên cứu thị trường, thu thập Google Trends, phân tích đối thủ bằng Perplexity, viết báo cáo với Claude và xuất PDF qua Autype."
slug: "tu-dong-hoa-nghien-cuu-thi-truong-voi-ai-perplexity-claude-autype"
tags: [n8n, automation, ai-agents, market-research, claude, perplexity]
keywords: [n8n workflow, tự động hóa nghiên cứu thị trường, perpexity ai, claude ai, autype pdf, google trends automation]
---

# 🚀 Tự động hóa Nghiên cứu Thị trường & Tạo báo cáo PDF chuyên nghiệp với AI

Việc làm báo cáo nghiên cứu thị trường (Market Research) theo cách thủ công thường ngốn rất nhiều thời gian: từ việc lên Google tìm kiếm đối thủ, tra cứu xu hướng (Google Trends), tổng hợp dữ liệu, phân tích SWOT cho đến việc căn chỉnh hình thức báo cáo, xuất file PDF sao cho đẹp mắt.

Giải pháp **Tự động hóa 100%** trong bài viết này sẽ giúp các sếp giải quyết triệt để nỗi đau đó. Chỉ với một form điền thông tin đơn giản về sản phẩm, hệ thống sẽ tự động thực hiện mọi công đoạn từ A-Z và trả về một bản báo cáo PDF chuyên nghiệp gửi thẳng lên Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ AI nặng mà không lo sập nguồn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần nhập liệu hay tìm kiếm thủ công, chỉ cần điền Form.
- **Dữ liệu thời gian thực:** Kết hợp Google Trends và Perplexity AI để lấy dữ liệu thị trường và đối thủ mới nhất.
- **Chất lượng nội dung đỉnh cao:** Sử dụng Anthropic Claude (qua OpenRouter) để viết báo cáo cấu trúc chuẩn xác (Executive Summary, Market Overview, SWOT, Competitor Landscape...).
- **Báo cáo PDF cực đẹp:** Xuất file PDF chuyên nghiệp thông qua Autype với định dạng Markdown mở rộng, màu sắc và font chữ chuẩn doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted instance** (Vì workflow này yêu cầu cài đặt Community Nodes).
- **SerpAPI Account** -- Gói miễn phí: 100 lượt tìm kiếm/tháng ([serpapi.com](https://serpapi.com)).
- **OpenRouter Account** -- Để sử dụng các mô hình AI như Perplexity Sonar và Claude Sonnet ([openrouter.ai](https://openrouter.ai)).
- **Autype Account** -- Lấy API Key tại `app.autype.com > Settings > API Keys` ([app.autype.com](https://app.autype.com)).
- **Google Drive OAuth2** (Tùy chọn) -- Để lưu file PDF tự động.
- **Community Nodes cần cài đặt trước:** `n8n-nodes-autype`, `n8n-nodes-serpapi` (Cài đặt qua mục *Settings > Community Nodes* trong n8n).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc file cung cấp, sau đó paste trực tiếp vào n8n Editor của mình. Đảm bảo các community nodes đã được cài đặt thành công trước khi import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes hoạt động nhịp nhàng theo các bước sau:

* **Market Research Form (formTrigger):** Nơi nhận thông tin đầu vào từ người dùng (Tên sản phẩm, Ngành hàng, Mô tả, Ngôn ngữ báo cáo). Các sếp có thể lấy URL của Form để gửi cho đội ngũ kinh doanh hoặc sử dụng nội bộ.
* **Google Trends & Search Competitors (SerpAPI nodes):** 
  - Cần cấu hình **SerpAPI Credentials**.
  - Node này tự động lấy dữ liệu quan tâm tìm kiếm trong 12 tháng qua và truy vấn các đối thủ cạnh tranh hàng đầu trên web.
* **AI Research Agent & OpenRouter Perplexity:** 
  - Sử dụng model `perplexity/sonar-pro` qua `openRouterApi`.
  - Nhiệm vụ phân tích sâu về thị trường dựa trên dữ liệu Google Search & Trends thời gian thực.
* **AI Report Writer & OpenRouter Anthropic Claude:** 
  - Sử dụng model `anthropic/claude-sonnet-4.6` (hoặc model Claude mới nhất).
  - Node này nhận toàn bộ ngữ cảnh nghiên cứu và cú pháp Autype Markdown để biên tập thành một bản báo cáo hoàn chỉnh.
* **Render Report PDF (Autype Node):** 
  - Cần cấu hình **Autype API Key** trong credentials.
  - Node này biến đổi Markdown thành một file PDF hoàn mỹ với phân cấp tiêu đề (H1, H2, H3), màu sắc biểu đồ, header/footer tự động.
* **Save Report to Drive (Google Drive Node):** 
  - Kết nối tài khoản Google Drive qua OAuth2 để lưu trữ file PDF vào thư mục chỉ định.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền thông tin vào Form.
- Kiểm tra kết quả trả về trong Google Drive, sau đó bật toggle **Active** để đưa workflow vào vận hành chính thức 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thay vì chỉ lưu Google Drive, các sếp có thể gắn thêm node **Slack** hoặc **Telegram** để bot gửi file PDF trực tiếp vào nhóm chat ngay khi báo cáo hoàn tất.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets trước khi kết thúc để lưu lại log gồm (Tên sản phẩm, Thời gian tạo, Link file PDF) tiện cho việc tra cứu sau này.
- **Tạo chiến dịch định kỳ:** Kết hợp thêm Schedule Trigger thay vì Form Trigger nếu muốn tự động chạy báo cáo nghiên cứu đối thủ hàng tuần/tháng cho các sản phẩm chủ lực.

---

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc kết hợp sức mạnh của No-code (n8n), Search APIs (SerpAPI), Multi-AI Agents (Perplexity + Claude) và công cụ render tài liệu hiện đại (Autype). Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm báo cáo thủ công cho doanh nghiệp của các sếp!