---
title: "🚀 Tự Động Hàng Ngày Nhập Khách Hàng Đã Xác Thực từ NocoDB sang Brevo (SendinBlue) - Giảm 90% Công Việc Nhập Liệu"
description: "Workflow tự động hóa hàng ngày nhập tất cả khách hàng mới từ NocoDB sang Brevo (SendinBlue) với kiểm tra đầy đủ trường dữ liệu và loại bỏ email tạm thời, giúp các sếp tiết kiệm thời gian và nâng cao chất lượng danh sách email."
slug: "tu-dong-nhap-khach-hang-nocodb-sang-brevo"
tags: [n8n, automation, no-code, marketing-automation, nocoDB, sendinblue, email-marketing]
keywords: [tự động hóa n8n, nhập liệu từ nocoDB sang Brevo, loại bỏ email tạm thời, workflow hàng ngày, marketing automation]
---

# 🚀 **Tự Động Hàng Ngày Nhập Khách Hàng Đã Xác Thực từ NocoDB sang Brevo (SendinBlue)**

### **Giải pháp hoàn hảo cho các sếp quản lý marketing**
Hãy tưởng tượng một ngày không phải mất **giờ đồng hồ** để nhập liệu khách hàng mới từ bảng Excel/NocoDB sang Brevo (SendinBlue) thủ công. Hay phải lo lắng về **email tạm thời** gây lãng phí chi phí quảng cáo? **Workflow này tự động hóa toàn bộ quy trình**, đảm bảo chỉ những khách hàng **đầy đủ thông tin và email hợp lệ** mới được nhập vào Brevo, đồng thời **cập nhật trạng thái** trong NocoDB để theo dõi hiệu quả.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** nhập liệu thủ công.
- **Loại bỏ email tạm thời** (tăng CTR và giảm chi phí quảng cáo).
- **Danh sách email sạch** với thông tin đầy đủ (first_name, last_name, email).
- **Cập nhật tự động trạng thái** trong NocoDB để theo dõi tiến trình.
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản NocoDB** với:
   - **API Token** (tạo tại `Settings > API`).
   - **Bảng dữ liệu** chứa khách hàng mới với cột `status` (giá trị `0-not-imported` cho khách hàng chưa nhập).
   - **Cột bắt buộc**: `first_name`, `last_name`, `email`.
2. **Tài khoản Brevo (SendinBlue)** với:
   - **API Key** (tạo tại `Settings > API keys`).
3. **Workflow n8n** được cài đặt trên VPS hoặc n8n.cloud (nếu dùng phiên bản cloud).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7216) hoặc copy toàn bộ mã JSON từ đây.
- Mở **n8n Editor** → Nhấn `Import` → Chọn file JSON hoặc dán mã JSON vào ô `Import Workflow`.
- **Lưu workflow** với tên `Daily Import Contacts from NocoDB to Brevo`.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **9 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu hình Credentials**
- **NocoDB**:
  - Đi đến `Credentials` → Tạo mới `nocoDbApiToken`.
  - Nhập **API Token** từ NocoDB.
  - Thêm **URL API** của NocoDB (thường là `https://<tên-máy-chủ>.<domain>.noco.run`).
- **Brevo (SendinBlue)**:
  - Đi đến `Credentials` → Tạo mới `sendInBlueApi`.
  - Nhập **API Key** từ Brevo.

##### **B. Cấu hình Node "NocoDB: Get new users list"**
- **Tham số quan trọng**:
  - `Table Name`: Tên bảng chứa khách hàng (ví dụ: `customers`).
  - `Filter`: `status = 0-not-imported` (lọc chỉ khách hàng chưa nhập).
  - **Lưu ý**: Nếu bảng có tên khác, thay thế tương ứng.

##### **C. Cấu hình Node "Brevo: Create Contact"**
- **Tham số bắt buộc**:
  - `First Name`: `$node["NocoDB: Get new users list"]["json"]["first_name"]`.
  - `Last Name`: `$node["NocoDB: Get new users list"]["json"]["last_name"]`.
  - `Email`: `$node["NocoDB: Get new users list"]["json"]["email"]`.
  - **Lưu ý**: Đảm bảo các trường này trùng khớp với tên cột trong NocoDB.

##### **D. Cấu hình Node "Check if email is Disposal"**
- **Sử dụng API kiểm tra email tạm thời**:
  - Các sếp có thể kết nối với **API như Hunter.io, ZeroBounce, hoặc MailboxValidator** để xác thực email.
  - **Lưu ý**: Nếu không có API này, có thể sử dụng **regex** đơn giản để loại bỏ email tạm thời (ví dụ: `@mailinator.com`, `@tempmail.com`).

##### **E. Cấu hình Node "NocoDB: change status to X"**
- **Cập nhật trạng thái** sau mỗi bước:
  - `1-empty-fields`: Khi thiếu trường dữ liệu.
  - `2-disposal-email`: Khi email là tạm thời.
  - `3-contact-created`: Khi thành công nhập vào Brevo.
- **Tham số**:
  - `Record ID`: `$node["NocoDB: Get new users list"]["json"]["id"]`.
  - `Status`: Giá trị tương ứng (`1`, `2`, `3`).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn node `Schedule Trigger` → Nhấn `Run Workflow` để kiểm tra.
  - Kiểm tra **log** trong n8n để đảm bảo không có lỗi.
- **Bật Active**:
  - Đặt **Schedule Trigger** chạy hàng ngày (ví dụ: `0 0 * * *` = hàng ngày lúc 00:00).
  - Bật `Active` trên workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `Slack` hoặc `Telegram Bot` để báo cáo kết quả mỗi ngày (ví dụ: "Đã nhập 50 khách hàng mới").
2. **Lưu log vào Google Sheets**:
   - Sử dụng node `Google Sheets` để ghi lại lịch sử nhập liệu (giúp theo dõi hiệu quả).
3. **Xử lý lỗi tự động**:
   - Thêm node `Set` để lưu lại `error` vào NocoDB nếu nhập thất bại.
4. **Tối ưu hóa batch size**:
   - Nếu Brevo có giới hạn API, điều chỉnh `Batch Size` trong `splitInBatches` để tránh bị block.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập liệu mòn mỏi, đồng thời **nâng cao chất lượng danh sách email** bằng cách loại bỏ email tạm thời. **Hãy áp dụng ngay** và bắt đầu tự động hóa marketing của mình!

**Bắt đầu từ hôm nay, hãy để n8n làm việc thay bạn!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/7216)**
**📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**