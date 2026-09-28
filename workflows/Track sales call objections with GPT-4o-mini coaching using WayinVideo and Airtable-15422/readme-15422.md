---
title: "🎤 Tự động hóa phân tích cuộc gọi bán hàng với GPT-4o-mini và Airtable"
description: "Hướng dẫn tự động hóa phân tích cuộc gọi bán hàng bằng công nghệ AI, lưu trữ dữ liệu vào Airtable để theo dõi và cải thiện hiệu suất bán hàng"
slug: "tu-dong-hoa-phan-tich-cuoc-goi-ban-hang-voi-gpt-4o-mini-airtable"
tags: [n8n, automation, no-code, ai, crm]
keywords: [n8n workflow, tự động hóa, phân tích cuộc gọi, GPT-4o-mini, Airtable]
---

# 🎤 Tự động hóa phân tích cuộc gọi bán hàng với GPT-4o-mini và Airtable

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp bán hàng thường phải tốn nhiều thời gian để xem lại và phân tích các cuộc gọi bán hàng. Với workflow này, các sếp có thể tự động hóa quá trình này bằng cách sử dụng công nghệ AI để phân tích cuộc gọi và lưu trữ dữ liệu vào Airtable.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian phân tích cuộc gọi bán hàng
- Phân tích chính xác các điểm yếu trong cuộc gọi
- Lưu trữ dữ liệu vào Airtable để theo dõi và cải thiện hiệu suất bán hàng
- Tự động hóa quá trình phân tích cuộc gọi bán hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo và API key
- Tài khoản OpenAI và API key
- Tài khoản Airtable và API key
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/15422
3. Click vào "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **2. WayinVideo — Submit Find Moments**: Thay thế YOUR_WAYINVIDEO_API_KEY bằng API key của bạn
- **4. WayinVideo — Get Moments Results**: Thay thế YOUR_WAYINVIDEO_API_KEY bằng API key của bạn
- **9. OpenAI — GPT-4o-mini Model**: Kết nối với tài khoản OpenAI của bạn
- **11. HTTP — Save to Airtable**: Thay thế YOUR_AIRTABLE_API_KEY, YOUR_AIRTABLE_BASE_ID, và YOUR_AIRTABLE_TABLE_NAME bằng thông tin của bạn

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có cuộc gọi mới
- Lưu log để theo dõi quá trình phân tích
- Gửi báo cáo định kỳ về hiệu suất bán hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình phân tích cuộc gọi bán hàng, tiết kiệm thời gian và cải thiện hiệu suất bán hàng. Các sếp có thể áp dụng ngay để nâng cao hiệu quả kinh doanh.