---
title: "🎤 Trợ lý AI Voice-to-Text: Ghi âm → Văn bản → Email với Claude Sonnet"
description: "Tự động chuyển đổi ghi âm thoại thành văn bản thông minh, xử lý bằng AI và gửi email kết quả chỉ trong vài giây. Giải phóng thời gian cho các sếp với công cụ không cần code này!"
slug: "tro-ly-ai-voice-to-text-voi-claude-sonnet"
tags: [n8n, automation, no-code, ai, productivity]
keywords: [voice to text, tự động hóa ghi âm, claude sonnet, n8n workflow, ai assistant]
---

# 🎤 Trợ lý AI Voice-to-Text: Ghi âm → Văn bản → Email với Claude Sonnet

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi ghi âm thoại thành văn bản chính xác với AI
- Xử lý thông minh bằng mô hình Claude Sonnet của Anthropic
- Lưu trữ dữ liệu vào cơ sở dữ liệu NocoDB
- Tự động gửi email kết quả với định dạng HTML đẹp mắt
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenRouter API (để sử dụng mô hình Claude Sonnet)
- Tài khoản NocoDB (để lưu trữ dữ liệu)
- Tài khoản Gmail (để gửi email kết quả)
- Ứng dụng ghi âm thoại (như Voicenotes) để gửi webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/6618)
2. Nhấn nút "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Node**:
   - Đảm bảo đường dẫn webhook duy nhất: `dbedd9a0-e0bd-4e70-8f62-87013f9dd9c3`
   - Cấu hình ứng dụng ghi âm thoại để gửi POST request đến URL này

2. **OpenRouter Chat Model**:
   - Thêm credentials "openRouterApi"
   - Đảm bảo đã chọn mô hình "anthropic/claude-sonnet-4"

3. **NocoDB Nodes**:
   - Thêm credentials "nocoDbApiToken"
   - Cấu hình đúng thông tin kết nối NocoDB
   - Đảm bảo bảng dữ liệu đã được tạo trước với cấu trúc phù hợp

4. **Gmail Node**:
   - Thêm credentials "gmailOAuth2"
   - Cấu hình đúng địa chỉ email nhận kết quả
   - Tùy chỉnh template email theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Thử chạy với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Kích hoạt workflow bằng cách nhấn nút "Active" trên thanh công cụ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi có ghi âm mới
2. Thêm node lưu log để theo dõi lịch sử xử lý
3. Tạo báo cáo định kỳ từ dữ liệu lưu trữ trong NocoDB
4. Tích hợp với các công cụ khác như Notion để lưu trữ văn bản

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày bằng cách tự động hóa quy trình chuyển đổi ghi âm thoại thành văn bản thông minh. Với khả năng tích hợp mạnh mẽ và giao diện đơn giản, đây là công cụ không thể thiếu cho bất kỳ ai làm việc với nội dung thoại.