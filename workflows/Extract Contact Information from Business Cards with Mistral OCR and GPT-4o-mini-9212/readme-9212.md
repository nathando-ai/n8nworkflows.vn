---
title: "🚀 Tự động trích xuất thông tin danh thiếp (Business Card) với Mistral OCR và GPT-4o-mini trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét ảnh/PDF danh thiếp bằng Mistral OCR, trích xuất dữ liệu có cấu trúc bằng OpenAI GPT-4o-mini và lưu vào Data Table."
slug: "trich-xuat-thong-tin-danh-thiep-mistral-ocr-gpt-4o-mini-n8n"
tags: [n8n, automation, no-code, ai-agent, ocr, openai, mistral]
keywords: [n8n workflow, trích xuất danh thiếp, business card scanner, mistral ocr, gpt-4o-mini, n8n data table]
---

# 🚀 Tự động trích xuất thông tin danh thiếp (Business Card) với Mistral OCR và GPT-4o-mini

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi đi hội nghị, sự kiện về và ôm một đống danh thiếp (business card) giấy, phải ngồi cặm cụi gõ từng cái tên, số điện thoại, email vào danh danh bạ hoặc CRM không? Việc này vừa tốn thời gian, dễ sai sót lại cực kỳ chán ngắt.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực đỉnh giúp tự động hóa 100% quy trình này: Chỉ cần upload ảnh hoặc file PDF của danh thiếp lên một form web, AI sẽ tự động đọc hiểu, trích xuất thông tin chuẩn xác và lưu thẳng vào database. Không cần viết một dòng code nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Số hóa tức thì:** Biến ảnh chụp danh thiếp hoặc file PDF thành dữ liệu danh bạ có cấu trúc chỉ trong vài giây.
- **Độ chính xác cao:** Kết hợp sức mạnh đọc chữ siêu việt của Mistral OCR và khả năng hiểu ngữ cảnh thông minh của GPT-4o-mini.
- **Tự động lưu trữ:** Tự động cập nhật (upsert) vào n8n Data Table dựa theo email, tránh trùng lặp dữ liệu.
- **Tiện lợi mọi lúc mọi nơi:** Giao diện Form Trigger đơn giản, có thể truy cập từ điện thoại hoặc máy tính để upload danh thiếp ngay tại sự kiện.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Mistral AI API Key** (Dùng cho node *Mistral OCR API* qua HTTP Bearer Auth).
3. **OpenAI API Key** (Dùng cho node *OpenAI Chat Model* với model `gpt-4o-mini`).
4. **n8n Data Table** đã được tạo sẵn để lưu thông tin liên hệ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (từ nguồn cung cấp) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **On form submission (Form Trigger):** Node này tạo ra một trang web upload. Các sếp có thể cấu hình giao diện form để cho phép người dùng tải lên các định dạng ảnh (`jpg`, `png`) hoặc file `pdf` của danh thiếp.
- **Data to base64 & JSON Parser:** Các node này có nhiệm vụ xử lý tệp tin tải lên, chuyển đổi định dạng nhị phân (binary) sang Base64 để gửi qua API của Mistral.
- **Mistral OCR API (HTTP Request):** 
  - Cần tạo Credential loại **HTTP Bearer Auth** và điền Mistral API Key vào.
  - Endpoint sẽ gọi tới dịch vụ OCR của Mistral để bóc tách toàn bộ văn bản có trong ảnh/PDF danh thiếp.
- **AI Agent & OpenAI Chat Model:**
  - Chọn model **`gpt-4o-mini`** trong phần cấu hình của node *OpenAI Chat Model*. Điền OpenAI API Key vào credentials tương ứng.
  - AI Agent sẽ nhận kết quả text thô từ Mistral OCR, kết hợp với **Structured Output Parser** để lọc ra các trường dữ liệu chuẩn xác như: Tên, Công ty, Email, Số điện thoại, Chức vụ, Website...
- **Upsert row(s) (Data Table):** 
  - Tạo một n8n Data Table tên là `business_cards` với các trường dữ liệu tương ứng.
  - Tại node này, chọn thao tác `upsert` và cấu hình dùng trường `email` làm khóa chính (key criteria) để nếu danh thiếp của một người đã tồn tại, hệ thống sẽ tự cập nhật thay vì tạo bản ghi trùng lặp.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** và upload thử một tấm hình danh thiếp lên Form để kiểm tra kết quả trả về ở Data Table.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack để bắn một tin nhắn thông báo kèm thông tin người vừa quét mỗi khi có danh thiếp mới được upload lên.
- **Đồng bộ CRM:** Thay vì chỉ lưu vào n8n Data Table, các sếp có thể nối thêm node để đẩy thẳng dữ liệu vào HubSpot, Google Sheets, hay Salesforce.
- **Gửi email chào mừng tự động:** Gửi ngay một email giới thiệu dịch vụ/sản phẩm của công ty tới địa chỉ email vừa quét được từ danh thiếp.

### 📌 Kết luận
Việc số hóa danh thiếp chưa bao giờ dễ dàng và tự động hóa đến thế với sự kết hợp giữa Mistral OCR, OpenAI và n8n. Hãy thiết lập ngay hôm nay để giải phóng bản thân khỏi những tác vụ nhập liệu thủ công nhàm chán! Chúc các sếp thành công!