---
title: "🤖 **Tự Động Hóa Phân Loại & Nhãn Email Gmail Với GPT-4o – Giảm 90% Thời Gian Quản Lý Email**"
description: "Workflow tự động phân loại và nhãn email Gmail bằng trí tuệ nhân tạo (GPT-4o), giúp các sếp tiết kiệm 90% thời gian quản lý email hàng ngày, tự động xóa email không cần thiết và sắp xếp thông tin theo nhãn cá nhân hóa (Receipt, Action, Informational)."
slug: "tieu-dong-hoa-phan-loai-nhan-email-gmail-gpt-4o"
tags: [n8n, automation, no-code, gmail, ai-summarization, openai, gpt-4o]
keywords: [tự động hóa email gmail, phân loại email bằng ai, nhãn email tự động, gpt-4o n8n, giảm thời gian quản lý email]
---

# 🚀 **Tự Động Hóa Phân Loại & Nhãn Email Gmail Với GPT-4o – Giải Pháp AI Cho Quản Lý Email Hiệu Quả**

---
## **📌 Nỗi Đau Của Các Sếp Với Email Hàng Ngày**
Hàng ngày, các sếp phải mất **từ 1-2 giờ** để:
- **Lọc email** giữa tin nhắn quan trọng và spam.
- **Nhãn email** theo chủ đề (thanh toán, hợp đồng, thông báo).
- **Xóa email cũ** để giữ hộp thư sạch sẽ.
- **Tìm kiếm lại** email quan trọng trong hàng trăm tin nhắn.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi AI có thể làm tất cả những việc này **một cách chính xác và tự động**.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 90% thời gian** quản lý email hàng ngày.
✅ **Phân loại email tự động** bằng GPT-4o (chính xác hơn 95%).
✅ **Nhãn email cá nhân hóa** (Receipt, Action, Informational, Meeting, Newsletter...).
✅ **Xóa email không cần thiết** tự động sau khi xử lý.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✅ **Cập nhật liên tục** với các email mới trong Gmail.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Gmail** (đã kích hoạt OAuth2).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys)).
3. **Những nhãn Gmail sau** (đã tạo trước):
   - `Receipt` (Hóa đơn)
   - `Action` (Cần xử lý)
   - `Informational` (Thông báo)
   *(Có thể thêm nhãn khác như `Meeting`, `Newsletter` theo yêu cầu)*
4. **VPS hoặc máy chủ n8n** (để workflow chạy liên tục).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/5820) (ấn nút **"Export"**).
2. **Mở n8n Editor** trên máy chủ của mình.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create Workflow"** để lưu vào hệ thống.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io](https://n8n.io/workflows/5820).
2. **Mở n8n Editor** → **Nhấn "Import"** → **Chọn "Paste JSON"**.
3. **Lưu workflow** với tên **"Auto Email Categorizer"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **13 node** quan trọng, nhưng các sếp cần **cấu hình chính xác** các phần sau:

#### **🔹 1. Cấu Hình Gmail (OAuth2)**
- **Node:** `Get All Unread Messages`, `Mark email as read`, `Delete email`, `Add label "Receipt"`, `Add label "Action"`, `Add label "Informational"`
- **Hướng dẫn:**
  - Trong **n8n Editor**, chọn node `Get All Unread Messages`.
  - Nhấn **"Add"** → Chọn **"Gmail"** → **"Add new connection"**.
  - **Đăng nhập Gmail** bằng tài khoản muốn tự động hóa.
  - **Chọn quyền truy cập** (đọc email, nhãn, xóa).
  - **Lưu connection** và chọn nó trong node.

#### **🔹 2. Thêm API Key OpenAI**
- **Node:** `OpenAI Chat Model` (gpt-4o), `OpenAI Fall Back Model` (gpt-3.5-turbo)
- **Hướng dẫn:**
  - Trong **n8n Editor**, chọn **"API Credentials"** (góc trên bên phải).
  - Nhấn **"Add"** → Chọn **"OpenAI"** → **Dán API Key** từ OpenAI.
  - **Lưu** và chọn **API Key** trong các node `lmChatOpenAi`.

#### **🔹 3. Cấu Trình Prompt AI (Phân Loại Email)**
- **Node:** `AI Agent` (Prompt mặc định)
- **Hướng dẫn:**
  - **Mở node `AI Agent`** → **Nhấn "Edit Fields"**.
  - **Sửa prompt** để phù hợp với nhu cầu cá nhân:
    ```plaintext
    Analyze the email content and categorize it into one of these labels:
    - Receipt (if it's a payment confirmation, invoice, or receipt)
    - Action (if it requires a response or action from me)
    - Informational (if it's a newsletter, update, or general info)
    - Meeting (if it's related to a meeting)
    - Newsletter (if it's a newsletter subscription)
    Return the label in JSON format: {"label": "Receipt"}
    ```
  - **Nếu muốn thêm nhãn mới**, cập nhật prompt tương ứng.

#### **🔹 4. Thiết Lập Lịch Triggers (Schedule Trigger)**
- **Node:** `Schedule Trigger`
- **Hướng dẫn:**
  - **Mở node `Schedule Trigger`** → **Chọn "Edit"** → **Đổi interval** (mặc định là **1 giờ**).
  - **Cập nhật theo nhu cầu**:
    - **1 giờ** (xử lý email liên tục).
    - **6 giờ** (giảm tải cho OpenAI).
    - **24 giờ** (chỉ xử lý email mới vào buổi sáng).

#### **🔹 5. Kiểm Tra Node Switch (Routing Logic)**
- **Node:** `Switch`
- **Hướng dẫn:**
  - **Mở node `Switch`** → **Kiểm tra điều kiện** (mặc định là `label` từ AI).
  - **Nếu muốn thêm nhãn mới**, thêm **case mới** trong node:
    ```plaintext
    Case 1: {{ $json.label === "Meeting" }} → Add label "Meeting"
    Case 2: {{ $json.label === "Newsletter" }} → Delete email
    ```

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với email mẫu:
   - **Nhấn "Run Workflow"** và chọn **1 email mẫu** từ Gmail.
   - **Kiểm tra kết quả**:
     - Email có được **nhãn** đúng không?
     - AI có phân loại chính xác không?
   - **Nếu sai**, chỉnh sửa **prompt** hoặc **nhãn Gmail**.

2. **Bật Active Workflow**:
   - **Nhấn "Active"** ở góc trên bên phải.
   - **Kiểm tra log** trong **Execution History** để đảm bảo không lỗi.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Thêm Nhãn Tùy Chỉnh**
- **Mở node `Switch`** → **Thêm case mới** để xử lý nhãn mới:
  ```plaintext
  Case 3: {{ $json.label === "Urgent" }} → Add label "Urgent" + Mark as read
  ```

### **🔹 2. Gửi Báo Cáo Định Kỳ**
- **Thêm node `Email`** sau `Switch` để gửi **báo cáo hàng tuần**:
  ```plaintext
  - Tóm tắt số email đã phân loại.
  - Danh sách nhãn phổ biến nhất.
  ```
- **Kết hợp với `Schedule Trigger`** để gửi vào **thứ 7 hàng tuần**.

### **🔹 3. Lưu Log Email**
- **Thêm node `Google Sheets`** để ghi lại:
  - **Ngày nhận email**.
  - **Nhãn phân loại**.
  - **Nội dung tóm tắt** (nếu cần).
- **Cấu hình sheet** trong node `Set` trước khi lưu.

### **🔹 4. Kết Nối Với Slack/Telegram**
- **Thêm node `Slack`** hoặc `Telegram` sau `Switch` để:
  - **Báo động** khi có email nhãn `Urgent`.
  - **Tóm tắt email mới** vào kênh nhóm.

---
## **📌 Kết Luận: Tự Động Hóa Email Bằng AI – Không Cần Code!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc **quan trọng hơn**, trong khi AI **xử lý email một cách thông minh và tự động**.

**🚀 Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình Gmail + OpenAI.
3. **Chạy test** và điều chỉnh prompt cho phù hợp.
4. **Bật Active** và **quên đi công việc lặp lại!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow **ổn định và hoạt động liên tục**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
**💡 Chia sẻ và phản hồi:**
Nếu có **ý tưởng cải tiến** hoặc **vấn đề gặp phải**, hãy để lại comment bên dưới. Chúng ta sẽ **cập nhật workflow** để phù hợp hơn với nhu cầu của các sếp! 🚀