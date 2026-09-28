---
title: "🚀 Tự động hóa tổng hợp tin Bitcoin bằng AI Gemini và đăng lên Discord"
description: "Hướng dẫn chi tiết cách tự động hóa việc tổng hợp tin tức Bitcoin bằng AI Gemini và đăng lên Discord mỗi 6 giờ, tiết kiệm thời gian và nâng cao hiệu quả truyền thông"
slug: "tu-dong-hoa-tong-hop-tin-bitcoin-bang-ai-gemini-va-dang-len-discord"
tags: [n8n, automation, no-code, AI, Discord, Google Sheets]
keywords: [n8n workflow, tự động hóa, AI tổng hợp, Discord, Bitcoin]
---

# 🚀 Tự động hóa tổng hợp tin Bitcoin bằng AI Gemini và đăng lên Discord

[Các sếp] có biết không? Với lượng tin tức về Bitcoin ngày càng tăng, việc theo dõi và tổng hợp thông tin thủ công thật sự tốn thời gian và dễ bỏ sót những điểm quan trọng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ lấy tin tức đến tổng hợp và đăng lên Discord mỗi 6 giờ, với sự hỗ trợ của AI Gemini.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ 30-60 phút/ngày.
- **Tin tức chính xác**: AI Gemini tổng hợp thông tin chính xác và ngắn gọn.
- **Truyền thông hiệu quả**: Bài đăng được định dạng chuyên nghiệp với hashtags.
- **Theo dõi hoạt động**: Log đầy đủ trên Google Sheets và thông báo Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt.
- API Key của Google Gemini (có thể sử dụng phiên bản miễn phí).
- Discord Webhook URL cho kênh mục tiêu.
- Tài khoản Slack để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14213](https://n8n.io/workflows/14213)
2. Chọn "Import" và sao chép JSON vào n8n Editor của các sếp.
3. Hoặc tải file JSON về và import trực tiếp từ n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Set config values**:
   - Điền Google Sheet ID (ID của bảng tính Google Sheets).
   - Điền Discord Webhook URL (URL webhook của kênh Discord mục tiêu).
   - Cập nhật hashtags (từ khóa liên quan đến Bitcoin).

2. **Google Gemini Chat Model**:
   - Thêm Google Gemini API credential (có thể sử dụng phiên bản miễn phí).

3. **Log to Google Sheets**:
   - Kết nối Google Sheets OAuth2 credential.

4. **Notify Slack**:
   - Thêm Slack credential và channel ID để nhận thông báo.

5. **Run every 6 hours**:
   - Có thể điều chỉnh thời gian chạy theo nhu cầu (mặc định là mỗi 6 giờ).

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết quả.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi URL RSS trong node "Set config values" để lấy tin từ nguồn khác.
- Chỉnh sửa prompt trong node "Basic LLM Chain" để thay đổi ngôn ngữ hoặc phong cách bài đăng.
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi có tin mới.
- Lưu log chi tiết hơn bằng cách thêm các trường thông tin bổ sung vào Google Sheets.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi và tổng hợp tin tức Bitcoin. Với sự hỗ trợ của AI Gemini, các sếp có thể nhận được tin tức chính xác và ngắn gọn, được định dạng chuyên nghiệp và đăng lên Discord một cách tự động. Hãy áp dụng ngay để nâng cao hiệu quả truyền thông và quản lý thông tin Bitcoin của các sếp!