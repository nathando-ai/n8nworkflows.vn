---
title: "🚀 Tự động hóa xử lý Lead từ Hostinger Form bằng OpenAI, Beehiiv & Google Sheets trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt lead từ Hostinger Form qua Gmail, phân loại thông tin bằng OpenAI, lưu trữ vào Google Sheets và đồng bộ subscriber sang Beehiiv."
slug: "tu-dong-hoa-xu-ly-lead-hostinger-form-openai-beehiiv-google-sheets"
tags: [n8n, automation, no-code, openai, googlesheets, beehiiv]
keywords: [n8n workflow, hostinger form lead capture, openai extract lead, beehiiv integration, google sheets automation]
---

# 🚀 Tự động hóa xử lý Lead từ Hostinger Form bằng OpenAI, Beehiiv & Google Sheets

Các sếp có đang gặp tình trạng xây dựng website trên Hostinger và sử dụng form liên hệ, nhưng lại cực kỳ đau đầu vì **Hostinger không lưu trữ dữ liệu form trực tiếp**? Mỗi khi khách hàng điền form, thông tin chỉ được gửi qua email. Việc copy thủ công từng email, đánh giá tiềm năng (qualify), đưa vào Google Sheets và thủ công thêm vào danh sách nhận bản tin (newsletter) tốn quá nhiều thời gian và dễ bỏ sót khách hàng.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-code automation) với n8n sẽ giúp các sếp giải quyết triệt để vấn đề này!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt lead tức thì:** Tự động phát hiện email thông báo từ Hostinger Form ngay khi khách hàng vừa bấm gửi.
- **AI thông minh hóa:** Sử dụng OpenAI để trích xuất dữ liệu thô từ email thành các trường dữ liệu JSON chuẩn hóa và tự động đánh giá độ tiềm năng của lead.
- **Đồng bộ đa nền tảng:** Tự động thêm lead mới vào Google Sheets để sales theo dõi và đồng thời đăng ký subscriber vào Beehiiv newsletter (nhớ ghi rõ trong Điều khoản & Điều kiện của website nhé).
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh copy-paste dữ liệu hay sợ quên chăm sóc khách hàng tiềm năng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- Tài khoản Gmail (nơi nhận thông báo form từ Hostinger).
- Tài khoản OpenAI (để lấy API Key sử dụng mô hình AI trích xuất dữ liệu).
- Tài khoản Beehiiv (để đồng bộ subscriber).
- Google Drive / Google Sheets (tạo sẵn một bảng tính để lưu thông tin lead).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình (hoặc import file JSON tải về từ trang chủ n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **New form trigger (`gmailTrigger`):** 
  - Kết nối tài khoản Gmail của các sếp qua `gmailOAuth2`.
  - Cấu hình điều kiện lọc (ví dụ: `from:no-reply@hostinger.com` hoặc tiêu đề email chứa nội dung form) để n8n chỉ bắt đúng email thông báo từ Hostinger Form.
- **Extract & Qualify (`openAi`):**
  - Kết nối `openAiApi` credentials.
  - Viết Prompt hướng dẫn OpenAI đọc nội dung email thô, trích xuất các thông tin quan trọng (Tên, Email, Số điện thoại, Nội dung tin nhắn) và đánh giá độ tiềm năng (Qualified/Unqualified) trả về dưới dạng JSON sạch.
- **insert in Sheets (`googleSheets`):**
  - Kết nối `googleSheetsOAuth2Api`.
  - Chọn file Google Sheets và Sheet Name đã chuẩn bị sẵn. Map các trường dữ liệu mà OpenAI vừa trích xuất vào các cột tương ứng trên Sheet (Operation: `append`).
- **List Beehiiv publications & Add Beehiiv subscriber (`httpRequest`):**
  - Kết nối `httpHeaderAuth` bằng Beehiiv API Key.
  - Node `List Beehiiv publications` giúp lấy ID publication của các sếp, sau đó truyền vào node `Add Beehiiv subscriber` để tự động thêm email khách hàng vào danh sách nhận tin.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một test form trên website Hostinger để kiểm tra xem dữ liệu có chảy mượt mà qua các node không.
- Nếu mọi thứ chạy xanh mướt, hãy bật nút **Active** để hệ thống tự động làm việc 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Telegram/Slack:** Gắn thêm một node Telegram hoặc Slack ngay sau khi insert vào Google Sheets để bắn thông báo "🔥 Có Lead mới!" về điện thoại cho đội ngũ Sales ngay lập tức.
- **Xử lý Lead chất lượng cao:** Nếu OpenAI đánh giá lead là "Hot Lead", có thể cấu hình thêm bước tự động gửi email chào mừng cá nhân hóa ngay lập tức.
- **Lưu log lỗi:** Thiết lập Error Trigger để nếu có lỗi API từ OpenAI hay Beehiiv, hệ thống sẽ gửi cảnh báo về nhóm kỹ thuật.

### 📌 Kết luận
Hostinger Form có thể thiếu tính năng lưu trữ native, nhưng với n8n, OpenAI và chút khéo léo trong tự động hóa, các sếp đã có ngay một hệ thống quản lý lead chuyên nghiệp không thua kém các CRM đắt đỏ. Chúc các sếp cấu hình thành công và chốt thật nhiều đơn hàng!