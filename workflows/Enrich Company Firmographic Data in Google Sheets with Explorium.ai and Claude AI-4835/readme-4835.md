---
title: "🚀 Tự động làm giàu dữ liệu doanh nghiệp trong Google Sheets với Explorium.ai và Claude AI"
description: "Hướng dẫn xây dựng workflow n8n tự động bổ sung thông tin firmographic cho công ty từ Google Sheets sử dụng Explorium MCP và Claude AI một cách chính xác."
slug: "tu-dong-lam-giau-du-lieu-doanh-nghiep-google-sheets-explorium-claude-ai"
tags: [n8n, automation, no-code, google-sheets, ai-agent, claude-ai]
keywords: [n8n workflow, làm giàu dữ liệu doanh nghiệp, explorium mcp, claude ai, google sheets automation]
---

# 🚀 Tự động làm giàu dữ liệu doanh nghiệp trong Google Sheets với Explorium.ai và Claude AI

Các sếp làm sales, marketing hay phát triển kinh doanh chắc chắn đã từng trải qua cảm giác mệt mỏi khi phải thủ công tra cứu thông tin chi tiết (firmographic) của hàng trăm, hàng ngàn doanh nghiệp: quy mô nhân sự, doanh thu, ngành nghề, công nghệ sử dụng, địa chỉ trụ sở... Việc này không chỉ tốn hàng chục giờ đồng hồ mà dữ liệu thu về còn dễ bị sai sót hoặc thiếu đồng bộ.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% này. Sự kết hợp giữa **Google Sheets**, **Explorium MCP (AI Tool)** và **Claude AI (Anthropic)** sẽ tự động "lên đời" danh sách khách hàng ngay khi các sếp thêm tên công ty hoặc website vào bảng tính. Không cần viết một dòng code nào phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn quy trình research và điền dữ liệu công ty, giải phóng thời gian cho đội sales chốt đơn.
- **Dữ liệu chuẩn xác, chuyên sâu:** Khai thác kho dữ liệu firmographic chất lượng cao từ Explorium.ai kết hợp khả năng suy luận thông minh của Claude AI.
- **Hoạt động trơn tru theo lô (Batch Processing):** Xử lý từng dòng tuần tự, đảm bảo không bỏ sót dữ liệu và không bị lỗi API rate limit.
- **Tự động cập nhật:** Dữ liệu sau khi làm giàu được đồng bộ ngược lại Google Sheets chính xác theo từng dòng doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** File chứa danh sách doanh nghiệp (cần có cột tên công ty hoặc website).
- **Explorium.ai Account & API Key:** Cung cấp dữ liệu doanh nghiệp thông qua Explorium MCP.
- **Anthropic API Key:** Để sử dụng model Claude AI (Claude Sonnet).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n.io/workflows/4835](https://n8n.io/workflows/4835), sau đó vào n8n Editor chọn **Import from File** hoặc copy toàn bộ nội dung JSON và dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Google Sheets Trigger & Update Company Row:** Kết nối tài khoản Google của các sếp. Chọn đúng file spreadsheet và sheet name chứa danh sách công ty. Node *Update Company Row* cần được cài đặt chế độ `appendOrUpdate` dựa trên khóa định danh (ví dụ: Tên công ty hoặc Website).
- **Anthropic Chat Model:** Thêm credentials API của Anthropic và chọn model chuẩn (khuyên dùng `claude-sonnet-4-20250514` hoặc các phiên bản Claude Sonnet mới nhất).
- **Explorium MCP:** Cấu hình xác thực HTTP Bearer Auth bằng Explorium API Key để AI Agent có quyền truy cập công cụ tra cứu dữ liệu doanh nghiệp.
- **Loop Over Items (Split in Batches):** Đặt kích thước batch là `1` để hệ thống xử lý từng công ty một cách tuần tự, đảm bảo AI Agent có đủ ngữ cảnh để phân tích chính xác từng trường hợp.

#### 3. Kích hoạt ⚡️
- Tạo vài dòng dữ liệu mẫu trong Google Sheets (Tên công ty + Website).
- Nhấn **Test Workflow** để kiểm tra quá trình xử lý qua từng node (Trigger → Filter → Loop → AI Agent → Code → Update Sheets).
- Nếu dữ liệu đổ về bảng tính chính xác, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Slack hoặc Telegram sau bước *Update Company Row* để bắn thông báo về nhóm mỗi khi có một khách hàng tiềm năng mới được làm giàu dữ liệu thành công.
- **Xử lý lỗi thông minh:** Sử dụng node *If* hoặc cấu hình Error Trigger để ghi lại log nếu một công ty nào đó không tìm thấy thông tin trên Explorium, giúp đội ngũ sales dễ dàng lọc lại.
- **Mở rộng dữ liệu:** Tùy biến *Output Parser* và prompt trong *AI Agent* để lấy thêm các trường dữ liệu nâng cao khác tùy theo nhu cầu ngành hàng của doanh nghiệp.

### 📌 Kết luận
Workflow tích hợp Explorium và Claude AI này chính là "vũ khí bí mật" giúp đội ngũ sales và marketing tự động hóa hoàn toàn khâu nghiên cứu khách hàng (Prospect Research). Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm việc và bứt phá doanh số cùng n8n!