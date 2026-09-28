---
title: "🚀 Tự Động Gửi Tin Nhắn Chào Mừng Cho Người Theo Dõi Mới Trên Bluesky Với Baserow - Không Cần Code!"
description: "Workflow tự động hóa gửi tin nhắn cá nhân hóa cho người theo dõi mới trên Bluesky, tránh trùng lặp và tiết kiệm thời gian marketing 100%. Sử dụng Baserow để quản lý danh sách và n8n để thực thi 24/7."
slug: "tu-dong-gui-tin-nhan-chao-mung-bluesky-baserow"
tags: [n8n, automation, marketing, bluesky, baserow, no-code]
keywords: [tự động hóa bluesky, gửi tin nhắn tự động, baserow n8n, marketing tự động, workflow n8n marketing]
---

# 🚀 **Tự Động Gửi Tin Nhắn Chào Mừng Cho Người Theo Dõi Mới Trên Bluesky - Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp Marketing Trên Bluesky**
Các sếp đang mất thời gian quý báu để:
- **Theo dõi thủ công** những người mới theo dõi tài khoản Bluesky.
- **Gửi tin nhắn cá nhân hóa** cho từng người, dễ bị bỏ quên hoặc trùng lặp.
- **Quản lý danh sách** người đã nhận tin nhắn bằng Excel/Google Sheets, dễ bị lỗi hoặc mất dữ liệu.

**Workflow này giải quyết tất cả!** Sử dụng **n8n + Baserow**, bạn có thể:
✅ **Tự động phát hiện** người theo dõi mới mỗi ngày.
✅ **Gửi tin nhắn chào mừng cá nhân hóa** (không trùng lặp).
✅ **Quản lý trạng thái** (đã gửi/t尚未送) trên Baserow.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng ngày.
- **Tăng tương tác**: Tin nhắn cá nhân hóa giúp tăng tỷ lệ phản hồi từ người theo dõi mới.
- **Tránh trùng lặp**: Baserow theo dõi trạng thái đã gửi/t尚未送.
- **Dữ liệu sạch**: Quản lý toàn bộ trên cơ sở dữ liệu Baserow (không phụ thuộc vào Excel).
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày lúc 9h.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Bluesky** (API Key và Session Token).
2. **Tài khoản Baserow** (để lưu trữ danh sách người theo dõi và trạng thái).
3. **API Key của Baserow** (để kết nối với n8n).
4. **Tin nhắn mẫu** (có thể chỉnh sửa trong workflow).

---
:::info[CHUẨN BỊ]
- **Bluesky**:
  - API Key và Session Token (tạo từ [Bluesky Developer Portal](https://bsky.app/developers)).
  - Đảm bảo tài khoản có quyền gửi tin nhắn tự động.
- **Baserow**:
  - Tạo một **bảng dữ liệu** (table) với các cột:
    - `username` (định danh người theo dõi).
    - `sentWelcome` (boolean, mặc định `FALSE`).
  - API Key từ **Settings > API Keys** trong Baserow.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở [n8n Workflow Editor](https://n8n.io/).
2. Nhấp vào **"Import"** và chọn file JSON (hoặc paste JSON).
3. Chọn **"Create Workflow"** để bắt đầu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **21 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình Bluesky Credentials**
- **Node: "Set Bluesky Credentials" (type: set)**
  - Điền vào `json`:
    ```json
    {
      "apiKey": "YOUR_BLUESKY_API_KEY",
      "sessionToken": "YOUR_BLUESKY_SESSION_TOKEN"
    }
    ```
  - Lấy từ [Bluesky Developer Portal](https://bsky.app/developers).

##### **B. Kết Nối Baserow**
- **Node: "Create Follower Record" & "Get Follower Record" (type: baserow)**
  - **Database URL**: `https://your-baserow-instance.com/api/database/`
  - **Table Name**: Tên bảng dữ liệu bạn tạo (ví dụ: `followers`).
  - **API Key**: API Key từ Baserow.

##### **C. Chỉnh Sửa Tin Nhắn Chào Mừng**
- **Node: "Create Welcome Message" (type: code)**
  - Mở node này và chỉnh sửa mã JavaScript để thay đổi nội dung tin nhắn:
    ```javascript
    // Ví dụ: Tin nhắn chào mừng cá nhân hóa
    return `Hi ${
      json["firstName"] || "new follower"
    }! Thanks for following me on Bluesky. Here’s a little welcome message...`;
    ```
  - **Lưu ý**: Node `"Get Firstname"` (type: code) cũng cần chỉnh sửa để trích xuất tên từ Bluesky (nếu có).

##### **D. Thiết Lập Lịch Triggers**
- **Node: "Run Daily at 9 AM" (type: scheduleTrigger)**
  - Đảm bảo **timezone** được đặt đúng (ví dụ: `Asia/Ho_Chi_Minh`).
  - Thời gian mặc định là **9h sáng hàng ngày**.

##### **E. Kiểm Tra Node "If Follower Exists"**
- Node này **lọc bỏ** người đã gửi tin nhắn trước đó (trạng thái `sentWelcome = TRUE`).
- Nếu không hoạt động, kiểm tra cột `sentWelcome` trong Baserow.

##### **F. Test Run Trước Khi Bật Active**
- **Nhấp vào "Run Workflow"** với dữ liệu mẫu để kiểm tra:
  - Tin nhắn có được gửi không?
  - Baserow có cập nhật trạng thái `sentWelcome = TRUE` không?
  - Không có lỗi API nào xuất hiện.

---

#### **3. Kích Hoạt ⚡️**
Sau khi kiểm tra:
1. **Nhấp vào "Active"** để bật workflow.
2. **Monitor logs** trong n8n để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
   - Ví dụ: `"Workflow completed! Sent welcome messages to ${
     $json["newFollowers"].length
   } new followers."`

2. **Lưu Log Tất Cả Các Tin Nhắn**
   - Thêm node **Google Sheets** hoặc **Baserow** để lưu toàn bộ lịch sử tin nhắn (ngày gửi, người nhận, nội dung).

3. **Tự Động Xóa Người Theo Dõi Trùng Lặp**
   - Sử dụng node **Code** để kiểm tra và xóa người theo dõi trùng lặp trong Baserow.

4. **Chỉnh Sửa Tin Nhắn Theo Thời Gian**
   - Ví dụ: Gửi tin nhắn khác nhau cho người theo dõi vào buổi sáng vs buổi tối.

5. **Kết Nối Với CRM (HubSpot, Notion...)**
   - Sử dụng node **HTTP Request** để gửi dữ liệu người theo dõi mới vào HubSpot/Notion.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào nội dung chất lượng hơn, trong khi **tự động hóa toàn bộ quy trình chào mừng người theo dõi mới trên Bluesky**. Với **Baserow**, bạn có thể quản lý danh sách một cách chuyên nghiệp, và **n8n** đảm bảo workflow chạy 24/7 **không cần code**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Bật Active** và để nó làm việc cho bạn.
3. **Monitor logs** để đảm bảo hoạt động ổn định.

**🚀 Cùng tự động hóa marketing của mình ngay hôm nay!** 🚀