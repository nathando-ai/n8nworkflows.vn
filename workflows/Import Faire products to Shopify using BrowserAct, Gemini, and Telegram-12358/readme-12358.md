---
title: "🚀 Tự động nhập sản phẩm từ Faire lên Shopify với BrowserAct, Google Gemini và Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình cào dữ liệu sản phẩm từ Faire, tối ưu nội dung bằng AI Gemini và đẩy lên cửa hàng Shopify qua Telegram Bot."
slug: "tu-dong-nhap-san-pham-faire-len-shopify-n8n"
tags: [n8n, automation, shopify, telegram, google-gemini, ai, e-commerce]
keywords: [n8n workflow, tự động hóa shopify, scrape faire product, browseract n8n, google gemini ai]
---

# 🚀 Tự động nhập sản phẩm từ Faire lên Shopify với BrowserAct, Google Gemini và Telegram

Việc copy thủ công từng sản phẩm từ các sàn sỉ như Faire lên cửa hàng Shopify của các sếp không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót về giá, mô tả hay hình ảnh. Chưa kể việc tối ưu SEO cho hàng loạt sản phẩm là một cơn ác mộng thực sự.

Đừng lo, workflow n8n đỉnh cao này sinh ra để giải quyết triệt để vấn đề đó! Chỉ với một tin nhắn gửi link sản phẩm qua **Telegram**, hệ thống sẽ tự động cào dữ liệu, dùng **Google Gemini** để viết lại mô tả chuẩn SEO, xử lý giá, hình ảnh và tạo sản phẩm hoàn chỉnh trên **Shopify** mà các sếp không cần đụng tay chân.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì copy-paste thủ công từng sản phẩm, bot sẽ lo từ A-Z chỉ trong vài giây.
- **Tối ưu SEO tự động:** Google Gemini tự động biên tập lại tiêu đề và mô tả sản phẩm hấp dẫn, chuẩn SEO HTML.
- **Tương tác mượt mà qua Telegram:** Nhận thông báo tiến độ, xác thực thủ công (nếu gặp CAPTCHA) và chat trực tiếp với bot.
- **Đồng bộ toàn diện:** Tự động tạo sản phẩm cơ bản, thêm giá, biến thể và toàn bộ hình ảnh lên Shopify.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **BrowserAct Account & API Key** (Cùng template **Product Importer Bot for Shopify**).
- **Google Gemini API Key** (Google PaLM/Gemini).
- **Shopify Custom App / Admin Access Token** (quyền truy cập đọc/ghi sản phẩm).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và thông số cho các node cốt lõi sau:
- **User Sends Message to Bot / Answer the User / Process Initialization Alert / Send Failure Alert / Ask User for Verification**: Chọn `telegramApi` và điền Bot Token tương ứng của các sếp.
- **Google Gemini / Google Gemini2 / Google Gemini3**: Cấu hình `googlePalmApi` với Gemini API Key để phục vụ các Agent phân tích và xử lý ngôn ngữ.
- **Scrape Product Data / Get Data From BrowserAct**: Cấu hình `browserActApi` và trỏ đúng vào template **Product Importer Bot for Shopify** trên nền tảng BrowserAct.
- **Create a product / Add Price to Product / Add Images to Product**: Kết nối `shopifyAccessTokenApi` và điền Store URL của Shopify để bot có quyền đẩy sản phẩm lên kệ hàng.
- **Human verification Switch & Validation Type Switch**: Kiểm tra lại các điều kiện rẽ nhánh để đảm bảo luồng xử lý link hợp lệ và cơ chế vượt CAPTCHA (nếu có) hoạt động trơn tru.

#### 3. Chạy thử nghiệm & Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một link sản phẩm Faire bất kỳ vào Telegram Bot của các sếp để kiểm tra log.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành tự động 24/7.

### ✍️ Nâng cấp & Gợi ý mở rộng
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để lưu lại danh sách các sản phẩm đã import thành công kèm link Shopify.
- **Thông báo đa kênh:** Gửi thêm thông báo về kênh Slack hoặc Microsoft Teams nội bộ của công ty mỗi khi có sản phẩm mới lên sàn.
- **Xử lý hàng đợi (Queue):** Tích hợp thêm tính năng nhận danh sách nhiều link cùng lúc để import hàng loạt (Bulk Import).

### 📌 Kết luận
Autom hóa quy trình nhập hàng từ Faire lên Shopify chưa bao giờ dễ dàng đến thế với sự kết hợp hoàn hảo giữa BrowserAct, AI Gemini và Telegram. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho cửa hàng E-commerce của các sếp!