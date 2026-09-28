---
title: "🚀 Tự động hóa Email Cá nhân hóa với Claude 3.7 và LinkedIn - Workflow n8n"
description: "Tự động tìm kiếm thông tin LinkedIn, tạo email cá nhân hóa với AI và gửi hàng loạt qua Gmail - Giảm 90% thời gian làm việc thủ công"
slug: "tu-dong-hoa-email-ca-nhan-hoa-voi-claude-37-va-linkedin"
tags: [n8n, automation, no-code, linkedin, gmail]
keywords: [n8n workflow, tự động hóa email, linkedin automation, claude 3.7, gmail automation]
---

# 🚀 Tự động hóa Email Cá nhân hóa với Claude 3.7 và LinkedIn - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 90% thời gian tìm kiếm thông tin LinkedIn thủ công
- Tạo email cá nhân hóa chất lượng cao với AI Claude 3.7
- Gửi hàng loạt email thông qua Gmail một cách tự động
- Xử lý hàng trăm leads trong một lần chạy workflow
- Tăng tỷ lệ mở email nhờ nội dung phù hợp với từng người nhận
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Gmail API)
- API Key từ OpenRouter (để truy cập Claude 3.7)
- Tài khoản Apify (cho các node tìm kiếm LinkedIn)
- Google Sheet chứa danh sách leads (cột: First Name, Last Name, Company, Email)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/8978)
2. Click "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Node quan trọng nhất cần cấu hình:**
- **Get Leads (Google Sheets):**
  - Chọn credentials Google Sheets OAuth2
  - Điền Spreadsheet ID và Sheet Name chứa danh sách leads
  - Đảm bảo các cột: First Name, Last Name, Company, Email

- **OpenRouter Chat Model:**
  - Thêm credentials OpenRouter API
  - Model đã được cấu hình sẵn: anthropic/claude-3.7-sonnet
  - Tùy chỉnh prompt trong node "Generate Personalized Email" nếu cần

- **Gmail Node:**
  - Thêm credentials Gmail OAuth2
  - Điền email người gửi (phải cùng domain với tài khoản OAuth2)
  - Tùy chỉnh template email trong node "Structured Output Parser"

- **HTTP Request Nodes (LinkedIn Search):**
  - Thêm credentials HTTP Header Auth (cho Apify)
  - Đảm bảo có API Key hợp lệ từ Apify

#### 3. Kích hoạt ⚡️
1. Chạy test với 1-2 leads mẫu để kiểm tra kết quả
2. Sau khi xác nhận hoạt động, bật Active workflow
3. Thiết lập trigger theo lịch (ví dụ: hàng ngày lúc 9h sáng)

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo khi workflow hoàn thành
- Lưu log kết quả vào Google Sheets để theo dõi hiệu suất
- Tạo bản sao lưu của workflow hàng tuần
- Thử nghiệm với các model khác từ OpenRouter (ví dụ: Mistral Large)
- Kết hợp với workflow khác để tự động hóa toàn bộ chuỗi làm việc bán hàng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc tìm kiếm thông tin và tạo email cá nhân hóa. Bằng cách tự động hóa toàn bộ quy trình từ tìm kiếm LinkedIn đến gửi email, các sếp có thể tập trung vào những nhiệm vụ có giá trị hơn trong công việc. Hãy thử ngay và trải nghiệm sự khác biệt mà tự động hóa mang lại!