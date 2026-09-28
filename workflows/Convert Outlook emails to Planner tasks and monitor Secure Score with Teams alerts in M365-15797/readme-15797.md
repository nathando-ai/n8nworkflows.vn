---
title: "🚀 Tự Động Hóa Email Outlook → Nhiệm Vụ Planner + Theo Dõi Điểm An Toàn M365 Với Thông Báo Teams (M365 Smart Inbox)"
description: "Workflow tự động hóa 100% không code chuyển email Outlook thành nhiệm vụ Planner, đồng thời theo dõi điểm an toàn Microsoft 365 và cảnh báo qua Teams khi điểm số dưới 80%. Giúp các sếp tiết kiệm 10+ giờ/tháng và giảm thiểu rủi ro an ninh."
slug: "tu-dong-hoa-email-outlook-nhiem-vu-planner-theo-doi-diem-an-toan-m365"
tags: [n8n, automation, microsoft-365, outlook, planner, teams, ai-summarization, security-monitoring]
keywords: [n8n workflow outlook planner, tự động hóa email thành nhiệm vụ, theo dõi điểm an toàn M365, cảnh báo Teams, Microsoft Graph API, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Email Outlook → Nhiệm Vụ Planner + Theo Dõi Điểm An Toàn M365 Với Thông Báo Teams**

## **📌 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Quét thủ công** hàng chục email trong Outlook để chuyển thành nhiệm vụ trong Planner (hay Trello, Asana...).
- **Quên kiểm tra** điểm an toàn Microsoft 365 (Secure Score) hàng tuần, dẫn đến rủi ro an ninh không phát hiện kịp thời.
- **Phải nhớ** gửi thông báo Teams cho team khi có nhiệm vụ mới hoặc điểm an toàn xuống dưới ngưỡng an toàn.
- **Mất thời gian** để phân loại, đặt ngày hạn và gán người thực hiện cho mỗi nhiệm vụ.

**Kết quả?** Thời gian làm việc bị "đắm chìm" trong công việc thủ công, năng suất giảm, và rủi ro an ninh tăng cao.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng** bằng cách tự động chuyển email thành nhiệm vụ Planner.
✅ **Không bao giờ quên** kiểm tra điểm an toàn M365 (Secure Score) hàng tuần.
✅ **Cảnh báo kịp thời** khi điểm an toàn xuống dưới 80% qua Teams.
✅ **Tự động phân loại** email có từ khóa hành động (URGENT, ACTION REQUIRED...) thành nhiệm vụ.
✅ **Tránh trùng lặp nhiệm vụ** bằng cơ chế kiểm tra nhiệm vụ đã tồn tại.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & Credentials**
- **Tài khoản Microsoft 365** (Outlook, Planner, Teams, Defender) với quyền:
  - `Mail.ReadWrite` (đọc/gửi email)
  - `Tasks.ReadWrite` (tạo/sửa nhiệm vụ Planner)
  - `ChannelMessage.Send` (gửi thông báo Teams)
  - `SecurityEvents.Read.All` (đọc điểm an toàn M365)
- **OAuth2 Credential** cho Microsoft Graph (cung cấp cho tất cả node M365).

### **2. Tham Số Cần Cấu Hình**
Các biến môi trường (Workflow Variables) cần thiết:
| **Tên Biến**               | **Mô Tả**                                                                 | **Giá Trị Mặc Định**                     |
|----------------------------|----------------------------------------------------------------------------|--------------------------------------------|
| `PLANNER_PLAN_ID`          | ID của Plan trong Planner (dùng để tạo nhiệm vụ)                          | *(Cần điền)*                              |
| `PLANNER_BUCKET_ID`        | ID của Bucket trong Plan (dùng để phân loại nhiệm vụ)                    | *(Cần điền)*                              |
| `TASK_ASSIGNEE_USER_ID`    | ID người dùng được gán nhiệm vụ (format: `user@domain.com`)              | *(Cần điền)*                              |
| `TEAMS_TEAM_ID`            | ID của Team trong Microsoft Teams (dùng để gửi thông báo)                | *(Cần điền)*                              |
| `TEAMS_CHANNEL_ID`         | ID của Channel trong Team (dùng để gửi thông báo)                        | *(Cần điền)*                              |
| `MONITORED_MAILBOX`        | Địa chỉ email của hộp thư cần theo dõi (UPN)                              | *(Cần điền)*                              |
| `ACTION_KEYWORDS`          | Danh sách từ khóa hành động (ngăn cách bởi dấu phẩy)                       | `ACTION REQUIRED,URGENT,TASK:,PLEASE REVIEW,CRITICAL` |
| `REPORT_TIMEZONE`          | Múi giờ cho việc xử lý ngày giờ (ví dụ: `Asia/Ho_Chi_Minh`)                | `Europe/Helsinki`                          |
| `ERROR_EMAIL_RECIPIENT`    | Email nhận thông báo lỗi (nếu workflow gặp sự cố)                        | *(Cần điền)*                              |

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/15797](https://n8n.io/workflows/15797) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên máy chủ self-hosted hoặc n8n.cloud.
3. Nhấn **Import** → Chọn file JSON vừa tải → Nhấn **Import**.

#### **Phương Pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. Trong n8n Editor, nhấn **Import** → Chọn **Paste JSON** → Dán nội dung JSON → Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Cấu Hình Credentials Microsoft Graph**
- **Tạo OAuth2 Credential** trong n8n:
  - Nhấn **Credentials** → **Add new credential** → Chọn **Microsoft Graph**.
  - Đăng nhập tài khoản M365 và cấp quyền cần thiết (xem phần **Yêu Cầu Cần Thiết**).
  - **Gán credential** cho tất cả node M365 trong workflow (Outlook, Planner, Teams, Security API).

#### **🔹 Cấu Hình Workflow Variables**
- Mở **Settings** → **Workflow Variables** trong n8n Editor.
- Thêm các biến môi trường theo bảng trên (đặc biệt là `PLANNER_PLAN_ID`, `PLANNER_BUCKET_ID`, `TASK_ASSIGNEE_USER_ID`).

#### **🔹 Node "Extract Task from Email" (Code Node)**
- **Mở node này** và kiểm tra script JavaScript để đảm bảo:
  - **Từ khóa hành động** (`ACTION_KEYWORDS`) được cấu hình chính xác.
  - **Định dạng ngày hạn** (ISO, `due:`, `by:`, hoặc từ khóa tương đối như `today`, `tomorrow`) được hỗ trợ.
  - **Múi giờ** (`REPORT_TIMEZONE`) được sử dụng trong logic tính ngày.

#### **🔹 Node "Create Planner Task" & "Set Task Details"**
- Kiểm tra **URL API** của Planner:
  - Đảm bảo `PLANNER_PLAN_ID` và `PLANNER_BUCKET_ID` được điền chính xác.
  - **Tham số `assignee`** phải là ID người dùng hợp lệ (format: `user@domain.com`).

#### **🔹 Node "Post Teams Notification"**
- **Kiểm tra `TEAMS_TEAM_ID` và `TEAMS_CHANNEL_ID`** đã được điền đúng.
- **Thông báo Teams** sẽ bao gồm:
  - Tiêu đề email.
  - Người gửi.
  - Từ khóa hành động.
  - Ngày hạn (nếu có).
  - Mô tả nhiệm vụ.

#### **🔹 Node "Get Latest Secure Score" (Pipeline 2)**
- **Kiểm tra API endpoint** của Microsoft Secure Score:
  - Đảm bảo `SecurityEvents.Read.All` được cấp quyền.
  - **Cấu trúc dữ liệu trả về** phải được xử lý trong node `Calculate Security Score Percentage` (Code Node).

#### **🔹 Node "Error Capture (Poison Pill Guard)"**
- **Script này** kiểm tra lỗi trong quá trình xử lý email.
- Nếu workflow gặp lỗi, nó sẽ:
  - **Gửi email thông báo lỗi** (địa chỉ email trong `ERROR_EMAIL_RECIPIENT`).
  - **Đánh dấu email là đã đọc** mà không tạo nhiệm vụ.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một email có từ khóa `URGENT` hoặc `ACTION REQUIRED` vào hộp thư được theo dõi.
   - Kiểm tra:
     - Nhiệm vụ có được tạo trong Planner không?
     - Thông báo Teams có xuất hiện không?
     - Email có được trả lời và đánh dấu là đã đọc không?
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Kiểm tra log** để đảm bảo không có lỗi.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Cho Nhiều Hộp Thư**
- **Sử dụng nhiều Workflow Variables** cho từng hộp thư:
  - Thay vì chỉ theo dõi một hộp thư (`MONITORED_MAILBOX`), tạo biến `MONITORED_MAILBOX_1`, `MONITORED_MAILBOX_2`...
  - **Sử dụng node `splitInBatches`** để xử lý từng hộp thư riêng biệt.

### **2. Thêm Log Lịch Sử**
- **Sử dụng node `stickyNote`** để ghi lại lịch sử xử lý:
  - Ghi ngày giờ, ID email, và kết quả (tạo nhiệm vụ thành công/thất bại).
  - **Lưu vào Google Sheets** hoặc **OneDrive** để theo dõi.

### **3. Cảnh Báo Trước Hạn Nhiệm Vụ**
- **Thêm một Workflow phụ** để cảnh báo khi nhiệm vụ sắp hết hạn:
  - **Poll Planner** hàng ngày để kiểm tra nhiệm vụ có ngày hạn trong 24h.
  - **Gửi thông báo Teams** hoặc email cho người gán nhiệm vụ.

### **4. Tích Hợp với Slack**
- **Thay thế Teams bằng Slack**:
  - Sử dụng node `n8n-nodes-base.slack` để gửi thông báo.
  - Cấu hình `SLACK_WEBHOOK_URL` trong Workflow Variables.

### **5. Tự Động Phân Loại Nhiệm Vụ**
- **Sử dụng AI (LLM)** để phân loại nhiệm vụ:
  - Thay vì chỉ dựa vào từ khóa, **gửi email vào node `n8n-nodes-ai.openai`** để phân tích nội dung và gán nhãn tự động.
  - Ví dụ: Nếu email đề cập đến "quy trình an ninh", gán nhãn `Security`.

---
## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa hoàn toàn** quá trình chuyển email thành nhiệm vụ.
✔ **Theo dõi điểm an toàn M365** một cách tự động và cảnh báo kịp thời.
✔ **Tiết kiệm thời gian** và tập trung vào công việc chiến lược.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (Self-hosted) để workflow hoạt động 24/7.
2. **Cấu hình credentials** và Workflow Variables theo hướng dẫn.
3. **Test Run** và bật Active để tự động hóa công việc!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng:**
- **Backup workflow** định kỳ để tránh mất dữ liệu.
- **Monitor log** để phát hiện lỗi sớm.
- **Cập nhật API permissions** nếu Microsoft thay đổi chính sách.

**Chúc các sếp thành công với việc tự động hóa!** 🚀