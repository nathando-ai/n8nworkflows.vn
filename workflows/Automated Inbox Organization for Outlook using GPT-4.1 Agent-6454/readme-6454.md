---
title: "🤖 **Tự Động Hóa Hộp Thư Outlook với AI GPT-4.1 – Sắp Xếp Email Như Người Thông Minh (Không Cần Code!)**"
description: "Workflow tự động phân loại, sắp xếp và chuyển email từ Outlook vào các thư mục phù hợp dựa trên trí tuệ nhân tạo GPT-4.1, giúp các sếp đạt **Inbox Zero** chỉ trong vài phút mỗi ngày. Giảm 80% thời gian quản lý email thủ công!"
slug: "tieu-dong-ho-thu-outlook-voi-gpt-4-1"
tags: [n8n, automation, outlook, ai, gpt-4, inbox-zero, no-code]
keywords: [tự động hóa email outlook, gpt-4 phân loại email, inbox zero với n8n, workflow outlook ai, tự động sắp xếp thư mục email]
---

# 🚀 **Tự Động Hóa Hộp Thư Outlook với AI GPT-4.1 – Sắp Xếp Email Như Người Thông Minh**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- **Lọc email** giữa tin nhắn quan trọng và spam.
- **Chuyển email** vào thư mục phù hợp (đơn hàng, hợp đồng, hỗ trợ khách hàng...).
- **Trả lời hoặc lưu trữ** những tin nhắn cần thiết.
- **Đánh dấu đã đọc** hàng loạt email để tránh bị "drowning" trong số lượng thông báo.

Kết quả? **Hộp thư Outlook của bạn trở thành "đống rác" số liệu**, làm giảm hiệu suất và tăng căng thẳng.

### **🎯 Giải Pháp: Workflow Tự Động Hóa AI với GPT-4.1**
Workflow này **tự động phân loại email mới** vào các thư mục phù hợp dựa trên **trí tuệ nhân tạo GPT-4.1**, giúp các sếp:
✅ **Giảm 80% thời gian quản lý email** mỗi ngày.
✅ **Đạt Inbox Zero** chỉ trong vài phút.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy.
✅ **Tự động chuyển email** vào thư mục đúng (đơn hàng, hợp đồng, hỗ trợ khách hàng, quảng cáo...).
✅ **Lọc bỏ email không cần thiết** (spam, tin nhắn cũ, tin nhắn từ người quen).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính riêng tư và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Tiết kiệm thời gian**    | Tự động sắp xếp email trong **vài giây** thay vì mất **30-60 phút/ngày**. |
| **Inbox Zero**            | Chỉ giữ lại email **quan trọng** trong hộp thư chính.                      |
| **Tính chính xác cao**    | AI GPT-4.1 phân loại email **như người thông minh**, không sai lầm.         |
| **Hoạt động 24/7**        | Workflow chạy tự động **mỗi khi có email mới**, không cần can thiệp.       |
| **Tùy chỉnh dễ dàng**     | Thêm/loại thư mục, thay đổi logic phân loại theo nhu cầu.                 |

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Microsoft Outlook** (đã kết nối với n8n).
✔ **API Key OpenRouter** (để sử dụng mô hình GPT-4.1).
✔ **Thư mục Outlook đã sẵn sàng** (ví dụ: "Đơn hàng", "Hợp đồng", "Hỗ trợ khách hàng", "Quảng cáo").
✔ **N8n Self-hosted** (để đảm bảo **tính riêng tư** và không bị giới hạn API).

---
:::info[CHUẨN BỊ]
- **Microsoft Outlook OAuth2 API**:
  - Cần **cấp quyền** cho n8n truy cập vào hộp thư Outlook.
  - Hướng dẫn cấp quyền: [Microsoft Graph API Permissions](https://learn.microsoft.com/en-us/graph/auth-v2-service).
- **OpenRouter API Key**:
  - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
  - Mô hình khuyến nghị: `openai/gpt-4.1` (hoặc các mô hình hỗ trợ **tool calls** như Claude, Gemini 2.5 Pro).
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/6454](https://n8n.io/workflows/6454) và import vào n8n Editor.
- **Copy/Paste JSON** từ trang trên vào **n8n Editor** (tab "Import").

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **8 node chính**, các sếp cần **cấu hình kỹ** các node sau:

##### **🔹 Node 1: Microsoft Outlook Trigger**
- **Resource**: `Message`
- **Operation**: `Trigger on new email`
- **Fields to Output**:
  - `from` (người gửi)
  - `subject` (chủ đề)
  - `body` (nội dung email)
  - `isRead` (tùy chọn)
- **Folders to Include**:
  - Chọn **Inbox** hoặc **thư mục cụ thể** (ví dụ: "All Mail" để bao gồm tất cả email mới).

##### **🔹 Node 2: Sanitize Email Body (Code Node)**
- **Mục đích**: Làm sạch nội dung email (xóa HTML, hình ảnh, liên kết, bảng) để AI xử lý chính xác.
- **Mã JavaScript**:
  ```javascript
  // Lấy nội dung Markdown từ node trước
  const markdownContent = $input.item.json["Email Body Markdown"];

  // Xóa các phần không cần thiết (hình ảnh, liên kết, bảng)
  const cleanedContent = markdownContent
    .replace(/!\[.*?\]\(.*?\)/g, "") // Xóa hình ảnh
    .replace(/\[.*?\]\(.*?\)/g, "") // Xóa liên kết
    .replace(/```.*?```/g, "") // Xóa code block
    .replace(/\|.*?\|/g, "") // Xóa bảng
    .substring(0, 4000); // Cắt ngắn nếu quá dài

  return { EmailBodyCleaned: cleanedContent };
  ```

##### **🔹 Node 3: AI Agent - Determine Category (Agent Node)**
- **Mô hình AI**: `openai/gpt-4.1` (đã cấu hình trong `OpenRouter Chat Model`).
- **Cấu hình Tool**:
  - **Move Message**: Chuyển email vào thư mục phù hợp.
  - **Get Folders**: Lấy danh sách thư mục Outlook.
  - **Get Contacts**: (Tùy chọn) Kiểm tra người gửi có trong danh bạ không.
- **Prompt AI**:
  - AI sẽ **tự động phân loại email** vào thư mục phù hợp (ví dụ: "Đơn hàng" nếu có từ khóa "order", "Hợp đồng" nếu có "contract").
  - **Quy tắc bảo mật**:
    - **Không chuyển email** từ người quen (đã lưu trong danh bạ).
    - **Không xóa email** – chỉ chuyển vào thư mục phù hợp.

##### **🔹 Node 4: OpenRouter Chat Model**
- **Model**: `openai/gpt-4.1` (hoặc mô hình hỗ trợ **tool calls** như Claude, Gemini 2.5 Pro).
- **API Key**: Điền **OpenRouter API Key** vào credentials.
- **Input**:
  ```json
  {
    "email": "{{$json["from"]}}",
    "subject": "{{$json["subject"]}}",
    "body": "{{$json["EmailBodyCleaned"]}}",
    "isRead": "{{$json["isRead"]}}"
  }
  ```
- **Output**: AI trả về **thư mục cần chuyển** (ví dụ: "Đơn hàng").

##### **🔹 Node 5: Move Message (Microsoft Outlook Tool)**
- **Operation**: `move`
- **Input**:
  - `messageId`: ID của email cần chuyển.
  - `folderId`: ID thư mục mục tiêu (được lấy từ `Get Folders`).

##### **🔹 Node 6: Get Folders (Microsoft Outlook Tool)**
- **Operation**: `getAll`
- **Resource**: `folder`
- **Output**: Danh sách thư mục Outlook để AI lựa chọn.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 email mẫu** để kiểm tra logic.
2. **Bật Active** workflow.
3. **Monitor** trong **n8n Dashboard** để đảm bảo không có lỗi.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Kết nối với **Slack** hoặc **Telegram** để nhận thông báo khi email được chuyển.
   - Ví dụ: `"Email từ [Người gửi] đã được chuyển vào [Thư mục]."`

2. **Lưu Log Email**:
   - Sử dụng **Google Sheets** hoặc **Notion** để lưu lịch sử chuyển email.
   - Cấu hình node **Google Sheets** để ghi dữ liệu:
     ```json
     {
       "email": "{{$json["from"]}}",
       "subject": "{{$json["subject"]}}",
       "folder": "{{$json["folderName"]}}",
       "timestamp": "{{$now}}"
     }
     ```

3. **Tự động Gửi Báo Cáo Hàng Tuần**:
   - Sử dụng **n8n Schedule Node** để gửi **báo cáo tổng hợp** về số lượng email đã chuyển mỗi tuần.
   - Ví dụ:
     - **"Từ 01/01 đến 07/01, đã chuyển 50 email vào 'Đơn hàng'."**

4. **Tùy Chỉnh AI Prompt**:
   - Nếu AI phân loại sai, **cập nhật prompt** để phù hợp với nghiệp vụ của doanh nghiệp.
   - Ví dụ:
     ```
     "Bạn là trợ lý Outlook chuyên nghiệp. Phân loại email vào thư mục phù hợp dựa trên:
     - Nếu có từ khóa 'order', chuyển vào 'Đơn hàng'.
     - Nếu có từ khóa 'contract', chuyển vào 'Hợp đồng'.
     - Nếu người gửi là người quen (đã lưu trong danh bạ), **không chuyển**.
     - Nếu email cũ hơn 30 ngày, **không chuyển**.
     ```

5. **Bảo Mật Dữ Liệu**:
   - **Không lưu email nguyên văn** trong n8n (chỉ lưu **ID email** và **thông tin cần thiết**).
   - Sử dụng **n8n Webhooks** để xử lý email **offline** nếu cần.

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **các nhiệm vụ chiến lược** thay vì bị "chìm" trong email. Với **AI GPT-4.1**, email sẽ được sắp xếp **như người thông minh**, giúp đạt **Inbox Zero** chỉ trong vài phút mỗi ngày.

🚀 **Hành động ngay hôm nay**:
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình **Microsoft Outlook + OpenRouter API**.
3. **Test Run** và **bật Active** để tự động hóa hộp thư của bạn!

**Cần hỗ trợ?** Đăng ký **khóa học tự động hóa n8n** tại [METAMATION](https://metamation.vn/) để học cách **tạo workflow tự động hóa phù hợp với doanh nghiệp của bạn!**

---
**#TựĐộngHóa #InboxZero #N8N #AI #OutlookAutomation**