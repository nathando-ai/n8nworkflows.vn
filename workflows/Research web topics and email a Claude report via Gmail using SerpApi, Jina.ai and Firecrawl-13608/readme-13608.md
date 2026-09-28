---
title: "🔍 **Tự Động Hoá Nghiên Cứu Thị Trường & Gửi Báo Cáo AI qua Email với SerpApi, Jina.ai & Firecrawl**"
description: "Workflow tự động hóa nghiên cứu chủ đề thị trường bằng AI Claude, kết hợp SerpApi và Jina.ai để phân tích nội dung web, tự động xử lý CAPTCHA và gửi báo cáo tổng hợp định dạng HTML qua email Gmail. Giúp các sếp tiết kiệm thời gian lên đến 80% trong quá trình nghiên cứu thị trường."
slug: "tieu-dong-hoa-nghien-cuu-thi-truong-ai-email"
tags: [n8n, automation, market-research, ai-rag, serpapi, jina-ai, firecrawl, gmail, anthropic]
keywords: [n8n workflow nghiên cứu thị trường, tự động hóa phân tích web, AI Claude báo cáo thị trường, SerpApi Jina.ai Firecrawl, gửi báo cáo email tự động]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Thị Trường & Gửi Báo Cáo AI qua Email**

Hãy tưởng tượng một tình huống: Các sếp phải dành hàng giờ mỗi tuần để **tìm kiếm, phân tích và tổng hợp thông tin từ hàng chục trang web** để xây dựng báo cáo thị trường. Quá trình này không chỉ tốn thời gian mà còn dễ bị lỗi do con người (quên bỏ qua nguồn tin không đáng tin cậy, phân tích không khách quan, hoặc bị chặn bởi CAPTCHA). **Workflow này giải quyết tất cả những vấn đề đó bằng AI và tự động hóa 100% không cần code!**

Dùng **SerpApi** để tìm kiếm Google, **Jina.ai** để scrape nội dung (miễn phí), **Claude (Anthropic)** để phân tích và tổng hợp, và **Firecrawl** làm backup khi bị chặn. Cuối cùng, workflow tự động **tổng hợp báo cáo định dạng HTML** và gửi qua **Gmail** cho các sếp. **Kết quả?** Các sếp chỉ cần nhập chủ đề và email nhận báo cáo, còn toàn bộ quá trình phân tích và gửi báo cáo sẽ được AI và n8n xử lý tự động.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo tính bảo mật và khả năng mở rộng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Tự động loại bỏ nguồn tin không đáng tin cậy** (Reddit, YouTube, PDF) và xử lý CAPTCHA/Firewall.
- **Báo cáo tổng hợp khách quan** do AI Claude phân tích và tổng hợp từ nhiều nguồn.
- **Định dạng báo cáo chuyên nghiệp** (HTML) với cấu trúc rõ ràng, dễ đọc.
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
- **Khả năng mở rộng** cho nhiều chủ đề và nguồn tin khác nhau.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - [SerpApi](https://serpapi.com/) (để tìm kiếm Google).
   - [Firecrawl](https://firecrawl.dev/) (backup khi Jina bị chặn).
   - [Anthropic Claude](https://www.anthropic.com/) (để phân tích nội dung).
   - [Gmail](https://mail.google.com/) (để gửi báo cáo).

2. **Credentials trong n8n**:
   - **SerpApi**: Thêm vào node `SerpApi Search` với tham số `api_key`.
   - **Firecrawl**: Thêm vào node `Firecrawl` với header `Authorization: Bearer YOUR_KEY`.
   - **Anthropic Claude**: Tạo credential OAuth2 và kết nối với các node `Claude Extractor`, `Claude Re-Analyzer`, và `Claude Synthesizer`.
   - **Gmail**: Tạo credential OAuth2 và kết nối với node `Send Gmail`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/13608).
2. Trong n8n, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và nhấn **Import from JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **29 node** và hoạt động theo logic phức tạp. Dưới đây là các bước **cần chú ý đặc biệt**:

##### **A. Cấu hình node `Research Form` (formTrigger)**
- Thêm các trường nhập liệu:
  - `topic` (chủ đề nghiên cứu).
  - `numSources` (số lượng nguồn tin).
  - `recipientEmail` (email nhận báo cáo).

##### **B. Cấu hình node `SerpApi Search` (httpRequest)**
- Thêm tham số `api_key` từ SerpApi vào query params.
- Cấu hình query để tìm kiếm Google với chủ đề từ `topic`.

##### **C. Cấu hình node `Jina Reader (Primary)` và `Firecrawl (Fallback)`**
- **Jina.ai** không cần API key (miễn phí), nhưng cần cấu hình header `User-Agent` để tránh bị chặn.
- **Firecrawl** chỉ hoạt động khi Jina bị chặn. Thêm API key vào header `Authorization`.

##### **D. Cấu hình node `Claude Extractor` và `Claude Synthesizer` (lmChatAnthropic)**
- Chọn model `claude-sonnet-4-5` (hoặc model mới nhất của Anthropic).
- Đảm bảo credential Anthropic đã được kết nối trong node.

##### **E. Cấu hình node `Send Gmail` (gmail)**
- Chọn operation `send` và resource `message`.
- Thiết lập chủ đề email và nội dung HTML từ node `Build HTML Report`.

##### **F. Cấu hình node `Error Trigger` (errorTrigger)**
- Để workflow bắt lỗi và gửi thông báo, các sếp cần:
  1. Vào **Workflow Settings** → **Error Workflow**.
  2. Chọn workflow hiện tại để bắt lỗi.
  3. (Nâng cao) Thêm node **Slack** hoặc **Telegram** sau `Format Error` để nhận cảnh báo lỗi.

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhập chủ đề (ví dụ: "Tendency of AI in Vietnam 2024").
   - Chọn số lượng nguồn tin (ví dụ: 5).
   - Nhập email nhận báo cáo (ví dụ: `sếp@example.com`).
   - Nhấn **Execute Workflow** để kiểm tra.
2. Sau khi test thành công, bật **Active** workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng số lượng nguồn tin**:
   - Mở rộng node `SerpApi Search` để lấy nhiều kết quả hơn (ví dụ: 20-30 trang).
   - Cấu hình node `Loop Over URLs` để xử lý batch lớn hơn.

2. **Lưu log và theo dõi**:
   - Thêm node **Google Sheets** sau `Aggregate Summaries` để lưu tất cả báo cáo.
   - Sử dụng node **Slack** hoặc **Telegram** để thông báo khi báo cáo hoàn thành.

3. **Tùy chỉnh báo cáo**:
   - Sửa node `Build HTML Report` để thay đổi định dạng (thêm logo, màu sắc, hoặc biểu đồ).
   - Thêm node **PDF** (n8n-nodes-base.pdf) để gửi báo cáo dưới dạng PDF.

4. **Xử lý CAPTCHA hiệu quả hơn**:
   - Nếu Firecrawl vẫn bị chặn, thử thêm node **Puppeteer** (n8n-nodes-base.puppeteer) để scrape thủ công.

5. **Tích hợp với CRM**:
   - Sau khi gửi email, thêm node **HubSpot** hoặc **Salesforce** để lưu báo cáo vào hệ thống CRM.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **nghiên cứu thị trường nhanh chóng, chính xác và tự động hóa**. Bằng cách kết hợp **SerpApi, Jina.ai, Firecrawl và Claude**, workflow không chỉ tìm kiếm và phân tích nội dung mà còn **tự động xử lý lỗi** và gửi báo cáo định dạng chuyên nghiệp. **Hãy thử ngay và tiết kiệm thời gian cho đội ngũ của mình!**

👉 **Bắt đầu ngay**: Import workflow và cấu hình theo hướng dẫn trên. Nếu có vấn đề, hãy để lại comment dưới đây! 🚀