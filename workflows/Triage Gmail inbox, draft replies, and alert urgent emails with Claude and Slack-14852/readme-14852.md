---
title: "🚀 Tự động hóa Inbox Gmail với Claude và Slack - Xử lý Email một cách thông minh"
description: "Hướng dẫn tự động hóa xử lý email Gmail với n8n, Claude AI và Slack. Tiết kiệm thời gian, giảm stress và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-inbox-gmail-voi-claude-va-slack"
tags: [n8n, automation, no-code, gmail, claude, slack, ai]
keywords: [n8n workflow, tự động hóa email, xử lý email thông minh, claude ai, slack alert, google sheets]
---

# 🚀 Tự động hóa Inbox Gmail với Claude và Slack - Xử lý Email một cách thông minh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Xử lý hàng trăm email mỗi ngày một cách tự động, không cần can thiệp thủ công.
- Giảm stress: Không còn phải lo lắng về việc bỏ lỡ email quan trọng.
- Nâng cao hiệu suất: Tập trung vào công việc quan trọng nhất thay vì xử lý email hàng ngày.
- Cá nhân hóa: Tùy chỉnh quy trình xử lý email theo nhu cầu cá nhân và doanh nghiệp.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail (đã kích hoạt API và bật IMAP)
- Tài khoản Anthropic (để sử dụng Claude AI)
- Tài khoản Slack (tùy chọn)
- Tài khoản Google Sheets (tùy chọn)
- API Key từ Anthropic (từ console.anthropic.com)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14852](https://n8n.io/workflows/14852)
2. Click vào nút "Import" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

Hoặc bạn có thể copy/paste JSON từ trang n8n.io vào n8n Editor bằng cách:
1. Click vào nút "Import from Clipboard"
2. Dán nội dung JSON từ trang n8n.io
3. Click "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Check for New Emails (gmailTrigger)**
   - Kết nối tài khoản Gmail của bạn
   - Đảm bảo đã bật IMAP trong cài đặt Gmail
   - Thời gian kiểm tra mặc định là 15 phút (có thể thay đổi)

2. **Claude Sonnet (lmChatAnthropic)**
   - Click vào sub-node Claude Sonnet
   - Thêm credential mới cho Anthropic
   - Nhập API Key từ console.anthropic.com
   - Chọn model "claude-sonnet-4-5"

3. **Notify Urgent Email (slack)**
   - Kết nối tài khoản Slack của bạn
   - Chọn channel hoặc DM để nhận thông báo
   - Nếu không dùng Slack, có thể tắt node này

4. **Label as Urgent (gmail)**
   - Kết nối tài khoản Gmail
   - Tạo label "AI-Urgent" trong Gmail
   - Nhập ID của label này vào node

5. **Save Draft Reply (gmail)**
   - Kết nối tài khoản Gmail
   - Đảm bảo đã bật quyền tạo draft trong cài đặt Gmail

6. **Log to Sheets (googleSheets)**
   - Tạo Google Sheet mới với các cột: Timestamp, Sender, Subject, Category, Summary, Draft Saved
   - Kết nối tài khoản Google của bạn
   - Nhập ID của Google Sheet và tên sheet vào node

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách click vào nút "Execute Workflow" trong n8n Editor
2. Kiểm tra kết quả trên Gmail, Slack và Google Sheets
3. Bật Active workflow bằng cách click vào nút "Activate" trong n8n Editor

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi tần suất kiểm tra email trong node "Check for New Emails" từ 15 phút sang giá trị khác phù hợp với nhu cầu của bạn
- Thêm danh sách VIP sender vào prompt của node "Classify Email Intent" để đảm bảo email từ những người quan trọng luôn được xử lý ưu tiên
- Mở rộng branch "Needs Reply" để tự động gửi những email đơn giản mà không cần lưu nháp
- Kết hợp với các dịch vụ khác như Telegram để nhận thông báo thay vì Slack
- Thêm node lưu log chi tiết hơn vào Google Sheets
- Tạo báo cáo định kỳ từ dữ liệu log để theo dõi hiệu suất xử lý email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình xử lý email hàng ngày, từ việc phân loại email đến tạo nháp trả lời và thông báo email quan trọng. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm hàng giờ mỗi ngày và tập trung vào công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự khác biệt mà tự động hóa mang lại!