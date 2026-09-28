---
title: "🚀 Tự Động Hóa Lên Lịch Facebook Từ Google Sheets Với Xác Nhận & Ảnh Từ Google Drive"
description: "Workflow tự động hóa lên lịch bài viết Facebook từ Google Sheets với hệ thống xác nhận tự động, tải ảnh từ Google Drive, và cập nhật URL bài viết đã đăng. Giúp quản lý nội dung Facebook hiệu quả hơn 100% không cần code."
slug: "tu-dong-hoa-len-lich-facebook-tu-google-sheets"
tags: [n8n, automation, social-media, google-sheets, facebook-graph-api]
keywords: [n8n workflow facebook, tự động hóa lên lịch bài viết, google sheets facebook, tự động hóa social media, công cụ lên lịch facebook]
---

# 🚀 **Tự Động Hóa Lên Lịch Facebook Từ Google Sheets Với Xác Nhận & Ảnh Từ Google Drive**

## **🔥 Bạn đã bao giờ phải làm thủ công việc này?**
- **Lên lịch bài viết Facebook hàng ngày** nhưng phải nhớ check lại Google Sheets để xác nhận bài viết đã được duyệt?
- **Tải ảnh từ Google Drive** và gắn vào bài viết trước khi đăng?
- **Cập nhật URL bài viết đã đăng** vào bảng Google Sheets để theo dõi hiệu quả?
- **Lo lắng bài viết có thể bị lỡ lịch** vì quên hoặc không tự động hóa?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lên lịch bài viết Facebook** từ Google Sheets vào 4 thời điểm khác nhau trong ngày.
✅ **Xác nhận tự động** chỉ bài viết có trạng thái **"Good"** (đã được duyệt).
✅ **Tải ảnh từ Google Drive** và gắn vào bài viết.
✅ **Cập nhật URL bài viết đã đăng** vào bảng Google Sheets.
✅ **Phân loại bài viết** (text-only hoặc photo post) và xử lý riêng biệt.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải lên lịch bài viết thủ công hàng ngày.
- **Chính xác 100%**: Bài viết chỉ được đăng khi đã được duyệt (Approval Status = "Good").
- **Tự động tải ảnh**: Ảnh được tải từ Google Drive tự động, không cần copy-paste.
- **Theo dõi hiệu quả**: URL bài viết đã đăng được cập nhật tự động vào Google Sheets.
- **Hoạt động liên tục**: Workflow chạy 4 lần/ngày (9:35, 10:35, 11:35, 12:35) mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với bảng dữ liệu có các cột sau:
   - `Scheduled On` (ngày lên lịch)
   - `Platform` (phải là "Facebook")
   - `Post Type` (text-only hoặc photo)
   - `Caption` (nội dung bài viết)
   - `Media URL` (đường dẫn ảnh trong Google Drive)
   - `Approval Status` (phải là "Good" để được đăng)
   - `Post URL` (sẽ được cập nhật sau khi đăng)

2. **Tài khoản Google Drive** để lưu trữ ảnh bài viết.

3. **Facebook Page ID và Page Access Token** (để kết nối với Graph API).

4. **Credentials OAuth2** cho:
   - Google Sheets
   - Google Drive

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/13301](https://n8n.io/workflows/13301) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13301) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Schedule Trigger**
- Workflow sẽ chạy **4 lần/ngày** vào các thời gian:
  - 9:35 AM, 10:35 AM, 11:35 AM, 12:35 PM.
- **Không cần chỉnh gì** nếu muốn giữ nguyên lịch trình.

##### **B. Cấu hình Google Sheets**
1. **Node "Load Facebook Credentials from Sheet"**:
   - Chọn **Sheet** chứa Facebook Page ID và Access Token (cột phải được đặt tên là `Facebook Page ID` và `Facebook Access Token`).
   - **Lưu ý**: Sheet này phải có **OAuth2 credentials** đã cấu hình trong n8n.

2. **Node "Read Approved Facebook Posts"**:
   - Chọn **Sheet chính** chứa danh sách bài viết.
   - **Range**: Chọn toàn bộ dữ liệu (ví dụ: `Sheet1!A1:Z1000`).

3. **Node "Update Sheet with Photo/Text Post URL"**:
   - Chọn **Sheet chính** cùng với cột `Post URL` để cập nhật sau khi đăng.

##### **C. Cấu hình Google Drive**
- **Node "Download Image from Google Drive"**:
  - Chọn **File ID** từ cột `Media URL` trong Google Sheets.
  - **Lưu ý**: File ID phải là đường dẫn đầy đủ từ Google Drive (ví dụ: `https://drive.google.com/file/d/1AbCdEfGhIjKlMnOp/view?usp=sharing` → **1AbCdEfGhIjKlMnOp**).

##### **D. Cấu hình Facebook Graph API**
- **Node "Schedule Facebook Photo Post" và "Schedule Facebook Text Post"**:
  - **URL**: `https://graph.facebook.com/v19.0/{Facebook Page ID}/feed` (cho text post) hoặc `https://graph.facebook.com/v19.0/{Facebook Page ID}/photos` (cho photo post).
  - **Headers**:
    - `Authorization: Bearer {Facebook Access Token}`
    - `Content-Type: application/json`
  - **Body (JSON)**:
    ```json
    {
      "message": "$$.json["Caption"]",
      "picture": "$$.json["Media URL"]", // Chỉ cần cho photo post
      "published": true
    }
    ```

##### **E. Cấu hình Node "Check if Platform is Facebook"**
- **Condition**: `$$.json["Platform"] === "Facebook"` (đảm bảo chỉ bài viết Facebook được xử lý).

##### **F. Cấu hình Node "Check if Not Story Post"**
- **Condition**: `$$.json["Post Type"] !== "Story"` (bỏ qua bài viết Story, vì không hỗ trợ tự động hóa).

##### **G. Cấu hình Node "Check if Text-Only or Photo Post"**
- **Text Post**: `$$.json["Post Type"] === "Text"`
- **Photo Post**: `$$.json["Post Type"] === "Photo"`

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Thêm một bài viết mẫu vào Google Sheets với `Approval Status = "Good"` và `Scheduled On = Today`.
   - Chạy **Manual Trigger** để kiểm tra workflow hoạt động như thế nào.

2. **Bật Active workflow**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi bài viết đã đăng thành công.

2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử bài viết đã đăng.

3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow riêng để tổng hợp số lượng bài viết đã đăng trong ngày và gửi báo cáo qua email.

4. **Hỗ trợ nhiều nền tảng**:
   - Mở rộng workflow để hỗ trợ **Instagram, LinkedIn** bằng cách thêm điều kiện `Platform` mới.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý nội dung Facebook, đồng thời **tăng độ chính xác** và **tự động hóa hoàn toàn** quy trình lên lịch bài viết. **Không cần code, không cần lo lắng lỡ lịch** – chỉ cần **import, cấu hình và bật chạy**!

**🚀 Hãy áp dụng ngay và tự động hóa quản lý Facebook của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/13301)**