---
title: "🚀 Tự Động Hóa Theo Dõi Proxmox VE: Báo Cáo VM, Tài Nguyên & Nhiệt Độ qua Telegram Mỗi 15 Phút"
description: "Workflow tự động hóa theo dõi trạng thái VM, tài nguyên máy chủ và nhiệt độ Proxmox VE, gửi báo cáo định kỳ qua Telegram để các sếp quản lý hiệu quả, tiết kiệm thời gian và phát hiện vấn đề sớm."
slug: "tieu-dong-hoa-theo-doi-proxmox-ve-telegram"
tags: [n8n, automation, proxmox, monitoring, telegram, ssh, api]
keywords: [tự động hóa proxmox, theo dõi vm status, báo cáo tài nguyên máy chủ, nhiệt độ server, telegram alert, n8n workflow]
---

# 🚀 **Tự Động Hóa Theo Dõi Proxmox VE: Báo Cáo VM, Tài Nguyên & Nhiệt Độ qua Telegram**

### **Giải pháp cho các sếp quản trị server:**
Hàng ngày, các sếp phải theo dõi **trạng thái VM, tài nguyên CPU/Memory, nhiệt độ máy chủ và lịch sử sự kiện** trên Proxmox VE một cách thủ công. Điều này không chỉ tốn thời gian mà còn dễ bỏ sót những vấn đề như **VM bị treo, nhiệt độ quá cao hoặc tài nguyên bị quá tải**. **Workflow này tự động hóa toàn bộ quy trình**, gửi báo cáo chi tiết qua **Telegram mỗi 15 phút**, giúp các sếp **quản lý hiệu quả, phát hiện sự cố sớm và tối ưu hóa hiệu suất**.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng ngày.
- **Phát hiện sự cố sớm**: Nhận cảnh báo về **VM bị treo, nhiệt độ quá cao, tài nguyên CPU/Memory quá tải**.
- **Báo cáo chi tiết**: Dữ liệu **VM đang chạy/ngừng**, **tài nguyên sử dụng**, **nhiệt độ sensor**, và **lịch sử sự kiện** được tổng hợp trong một báo cáo HTML.
- **Hoạt động 24/7**: Workflow chạy tự động mỗi 15 phút, không phụ thuộc vào thời gian làm việc.
- **Cá nhân hóa thông báo**: Gửi qua **Telegram** với định dạng HTML đẹp mắt, dễ đọc.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Thông tin Proxmox**:
   - **IP/Mã máy chủ Proxmox** (ví dụ: `192.168.1.100`).
   - **Port Proxmox** (thường là `8006`).
   - **Tên Node Proxmox** (ví dụ: `pve`).
   - **Tài khoản Proxmox** (định dạng: `username@realm`, ví dụ: `root@pam`).
   - **Mật khẩu Proxmox**.

2. **Thiết lập SSH**:
   - **lm-sensors** phải được cài đặt trên máy chủ Proxmox (để đọc nhiệt độ).
   - **Credentials SSH** trong n8n (điền **IP, Port, Username, Password** của Proxmox).

3. **Telegram Bot**:
   - Tạo **bot Telegram** qua [@BotFather](https://t.me/BotFather).
   - Lấy **Token API** của bot và thêm vào **credentials "telegramApi"** trong n8n.
   - **Chat ID** của bot (có thể lấy bằng cách gửi tin nhắn cho bot và copy link URL).

4. **Hệ thống n8n**:
   - Workflow chạy trên **n8n Self-hosted** (không dùng phiên bản cloud).
   - **VPS 4GB RAM** (để chạy ổn định 24/7).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9733](https://n8n.io/workflows/9733).
- Trong **n8n Editor**, chọn **Import Workflow** và chọn file JSON đã tải.
- **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **11 node**, các sếp cần **cấu hình chính xác** các node sau:

##### **A. Node "Set Variables" (Thiết lập biến)**
- **Tham số cần điền**:
  - `PROXMOX_IP`: IP của máy chủ Proxmox (ví dụ: `192.168.1.100`).
  - `PROXMOX_PORT`: Port Proxmox (thường `8006`).
  - `PROXMOX_NODE`: Tên node Proxmox (ví dụ: `pve`).
  - `PROXMOX_USERNAME`: Tài khoản Proxmox (định dạng `username@realm`, ví dụ: `root@pam`).
  - `PROXMOX_PASSWORD`: Mật khẩu Proxmox.
  - `TELEGRAM_CHAT_ID`: Chat ID của bot Telegram (lấy từ link URL khi gửi tin nhắn cho bot).

##### **B. Node "Proxmox Login" (Đăng nhập Proxmox)**
- **Method**: `POST`
- **URL**: `https://{PROXMOX_IP}:{PROXMOX_PORT}/api2/json/access/ticket`
- **Headers**:
  - `Content-Type: application/json`
- **Body**:
  ```json
  {
    "username": "{{ $node["Set Variables"].json["PROXMOX_USERNAME"] }}",
    "password": "{{ $node["Set Variables"].json["PROXMOX_PASSWORD"] }}"
  }
  ```
  *(Sử dụng biến từ node "Set Variables")*

##### **C. Node "SSH - Get Sensors" (Đọc nhiệt độ)**
- **Credentials**: Chọn `sshPassword` (đã cấu hình trước).
- **Command**: `sensors`
- **Host**: `{{ $node["Set Variables"].json["PROXMOX_IP"] }}`
- **Port**: `22` (mặc định)
- **Username**: `root` (hoặc tài khoản SSH của Proxmox)
- **Password**: Điền mật khẩu SSH (nếu không dùng key).

##### **D. Node "Telegram" (Gửi báo cáo)**
- **Credentials**: Chọn `telegramApi` (đã thêm Token API).
- **Chat ID**: Điền `{{ $node["Set Variables"].json["TELEGRAM_CHAT_ID"] }}`.
- **Message**: Dữ liệu từ node "Generate Formatted Message" (sẽ được xử lý trong node Code).

##### **E. Node "Process Data" & "Generate Formatted Message" (Xử lý & Định dạng)**
- **Không cần chỉnh sửa** (n8n tự động xử lý logic từ code đã viết).
- **Node Code** sử dụng JavaScript để:
  - Tách dữ liệu từ API Proxmox.
  - Xử lý nhiệt độ từ SSH.
  - Định dạng báo cáo HTML cho Telegram.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và kiểm tra kết quả trong **Telegram**.
   - Nếu có lỗi, kiểm tra lại **credentials** và **URL API**.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - Workflow sẽ chạy **mỗi 15 phút** theo lịch trình.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm cảnh báo Slack**:
   - Sử dụng **node Slack** để gửi báo cáo cùng Telegram.
   - Cấu hình **webhook Slack** trong node `httpRequest`.

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử báo cáo.
   - Dùng node **Code** để định dạng dữ liệu trước khi lưu.

3. **Cảnh báo email cho admin**:
   - Kết hợp với **node Email** (Gmail/SMTP) để gửi báo cáo khi phát hiện sự cố.

4. **Tự động khắc phục VM bị treo**:
   - Sử dụng **node SSH** để chạy lệnh `pvesh` để khởi động lại VM tự động nếu bị treo.

5. **Báo cáo định kỳ qua Email**:
   - Thêm node **ScheduleTrigger** chạy hàng ngày (ví dụ: 8h sáng) để gửi báo cáo tổng hợp qua Email.
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản trị Proxmox VE, giúp **tự động hóa theo dõi VM, tài nguyên và nhiệt độ**, đồng thời **gửi báo cáo chi tiết qua Telegram mỗi 15 phút**. **Không cần code**, chỉ cần **cấu hình đúng credentials**, workflow sẽ hoạt động 24/7, giúp các sếp **tiết kiệm thời gian và phát hiện sự cố sớm**.

👉 **Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy ổn định).
2. **Import workflow** và **cấu hình credentials** theo hướng dẫn.
3. **Bật Active** và **nhận báo cáo tự động** mỗi 15 phút!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::