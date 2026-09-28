---
title: "🧱 Tự động biến ảnh thành phong cách Lego bằng Line và DALL-E"
description: "Hướng dẫn tự động hóa chuyển đổi ảnh thành phong cách Lego chỉ với 1 tin nhắn Line, tiết kiệm thời gian và tạo ra những hình ảnh độc đáo cho doanh nghiệp"
slug: "tu-dong-bien-anh-thanh-phong-cach-lego-bang-line-va-dall-e"
tags: [n8n, automation, no-code, ai, line, dall-e]
keywords: [n8n workflow, tự động hóa, line bot, dall-e, ảnh lego]
---

# 🧱 Tự động biến ảnh thành phong cách Lego bằng Line và DALL-E

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi làm việc với hình ảnh, các sếp thường gặp khó khăn khi cần chuyển đổi phong cách ảnh một cách nhanh chóng và chuyên nghiệp. Đặc biệt là khi muốn tạo ra những hình ảnh phong cách Lego độc đáo cho các chiến dịch marketing. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình chỉ với 1 tin nhắn Line, tiết kiệm thời gian đáng kể và nâng cao tính chuyên nghiệp của hình ảnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong quá trình chuyển đổi phong cách ảnh
- Tạo ra những hình ảnh phong cách Lego chuyên nghiệp và độc đáo
- Tự động hóa toàn bộ quá trình chỉ với 1 tin nhắn Line
- Tăng tính chuyên nghiệp cho các chiến dịch marketing
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Line Business (để tạo và quản lý Line Bot)
- API Key của OpenAI (để sử dụng dịch vụ DALL-E)
- URL của n8n instance (để cấu hình webhook)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang workflow gốc: [Transform Image to Lego Style Using Line and Dall-E](https://n8n.io/workflows/2738)
2. Nhấp vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow vào ô tương ứng
4. Nhấp vào nút "Import" để hoàn tất quá trình import

Hoặc các sếp cũng có thể copy/paste JSON workflow vào n8n Editor bằng cách:

1. Mở n8n Editor
2. Nhấp vào nút "Import from Clipboard"
3. Dán JSON workflow vào ô tương ứng
4. Nhấp vào nút "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Receive a Line Webhook** (webhook):
   - Cấu hình path: `/lineimage`
   - Chọn HTTP Method: `POST`

2. **Receive Line Messages** (httpRequest):
   - Không cần cấu hình gì thêm, node này sẽ tự động nhận tin nhắn từ Line

3. **Creating a Prompt for Dall-E (Lego Style)** (openAi):
   - Chọn credentials: `openAiApi`
   - Cấu hình operation: `analyze`
   - Cấu hình resource: `image`

4. **Creating an Image using Dall-E** (openAi):
   - Chọn credentials: `openAiApi`
   - Cấu hình resource: `image`
   - Cấu hình prompt: `={{ $json.content }}`

5. **Send Back an Image through Line** (httpRequest):
   - Không cần cấu hình gì thêm, node này sẽ tự động gửi hình ảnh về Line

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình xong các node, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Test run dữ liệu mẫu:
   - Gửi một tin nhắn chứa ảnh đến Line Bot
   - Kiểm tra xem workflow có hoạt động đúng không
   - Đảm bảo hình ảnh được chuyển đổi thành phong cách Lego và gửi lại đúng người dùng

2. Bật Active workflow:
   - Nhấp vào nút "Activate" ở góc trên bên phải của workflow
   - Đảm bảo workflow đang ở trạng thái "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với các dịch vụ khác như Slack hoặc Telegram để tạo ra một hệ thống tự động hóa hoàn chỉnh
- Có thể lưu log các hình ảnh đã được chuyển đổi để theo dõi và quản lý dễ dàng hơn
- Có thể gửi báo cáo định kỳ về số lượng hình ảnh đã được chuyển đổi và thời gian trung bình để xử lý

### 📌 Kết luận
Workflow "Transform Image to Lego Style Using Line and Dall-E" là một giải pháp tự động hóa hoàn hảo cho các sếp muốn chuyển đổi phong cách ảnh một cách nhanh chóng và chuyên nghiệp. Với workflow này, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao tính chuyên nghiệp của hình ảnh. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!