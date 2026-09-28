---
title: "🚀 Tự Động Hóa Tạo Nhiệm Vụ Smenso Từ Gmail Với Giao Nhiệm Tuỳ Chỉnh Tự Động"
description: "Workflow này tự động chuyển đổi email có chủ đề 'smenso Task' thành nhiệm vụ trong Smenso, gán tự động vào dự án phù hợp dựa trên từ khóa trong tiêu đề, gửi phản hồi xác nhận và đánh dấu email là đã đọc. Giúp tiết kiệm thời gian quản lý nhiệm vụ lên đến 80% cho các sếp."
slug: "tu-dong-hoa-tao-nhiem-vu-smenso-tu-gmail"
tags: [n8n, automation, project-management, smenso, gmail-integration]
keywords: [n8n workflow smenso, tự động hóa quản lý dự án, tạo nhiệm vụ từ email, gmail automation, smenso api]
---

# 🚀 **Tự Động Hóa Tạo Nhiệm Vụ Smenso Từ Gmail Với Giao Nhiệm Tuỳ Chỉnh Tự Động**

### **Giải quyết vấn đề gì?**
Các sếp thường phải mất **thời gian quý báu** để:
- **Quét email** tìm những yêu cầu nhiệm vụ mới từ khách hàng/đội ngũ.
- **Gán nhiệm vụ** vào dự án phù hợp trong Smenso thủ công.
- **Gửi phản hồi xác nhận** để tránh nhầm lẫn.
- **Đánh dấu email đã đọc** để tránh trùng lặp.

Workflow này **tự động hóa toàn bộ quy trình** chỉ với **một dòng email**, giúp các sếp **tiết kiệm thời gian lên đến 80%** và giảm thiểu lỗi nhân sự.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo an toàn và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **80%** trong quản lý nhiệm vụ.
✅ **Giao nhiệm vụ tự động** dựa trên từ khóa trong tiêu đề email.
✅ **Phản hồi tự động** cho người gửi, giảm thiểu nhầm lẫn.
✅ **Đánh dấu email đã đọc** để tránh trùng lặp.
✅ **Hoạt động liên tục** 24/7 mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kết nối OAuth2 với n8n).
2. **API Key của Smenso** (để tạo nhiệm vụ tự động).
3. **Danh sách dự án Smenso** (để workflow tìm kiếm dự án phù hợp).
4. **Địa chỉ email domain** của công ty (để lọc email từ người gửi tin cậy).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/15660) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần **cấu hình kỹ lưỡng** các node sau:

##### **🔹 Node 1: Gmail Trigger (n8n-nodes-base.gmailTrigger)**
- **Cấu hình:**
  - Chọn **OAuth2 Credentials** đã kết nối với Gmail.
  - Thiết lập **polling interval = 1 phút** (để workflow kiểm tra email thường xuyên).
  - **Lọc email** có tiêu đề chứa từ khóa: `smenso Task`.

##### **🔹 Node 2: Filter by Sender Domain (n8n-nodes-base.filter)**
- **Cấu hình:**
  - Thay thế `@YOUR-DOMAIN.com` bằng **domain email của công ty** (ví dụ: `@acme.com`).
  - Chỉ cho phép email từ **người gửi tin cậy** (không phải từ bất kỳ ai).

##### **🔹 Node 3: Get All Projects (n8n-nodes-smenso.smenso)**
- **Cấu hình:**
  - Kết nối **API Key Smenso** đã chuẩn bị.
  - **Lấy tất cả dự án hoạt động** để workflow có thể tìm kiếm dự án phù hợp.

##### **🔹 Node 4: Match Project by Keyword (n8n-nodes-base.code)**
- **Cấu hình:**
  - **Thay thế `YOUR_DEFAULT_PROJECT_ID_HERE`** bằng **ID dự án mặc định** (dùng khi không tìm thấy dự án phù hợp).
  - **Cách hoạt động:**
    - Workflow **trích xuất từ khóa trong dấu `[]`** của tiêu đề email (ví dụ: `smenso Task [Marketing]: Tạo brief` → từ khóa là `Marketing`).
    - **Tìm dự án Smenso** có tên chứa từ khóa đó.
    - Nếu không tìm thấy, **sử dụng dự án mặc định**.

##### **🔹 Node 5: Create smenso Task (n8n-nodes-smenso.smenso)**
- **Cấu hình:**
  - **Tạo nhiệm vụ** trong dự án đã chọn.
  - **Tiêu đề nhiệm vụ** = Tiêu đề email.
  - **Mô tả nhiệm vụ** = Nội dung email.
  - **Kết nối API Smenso** đã cấu hình.

##### **🔹 Node 6: Send Confirmation Reply (n8n-nodes-base.gmail)**
- **Cấu hình:**
  - **Thay thế `YOUR_WORKSPACE`** bằng **subdomain Smenso** của công ty (ví dụ: `acme.smenso.cloud` → `acme`).
  - **Nội dung phản hồi tự động** (có thể tùy chỉnh):
    ```
    Xin chào [Tên người gửi],

    Nhiệm vụ của bạn đã được tạo thành công trong Smenso và đã được gán vào dự án [Tên dự án].

    Cảm ơn bạn!
    ```

##### **🔹 Node 7: Mark as Read (n8n-nodes-base.gmail)**
- **Cấu hình:**
  - **Đánh dấu email đã đọc** để workflow không lấy lại lần nữa.

#### **3. Kích hoạt ⚡️**
- **Test run** với một email mẫu (ví dụ: `smenso Task [Marketing]: Tạo brief`).
- **Bật Active workflow** để nó hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm **node Slack/Telegram** để thông báo khi nhiệm vụ được tạo thành công.

2. **Lưu log hoạt động**
   - Sử dụng **node StickyNote** để ghi lại lịch sử nhiệm vụ đã tự động hóa.

3. **Gửi báo cáo định kỳ**
   - Thêm **node Email/Slack** để gửi báo cáo tổng hợp nhiệm vụ mới mỗi ngày.

4. **Dùng cho Outlook/IMAP**
   - Thay thế **Gmail Trigger** bằng **Outlook/IMAP Trigger** nếu công ty sử dụng hệ thống khác.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc chiến lược hơn, đồng thời **giảm thiểu lỗi** trong quản lý nhiệm vụ. **Hãy áp dụng ngay** và trải nghiệm sự **tiện lợi và hiệu quả** mà tự động hóa mang lại!

👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow](https://n8n.io/workflows/15660) và cài đặt trên VPS của mình.