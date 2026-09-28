---
title: "🚀 Tự động trích xuất thông tin từ Logo Sheet bằng AI Vision và Airtable trong n8n"
description: "Hướng dẫn xây dựng workflow n8n sử dụng AI Vision (GPT-4o) để phân tích hình ảnh logo sheet, tự động trích xuất danh sách sản phẩm, thuộc tính và đồng bộ dữ liệu thông minh lên Airtable."
slug: "trich-xuat-thong-tin-logo-sheet-ai-airtable"
tags: [n8n, automation, ai-vision, airtable, openai]
keywords: [n8n workflow, ai vision n8n, trich xuat logo sheet, airtable automation, openai gpt-4o]
keywords: [n8n workflow, ai vision n8n, trich xuat logo sheet, airtable automation, openai gpt-4o]
---

# 🚀 Tự động trích xuất thông tin từ Logo Sheet bằng AI Vision và Airtable

Các sếp có bao giờ gặp khó khăn khi phải thủ công phân tích các hình ảnh chứa hàng loạt logo sản phẩm, bảng so sánh tính năng (Logo Sheet) rồi nhập liệu rệu rã vào cơ sở dữ liệu chưa? Công việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót khi nhập tên, thuộc tính hay liên kết dữ liệu quan trọng.

Giải pháp ở đây là gì? Workflow n8n siêu việt này sẽ thay các sếp làm toàn bộ công việc nặng nhọc đó! Chỉ với một thao tác upload ảnh đơn giản qua Web Form, AI Vision sẽ "nhai" bức ảnh, bóc tách toàn bộ thông tin sản phẩm, thuộc tính, mối quan hệ và tự động cập nhật gọn gàng vào Airtable mà không cần viết một dòng code thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh ngồi nhìn ảnh rồi gõ tay từng tên sản phẩm, công ty hay thuộc tính vào bảng.
- **AI Vision thông minh:** Tự động đọc hiểu ngữ cảnh từ hình ảnh, phân loại sản phẩm (Tools) và các đặc tính đi kèm (Attributes) cực kỳ chính xác.
- **Đồng bộ tự động hóa thông minh:** Tự động kiểm tra trùng lặp, tạo mới hoặc cập nhật (Upsert) dữ liệu vào Airtable kèm theo các liên kết (Relations) hoàn chỉnh.
- **Hoạt động không giới hạn:** Nhận dữ liệu đầu vào qua Form trực quan, sẵn sàng xử lý mọi lúc mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain và AI nodes).
- **OpenAI Account & API Key:** Sử dụng model `gpt-4o` có khả năng đọc hiểu hình ảnh (Vision).
- **Airtable Account:** Tài khoản Airtable để lưu trữ cấu trúc bảng dữ liệu (Tools & Attributes).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (ID: 2650) hoặc copy toàn bộ mã JSON của workflow, sau đó dán trực tiếp vào n8n Editor của các sếp bằng cách chọn **New workflow** -> Dán (`Ctrl + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:

- **Node `On form submission` (Form Trigger):** Nơi nhận file ảnh Logo Sheet do người dùng upload lên. Các sếp có thể tuỳ chỉnh giao diện form theo ý thích.
- **Node `gpt-4o` & `Retrieve and Parser Agent`:** 
  - Chọn Credentials của OpenAI.
  - Kiểm tra và tinh chỉnh lại **Prompt** của Agent nếu danh mục sản phẩm hoặc đặc thù logo sheet của các sếp có cấu trúc riêng biệt.
- **Các node Airtable (`Check if Attribute exists`, `Create if not Exist`, `It Should exists`, `Save all this juicy data`, `Get Schema`):**
  - Cần tạo các bảng (Tables) trên Airtable theo đúng cấu trúc mẫu (xem phần cấu trúc bên dưới).
  - Kết nối Airtable API Token cho tất cả các node Airtable này.

**Cấu trúc bảng Airtable mẫu:**
* **Bảng `Tools` (Required Fields):**
  - `Name` (singleLineText)
  - `Attributes` (multipleRecordLinks = Link tới bảng Attributes)
  - `Hash` (singleLineText - tạo mã định danh độc nhất bằng MD5)
  - `Similar` (multipleRecordLinks = Link chính bảng Tools để gộp nhóm tương tự)
  - _Các trường tùy chọn khác:_ `Description` (multilineText), `Website` (url), `Category` (multipleSelects).
* **Bảng `Attributes` (Required Fields):**
  - `Name` (singleLineText)
  - `Tools` (multipleRecordLinks = Link tới bảng Tools)

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử upload một hình ảnh Logo Sheet mẫu để test luồng dữ liệu.
- Sau khi kiểm tra dữ liệu trên Airtable đã khớp, bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy mỗi khi có một Logo Sheet mới được phân tích và lưu thành công.
- **Xử lý hàng loạt (Batch Processing):** Nếu các sếp thường xuyên phải xử lý hàng chục ảnh cùng lúc, hãy tối ưu hóa node `Split In Batches` để tránh bị giới hạn Rate Limit từ OpenAI API.
- **Multi-Agent Validation:** Đối với các tài liệu cực kỳ quan trọng đòi hỏi độ chính xác 100%, có thể bổ sung thêm một Agent bước sau để đóng vai trò "Kiểm toán viên" đối chiếu lại kết quả trích xuất.

### 📌 Kết luận
Việc tự động hóa trích xuất dữ liệu từ hình ảnh chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n, AI Vision và Airtable. Hãy áp dụng ngay workflow này để giải phóng sức lao động thủ công và tối ưu hóa hệ thống dữ liệu của doanh nghiệp các sếp ngay hôm nay!