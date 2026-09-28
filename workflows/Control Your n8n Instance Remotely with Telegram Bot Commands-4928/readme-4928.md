---
title: "🤖 **N8n Commander: Quản Lý n8n Trực Tuyến qua Telegram - Không Cần Code!**"
description: "Tự động hóa quản lý workflow n8n từ xa bằng Telegram: kích hoạt/ngừng, chạy, sao lưu, xóa lưu trữ... Tiết kiệm 100% thời gian admin với chỉ vài lệnh chat."
slug: "quan-ly-n8n-telegram-bot"
tags: [n8n, automation, devops, telegram-bot, remote-control, self-hosted]
keywords: [n8n workflow quản lý từ xa, tự động hóa n8n bằng telegram, backup workflow n8n, kích hoạt workflow n8n từ telegram, quản lý n8n không code]
---

# 🚀 **N8n Commander: Quản Lý n8n Trực Tuyến qua Telegram**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Kích hoạt/ngừng workflow** chỉ bằng 1 lệnh Telegram.
- **Chạy workflow từ xa** mà không cần vào UI n8n.
- **Sao lưu toàn bộ workflow + credentials** tự động.
- **Xóa lưu trữ cũ** để tiết kiệm dung lượng.
- **Nhận thông báo lỗi** khi workflow bị crash.
- **Liệt kê tất cả workflow** và lịch sử chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần vào UI n8n để quản lý, chỉ cần chat với bot Telegram.
✅ **Chính xác 100%**: Tránh sai sót khi kích hoạt/ngừng workflow thủ công.
✅ **An toàn**: Sao lưu tự động và xóa lưu trữ cũ để bảo vệ dữ liệu.
✅ **Hỗ trợ 24/7**: Nhận thông báo lỗi ngay khi workflow bị crash.
✅ **Dễ dàng mở rộng**: Thêm lệnh mới hoặc kết hợp với Slack/Email.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key của n8n**:
   - Tạo tại **Settings → n8n API** trong n8n Dashboard.
   - Lưu trữ an toàn vì chỉ hiện 1 lần.
2. **Bot Telegram**:
   - Tạo bot tại [@BotFather](https://t.me/BotFather) với lệnh `/newbot`.
   - Lấy **Chat ID** của mình (sử dụng [@userinfobot](https://t.me/userinfobot)).
3. **VPS Self-hosted** (n8n phải chạy trên máy chủ riêng).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4928](https://n8n.io/workflows/4928).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Workflow → Import** → Chọn file JSON.
  - Hoặc **copy/paste** JSON từ file vào **Create Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
- **n8n API**:
  - Tất cả node có `credentials: ["n8nApi"]` cần chọn **n8n API credential** mới tạo.
  - Điền **Server Address** (ví dụ: `http://localhost:5678` nếu chạy local, hoặc IP VPS nếu self-hosted).
- **Telegram API**:
  - Tất cả node có `credentials: ["telegramApi"]` cần chọn **Telegram API credential**.
  - Điền **Token Bot** và **Chat ID** của mình (để bot chỉ phản hồi với bạn).

#### **B. Cấu hình Telegram Trigger**
- Node **"Telegram Trigger"** phải được cấu hình:
  - **Credentials**: Chọn `telegramApi`.
  - **Chat ID**: Điền số điện thoại Telegram của bạn (ví dụ: `123456789`).
  - **Restrict to Chat IDs**: Điền lại số điện thoại để bot chỉ hoạt động với bạn.

#### **C. Cấu hình Workflow Name**
- Node **"List Workflows"** sẽ lấy danh sách tất cả workflow.
- Các node **"Find Workflow"** sẽ lọc workflow theo tên khi bạn gửi lệnh.

#### **D. Kích hoạt Backup (Nếu cần)**
- Node **"Backup Workflows"** và **"Backup Credentials"** sẽ tạo **tarball** của toàn bộ n8n.
- **Lưu ý an toàn**: File backup chứa **credentials đã giải mã**, nên lưu trên **ổ cứng an toàn** hoặc dịch vụ cloud như Google Drive.

---

### **3. Kích hoạt ⚡️**
1. **Test run** với lệnh mẫu:
   - Gửi `/help` trên Telegram để kiểm tra bot hoạt động.
   - Gửi `/workflows` để liệt kê tất cả workflow.
2. **Bật Active workflow** trong n8n Dashboard.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Lệnh cơ bản**
| Lệnh | Mô tả |
|------|--------|
| `/workflows` | Liệt kê tất cả workflow |
| `/execute [tên_workflow]` | Chạy workflow từ xa |
| `/activate [tên_workflow]` | Kích hoạt workflow |
| `/deactivate [tên_workflow]` | Ngừng workflow |
| `/executions [tên_workflow]` | Liệt kê lịch sử chạy |
| `/cleanup` | Xóa lưu trữ cũ |
| `/backup` | Sao lưu toàn bộ workflow + credentials |
| `/help` | Hiển thị danh sách lệnh |

### **2. Cách kết hợp với Slack/Email**
- Thay thế node **Telegram** bằng **Slack** hoặc **Email** trong các node phản hồi (`Executed`, `Activated`, `Error`).
- Cấu hình tại **Settings → Credentials** cho Slack/Email.

### **3. Lưu log hoạt động**
- Thêm node **ReadWriteFile** để ghi log vào file `.txt` trên VPS.
- Dùng lệnh `cat /path/to/log.txt` để xem lịch sử.

### **4. Tự động xóa lưu trữ cũ**
- Cấu hình **cron job** trên VPS để chạy `/cleanup` định kỳ (ví dụ: hàng tháng).

---

## 📌 **Kết luận**
**N8n Commander** là công cụ **miễn phí, không cần code** giúp các sếp quản lý n8n từ xa một cách **tiện lợi và an toàn**. Từ **kích hoạt workflow** đến **sao lưu dữ liệu**, tất cả chỉ cần **những lệnh Telegram đơn giản**.

👉 **Hãy import ngay và thử nghiệm!** Nếu có vấn đề, hãy comment bên dưới hoặc liên hệ admin n8n cho hỗ trợ.

---
**#n8n #Automation #DevOps #TelegramBot #SelfHosted**