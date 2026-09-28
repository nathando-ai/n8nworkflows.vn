---
title: "🚀 Tự động tạo Hồ sơ khách hàng lý tưởng (ICP) & Tìm kiếm công ty tương tự (Lookalike) với Implisense & OpenAI"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích dữ liệu B2B, gọi Implisense API tìm kiếm lookalike companies và kết hợp OpenAI tạo báo cáo ICP chi tiết."
slug: "tao-b2b-icp-va-tim-kiem-lookalike-voi-implisense-api"
tags: [n8n, automation, implisense, openai, b2b-marketing, sales-automation]
keywords: [n8n workflow, implisense api, b2b icp, lookalike companies, ai summarization, sales automation]
---

# 🚀 Tự động tạo Hồ sơ khách hàng lý tưởng (ICP) & Tìm kiếm công ty tương tự (Lookalike)

Việc nghiên cứu thị trường B2B và tìm kiếm các khách hàng tiềm năng có cùng chân dung (Lookalike Companies) thường ngốn rất nhiều thời gian của đội ngũ sales và marketing. Các sếp thường phải thủ công tra cứu từng doanh nghiệp, phân tích đặc điểm chung rồi mới phác thảo ra Chân dung khách hàng lý tưởng (ICP). 

Giải pháp tự động hóa 100% không cần code dưới đây sẽ giúp các sếp giải quyết triệt để bài toán này. Workflow kết hợp sức mạnh của **Implisense API** để quét dữ liệu doanh nghiệp và **OpenAI LLM** để tự động tổng hợp báo cáo ICP chuyên sâu chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhập danh sách công ty mẫu (Base Companies) và nhận về danh sách lookalike companies sạch sẽ, sẵn sàng đưa vào CRM.
- **Báo cáo ICP thông minh:** Tận dụng AI (OpenAI) phân tích thống kê tính năng từ Implisense để viết báo cáo tường thuật ICP chi tiết.
- **Lọc thông minh đa chiều:** Dễ dàng giới hạn kết quả theo vị trí địa lý, ngành nghề (NACE codes) và quy mô công ty.
- **Tối ưu hóa thời gian:** Thay vì mất hàng giờ nghiên cứu thủ công, toàn bộ quy trình diễn ra trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Implisense API Account:** Tài khoản và API Token/Credentials từ Implisense ([Đăng ký tại đây](https://implisense.com/de/contact)).
- **OpenAI API Key:** Tài khoản OpenAI để sử dụng node `generate_icp_report`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn gốc (ID: 11709) và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm 21 nodes được thiết kế mạch lạc từ khâu input, gọi API, xử lý dữ liệu đến xuất báo cáo AI.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau:
- **Mock ICP Companies based on Implisense-ID (Node `code`):** Thay thế dữ liệu mẫu bằng danh sách ID công ty thực tế từ cơ sở dữ liệu Implisense. Đảm bảo output trả về trường `id`.
- **Authorization & Get Lookalikes (Nodes `set`, `httpRequest`):** Cấu hình thông tin xác thực API của Implisense (Basic Auth hoặc Header) sử dụng API Token đã đăng ký.
- **Configuration (Node `set`):** Tinh chỉnh các bộ lọc như `locationsFilter` (ví dụ: `de-be`, `de-by`), `industriesFilter` (mã NACE như `J62` cho ngành IT), và `sizesFilter` (`MICRO`, `SMALL`, `MEDIUM`, `LARGE`).
- **Generate ICP Report (Node `openAi`):** Chọn đúng credentials `openAiApi` và kiểm tra prompt để AI sinh báo cáo theo đúng văn phong mong muốn.
- **List of Companies (Node `set`):** Map lại các trường dữ liệu cho khớp với schema của CRM hiện tại trước khi đẩy dữ liệu vào bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** chạy thử với dữ liệu mẫu (Manual Trigger) để kiểm tra kết quả trả về ở các nhánh `icp_report` và `list_of_companies`.
- Sau khi test thành công, bật **Active** để hệ thống sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM tự động:** Thêm một node HubSpot, Salesforce hoặc Google Sheets ngay sau node `list_of_companies` để tự động đẩy dữ liệu công ty lookalike vào hệ thống quản lý khách hàng.
- **Cảnh báo qua Slack/Telegram:** Thêm node thông báo để gửi báo cáo ICP tóm tắt về group chat ngay khi workflow chạy xong.
- **Chất lượng dữ liệu đầu vào:** Hãy sử dụng các công ty mẫu có độ tương đồng cao với chân dung khách hàng mục tiêu để AI và thuật toán Implisense trả về kết quả chính xác nhất, tránh dùng danh sách quá tạp nham.

### 📌 Kết luận
Workflow tự động hóa tìm kiếm B2B Lookalike và tạo báo cáo ICP này là vũ khí cực mạnh cho các đội ngũ Sales & Marketing hiện đại. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa phễu khách hàng ngay hôm nay!