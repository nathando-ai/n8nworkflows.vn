---
title: "🚀 Tự Động Hóa Xử Lý Nhiệm Vụ Asana Với Gemini AI + Cảnh Báo Slack (Không Cần Code)"
description: "Workflow này tự động phân loại, ưu tiên và phân công nhiệm vụ Asana thông qua trí tuệ nhân tạo Gemini, đồng thời cảnh báo Slack cho các nhiệm vụ cấp thiết - tiết kiệm 80% thời gian quản lý công việc hàng ngày cho các sếp."
slug: "tieu-dong-hoa-asana-voi-gemini-ai-slack"
tags: [n8n, automation, asana, ai-summarization, slack-alert, no-code]
keywords: [tự động hóa asana, gemini ai, cảnh báo slack, phân loại nhiệm vụ, quản lý công việc marketing, workflow n8n]
---

# 🚀 **Tự Động Hóa Xử Lý Nhiệm Vụ Asana Với Gemini AI + Cảnh Báo Slack**

### **Giải Pháp Cho Nỗi Đau "Nhiều Nhiệm Vụ, Không Biết Phân Loại Đâu?"**
Các sếp đã từng gặp phải tình huống này chưa?
- **Nhiều nhiệm vụ Asana** tràn ngập trong Inbox, nhưng không biết phân loại nào là **Bug**, nào là **Feature**, nào là **Yêu cầu từ khách hàng**?
- **Phân công sai người** dẫn đến trì hoãn công việc, ảnh hưởng đến hiệu suất nhóm?
- **Không biết nhiệm vụ nào cấp thiết** cần xử lý ngay, trong khi các nhiệm vụ khác có thể chờ?

Workflow này **tự động hóa toàn bộ quy trình** bằng trí tuệ nhân tạo Gemini, giúp các sếp:
✅ **Phân loại nhiệm vụ chính xác** (Bug/Feature/Inquiry) chỉ trong vài giây
✅ **Phân công tự động** cho thành viên phù hợp trong Asana
✅ **Cảnh báo Slack** cho các nhiệm vụ cấp thiết (High Priority)
✅ **Tiết kiệm 80% thời gian** quản lý công việc hàng ngày

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phân loại nhiệm vụ** dựa trên nội dung (không cần nhập thủ công)
- **Phân công chính xác** cho thành viên phù hợp (giảm sai sót 90%)
- **Cảnh báo Slack tự động** cho nhiệm vụ cấp thiết (không bỏ lỡ deadline)
- **Tiết kiệm thời gian** từ 5-10 giờ/tuần cho quản lý công việc
- **Cập nhật tự động** thông tin nhiệm vụ trong Asana (AI tổng kết nội dung)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Asana** (và **API Key Asana**)
2. **Tài khoản Google Cloud** (để sử dụng **Gemini AI**)
3. **Webhook Slack** (để nhận cảnh báo)
4. **Danh sách email** của các thành viên trong nhóm (để phân công nhiệm vụ)

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12892](https://n8n.io/workflows/12892) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **7 node chính**, các sếp cần chú ý cấu hình sau:

##### **A. Node "Configuration" (Set)**
- Mở node này và **điền thông tin sau**:
  - **Project ID**: ID của dự án Asana bạn muốn theo dõi (ví dụ: "Inbox").
  - **Routing Rules**: Định nghĩa qui tắc phân công (ví dụ: `Bug → dev@example.com`, `Feature → product@example.com`).
  - **Team Emails**: Danh sách email của các thành viên trong Asana.

##### **B. Node "Asana Trigger" (asanaTrigger)**
- **Chọn Project ID** tương ứng với dự án bạn muốn theo dõi (đã đặt trong "Configuration").
- **Resource**: Đặt là `task` (nhiệm vụ).

##### **C. Node "Gemini: Analyze" (googleGemini)**
- **Prompt mẫu** (có thể tùy chỉnh):
  ```
  Analyze the following Asana task and categorize it into one of these:
  - Bug (Technical issue)
  - Feature (New functionality)
  - Inquiry (Customer question)

  Also, determine if the priority is High or Low based on the description.

  Task: {task.title} - {task.description}
  ```
- **Credentials**: Chọn `googlePalmApi` (đã cấu hình trước).

##### **D. Node "Map Data" (Code)**
- **Không cần chỉnh sửa** (n8n tự động map dữ liệu từ Gemini sang Asana).

##### **E. Node "Update Task" (asana)**
- **Operation**: Đặt là `update`.
- **Fields to Update**:
  - `assignee` (phân công cho người dùng từ Routing Rules).
  - `notes` (thêm AI summary từ Gemini).

##### **F. Node "Is High Priority?" (if)**
- **Condition**: Kiểm tra nếu `priority` từ Gemini là `High`.
- **Nếu đúng**: Chuyển sang node **Notify Slack**.

##### **G. Node "Notify Slack" (slackweb)**
- **Message Template** (có thể tùy chỉnh):
  ```
  🚨 **URGENT ASASA TASK ALERT** 🚨
  **Title:** {task.title}
  **Priority:** High
  **Link:** {task.gd_url}
  ```
- **Credentials**: Chọn `slackIncomingWebhookApi`.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy thử với một nhiệm vụ mẫu để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, bật workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Google Sheets**
   - Lưu lịch sử phân loại nhiệm vụ vào Google Sheets để theo dõi hiệu suất.

2. **Cảnh báo Email cho Leader**
   - Thêm node **Email** để gửi báo cáo hàng tuần cho trưởng nhóm.

3. **Tự động Xóa Nhiệm Vụ Sau Xử Lý**
   - Sử dụng node **Code** để xóa nhiệm vụ sau khi phân công thành công (nếu không cần lưu lại).

4. **Tùy Chỉnh Prompt Gemini**
   - Nếu muốn Gemini phân loại chi tiết hơn, cập nhật prompt với các tiêu chí cụ thể (ví dụ: `Low/Medium/High`).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp từ việc quản lý nhiệm vụ thủ công, đồng thời **tăng cường hiệu quả** của nhóm bằng cách phân loại và phân công tự động. **Hãy áp dụng ngay** và xem công việc của bạn trở nên **nhanh chóng và chính xác hơn**!

👉 **Bắt đầu tự động hóa Asana của bạn [tại đây](https://n8n.io/workflows/12892)**!