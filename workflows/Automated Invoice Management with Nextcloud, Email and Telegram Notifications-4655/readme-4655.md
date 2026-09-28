---
title: "🚀 Quản Lý Hóa Đơn Tăng Động với Nextcloud, Email & Telegram"
description: "Tự động lấy, gửi và lưu trữ hóa đơn PDF từ Nextcloud, gửi email và thông báo Telegram, giúp doanh nghiệp tiết kiệm thời gian và giảm lỗi."
slug: "quan-ly-hoa-don-tang-dien-voi-nextcloud-email-telegram"
tags: [n8n, automation, no-code, finance, nextcloud, telegram, email]
keywords: [n8n workflow, tự động hóa, quản lý hóa đơn, Nextcloud, Telegram, email, invoice]
---

# 🚀 Quản Lý Hóa Đơn Tăng Động với Nextcloud, Email & Telegram

Bạn đang phải lướt qua hàng trăm tệp PDF, gửi chúng qua email, lưu lại và nhớ lại lịch sử?  
Workflow này sẽ **đánh bại** những công việc thủ công đó, tự động lấy tệp từ Nextcloud, gửi email, gửi thông báo Telegram và lưu trữ ngay trong cùng một chuỗi hành động 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lấy và gửi hóa đơn, không cần thao tác thủ công.  
- **Chính xác 100%**: Không còn sai sót khi nhập dữ liệu hoặc gửi tệp.  
- **Lưu trữ an toàn**: Tất cả tệp được di chuyển sang thư mục lưu trữ tự động.  
- **Công việc liên tục**: Chạy theo lịch (ví dụ: hàng ngày lúc 9:00) mà không cần can thiệp.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / API | Mô tả | Credential cần thiết |
|---|---|---|
| **Nextcloud** | Lưu trữ và truy xuất tệp PDF | `nextCloudApi` (URL, username, password / token) |
| **SMTP** | Gửi email | `smtp` (host, port, username, password) |
| **Telegram Bot** | Gửi thông báo | `telegramApi` (bot token, chat ID) |
| **n8n** | Chạy workflow | Đăng ký tài khoản n8n (hoặc tự host) |

> **Lưu ý**: Đảm bảo các thư mục `/Invoice/2025` và `/Invoice/Archive/2025` đã tồn tại trong Nextcloud.

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ trang gốc: <https://n8n.io/workflows/4655>.  
2. Trong n8n Editor, chọn **Import** → **Import from file** → chọn file JSON.  
3. Hoặc copy toàn bộ JSON và dán vào **Raw JSON** trong tab **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Mô tả | Tham số cần cấu hình |
|---|---|---|---|
| **Start** | `scheduleTrigger` | Lên lịch chạy workflow | *Chọn thời gian* (ví dụ: `09:00` hàng ngày) |
| **Set Parameters** | `set` | Đặt các biến cần dùng (đường dẫn, email, chat ID) | `nextcloud_income` = `/Invoice/2025` <br> `email_recipient` = `invoice@example.com` <br> `telegram_chat_id` = `@yourchatid` |
| **List Incoming Invoices** | `nextCloud` (list) | Liệt kê tệp trong thư mục | `path` = `={{ $json.nextcloud_income }}` |
| **File Exists?** | `if` | Kiểm tra có tệp nào không | *Chọn điều kiện* `{{ $json.length > 0 }}` |
| **Download Invoice** | `nextCloud` (download) | Tải tệp PDF | `path` = `={{ $json.path }}` |
| **Send Email** | `emailSend` | Gửi email kèm tệp | `to` = `={{ $json.email_recipient }}` <br> `attachments` = `{{ $json.downloadedFile }}` |
| **Archive File** | `nextCloud` (move) | Di chuyển tệp sang thư mục lưu trữ | `path` = `={{ $('Download Invoice').item.json.path }}` <br> `destination` = `/Invoice/Archive/2025` |
| **Notify Telegram** | `telegram` | Gửi tin nhắn thông báo | `chatId` = `={{ $json.telegram_chat_id }}` <br> `text` = `"✅ Hóa đơn {{ $json.filename }} đã được gửi và lưu trữ"` |

> **Tip**: Nếu workflow có nhiều tệp trong thư mục, hãy sử dụng **SplitInBatches** hoặc **Loop** để xử lý từng tệp một.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo tệp PDF có trong thư mục).  
2. Kiểm tra email và Telegram đã nhận tin.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi báo cáo tuần**: Thêm node `scheduleTrigger` khác chạy vào cuối tuần, tổng hợp số lượng hóa đơn đã xử lý và gửi email báo cáo.  
- **Lưu log**: Sử dụng node `writeBinaryFile` để ghi log vào Nextcloud hoặc gửi log tới Slack.  
- **Cảnh báo khi lỗi**: Thêm node `if` kiểm tra lỗi, gửi thông báo Telegram kèm chi tiết lỗi.  
- **Tích hợp với Zapier**: Khi tệp được lưu trữ, trigger Zapier để cập nhật bảng tính Google Sheets.  

## 📌 Kết luận

Workflow “Automated Invoice Management with Nextcloud, Email and Telegram Notifications” là giải pháp hoàn hảo cho các doanh nghiệp nhỏ và vừa muốn **tự động hóa quy trình quản lý hóa đơn** mà không cần viết mã.  
Hãy tải, cấu hình và bật nó lên ngay hôm nay – bạn sẽ thấy thời gian làm việc giảm gấp đôi, sai sót giảm 100% và công việc trở nên minh bạch hơn bao giờ hết.  

**Các sếp, hãy áp dụng ngay và cảm nhận sự khác biệt!**