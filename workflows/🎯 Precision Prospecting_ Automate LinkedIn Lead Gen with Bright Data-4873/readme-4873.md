---
title: "🎯 Tự động hóa tìm kiếm lead LinkedIn với Bright Data và AI"
description: "Hướng dẫn tự động hóa tìm kiếm lead LinkedIn chuyên nghiệp với Bright Data và OpenAI, tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng"
slug: "tu-dong-hoa-tim-kiem-lead-linkedin-voi-bright-data-va-ai"
tags: [n8n, automation, no-code, linkedin, sales]
keywords: [n8n workflow, tự động hóa lead, linkedin automation, bright data, openai]
---

# 🎯 Tự động hóa tìm kiếm lead LinkedIn với Bright Data và AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian tìm kiếm lead thủ công
- Tăng độ chính xác trong việc xác định lead tiềm năng
- Tự động hóa quá trình phân tích thông tin từ LinkedIn
- Tích hợp AI để cá nhân hóa thông điệp chăm sóc khách hàng
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI (API Key)
- Tài khoản Bright Data (API Key)
- Workflow ID của workflow hiện tại trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import" trên thanh công cụ
3. Chọn file JSON workflow hoặc copy/paste JSON vào editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Search LinkedIn URI"**:
   - Cập nhật Workflow ID của workflow hiện tại
   - Để tìm Workflow ID, truy cập vào workflow trong n8n và kiểm tra URL (ví dụ: nếu URL là `https://n8n-ai.cr.vps2.clients.killia.com/workflow/fjEIEQ1L6n2IKqlx`, Workflow ID là `fjEIEQ1L6n2IKqlx`)

2. **Node "Get LinkedIn Profile Data" và "Get 1 Google Result"**:
   - Thêm Bright Data API Key vào credentials
   - Đảm bảo tài khoản Bright Data có quyền truy cập vào các công cụ cần thiết

3. **Node "OpenAI Chat Model"**:
   - Thêm OpenAI API Key vào credentials
   - Chọn model phù hợp (gợi ý: gpt-4o-mini)

4. **Node "Filter only LinkedIn Profiles"**:
   - Điều chỉnh bộ lọc để phù hợp với tiêu chí tìm kiếm lead của bạn

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu tự động hóa

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi tìm thấy lead mới
2. Lưu log các lead tìm được vào Google Sheets để theo dõi
3. Tích hợp với email marketing để gửi thông điệp chăm sóc khách hàng tự động
4. Thiết lập báo cáo định kỳ về hiệu suất tìm kiếm lead

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá trong việc tìm kiếm lead LinkedIn, đồng thời tăng độ chính xác và cá nhân hóa trong quá trình chăm sóc khách hàng. Hãy thử ngay và nâng cao hiệu quả kinh doanh của bạn!