---
title: "🚀 Tự động làm giàu và đánh giá tiềm năng Lead với Azure OpenAI, Bright Data MCP & HubSpot CRM"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình thu thập form, làm giàu thông tin lead bằng AI, chấm điểm ICP và đồng bộ dữ liệu vào HubSpot CRM."
slug: "tu-dong-lam-giau-va-danh-gia-lead-voi-azure-openai-bright-data-mcp-hubspot"
tags: [n8n, automation, ai, lead-generation, hubspot, azure-openai]
keywords: [n8n workflow, làm giàu lead, đánh giá lead, azure openai, bright data mcp, hubspot crm, tự động hóa bán hàng]
---

# 🚀 Tự động làm giàu và đánh giá tiềm năng Lead với Azure OpenAI, Bright Data MCP & HubSpot CRM

Các sếp có bao giờ cảm thấy mệt mỏi khi đội ngũ sales phải tốn hàng giờ đồng hồ để tra cứu thông tin khách hàng thủ công mỗi khi có lead mới đăng ký form? Việc thu thập thông tin chức danh, quy mô công ty, LinkedIn profile hay đánh giá xem lead có thực sự phù hợp với chân dung khách hàng lý tưởng (ICP) hay không thường rất mất thời gian.

Workflow này do **Sparsh từ Automation Jinn** thiết kế sẽ giải quyết triệt để vấn đề đó. Nó biến các thông tin thô sơ từ form đăng ký thành **hồ sơ CRM đầy đủ chi tiết, tự động chấm điểm tiềm năng và phân luồng thông báo** mà không cần con người nhúng tay vào 100% tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động làm giàu dữ liệu (Enrichment):** Tự động tìm kiếm chức danh, link LinkedIn, quốc gia, quy mô công ty, doanh thu... từ thông tin email đơn giản.
- **Chấm điểm thông minh (Lead Scoring):** AI tự động phân tích và cho điểm Fit Score từ 0-100 dựa trên tiêu chí ICP của doanh nghiệp.
- **Phân luồng thông minh:** Lead chất lượng cao (>70 điểm) sẽ được đẩy ngay lên Slack cho đội Sales và cập nhật HubSpot, trong khi các lead khác vẫn được lưu trữ gọn gàng vào CRM để nurturing.
- **Tiết kiệm 100% thời gian thủ công:** Đội ngũ sales chỉ việc tập trung chốt đơn với những khách hàng thực sự tiềm năng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Azure OpenAI API** (dùng cho các node `Azure OpenAI Chat Model`, `Lead Enricher Agent`, `Lead Scoring Agent`).
- **Bright Data MCP Client** (dùng cho công cụ thu thập thông tin web/doanh nghiệp).
- **HubSpot CRM Account** (với App Token để tạo/cập nhật Contact và Company).
- **Slack Workspace & Bot Token** (để gửi thông báo khi có lead chất lượng cao).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow từ nguồn cung cấp, sau đó paste trực tiếp vào n8n Editor của mình thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy kiểm tra và cấu hình các node sau cho chính xác với hệ thống của các sếp:
- **On form submission (`formTrigger`):** Điền các trường thông tin thu thập từ form (ví dụ: Name, Email).
- **Azure OpenAI Chat Model & Azure OpenAI Chat Model1:** Kết nối credentials `azureOpenAiApi` và chọn model phù hợp (ví dụ: `openai` hoặc GPT-4 theo cấu hình của sếp).
- **MCP Client (`mcpClientTool`):** Cấu hình kết nối với Bright Data MCP để AI có khả năng crawl và tìm kiếm thông tin doanh nghiệp.
- **Các node HubSpot (`Create or update a contact`, `Search for a company by Domain`, `Update a company`, v.v.):** Chọn đúng `hubspotAppToken` credentials. Đảm bảo ánh xạ (mapping) đúng các trường dữ liệu tên, email, domain công ty vào HubSpot.
- **Send a message (`slack`):** Chọn credentials Slack và chọn kênh (Channel) mà sếp muốn bot bắn thông báo lead mới về.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với dữ liệu mẫu từ Form để kiểm tra xem quá trình enrich và chấm điểm của AI có trả về đúng Structured Output không.
- Sau khi test thành công, gạt công tắc sang chế độ **Active workflow** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể nhân bản node thông báo để gửi tin nhắn đồng thời qua Telegram hoặc Zalo OA cho đội sales.
- **Lưu lịch sử vào Google Sheets / Airtable:** Thêm một node Google Sheets ở cuối luồng để lưu lại toàn bộ lịch sử lead được chấm điểm phục vụ việc phân tích marketing sau này.
- **Mở rộng bộ lọc (If node):** Tùy chỉnh điều kiện điểm số trong node `If` (mặc định là 70 điểm) cho phù hợp với đặc thù sản phẩm B2B hay B2C của doanh nghiệp.

### 📌 Kết luận
Workflow tích hợp AI Agent và MCP này là một "vũ khí tối tân" giúp tự động hóa hoàn toàn quy trình xử lý lead đầu vào. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa năng suất đội ngũ sales và không bỏ lỡ bất kỳ khách hàng tiềm năng nào nhé!