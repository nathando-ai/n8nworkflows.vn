---
title: "🚀 Tự động đồng bộ sản phẩm từ Shopify sang WooCommerce với Gemini, BrowserAct và Slack"
description: "Hướng dẫn chi tiết cách tự động đồng bộ sản phẩm từ Shopify sang WooCommerce với AI Gemini, BrowserAct và Slack. Tiết kiệm thời gian, tránh trùng lặp và nhận thông báo hoàn thành."
slug: "tu-dong-dong-bo-san-pham-shopify-woocommerce-gemini-browseract-slack"
tags: [n8n, automation, no-code, shopify, woocommerce, ai, browseract, slack]
keywords: [n8n workflow, tự động hóa, shopify, woocommerce, ai, browseract, slack]
---

# 🚀 Tự động đồng bộ sản phẩm từ Shopify sang WooCommerce với Gemini, BrowserAct và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc đồng bộ sản phẩm giữa các nền tảng
- Tránh trùng lặp sản phẩm trong kho hàng WooCommerce
- Tự động phân loại và tối ưu hóa thông tin sản phẩm nhờ AI Gemini
- Nhận thông báo hoàn thành hoặc lỗi qua Slack
- Tích hợp thông tin bổ sung từ các nguồn khác nhờ BrowserAct
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản WooCommerce với quyền quản trị
- API Key của BrowserAct (Template: Shopify to WooCommerce Multi-Store Sync)
- API Key của Google Gemini (Google PaLM)
- Tài khoản Slack với quyền gửi tin nhắn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Google Gemini** và **Google Gemini1**:
   - Chọn credentials "googlePalmApi"
   - Đảm bảo API key đã được kích hoạt và có quyền truy cập

2. **Get Shopify Products**:
   - Chọn credentials "shopifyAccessTokenApi"
   - Đảm bảo API key có quyền truy cập đầy đủ đến sản phẩm

3. **Search for Product Info**:
   - Chọn credentials "browserActApi"
   - Đảm bảo đã lưu template "Shopify to WooCommerce Multi-Store Sync"

4. **Get WooCommerce Products** và **Import Product to WooCommerce**:
   - Chọn credentials "wooCommerceApi"
   - Đảm bảo API key có quyền tạo và đọc sản phẩm

5. **Send Error** và **Notify Slack Team of Completion**:
   - Chọn credentials "slackApi"
   - Đảm bảo channel đã được cấu hình đúng trong Slack

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node lịch trình để tự động chạy workflow theo lịch định kỳ
- Kết hợp với các dịch vụ khác như Telegram để nhận thông báo
- Tùy chỉnh prompt cho AI để phù hợp với ngành hàng cụ thể
- Thêm bước xác nhận trước khi tạo sản phẩm mới trong WooCommerce
- Lưu log các hoạt động quan trọng để theo dõi sau này

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc đồng bộ sản phẩm giữa Shopify và WooCommerce. Nhờ tích hợp AI Gemini và BrowserAct, thông tin sản phẩm được tối ưu hóa và bổ sung đầy đủ. Với thông báo qua Slack, các sếp luôn được cập nhật tình trạng đồng bộ một cách tức thì. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh!