---
title: "🚀 Tự Động Hóa Quá Trình Xử Lý Email Từ Notion → Gmail, Slack & Jira (Không Cần Code)"
description: "Workflow này tự động hóa việc xử lý email từ Notion sang Gmail (trả lời/forward), Slack (đại lý), và Jira (đặt ticket), đồng thời cập nhật trạng thái tự động. Giúp tiết kiệm 8+ giờ/tuần cho các sếp quản lý ticket và email."
slug: "tieu-dong-hoa-email-notion-gmail-slack-jira"
tags: [n8n, automation, ticket-management, notion, gmail, slack, jira, no-code]
keywords: [n8n workflow email, tự động hóa email từ notion, xử lý ticket tự động, quản lý email không code, tự động hóa slack jira]
---

# 🚀 **Tự Động Hóa Xử Lý Email Từ Notion Sang Gmail, Slack & Jira (Không Cần Code)**

### **🔥 Nỗi Đau Của Các Sếp Quản Lý Ticket & Email**
Các sếp thường phải:
- **Lặp đi lặp lại** việc kiểm tra email, cập nhật trạng thái trên Notion, và chuyển tiếp thông tin sang Slack/Jira.
- **Mất thời gian** để tra cứu email cũ, viết lại nội dung trả lời, hoặc tạo ticket mới.
- **Rủi ro sai sót** khi cập nhật trạng thái thủ công (ví dụ: quên cập nhật Notion sau khi trả lời email).
- **Không theo dõi được tiến trình** của các ticket sau khi chuyển giao cho đồng nghiệp.

**Workflow này giải quyết tất cả đó!** Nó tự động:
✅ **Trả lời email** từ Gmail dựa trên trạng thái trong Notion.
✅ **Chuyển tiếp email** sang Slack (đại lý) hoặc Jira (ticket).
✅ **Cập nhật trạng thái** trong Notion một cách tự động.
✅ **Áp dụng nhãn/label** cho email đã xử lý.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/tuần** (không phải kiểm tra email thủ công).
- **Trả lời email nhanh chóng** với nội dung chuẩn hóa từ Notion.
- **Chuyển giao ticket an toàn** sang Slack/Jira mà không lo quên cập nhật.
- **Theo dõi được tiến trình** toàn bộ qua Notion (trạng thái "Processed" + timestamp).
- **Giảm sai sót** do tự động hóa cập nhật trạng thái.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Notion** với cơ sở dữ liệu "Email Intelligence" (cấu trúc phải có trường `Status` và `Email`).
2. **Tài khoản Gmail** (đã kích hoạt API và tạo `OAuth 2.0 Client ID`).
3. **Tài khoản Slack** (đã tạo `Slack App` và cấp quyền `chat:write`).
4. **Tài khoản Jira** (nếu muốn tạo ticket, cần `API Token` và `Email Address`).
5. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14120](https://n8n.io/workflows/14120) hoặc copy toàn bộ JSON từ canvas.
- **Mở n8n Editor** → Nhấn `Import` → Dán JSON hoặc tải file `.json`.
- **Kiểm tra cấu trúc** trước khi kích hoạt:
  ```json
  {
    "nodes": [
      {"id": "1", "name": "Poll Email Intelligence", "type": "notion"},
      {"id": "2", "name": "Extract Email Data", "type": "code"},
      ...
    ],
    "connections": {...}
  }
  ```

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow có **4 trạng thái chính** được xử lý bởi `Switch by Status` và `Switch by Route Destination`. Các sếp cần cấu hình **cẩn thận** các node sau:

#### **A. Cấu Hình Notion (Cơ Sở Dữ Liệu "Email Intelligence")**
- **Trường bắt buộc**:
  - `Status` (giá trị: `Responded`, `Delegated`, `Routed`, `Archived`).
  - `Email` (địa chỉ email cần xử lý).
  - `Subject` (tiêu đề email).
  - `Body` (nội dung email).
- **Lưu ý**:
  - Nếu cơ sở dữ liệu có tên khác, **cập nhật `resource` trong node Notion** (ví dụ: `"databasePage"` → `"your-database-name"`).
  - **Không có trường `Processed`?** Thêm trường mới trong Notion để lưu timestamp.

#### **B. Cấu Hình Gmail**
1. **Tạo OAuth 2.0 Client ID**:
   - Mở [Google Cloud Console](https://console.cloud.google.com/).
   - Tạo **OAuth Client ID** với loại `Web Application`.
   - **Authorized JavaScript Origins**: `http://localhost:5678` (n8n self-hosted).
   - **Authorized Redirect URIs**: `http://localhost:5678/connect/generic/oauth/callback/gmail`.
   - **Copy `Client ID` và `Client Secret`** để thêm vào n8n (Settings → Credentials → Gmail).

2. **Node `Gmail Send Reply`**:
   - **Chọn `OAuth 2.0`** trong Credentials.
   - **Điền template trả lời** trong `Code` node (`Extract Email Data`):
     ```javascript
     // Ví dụ: Trả lời email khi trạng thái = "Responded"
     const replyBody = `Xin chào,\n\nTôi đã xử lý yêu cầu của bạn.\n\nTrạng thái: ${status}\n\nCảm ơn!`;
     return { reply: replyBody };
     ```

#### **C. Cấu Hình Slack**
1. **Tạo Slack App**:
   - Mở [Slack API](https://api.slack.com/apps).
   - Tạo `New App` → Chọn workspace.
   - Cấp quyền:
     - `chat:write` (để gửi DM).
     - `users:read` (đọc thông tin người dùng).
   - **Copy `Signing Secret` và `Bot Token`** để thêm vào n8n (Settings → Credentials → Slack).

2. **Node `Slack DM Delegate`**:
   - **Chọn `Bot Token`** trong Credentials.
   - **Điền ID người dùng** (đại lý) trong `user_id` (tìm bằng `/users.list` trong Slack).

#### **D. Cấu Hình Jira (Nếu Có)**
- **Tạo API Token**:
  - Mở [Jira Settings](https://your-jira.atlassian.net/secure/Dashboard.jspa) → **User Settings** → **API Tokens**.
  - **Copy token** và thêm vào n8n (Settings → Credentials → Jira).
- **Node `Create in Signal Stream`**:
  - **Cấu hình URL API** của Jira (ví dụ: `https://your-jira.atlassian.net/rest/api/2/issue`).
  - **Điền trường ticket** (ví dụ: `summary`, `description`, `project`).

#### **E. Cấu Hình Switch Cases**
- **Node `Switch by Status`**:
  - **Kiểm tra giá trị `status`** trong Notion (ví dụ: `Responded` → chuyển đến `Gmail Send Reply`).
- **Node `Switch by Route Destination`**:
  - **Chọn đường dẫn** cho mỗi trạng thái (ví dụ: `Routed` → `Create in Signal Stream` hoặc `Gmail Forward`).

#### **F. Node Code (Bắt Buộc)**
- **`Extract Email Data`**:
  - **Sửa code** để trích xuất email từ Notion:
    ```javascript
    return {
      email: item.json.email,
      subject: item.json.subject,
      body: item.json.body,
      status: item.json.status
    };
    ```
- **`Prepare Route Data`**:
  - **Định dạng dữ liệu** cho Jira/Slack (ví dụ: chuyển đổi `status` thành `priority` cho Jira).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - **Chọn một email** trong Notion có `Status = Responded`.
   - **Run workflow** và kiểm tra:
     - Email có được trả lời không?
     - Trạng thái trong Notion có cập nhật thành `Processed` không?
     - Nếu `Delegated`, Slack DM có được gửi không?
2. **Bật Active**:
   - Sau khi test thành công, **bật `Active`** và **set Polling Interval** (ví dụ: 5 phút) để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
- **Gửi báo cáo định kỳ**:
  - Thêm node `Set Interval` để gửi **báo cáo hàng ngày** về số email đã xử lý qua Slack/Email.
  - **Code ví dụ**:
    ```javascript
    // Node Set Interval (thêm vào cuối workflow)
    return {
      data: {
        email_count: item.json.processed_emails,
        timestamp: new Date().toISOString()
      }
    };
    ```
- **Lưu log chi tiết**:
  - Sử dụng node `StickyNote` để ghi lại **lịch sử xử lý** (ví dụ: "Email XYZ đã được trả lời lúc 10:00").
- **Kết hợp với Google Sheets**:
  - Thêm node `Google Sheets` để **lưu dữ liệu email** vào bảng tính cho báo cáo.
- **Tự động chuyển nhãn email**:
  - Trong node `Prepare Archive Labels`, **định nghĩa nhãn** cho email đã xử lý (ví dụ: `Processed`, `Closed`).
- **Cảnh báo khi lỗi**:
  - Thêm node `If` để **gửi cảnh báo Slack** nếu workflow bị lỗi (ví dụ: email không tồn tại).
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý ticket và email, đồng thời **giảm thiểu sai sót** bằng cách tự động hóa toàn bộ chu trình:
✔ **Trả lời email** → ✔ **Chuyển tiếp Slack/Jira** → ✔ **Cập nhật Notion** → ✔ **Áp dụng nhãn**.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/14120](https://n8n.io/workflows/14120).
2. **Cấu hình Notion, Gmail, Slack, Jira** theo hướng dẫn.
3. **Test và kích hoạt** để tiết kiệm thời gian hàng tuần!

:::success[💡 LƯU Ý CUỐI CUNG]
- **N8n Self-hosted** là **bắt buộc** vì phiên bản cloud không hỗ trợ Polling Interval.
- **Đăng ký VPS** với **TinoHost** (mã giảm giá **VPSN8N**) hoặc **BNIX** để chạy 24/7:
  👉 [TinoHost - VPS N8n](https://tino.vn/vps-n8n?affid=388)
  👉 [BNIX - Xeon 4GB](https://my.bnix.one/aff.php?aff=172)
:::

**Hãy tự động hóa ngay hôm nay và tập trung vào việc quan trọng hơn!** 🚀