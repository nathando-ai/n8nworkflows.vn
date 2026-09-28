---
title: "📊 Tự động hóa báo cáo hiệu suất Google Ads hàng tuần với AI GPT-5.1 và Gmail"
description: "Hướng dẫn tự động hóa báo cáo hiệu suất Google Ads hàng tuần bằng n8n, tích hợp AI GPT-5.1 và gửi email thông qua Gmail. Tiết kiệm thời gian và nâng cao hiệu quả quảng cáo."
slug: "tu-dong-hoa-bao-cao-hieu-suat-google-ads-hang-tuan-voi-ai-gpt-5-1-va-gmail"
tags: [n8n, automation, no-code, google-ads, ai, gmail]
keywords: [n8n workflow, tự động hóa báo cáo, google ads, ai phân tích, gmail]
---

# 📊 Tự động hóa báo cáo hiệu suất Google Ads hàng tuần với AI GPT-5.1 và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa báo cáo hàng tuần, không cần can thiệp thủ công.
- Chính xác: So sánh dữ liệu hiệu suất quảng cáo tuần này với tuần trước.
- Cá nhân hóa: Nhận báo cáo chi tiết về các chiến dịch hiệu quả và cần cải thiện.
- Hoạt động liên tục: Tự động gửi báo cáo mỗi tuần vào thứ Hai lúc nửa đêm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Ads với quyền truy cập API.
- Tài khoản Gmail để gửi báo cáo.
- API Key của OpenAI để sử dụng mô hình GPT-5.1.
- Thông tin Customer ID và Developer Token từ Google Ads.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12288](https://n8n.io/workflows/12288) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy/paste nội dung JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "OpenAI Chat Model"**:
   - Chọn credentials "openAiApi".
   - Đảm bảo mô hình "gpt-5.1" được chọn.

2. **Node "Email Report to User"**:
   - Chọn credentials "gmailOAuth2".
   - Cập nhật địa chỉ email nhận báo cáo.

3. **Node "Get Previous Week Data" và "Get Last Week Data"**:
   - Chọn credentials "googleAdsOAuth2Api".
   - Thay thế `[Customer ID]` trong URL bằng Customer ID thực tế của bạn.
   - Thêm Developer Token vào header parameters.

4. **Node "Weekly Trigger"**:
   - Đảm bảo lịch trình được đặt để chạy mỗi thứ Hai lúc nửa đêm.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa báo cáo hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo báo cáo.
- Lưu log dữ liệu để theo dõi hiệu suất dài hạn.
- Gửi báo cáo định kỳ hàng tháng với tổng hợp dữ liệu.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa báo cáo hiệu suất Google Ads hàng tuần, tiết kiệm thời gian và nâng cao hiệu quả quảng cáo. Hãy áp dụng ngay để tối ưu hóa chiến dịch quảng cáo của bạn!