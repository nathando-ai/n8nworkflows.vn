---
title: "🚀 Hệ Thống Đặt Lịch Demo Tự Động Hóa với Outlook & Zoom - Giảm 90% Thời Gian Chăm Sóc Khách Hàng"
description: "Workflow tự động hóa hoàn toàn cho việc đặt lịch demo trực tiếp, tích hợp Outlook Calendar và Zoom, giúp doanh nghiệp tiết kiệm thời gian, tránh trùng lịch và tự động tạo link Zoom. Chỉ cần 1 phút để cấu hình và bắt đầu hoạt động 24/7."
slug: "automated-demo-scheduling-outlook-zoom"
tags: [n8n, automation, outlook, zoom, no-code, sales-automation, CRM]
keywords: [tự động hóa đặt lịch demo, n8n workflow outlook zoom, giảm thời gian chăm sóc khách hàng, tự động tạo link zoom, tránh trùng lịch, CRM tự động hóa]
---

# 🚀 **Hệ Thống Đặt Lịch Demo Tự Động Hóa với Outlook & Zoom**

### **Giải pháp nào giúp bạn:**
- **Tiết kiệm 90% thời gian** trong việc quản lý lịch demo thủ công?
- **Tránh trùng lịch** và tự động cập nhật lịch khi khách hàng đặt lịch?
- **Tạo link Zoom tự động** và gửi thông báo lịch ngay lập tức?
- **Cá nhân hóa trải nghiệm** cho khách hàng với lịch trình linh hoạt?

Nếu các sếp đang mệt mỏi với việc phải tra cứu lịch Outlook, tạo link Zoom thủ công và lo lắng về việc trùng lịch, thì **Automated Demo Scheduling System** chính là giải pháp hoàn hảo cho doanh nghiệp!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tra cứu lịch hoặc tạo link Zoom thủ công.
- **Tránh trùng lịch**: Hệ thống tự động kiểm tra và chặn slot đã được đặt.
- **Cá nhân hóa**: Khách hàng được chọn ngày và giờ phù hợp với lịch trình của doanh nghiệp.
- **Hoạt động liên tục**: Workflow tự động chạy 24/7, không cần can thiệp của con người.
- **Tăng hiệu quả chăm sóc khách hàng**: Khách hàng nhận được thông báo lịch ngay lập tức.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Microsoft Outlook** với **OAuth2 API** (đăng ký tại [Microsoft Developer Portal](https://developer.microsoft.com/)).
2. **Tài khoản Zoom** với **OAuth2 API** (đăng ký tại [Zoom Developer Portal](https://marketplace.zoom.us/)).
3. **Lịch Outlook đã tạo sẵn** với các sự kiện có **subject "Online Meeting Slot"** (để hệ thống kiểm tra sẵn có).
4. **n8n self-hosted** (khuyến nghị sử dụng VPS để đảm bảo tính riêng tư và hiệu suất).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **"Import"** và chọn file JSON hoặc paste JSON từ [đây](https://n8n.io/workflows/8456).
3. Chọn **"Import"** để hoàn tất.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **16 node** và cần cấu hình một số node quan trọng như sau:

#### **A. Cấu hình OAuth2 cho Outlook và Zoom**
- **Outlook Calendar CheckAvailability** và **Outlook Update Event**:
  - Đăng nhập vào [Microsoft Developer Portal](https://developer.microsoft.com/) để tạo **OAuth2 API**.
  - Trong n8n, chọn **"microsoftOutlookOAuth2Api"** và điền **Client ID**, **Client Secret**, và **Redirect URI**.
  - Thực hiện **OAuth2 Flow** để kết nối tài khoản Outlook.

- **Create Zoom meeting**:
  - Đăng nhập vào [Zoom Developer Portal](https://marketplace.zoom.us/) để tạo **OAuth2 API**.
  - Trong n8n, chọn **"zoomOAuth2Api"** và điền **Client ID**, **Client Secret**, và **Redirect URI**.
  - Thực hiện **OAuth2 Flow** để kết nối tài khoản Zoom.

#### **B. Cấu hình Form và Logic**
- **Client Details**: Điền thông tin về công ty, tên liên hệ, email, và số điện thoại.
- **Select Date&Time**: Hệ thống sẽ tự động kiểm tra sẵn có của ngày và giờ.
- **Set Event Fields**: Đảm bảo các trường như **Zoom link**, **Client Details**, và **Subject** được cập nhật chính xác.

#### **C. Logic kiểm tra sẵn có**
- **Outlook Calendar CheckAvailability**: Hệ thống sẽ kiểm tra sự kiện có **subject "Online Meeting Slot"** trên ngày được chọn.
- **New Slot Available?**: Nếu không có slot sẵn có, hệ thống sẽ yêu cầu khách hàng chọn ngày mới.
- **Selected Date Has Slot Available?**: Nếu có slot sẵn có, hệ thống sẽ hiển thị **3 slot thời gian gần nhất**.

#### **D. Tạo Zoom Meeting và Cập nhật Outlook**
- **Create Zoom meeting**: Khi khách hàng chọn ngày và giờ, hệ thống sẽ tự động tạo **Zoom link**.
- **Outlook Update Event**: Hệ thống sẽ cập nhật sự kiện với:
  - **Zoom link URL**
  - **Client Details**
  - **Subject "Booked Live Demo"** (để chặn trùng lịch).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**: Chạy workflow với dữ liệu mẫu để kiểm tra logic.
2. **Bật Active**: Sau khi kiểm tra thành công, nhấp vào **"Active"** để workflow bắt đầu hoạt động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo qua Slack/Telegram**: Khi có lịch mới được đặt, hệ thống có thể gửi thông báo tự động đến nhóm quản lý.
2. **Lưu log lịch sử**: Sử dụng node **stickyNote** hoặc **database** để lưu lịch sử đặt lịch và theo dõi.
3. **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo số lượng lịch đã đặt và tỷ lệ thành công.
4. **Tích hợp với CRM**: Nếu doanh nghiệp sử dụng **HubSpot**, **Salesforce**, hoặc **Zoho CRM**, có thể tích hợp để cập nhật thông tin khách hàng tự động.
5. **Cá nhân hóa email**: Sử dụng node **email** để gửi email xác nhận lịch với nội dung cá nhân hóa.
:::

---

## 📌 **Kết luận**
**Automated Demo Scheduling System** là giải pháp hoàn hảo để **tự động hóa hoàn toàn** quá trình đặt lịch demo, giúp doanh nghiệp **tiết kiệm thời gian**, **tránh trùng lịch**, và **tăng hiệu quả chăm sóc khách hàng**.

👉 **Hãy áp dụng ngay workflow này và bắt đầu tự động hóa quy trình của mình!**
👉 **Cần hỗ trợ thêm?** Liên hệ với [AureusR](https://n8n.io/workflows/8456) để có một **bài tư vấn cá nhân hóa** về cách tối ưu hóa workflow cho doanh nghiệp của các sếp!

---