---
title: "🚀 Tự động hóa nghiên cứu khách hàng tiềm năng B2B với Explorium MCP và Claude AI"
description: "Hướng dẫn sử dụng n8n workflow để tự động nghiên cứu thông tin doanh nghiệp, đối thủ cạnh tranh bằng AI và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-nghien-cuu-khach-hang-claude-ai-explorium-mcp"
tags: [n8n, automation, no-code, ai-research, google-sheets, claude-ai]
keywords: [n8n workflow, tự động hóa nghiên cứu công ty, Claude AI, Explorium MCP, GTM Research, Google Sheets automation]
---

# 🚀 Tự động hóa nghiên cứu khách hàng tiềm năng B2B với Explorium MCP và Claude AI

Các sếp có đang tốn hàng giờ liền để lướt website đối thủ, tìm kiếm thông tin về gói giá (pricing), xác định xem họ có bản miễn phí (free trial), có API hay không để phục vụ cho các chiến dịch GTM (Go-to-Market) không? Việc tra cứu thủ công này vừa chậm, dễ sai sót lại vừa lãng phí nhân lực.

Giải pháp ở đây chính là workflow n8n sử dụng **Claude AI kết hợp Explorium MCP**, tự động hóa 100% quy trình nghiên cứu doanh nghiệp chỉ từ tên miền (domain) hoặc tên công ty, sau đó trả kết quả gọn gàng về Google Sheets. Không cần code phức tạp, các sếp chỉ cần "lên đồ" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhập danh sách domain/tên công ty, AI sẽ tự động duyệt web và tổng hợp thông tin.
- **Dữ liệu cấu trúc chuẩn xác:** Trả về các trường thông tin cụ thể: Domain, LinkedIn URL, gói giá rẻ nhất, có trial hay không, có gói Enterprise, có API hay thị trường B2B/B2C.
- **Đồng bộ trực tiếp:** Tự động cập nhật kết quả nghiên cứu thẳng vào Google Sheets theo từng dòng.
- **Linh hoạt tùy biến:** Dễ dàng thay đổi câu lệnh (prompt) và định dạng đầu ra để lấy bất kỳ thông tin nào các sếp muốn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Anthropic API Key** (để sử dụng model Claude 3.7 Sonnet).
- **Tài khoản Google Sheets** và credentials kết nối OAuth2 với n8n.
- **Explorium MCP Client Credentials** (hoặc cấu hình HTTP Header Auth tương ứng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ thư viện n8n (hoặc copy toàn bộ JSON), sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Google Sheets - Get rows to enrich** & **Google Sheets - Update Row with data**: 
  - Kết nối tài khoản Google Sheets OAuth2.
  - Sử dụng [Google Sheets Template mẫu](https://docs.google.com/spreadsheets/d/1vR6s2nlTwu01v3GP7wvSRWS5W49FJIh20ZF7AUkmMDo/edit?usp=sharing) (hãy nhấn Make a copy).
  - Dán Link Google Sheet của các sếp vào cả 2 node này để hệ thống biết nguồn đọc dữ liệu và đích ghi kết quả.
- **Anthropic Chat Model**: Chọn credentials `anthropicApi` và cấu hình model `claude-3-7-sonnet-20250219`.
- **MCP Client**: Điền thông tin xác thực `httpHeaderAuth` để kết nối với Explorium MCP Server.
- **Structured Output Parser & AI company researcher**: Tùy chỉnh prompt bên trong AI Agent và cấu trúc dữ liệu đầu ra nếu các sếp muốn thu thập các trường thông tin khác ngoài danh sách mặc định (ví dụ: số lượng nhân viên, công nghệ sử dụng...).

#### 3. Kích hoạt ⚡️
- Nhấn **"Test workflow"** bằng tay để kiểm tra xem dữ liệu từ Google Sheets được đọc lên và AI xử lý có mượt mà không.
- Sau khi test thành công, bật công tắc **Active** để workflow chạy tự động theo lịch trình hoặc trigger mong muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Slack hoặc Telegram sau bước cập nhật Google Sheets để team sales nhận được thông báo ngay khi có profile khách hàng mới được nghiên cứu xong.
- **Chia mẻ (Batching):** Workflow đã sử dụng node `Loop Over Items` (Split In Batches) giúp xử lý danh sách lớn an toàn, không sợ bị quá tải API rate limit.
- **Lưu log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để ghi nhận lại các domain chết hoặc lỗi phát sinh trong quá trình AI gọi tool tìm kiếm.

### 📌 Kết luận
Ứng dụng AI kết hợp MCP và các công cụ tự động hóa như n8n chính là "vũ khí bí mật" giúp đội ngũ Sales và GTM tăng tốc gấp 10 lần. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình nghiên cứu thị trường của doanh nghiệp các sếp nhé!