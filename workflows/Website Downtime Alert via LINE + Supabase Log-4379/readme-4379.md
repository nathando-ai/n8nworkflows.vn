---
title: "🚨 [Tự động cảnh báo website bị down qua LINE + ghi log vào Supabase]"
description: "Workflow n8n tự động kiểm tra website định kỳ, cảnh báo ngay khi down qua LINE và lưu log vào Supabase. Giảm thời gian phản hồi và tăng tính minh bạch cho hệ thống."
slug: "tu-dong-can-bao-website-down-qua-line-supabase"
tags: [n8n, automation, no-code, devops, supabase]
keywords: [n8n workflow, tự động hóa website, uptime monitor, cảnh báo LINE, log hệ thống]
---

# 🚨 Tự động cảnh báo website bị down qua LINE + ghi log vào Supabase

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công tình trạng hoạt động của website, dẫn đến thời gian phản hồi chậm và không thể đảm bảo tính ổn định của hệ thống. Workflow này sẽ tự động hóa toàn bộ quy trình kiểm tra, cảnh báo và lưu log, giúp các sếp tiết kiệm thời gian và tăng tính minh bạch cho hệ thống.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hệ thống tự động kiểm tra website theo lịch trình.
- **Cảnh báo tức thời**: Nhận thông báo ngay khi website down qua LINE, giảm thời gian phản hồi.
- **Lưu trữ log chuyên nghiệp**: Tất cả các sự kiện được lưu vào Supabase, giúp theo dõi và phân tích hiệu suất hệ thống.
- **Tăng tính minh bạch**: Các sếp và team có thể xem lịch sử hoạt động của website một cách dễ dàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản UptimeRobot (để theo dõi website).
- Tài khoản OpenAI (để sử dụng LLM).
- Tài khoản LINE Notify (để nhận cảnh báo).
- Tài khoản Supabase (để lưu log).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/4379](https://n8n.io/workflows/4379).
3. Hoặc tải file JSON về và import từ local.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Monitors"**:
   - Chọn credentials là `uptimeRobotApi`.
   - Đảm bảo tài khoản UptimeRobot đã được cấu hình đúng.

2. **Node "LLM Message Format"**:
   - Cấu hình prompt để định dạng thông báo cảnh báo.

3. **Node "OpenAI GPT-4o Mini"**:
   - Chọn credentials là `openAiApi`.
   - Đảm bảo tài khoản OpenAI đã được cấu hình đúng.

4. **Node "Send to LINE"**:
   - Cấu hình URL và headers cho LINE Notify.
   - Thêm tham số `message` để gửi thông báo.

5. **Node "Save to Supabase"**:
   - Chọn credentials là `supabaseApi`.
   - Cấu hình table và các trường cần lưu (ví dụ: `monitor_id`, `status`, `timestamp`).

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy định kỳ.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi cảnh báo qua các kênh khác.
- **Lưu log chi tiết hơn**: Thêm các trường thông tin bổ sung vào Supabase.
- **Cảnh báo định kỳ**: Thêm node để gửi báo cáo trạng thái website định kỳ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình kiểm tra, cảnh báo và lưu log cho website. Với tính năng cảnh báo tức thời và lưu trữ log chuyên nghiệp, các sếp có thể giảm thời gian phản hồi và tăng tính minh bạch cho hệ thống. Hãy áp dụng ngay để nâng cao hiệu suất và tính ổn định của hệ thống!