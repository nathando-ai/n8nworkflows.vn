---
title: "🚀 Tự động phân loại ticket Jira với AI Gemini - Giải pháp toàn diện cho đội ngũ hỗ trợ"
description: "Hướng dẫn chi tiết cách tự động phân loại ticket Jira với AI Gemini, tiết kiệm thời gian và nâng cao chất lượng hỗ trợ khách hàng"
slug: "tu-dong-phan-loai-ticket-jira-voi-ai-gemini"
tags: [n8n, automation, no-code, jira, ai, google-gemini]
keywords: [n8n workflow, tự động hóa, jira, ai, google gemini, phân loại ticket]
---

# 🚀 Tự động phân loại ticket Jira với AI Gemini - Giải pháp toàn diện cho đội ngũ hỗ trợ

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 60% thời gian phân loại ticket thủ công
- Nâng cao độ chính xác phân loại lên 90% với AI Gemini
- Tự động cập nhật thông tin ticket (Priority, Component, Labels)
- Tạo audit trail rõ ràng cho mỗi quyết định của AI
- Theo dõi hiệu suất của hệ thống tự động hóa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Jira với quyền truy cập API
- API Key từ Google Gemini
- Thông tin xác thực HTTP Basic Auth cho Jira
- Dữ liệu domain knowledge (từ Trello) về sản phẩm/phần mềm của bạn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/8713
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node Webhook**:
   - Đảm bảo đường dẫn webhook duy nhất: `dcc89146-5bdb-4330-9bc1-2d021db266cd`
   - Cấu hình để nhận ticket Jira theo thời gian thực

2. **Node SET_SETUP**:
   - Cập nhật thông tin domain knowledge trong sticky note
   - Điều chỉnh ngưỡng độ tin cậy (confidence threshold) theo nhu cầu

3. **Node AI Case Triage**:
   - Kết nối với Google Gemini API
   - Cấu hình credentials "googlePalmApi" với API Key của bạn

4. **Node JIRA Update & JIRA Add Comment**:
   - Cấu hình credentials "httpBasicAuth" với thông tin xác thực Jira
   - Kiểm tra endpoint API của Jira (thường là `https://your-domain.atlassian.net/rest/api/2/issue/{issueId}`)

5. **Node Build Payload for LLM**:
   - Điều chỉnh prompt để phù hợp với ngữ cảnh của bạn
   - Thêm thông tin domain knowledge cụ thể

#### 3. Kích hoạt ⚡️
1. Test run với ticket mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Kiểm tra kết quả trên Jira để xác nhận:
   - Thay đổi Priority/Component/Labels
   - Bình luận audit của AI
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để thông báo kết quả phân loại
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets hoặc database
3. **Báo cáo định kỳ**: Tạo workflow con để tổng hợp metrics hàng ngày
4. **Mở rộng domain knowledge**: Thêm thông tin chi tiết hơn về sản phẩm của bạn

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động phân loại ticket Jira với AI Gemini, giúp đội ngũ hỗ trợ tập trung vào những vấn đề thực sự quan trọng. Với khả năng cấu hình linh hoạt và audit trail rõ ràng, nó không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng hỗ trợ khách hàng. Hãy thử ngay và trải nghiệm sự khác biệt!