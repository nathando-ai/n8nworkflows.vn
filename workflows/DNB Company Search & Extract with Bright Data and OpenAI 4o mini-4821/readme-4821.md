---
title: "🚀 Tự động tra cứu và trích xuất dữ liệu doanh nghiệp D&B với Bright Data & OpenAI"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm, trích xuất và chuẩn hóa thông tin doanh nghiệp từ Dun & Bradstreet sử dụng Bright Data MCP và OpenAI GPT-4o-mini."
slug: "tu-dong-tra-cuu-trich-xuat-du-lieu-doanh-nghiep-dnb-bright-data-openai"
tags: [n8n, automation, ai, bright-data, openai, mcp, web-scraping]
keywords: [n8n workflow, dnb data extract, bright data mcp, openai gpt-4o-mini, tu dong hoa du lieu doanh nghiep, web scraping n8n]
---

# 🚀 Tự động tra cứu và trích xuất dữ liệu doanh nghiệp D&B với Bright Data & OpenAI

Các sếp có bao giờ mất hàng giờ liền để thủ công tra cứu thông tin công ty trên Dun & Bradstreet (D&B), sau đó copy-paste dữ liệu để phân tích đối thủ hoặc làm báo cáo thị trường? Công việc lặp đi lặp lại này vừa tốn thời gian, vừa dễ sai sót.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó cho các sếp! Bằng cách kết hợp sức mạnh của **Bright Data MCP (Model Context Protocol)** và **OpenAI GPT-4o-mini**, hệ thống sẽ tự động tìm kiếm, trích xuất dữ liệu web, cấu trúc hóa thông tin doanh nghiệp, lưu trữ và gửi thông báo qua Webhook một cách hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
⚠️ **Lưu ý quan trọng:** Template này sử dụng **Community Node cho MCP Client**, do đó chỉ hỗ trợ trên các phiên bản **n8n Self-hosted**.
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ hoàn toàn thao tác tra cứu thủ công trên trang D&B.
- **Trích xuất thông minh:** Ứng dụng OpenAI GPT-4o-mini để lọc và cấu trúc hóa dữ liệu đầu ra chính xác theo định dạng mong muốn.
- **Lưu trữ linh hoạt:** Tự động ghi file kết quả cấu trúc vào ổ đĩa hệ thống.
- **Tích hợp liền mạch:** Gửi thông báo kết quả tức thì qua Webhook đến hệ thống thứ ba (Slack, CRM, hoặc Webhook.site để test).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted instance** (bắt buộc vì dùng node MCP Client).
- **Bright Data API / Credentials** (để cấu hình `mcpClientApi`).
- **OpenAI API Key** (cho các node sử dụng mô hình `gpt-4o-mini`).
- **Webhook Endpoint** (có thể dùng [Webhook.site](https://webhook.site/) để test ban đầu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã JSON từ nguồn cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình các node sau:
- **Set input fields**: Nhập từ khóa tìm kiếm (search query) về doanh nghiệp các sếp muốn tra cứu trên D&B.
- **Các node MCP Client** (`List all tools for Bright Data`, `MCP Client for Search Engine`, `Bright Data MCP Client For DNB`): Kết nối thông tin đăng nhập `mcpClientApi` của Bright Data.
- **OpenAI Chat Model nodes** (`OpenAI Chat Model for URL Data Extract`, `OpenAI Chat Model for DNB Structured Data Extract`): Chọn credential `openAiApi` đã điền API Key của OpenAI, đảm bảo model được chọn là `gpt-4o-mini`.
- **Initiate a Webhook Notification for Structured Data**: Thay đổi URL đích đến Webhook của các sếp (có thể tạo nhanh một URL test tại [Webhook.site](https://webhook.site/)).

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm với dữ liệu mẫu và kiểm tra kết quả trả về ở các node.
- Nếu mọi thứ hoạt động chính xác, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì chỉ ghi file vào disk bằng node `Write the structured content to disk`, các sếp có thể kết nối thêm node Google Sheets hoặc Airtable để lưu danh sách hàng loạt công ty.
- **Cảnh báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau bước trích xuất dữ liệu để nhận thông tin tóm tắt về doanh nghiệp ngay trên điện thoại.
- **Chạy hàng loạt (Batch Processing):** Kết hợp thêm node Code hoặc Loop để quét danh sách hàng trăm công ty từ file CSV đầu vào.

### 📌 Kết luận
Workflow "DNB Company Search & Extract with Bright Data and OpenAI 4o mini" là một trợ thủ đắc lực cho các đội ngũ Sales, Marketing và Nghiên cứu thị trường. Hãy triển khai ngay trên hệ thống n8n self-hosted của các sếp để tối ưu hóa quy trình khai thác dữ liệu doanh nghiệp!