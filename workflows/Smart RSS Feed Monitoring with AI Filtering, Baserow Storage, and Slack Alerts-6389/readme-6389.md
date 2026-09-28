---
title: "🚀 Tự động hóa RSS Feed với AI Lọc Tin và Thông báo Slack"
description: "Workflow n8n tự động theo dõi RSS Feed, lọc tin mới bằng AI, lưu vào Baserow và gửi thông báo Slack. Giúp tiết kiệm thời gian và tránh thông tin trùng lặp."
slug: "tu-dong-hoa-rss-feed-voi-ai-loc-tin-va-thong-bao-slack"
tags: [n8n, automation, no-code, rss, ai, baserow, slack]
keywords: [n8n workflow, tự động hóa, rss feed, ai lọc tin, baserow, slack notification]
---

# 🚀 Tự động hóa RSS Feed với AI Lọc Tin và Thông báo Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động theo dõi và lọc tin mới từ nhiều nguồn RSS.
- Chính xác: AI lọc tin giúp loại bỏ thông tin trùng lặp và không liên quan.
- Cá nhân hóa: Chỉ nhận thông báo về tin tức quan tâm.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Baserow với 2 bảng dữ liệu đã cấu hình (chi tiết bên dưới).
- API Key OpenAI để sử dụng AI lọc tin.
- Tài khoản Slack với quyền gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Click vào "New" -> "Import from JSON".
3. Dán nội dung JSON của workflow vào ô nhập liệu.
4. Click "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Read Rss Link"**:
   - Cấu hình credentials Baserow.
   - Đảm bảo bảng dữ liệu chứa RSS Links đã được tạo với cấu trúc đúng (Database ID: 243547, Table ID: 579115, cột `rssLink`).

2. **Node "Get Seen Products"**:
   - Cấu hình credentials Baserow.
   - Đảm bảo bảng dữ liệu "Seen Products" đã được tạo với cấu trúc đúng (Database ID: 243547, Table ID: 578089, cột `Nom`).

3. **Node "OpenAI Chat Model"**:
   - Cấu hình credentials OpenAI.
   - Đảm bảo đã chọn model phù hợp (gpt-4o-mini trong ví dụ).

4. **Node "Slack"**:
   - Cấu hình credentials Slack (OAuth hoặc Webhook).
   - Chọn channel phù hợp để nhận thông báo.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để chạy thử với dữ liệu mẫu.
2. Kiểm tra kết quả trên Slack và Baserow.
3. Bật Active workflow bằng cách toggle nút ở góc trên bên phải của n8n Editor.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Schedule Trigger" để workflow chạy tự động theo lịch (ví dụ: mỗi giờ).
- Kết hợp với Telegram bằng node "Telegram" để nhận thông báo trên cả hai nền tảng.
- Lưu log hoạt động vào Google Sheets bằng node "Google Sheets" để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về số lượng tin mới đã xử lý bằng node "Email".

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi tin tức từ nhiều nguồn khác nhau. Bằng cách kết hợp AI lọc tin và lưu trữ dữ liệu trong Baserow, workflow đảm bảo chỉ nhận thông báo về tin tức mới và quan trọng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc! 🚀