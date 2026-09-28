---
title: "🚀 Tự Động Hóa Báo Cáo Nghiên Cứu Cổ Phiếu Hàng Tuần Với n8n, AI Và Financial Modeling Prep"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu tài chính, tin tức thị trường, phân tích SWOT bằng AI và gửi báo cáo PDF qua Gmail hàng tuần."
slug: "tu-dong-hoa-bao-cao-nghien-cuu-co-phieu-n8n-ai"
tags: [n8n, automation, ai-agent, google-sheets, openai, finance]
keywords: [n8n workflow, nghiên cứu cổ phiếu tự động, ai financial report, fmp api, openai gpt, tự động hóa chứng khoán]
---

# 🚀 Tự Động Hóa Báo Cáo Nghiên Cứu Cổ Phiếu Hàng Tuần Với AI

Việc tổng hợp dữ liệu tài chính, phân tích báo cáo kết quả kinh doanh, cập nhật tin tức thị trường và viết báo cáo nghiên cứu cổ phiếu (Equity Research) cho hàng loạt mã chứng khoán thủ công tiêu tốn rất nhiều thời gian và dễ xảy ra sai sót. 

Giải pháp? Workflow n8n tự động hóa toàn diện này do chuyên gia **Rahul Joshi** thiết kế sẽ thay thế hoàn toàn quy trình thủ công đó. Hệ thống tự động lấy danh sách công ty từ Google Sheets, gọi API tài chính từ **Financial Modeling Prep (FMP)**, quét tin tức từ **NewsAPI**, sử dụng trí tuệ nhân tạo **OpenAI (GPT-4o-mini)** để phân tích SWOT, đánh giá rủi ro/triển vọng tăng trưởng, sau đó tự động xuất file PDF chuyên nghiệp và gửi email qua **Gmail** vào mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Lên lịch chạy hàng tuần (`Weekly Equity Research Trigger`) mà không cần can thiệp thủ công.
- **Phân tích thông minh bằng AI:** Tận dụng OpenAI Agents để tạo phân tích SWOT, nhận diện rủi ro và dự báo tăng trưởng dựa trên dữ liệu tài chính thực tế.
- **Báo cáo chuẩn chỉnh:** Tự động convert dữ liệu thành file PDF đẹp mắt thông qua HTML-to-PDF.
- **Quản lý danh sách linh hoạt:** Dễ dàng thêm/bớt mã cổ phiếu trực tiếp trên Google Sheets bằng cột `Enabled`.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Sheets API / OAuth2 Credentials** (Để đọc danh sách công ty và lưu log báo cáo).
- **Financial Modeling Prep (FMP) API Key** (Lấy dữ liệu báo cáo tài chính 5 năm gần nhất).
- **NewsAPI Key** (Lấy tin tức thị trường mới nhất về công ty).
- **OpenAI API Key** (Chạy các model phân tích AI như `gpt-4.1-mini`).
- **HTML/CSS to PDF API / Credentials** (Render báo cáo thành file PDF).
- **Gmail OAuth2 Credentials** (Gửi email báo cáo tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow từ nguồn cung cấp, sau đó paste trực tiếp vào giao diện n8n Editor (chọn **Import from JSON**).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Fetch Company List & Log Report Metadata (Google Sheets):** Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`. Trỏ tới file Google Sheets chứa danh sách mã cổ phiếu (Ticker) và trạng thái `Enabled`.
- **Fetch Income Statement, Balance Sheet, Cash Flow & Market Data (HTTP Request):** Điền API Key của *Financial Modeling Prep (FMP)* và *NewsAPI* vào phần Header hoặc Query Parameters tương ứng.
- **LLM – SWOT Analysis Model & LLM – Risk and Growth Model (OpenAI):** Chọn credential OpenAI (`openAiApi`) và cấu hình model `gpt-4.1-mini` (hoặc model tương đương).
- **Render Research Report to PDF:** Cấu hình credentials cho node `Render Research Report to PDF` để chuyển đổi cấu trúc HTML thành file PDF hoàn chỉnh.
- **Send Email Equity Research Report (Gmail):** Kết nối tài khoản Gmail cá nhân hoặc Workspace qua `gmailOAuth2` để hệ thống tự động gửi email kèm file PDF cho các bên liên quan.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với một vài mã cổ phiếu mẫu.
- Kiểm tra kết quả trả về ở Gmail và file log trên Google Sheets.
- Nếu mọi thứ trơn tru, hãy bật công tắc **Active** ở góc trên bên phải màn hình để workflow tự động chạy theo lịch hẹn hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc nội bộ:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay khi báo cáo PDF được tạo thành công vào nhóm chat của đội ngũ đầu tư.
- **Lưu trữ Cloud Storage:** Kết nối thêm node Google Drive hoặc AWS S3 để lưu trữ tất cả các báo cáo PDF hàng tuần làm tài liệu lưu trữ dài hạn.
- **Tùy chỉnh Prompt AI:** Tinh chỉnh system prompt trong các AI Agent để điều chỉnh văn phong phân tích phù hợp với khẩu vị rủi ro của quỹ hoặc cá nhân các sếp.

### 📌 Kết luận
Workflow tự động hóa nghiên cứu cổ phiếu này là một trợ lý đắc lực cho các nhà đầu tư cá nhân lẫn chuyên nghiệp, giúp tiết kiệm hàng chục giờ phân tích thủ công mỗi tuần. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình đầu tư ngay hôm nay!