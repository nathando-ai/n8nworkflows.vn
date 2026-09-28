---
title: "🚀 Số hóa danh thiếp (Business Card) vào Notion tự động bằng Gemini Vision AI"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc ảnh danh thiếp bằng Google Gemini Vision OCR, chuẩn hóa dữ liệu JSON và lưu trữ vào Notion Database nhanh chóng."
slug: "so-hoa-danh-thiep-vao-notion-voi-gemini-vision"
tags: [n8n, automation, no-code, notion, ai, ocr, gemini]
keywords: [n8n workflow, scan danh thiếp, business card ocr, notion database, google gemini vision, tự động hóa nhập liệu]
---

# 🚀 Số hóa danh thiếp (Business Card) vào Notion tự động bằng Gemini Vision AI

Mỗi khi tham gia các sự kiện networking, hội thảo hay gặp gỡ đối tác, các sếp thường cầm về cả tập danh thiếp (business card). Việc ngồi gõ thủ công từng tên, số điện thoại, email, chức vụ vào Notion hay CRM vừa tẻ nhạt, mất thời gian lại dễ xảy ra sai sót.

Bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Chỉ cần vài giây tải ảnh danh thiếp lên form, **Google Gemini Vision AI** sẽ trích xuất toàn bộ thông tin chuẩn xác, sau đó tự động "bơm" thẳng vào **Notion Database** của các sếp mà không cần đụng tay gõ chữ nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh cặm cụi gõ tay từng chiếc danh thiếp sau mỗi chuyến đi gặp khách hàng.
- **AI thông minh vượt trội:** Google Gemini Vision nhận diện cực tốt các font chữ nghệ thuật, logo công ty và bố cục phức tạp trên danh thiếp.
- **Đồng bộ hóa tức thì:** Dữ liệu được cấu trúc sạch sẽ và lưu trữ ngay lập tức vào Notion Database (`Customer Business Cards`).
- **Hoạt động 24/7:** Giao diện Form gọn nhẹ, có thể truy cập và upload ảnh danh thiếp ngay trên điện thoại di động mọi lúc mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **Hệ thống n8n:** Đã cài đặt và sẵn sàng sử dụng.
2. **Google Gemini API Key:** Để kết nối với node AI phân tích hình ảnh.
3. **Notion Account & Database:** Chuẩn bị sẵn một Notion Database có các trường (properties) tương ứng như: Tên, Chức vụ, Số điện thoại, Email, Công ty, Địa chỉ, Website...
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của template (Workflow ID: `9180`) hoặc sử dụng file JSON tương ứng để import trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp cần cấu hình chuẩn xác các điểm sau:

- **On form submission (`formTrigger`):**
  - Node này đóng vai trò tạo một trang Web Form công khai để upload ảnh danh thiếp (`.jpg`, `.png`, `.jpeg`) kèm theo phân loại (nếu muốn).
  - Các sếp có thể chỉnh sửa tiêu đề form, thêm trường thông tin cho phù hợp với nhu cầu thực tế.

- **Analyze image (`googleGemini`):**
  - Kết nối với tài khoản bằng **Google Palm API / Gemini API Credentials**.
  - Node này sử dụng công nghệ Vision để quét hình ảnh danh thiếp vừa được upload từ Form, sau đó trích xuất toàn bộ thông tin thô dạng chữ (Tên, Chức vụ, Số điện thoại, Email, Công ty, Địa chỉ, Website...).

- **Parse to Json (`code`):**
  - Sử dụng đoạn mã Javascript nhỏ để làm sạch dữ liệu văn bản thô do AI trả về, chuyển đổi và ép kiểu thành định dạng JSON chuẩn chỉnh, sẵn sàng đẩy vào database. Dữ liệu mẫu sau khi parse sẽ có cấu trúc như sau:
    ```json
    {
      "Name": "Jin Park",
      "Position": "Head of Development",
      "Phone": "021231234",
      "Mobile": "0101231234",
      "Email": "abc@dc.com",
      "Company": "",
      "Address": "6F, Donga Building, 212, Yeoksam-ro, Gangnam-gu, Seoul",
      "Website": "www.tov.com"
    }
    ```

- **Create a database page (`notion`):**
  - Kết nối bằng **Notion API Credentials**.
  - Chọn đúng **Database** (`Customer Business Cards`) mà các sếp đã chuẩn bị sẵn trên Notion.
  - Map các trường dữ liệu từ output của node *Parse to Json* vào các cột tương ứng trong Notion Database (Name -> Name, Email -> Email, Phone -> Phone...).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách upload một bức ảnh danh thiếp mẫu lên form.
- Kiểm tra lại Notion Database xem dữ liệu đã được điền đầy đủ và chính xác chưa.
- Nếu mọi thứ mượt mà, các sếp chỉ cần gạt công tắc sang **Active** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống quản lý khách hàng (CRM mini trên Notion) thêm phần chuyên nghiệp, các sếp có thể mở rộng workflow này với các ý tưởng:
- **Tích hợp Telegram/Slack Bot:** Gửi thông báo kèm ảnh danh thiếp và tóm tắt thông tin vào nhóm chat nội bộ ngay khi có người upload form.
- **Tự động gửi email chào mừng:** Thêm node Gmail hoặc Resend để tự động gửi email giới thiệu dịch vụ/công ty của các sếp đến địa chỉ email vừa quét được trên danh thiếp.
- **Kiểm tra trùng lặp:** Thêm bước kiểm tra xem email hoặc số điện thoại đã tồn tại trong Notion Database chưa trước khi tạo trang mới để tránh việc lưu trùng lặp dữ liệu.

### 📌 Kết luận
Số hóa danh thiếp chưa bao giờ dễ dàng và thông minh đến thế nhờ sự kết hợp giữa n8n và Gemini Vision AI. Hãy cài đặt ngay workflow này để biến tệp danh thiếp giấy lộn xộn thành một cơ sở dữ liệu khách hàng số hóa chuyên nghiệp trên Notion ngay hôm nay các sếp nhé!