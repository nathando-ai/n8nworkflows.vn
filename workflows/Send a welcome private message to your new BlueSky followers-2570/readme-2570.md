---
title: "🚀 Tự Động Gửi Tin Nhắn Chào Mừng Riêng Tư Cho Người Theo Dõi Mới Trên BlueSky - Không Cần Code"
description: "Workflow tự động hóa gửi tin nhắn chào mừng cá nhân hóa đến người theo dõi mới trên BlueSky, tiết kiệm thời gian và tăng cường tương tác. Hoạt động 24/7 mà không cần can thiệp thủ công."
slug: "tieu-dong-gui-tin-nhan-chao-mung-blue-sky"
tags: [n8n, automation, marketing, blue-sky, no-code]
keywords: [tự động hóa blue sky, gửi tin nhắn blue sky, marketing tự động, n8n workflow blue sky, tự động hóa xã hội mạng]
---

# 🚀 **Tự Động Gửi Tin Nhắn Chào Mừng Riêng Tư Cho Người Theo Dõi Mới Trên BlueSky**

## **📌 Nỗi Đau Của Các Sếp?**
Bạn đã bao giờ phải **quét danh sách người theo dõi mới** trên BlueSky mỗi ngày, sau đó **gửi tin nhắn chào mừng một cách thủ công** cho từng người? Điều này không chỉ **tốn thời gian** mà còn **không hiệu quả** khi bạn phải nhớ gửi cho tất cả và đảm bảo tin nhắn cá nhân hóa.

Với **workflow này**, các sếp sẽ **tự động hóa toàn bộ quy trình** – từ **lấy danh sách người theo dõi mới** đến **gửi tin nhắn chào mừng riêng tư** – **một cách hoàn toàn tự động**, **không cần code** và **hoạt động 24/7**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** – Không phải quét danh sách người theo dõi thủ công hàng ngày.
✅ **Tương tác cá nhân hóa** – Gửi tin nhắn riêng tư với nội dung tự định nghĩa.
✅ **Hoạt động liên tục** – Workflow chạy tự động mỗi **60 phút**, không cần can thiệp.
✅ **Danh sách người theo dõi được cập nhật** – Luôn giữ danh sách mới nhất để tránh trùng lặp.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần:
✔ **Tài khoản BlueSky** (đăng nhập để lấy thông tin API).
✔ **App Password** (không phải mật khẩu chính) – **Cần quyền gửi tin nhắn riêng tư**.
✔ **Tên người dùng BlueSky** (để xác định tài khoản).
✔ **Danh sách người theo dõi hiện tại** (sẽ được lưu trong file JSON).
✔ **Nội dung tin nhắn chào mừng** (có thể chứa link, giới thiệu cá nhân).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2570](https://n8n.io/workflows/2570) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** để thêm workflow vào n8n của mình.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 Bước 1: Cấu Hình Tài Khoản BlueSky**
- **Node "Create Session"** (HTTP Request):
  - **Method:** `POST`
  - **URL:** `https://bsky.app/api/login`
  - **Headers:**
    ```json
    {
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "identifier": "your_bluesky_username",  // Thay bằng tên tài khoản BlueSky của bạn
      "password": "your_app_password"         // Thay bằng App Password
    }
    ```
  - **Lưu kết quả vào `JSON`** để sử dụng trong các node tiếp theo.

- **Node "List followers"** (HTTP Request):
  - **Method:** `GET`
  - **URL:** `https://bsky.app/api/user/{your_bluesky_username}/followers` (thay `{your_bluesky_username}` bằng tên tài khoản).
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer {{ $node["Create Session"].json["accessToken"] }}"
    }
    ```
  - **Lưu kết quả vào `JSON`** để xử lý tiếp.

#### **🔹 Bước 2: Xử Lý Danh Sách Người Theo Dõi**
- **Node "Convert to File"** (convertToFile):
  - **Operation:** `toJson`
  - **File Name:** `followers.json`
  - **Lưu danh sách người theo dõi hiện tại vào file**.

- **Node "Save followers to file"** (readWriteFile):
  - **Operation:** `write`
  - **File Path:** `followers.json`
  - **Content:** `{{ $node["Convert to File"].file }}`
  - **⚠️ LƯU Ý:** **Phải chạy node này 1 lần thủ công trước khi bật workflow** để lưu danh sách ban đầu.

#### **🔹 Bước 3: Xác Định Tin Nhắn Chào Mừng**
- **Node "Define welcome message"** (set):
  - **Set giá trị** cho `welcomeMessage` (ví dụ: `"Xin chào! Tôi là [Tên], rất vui khi bạn theo dõi tôi. Đừng quên ghé thăm [Link] của tôi! 🚀"`).

#### **🔹 Bước 4: Gửi Tin Nhắn Riêng Tư**
- **Node "Send message"** (HTTP Request):
  - **Method:** `POST`
  - **URL:** `https://bsky.app/api/post/create`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer {{ $node["Create Session"].json["accessToken"] }}"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "reply": {
        "parent": "{{ $node["Get conversation ID"].json["uri"] }}"
      },
      "text": "{{ $node["Define welcome message"].json["welcomeMessage"] }}"
    }
    ```
  - **Lưu ý:** Node **"Get conversation ID"** (HTTP Request) cần lấy **URI của cuộc trò chuyện** trước khi gửi tin nhắn.

#### **🔹 Bước 5: Lặp Lại Mỗi 60 Phút**
- **Node "Each 60 minutes"** (scheduleTrigger):
  - **Cài đặt:** `*/60 * * * *` (chạy mỗi 60 phút).
  - **Kích hoạt workflow tự động**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram** để thông báo khi có người theo dõi mới:
   - Thêm node **Slack/Telegram Webhook** sau node **"Find new followers"** để gửi thông báo.

2. **Lưu log hoạt động** để theo dõi:
   - Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại danh sách người đã gửi tin nhắn.

3. **Cá nhân hóa tin nhắn** bằng thông tin từ BlueSky:
   - Sử dụng **JavaScript Code Node** để lấy thông tin người theo dõi (ví dụ: tên, avatar) và thay thế vào tin nhắn.

4. **Bật chế độ debug** để kiểm tra lỗi:
   - Mở **Settings > Debug Mode** trong n8n để dễ dàng theo dõi flow.

---
## **📌 Kết Luận**
Với **workflow này**, các sếp đã **tự động hóa hoàn toàn quy trình tương tác với người theo dõi mới trên BlueSky**, **tiết kiệm thời gian** và **tăng cường tương tác** một cách chuyên nghiệp.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa marketing của mình!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**❓ Có thắc mắc? Hãy để lại comment bên dưới!** 👇