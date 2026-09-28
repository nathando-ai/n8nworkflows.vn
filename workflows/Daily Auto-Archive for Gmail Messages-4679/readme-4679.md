---
title: "🗂️ Tự Động Xóa Hàng Ngày Email Trên Gmail - Giảm 90% Thời Gian Quản Lý Inbox"
description: "Workflow tự động hóa 100% không code giúp các sếp tự động xóa (archive) tất cả email trong Inbox Gmail hàng ngày vào 4h sáng, giữ gìn trật tự và tăng hiệu suất làm việc. Giúp giảm thiểu stress và tiết kiệm tối thiểu 2 giờ/ngày."
slug: "tieu-dong-xoa-email-gmail-hang-ngay"
tags: [n8n, automation, gmail, no-code, email-management]
keywords: [tự động hóa gmail, xóa email hàng ngày, n8n workflow gmail, quản lý inbox tự động, giảm thiểu email rác]
---

# 🗂️ **Tự Động Xóa Hàng Ngày Email Trên Gmail - Giải Pháp "Không Code" Cho Các Sếp Bận Rộn**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải đối mặt với **lũ email không ngừng** tràn vào Inbox: tin nhắn quảng cáo, báo cáo định kỳ, thông báo từ hệ thống, và những tin nhắn cũ không cần thiết. Kết quả?
- **Tốn thời gian**: Phải dành **2-3 giờ/ngày** để sắp xếp, xóa, hoặc đánh dấu email.
- **Stress cao**: Inbox tràn ngập làm giảm tập trung và hiệu suất làm việc.
- **Rủi ro mất tin**: Email quan trọng bị "chìm" dưới đống tin nhắn cũ.

**Workflow này giải quyết tất cả!** Với **4 node đơn giản**, nó sẽ **tự động xóa (archive) tất cả email trong Inbox hàng ngày vào 4h sáng**, giúp các sếp bắt đầu ngày mới với một Inbox sạch sẽ và tập trung vào công việc quan trọng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2+ giờ/ngày**: Không còn phải lo lắng về việc quản lý Inbox.
- **Inbox luôn sạch sẽ**: Email cũ tự động được xóa (archive) hàng ngày.
- **Tăng hiệu suất**: Bắt đầu ngày với một không gian làm việc sạch sẽ.
- **Không cần kỹ thuật**: Cài đặt và chạy chỉ trong **5 phút**, không cần viết code.
- **Hoạt động 24/7**: Duy trì trật tự Inbox ngay cả khi các sếp nghỉ ngơi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail chính thức** (không phải tài khoản Google Workspace nếu không cần thiết).
2. **API Key OAuth2 cho Gmail**:
   - Đăng ký **OAuth2 Credentials** trên [Google Cloud Console](https://console.cloud.google.com/).
   - Cấp quyền cho **Gmail API** và **Google Drive API**.
   - Lưu **Client ID** và **Client Secret** để cấu hình trong n8n.
3. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud để đảm bảo hoạt động liên tục).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo **2 cách**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4679) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ file vào **n8n Editor** (đảm bảo không có lỗi syntax).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này chỉ hoạt động khi cấu hình **2 node quan trọng** sau:

##### **A. Cấu Hình Credentials Gmail (gmailOAuth2)**
- **Node**: `Fetch Gmail Inbox Emails` và `Archive Message (Remove INBOX Label)`
- **Hướng dẫn**:
  1. Vào **Credentials** trong n8n Editor.
  2. Tạo **mới credential OAuth2** với tên `gmailOAuth2`.
  3. Điền:
     - **Client ID**: Từ Google Cloud Console.
     - **Client Secret**: Từ Google Cloud Console.
     - **Refresh Token**: Lấy từ quá trình **OAuth2 Authorization** (bước này sẽ yêu cầu các sếp **đăng nhập Gmail** và cho phép quyền truy cập).
  4. **Lưu** và chọn `gmailOAuth2` cho cả hai node Gmail.

##### **B. Kiểm Tra Node ScheduleTrigger**
- **Node**: `Daily Trigger at 4AM`
- **Lưu ý**:
  - Workflow sẽ **khởi động tự động hàng ngày vào 4h sáng** (theo giờ máy chủ n8n).
  - Nếu các sếp muốn **đổi giờ**, chỉnh sửa **cron expression** trong node này (ví dụ: `0 4 * * *` để chạy vào 4h sáng).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và kiểm tra nếu email trong Inbox được **xóa (archive)** thành công.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active** để nó hoạt động tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM NÊN HIỆU QUẢ HƠN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành (ví dụ: *"Inbox đã được xóa hàng ngày vào 4h sáng!"*).
2. **Lưu Log Hoạt Động**:
   - Sử dụng node **Google Sheets** hoặc **Notion** để ghi lại lịch sử hoạt động của workflow (ngày, số email được xử lý).
3. **Tùy Chỉnh Thời Gian**:
   - Nếu 4h sáng không phù hợp, thay đổi **cron expression** trong node `Daily Trigger` (ví dụ: `0 8 * * *` để chạy vào 8h sáng).
4. **Lọc Email Trước Khi Xóa**:
   - Thêm node **Filter** để chỉ xóa email **trước 30 ngày** (tránh xóa email quan trọng).
5. **Sử Dụng Label Tùy Chỉnh**:
   - Thay vì xóa label `INBOX`, các sếp có thể **đánh dấu email** vào một label tùy chỉnh (ví dụ: `archive-daily`).
:::

---

### 📌 **Kết Luận: Bắt Đầu Sống Với Inbox Sạch Sẽ Ngay Hôm Nay!**
Workflow này **giải phóng các sếp khỏi gánh nặng quản lý email**, giúp họ **tập trung vào công việc quan trọng** mà không lo lắng về Inbox tràn ngập. Với **cấu hình đơn giản và hiệu quả 100%**, đây là **công cụ không thể thiếu** cho bất kỳ ai muốn **tăng hiệu suất và giảm stress**.

👉 **Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình credentials Gmail.
3. **Bật Active** và **nghỉ ngơi yên tâm** - Inbox của các sếp sẽ được tự động xóa hàng ngày!

---
:::note[CHÚ Ý]
- Workflow **không xóa vĩnh viễn** email, mà chỉ **xóa label `INBOX`** (archive). Các sếp vẫn có thể tìm thấy email trong **All Mail**.
- Nếu gặp lỗi OAuth2, hãy **xóa credential cũ** và **tạo mới** trong Google Cloud Console.
:::