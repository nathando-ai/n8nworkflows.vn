---
title: "🤖 **Tự Động Hóa Phân Loại & Sắp Xếp Email Outlook Bằng AI (GPT-4o) – Không Cần Code!**"
description: "Workflow tự động phân loại, tóm tắt và sắp xếp email Outlook theo chủ đề thông minh bằng AI, tiết kiệm thời gian cho các sếp lên tới 80% công việc thủ công. Hoạt động 24/7, không cần can thiệp."
slug: "tu-dong-hoa-phan-loai-email-outlook-bang-ai"
tags: [n8n, automation, outlook, ai-summarization, gpt-4o, no-code]
keywords: [tự động hóa email outlook, phân loại email bằng AI, n8n workflow outlook, tự động hóa công việc email, sắp xếp email thông minh]
---

# 🚀 **Tự Động Hóa Phân Loại Email Outlook Bằng AI – Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp**

### **Nỗi Đau Của Các Sếp Với Email**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Lọc và phân loại** email vào các folder phù hợp (giao dịch, khách hàng, báo cáo, spam...).
- **Tóm tắt nội dung** email dài để đọc nhanh.
- **Trả lời hoặc chuyển tiếp** email quan trọng một cách hiệu quả.
- **Tránh bỏ lỡ** email từ khách hàng hoặc đồng nghiệp cấp trên.

**Workflow này giải quyết tất cả vấn đề trên bằng AI + n8n – một giải pháp tự động hóa 100% không cần code!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ nhanh, không lag)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Phân loại và tóm tắt email tự động, giảm **80% công việc thủ công**.
✅ **Chính xác cao**: AI phân loại email theo **ngôn ngữ tự nhiên**, không sai lầm như quy tắc thủ công.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
✅ **Tóm tắt thông minh**: AI tóm tắt email dài thành **câu chính**, giúp đọc nhanh.
✅ **Sắp xếp tự động**: Email được **di chuyển vào folder phù hợp** ngay khi nhận.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Microsoft Outlook** (đã kết nối OAuth2).
✔ **API Key OpenRouter** (để sử dụng mô hình AI **DeepSeek Chat v3.1:free**).
✔ **Các folder Outlook đã tạo sẵn** (ví dụ: "Giao dịch", "Khách hàng", "Báo cáo", "Spam").
✔ **n8n Self-hosted** (cài đặt trên VPS để tránh giới hạn phiên bản cloud).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không hỗ trợ phiên bản n8n Cloud** (do giới hạn API và thời gian chạy).
- Các sếp cần **cấu hình OAuth2 Outlook** và **API Key OpenRouter** trước khi import.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/8336) (nút "Export").
2. **Mở n8n Editor** (trang chủ của n8n sau khi cài đặt).
3. Nhấn **"Import"** → Chọn file JSON vừa tải → **"Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [đây](https://n8n.io/workflows/8336) (nút "Export").
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** → **"Import"**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình các node quan trọng** sau:

#### **🔹 Node "Microsoft Outlook" (OAuth2)**
- **Tạo credentials mới**:
  - Trong n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"Microsoft Outlook OAuth2"**.
  - **Đăng nhập Outlook** và cho phép quyền truy cập.
  - **Lưu credentials** với tên **"microsoftOutlookOAuth2Api"**.

#### **🔹 Node "OpenRouter Chat Model" (API Key)**
- **Tạo credentials mới**:
  - Trong n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"OpenRouter API"**.
  - **Nhập API Key** từ [OpenRouter](https://openrouter.ai/) (miễn phí cho mô hình **DeepSeek Chat v3.1:free**).
  - **Lưu credentials** với tên **"openRouterApi"**.

#### **🔹 Node "Schedule Trigger" (Lịch chạy tự động)**
- **Cấu hình thời gian chạy**:
  - Mở node **"Schedule Trigger"** → **"Edit"** → Chọn **thời gian chạy** (ví dụ: **mỗi 5 phút** để kiểm tra email mới).
  - **Lưu lại**.

#### **🔹 Node "AI Agent" (Cấu hình AI phân loại)**
- **Không cần chỉnh sửa** (AI đã được cấu hình sẵn để phân loại email theo **ngôn ngữ tự nhiên**).
- **Nếu muốn thay đổi logic**, mở node **"Code"** (nếu có) và chỉnh sửa logic phân loại.

#### **🔹 Node "Update Category" & "Move Folder"**
- **Kiểm tra folder mục tiêu**:
  - Workflow sẽ **di chuyển email** vào folder đã định nghĩa trong **Microsoft Outlook**.
  - **Đảm bảo folder đã tồn tại** trước khi chạy.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run (kiểm tra thử)**:
   - Chọn **"Test"** trên node **"Schedule Trigger"** → Nhấn **"Run Workflow"**.
   - Kiểm tra **email mẫu** có được phân loại và di chuyển đúng folder không.

2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** trên node **"Schedule Trigger"**.
   - Workflow sẽ **chạy tự động** theo lịch đã đặt.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết hợp với Slack/Telegram để báo cáo**
- **Thêm node "Webhook"** để gửi thông báo khi email mới được phân loại.
- **Cấu hình Slack/Telegram Webhook** trong n8n để nhận tin nhắn tự động.

### **2. Lưu log hoạt động**
- **Thêm node "StickyNote"** để ghi lại lịch sử phân loại email.
- **Dùng node "Markdown"** để tạo báo cáo định kỳ (ví dụ: **tóm tắt email quan trọng hàng tuần**).

### **3. Tóm tắt email dài thành văn bản ngắn**
- **Sử dụng node "Summarize"** để tóm tắt nội dung email dài thành **câu chính**.
- **Hiển thị tóm tắt trong Outlook** hoặc gửi qua email.

### **4. Phân loại email theo từ khóa cụ thể**
- **Chỉnh sửa node "If"** để thêm **điều kiện phân loại** (ví dụ: email chứa từ "giao dịch" → folder "Giao dịch").

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **phân loại email thủ công**, đồng thời **tăng cường hiệu quả** với AI phân loại thông minh. **Chỉ cần import, cấu hình OAuth2 và API Key – workflow sẽ hoạt động tự động!**

👉 **Hãy thử ngay và tiết kiệm **80% thời gian** cho công việc email!**
👉 **Cài n8n trên VPS để tránh giới hạn phiên bản cloud** → **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N**).

---
**Chia sẻ ý kiến hoặc gặp vấn đề, các sếp có thể comment bên dưới hoặc liên hệ qua [ubden.com](https://ubden.com) (tác giả của workflow).** 🚀