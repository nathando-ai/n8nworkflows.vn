---
title: "🎨 Tự Động Thêm Logo/Nước Màu Cho Ảnh qua Telegram + ImageKit.io (Không Cần Code)"
description: "Workflow tự động hóa chèn logo hoặc watermark vào ảnh từ Telegram, tiết kiệm thời gian cho các sếp marketing và content creator. Hoạt động 24/7, kết quả chính xác, không cần viết code."
slug: "tu-dong-them-logo-cho-anh-qua-telegram-imagekit"
tags: [n8n, automation, content-creation, multimodal-ai, image-processing, telegram-bot]
keywords: [tự động hóa logo ảnh, watermark ảnh tự động, n8n workflow imagekit, chèn logo qua telegram, tự động hóa content creator]
---

# 🎨 **Tự Động Thêm Logo/Nước Màu Cho Ảnh qua Telegram + ImageKit.io**

### **Giải pháp hoàn hảo cho các sếp marketing & content creator**
Hết sức phiền phức phải chèn logo/nước màu vào từng ảnh thủ công, phải không? Hay phải mất thời gian tải ảnh lên máy tính, chỉnh sửa, sau đó mới gửi lại cho khách hàng? **Workflow này tự động hóa toàn bộ quá trình chỉ với một tin nhắn Telegram!** Khi bạn gửi ảnh lên chat Telegram, hệ thống sẽ tự động:
✅ **Kiểm tra** xem ảnh có phải là file ảnh không?
✅ **Tải ảnh** từ Telegram về máy chủ
✅ **Chèn logo/nước màu** bằng API ImageKit.io
✅ **Gửi ảnh đã chỉnh sửa** về Telegram ngay lập tức

Không cần viết một dòng code nào, chỉ cần **cài đặt workflow này và bật chế độ tự động** là xong!

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần chỉnh sửa từng ảnh thủ công (giảm 90% thời gian).
- **Chính xác 100%**: Logo/nước màu được chèn theo kích thước và vị trí chính xác.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp của con người.
- **Tích hợp hoàn hảo**: Hoạt động với Telegram, không cần ứng dụng bên thứ ba.
- **Dễ dàng mở rộng**: Có thể kết hợp với Slack, Email hoặc lưu ảnh vào Google Drive.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **Token API** của bot Telegram (để kích hoạt trigger).
2. **Tài khoản ImageKit.io** và **API Key** (để chèn logo/nước màu).
3. **Logo/nước màu** (file ảnh PNG hoặc JPG) để chèn vào ảnh.
4. **URL của ảnh mẫu** (để test workflow).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/11229) hoặc copy toàn bộ JSON từ link trên.
- **Bước 2**: Mở **n8n Editor** trên máy chủ của bạn (Self-hosted).
- **Bước 3**: Nhấn **"Import"** và dán JSON vào hoặc tải file JSON đã tải xuống.
- **Bước 4**: Workflow sẽ xuất hiện với 8 node như trong danh sách dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **8 node chính**, các sếp cần **cấu hình cẩn thận** các node sau:

##### **🔹 Node 1: Telegram Trigger1 (n8n-nodes-base.telegramTrigger)**
- **Cấu hình**:
  - **Bot Token**: Điền **Token API** của bot Telegram (một chuỗi dài bắt đầu bằng `1xxxxxx:`).
  - **Chat ID**: Điền **Chat ID** của chat Telegram bạn muốn kích hoạt workflow (có thể tìm bằng cách gửi `/get_id` cho bot).
  - **Command**: Để trống (workflow sẽ hoạt động với **tất cả tin nhắn ảnh**).

##### **🔹 Node 2: Check if Photo1 (n8n-nodes-base.if)**
- **Cấu hình**:
  - **Condition**: Chọn **"File Type"** và **"is"** với giá trị **"image"**.
  - **Nếu không phải ảnh**: Workflow sẽ gửi tin nhắn lỗi qua Telegram (node **Send Error Message1**).

##### **🔹 Node 3: Get File Path (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://api.telegram.org/bot<BOT_TOKEN>/getFile?file_id=<FILE_ID>`
    *(Thay `<BOT_TOKEN>` và `<FILE_ID>` bằng giá trị từ node Telegram Trigger)*
  - **Response Format**: Chọn **"JSON"**.

##### **🔹 Node 4: Download Image (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://api.telegram.org/file/bot<BOT_TOKEN>/<FILE_PATH>`
    *(Lấy `<FILE_PATH>` từ node **Get File Path**)*
  - **Response Format**: Chọn **"Binary"** (để tải ảnh về dưới dạng file).

##### **🔹 Node 5: Add Logo1 (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.imagekit.io/v1/images/upload/url`
  - **Headers**:
    ```
    {
      "Authorization": "Private <IMAGEKIT_API_KEY>",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "url": "<DOWNLOADED_IMAGE_URL>",
      "file": "<BASE64_ENCODED_LOGO>",
      "overlay": {
        "width": 100,
        "height": 100,
        "position": "bottom-right",
        "opacity": 0.7
      }
    }
    ```
    *(Thay `<DOWNLOADED_IMAGE_URL>` và `<BASE64_ENCODED_LOGO>` bằng giá trị từ node trước)*
  - **Lưu ý**:
    - **Logo/nước màu** phải được **encode thành Base64** trước khi gửi.
    - Cấu hình **kích thước, vị trí và độ trong suốt** của logo theo ý muốn.

##### **🔹 Node 6: Send Watermarked Photo (n8n-nodes-base.telegram)**
- **Cấu hình**:
  - **Chat ID**: Điền lại **Chat ID** của chat Telegram.
  - **Message**: Chọn **"Photo"** và điền **URL của ảnh đã watermark** từ node **Add Logo1**.

##### **🔹 Node 7: Send Error Message1 (n8n-nodes-base.telegram)**
- **Cấu hình**:
  - **Chat ID**: Điền **Chat ID** của chat Telegram.
  - **Message**: `"Đây không phải là ảnh! Vui lòng gửi lại."`

---

#### **3. Kích hoạt ⚡️**
- **Bước 1**: **Test Run** với một ảnh mẫu (ví dụ: gửi ảnh lên chat Telegram).
- **Bước 2**: Kiểm tra **log** trong n8n Editor để xác nhận workflow hoạt động.
- **Bước 3**: Nhấn **"Active"** để bật workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Lưu ảnh đã watermark vào Google Drive/OneDrive**:
   - Thêm node **Google Drive** hoặc **OneDrive** sau node **Add Logo1** để lưu ảnh vào cloud.
2. **Gửi báo cáo định kỳ**:
   - Thêm node **Email** hoặc **Slack** để báo cáo số lượng ảnh đã xử lý mỗi ngày.
3. **Tích hợp với Slack**:
   - Thay vì Telegram, bạn có thể sử dụng **Slack Trigger** và **Slack Bot** để tương tác.
4. **Sử dụng AI để tự động chọn logo**:
   - Nếu logo khác nhau tùy theo khách hàng, bạn có thể thêm node **LLM** (như **n8n-nodes-base.llm**) để phân loại và chọn logo phù hợp.
5. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** (n8n-nodes-base.stickyNote) để ghi lại lịch sử hoạt động của workflow.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing và content creator, giúp họ **tự động hóa quá trình chèn logo/nước màu chỉ với một tin nhắn Telegram**. Không cần viết code, không cần kiến thức kỹ thuật cao, chỉ cần **cài đặt và bật hoạt động** là xong!

**Hãy thử ngay và tiết kiệm thời gian cho công việc hàng ngày!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::