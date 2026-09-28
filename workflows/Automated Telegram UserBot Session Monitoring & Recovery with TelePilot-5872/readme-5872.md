---
title: "🚀 Tự động giám sát & khôi phục phiên Telegram UserBot với TelePilot"
description: "Giải pháp n8n giám sát liên tục trạng thái phiên Telegram UserBot, tự động khởi động lại khi bị ngắt, giảm downtime và không cần viết code."
slug: "tu-dong-giam-sat-khoi-phuc-phien-telegram-userbot-telepilot"
tags: [n8n, automation, no-code, telegram, telepilot, devops]
keywords: [n8n workflow, tự động hóa telegram, TelePilot, giám sát phiên, bot]
---

# 🚀 Tự động giám sát & khôi phục phiên Telegram UserBot với TelePilot

Khi các **sếp** vận hành Telegram UserBot, việc mất kết nối hoặc phiên bị đóng bất ngờ là nỗi ám ảnh lớn: phải dừng công việc, mất thời gian đăng nhập lại, thậm chí mất dữ liệu quan trọng.  
Workflow này sẽ **giám sát 24/7** trạng thái phiên Telegram, tự động dừng/kết nối lại và thông báo ngay qua Telegram khi có sự cố – **không cần một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Giảm downtime**: Phiên bị ngắt sẽ tự động khởi động lại trong vòng vài giây.  
- **Tiết kiệm thời gian**: Không còn phải đăng nhập lại thủ công, mọi thao tác được tự động hoá.  
- **Thông báo tức thời**: Nhận tin nhắn Telegram ngay khi có lỗi hoặc khi phiên đã được khôi phục.  
- **Hoạt động liên tục**: Workflow chạy nền 24/7, luôn sẵn sàng giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản TelePilot**: API key (`telePilotApi`) để gọi các endpoint login, logout.  
- **Telegram Bot**: Bot token (`telegramApi`) để gửi tin nhắn thông báo.  
- **Telegram User Credential**: `apiId`, `apiHash`, `phoneNumber` đã được cấu hình trong **Chat Trigger** của TelePilot.  
- **n8n** (phiên bản mới nhất) được cài đặt trên server hoặc Docker.  
- **Kết nối internet ổn định** cho cả n8n và TelePilot.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc https://n8n.io/workflows/5872).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → Nhấn **Import**.  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|-------------------|
| **When chat message received** (`chatTrigger`) | Nhận lệnh từ người dùng qua Telegram. | Chọn **Credentials** → `telePilotApi`. Đảm bảo **Chat ID** trùng với bot Telegram của bạn. |
| **Schedule Trigger** | Kiểm tra trạng thái phiên định kỳ (mặc định mỗi 5 phút). | Điều chỉnh **Cron** nếu muốn tần suất khác. |
| **Stop auth** / **Start auth** / **Manual control** / **Automatic control** (`telePilot`) | Gọi API TelePilot để dừng, khởi động, hoặc chuyển đổi chế độ điều khiển. | Chọn **Credentials** → `telePilotApi`. Đảm bảo **resource** = `login`. |
| **Get Session Status** (`set`) | Đặt biến `sessionStatus` dựa trên kết quả trả về từ TelePilot. | Không cần thay đổi, chỉ kiểm tra trường dữ liệu `status`. |
| **Stop Session** (`set`) | Đánh dấu trạng thái “stopped”. | Kiểm tra giá trị `sessionAction = "stop"`. |
| **Start Session** (`set`) | Đánh dấu trạng thái “started”. | Kiểm tra giá trị `sessionAction = "start"`. |
| **Pass on Closed Status** (`filter`) | Lọc ra các phiên đã đóng. | Điều kiện: `sessionStatus == "closed"`. |
| **Send Closed Status message** (`telegram`) | Gửi tin nhắn thông báo phiên đã đóng. | Chọn **Credentials** → `telegramApi`. Nội dung mẫu: `🚨 Phiên Telegram đã bị đóng! Đang thực hiện khởi động lại…`. |
| **Check Session Connection** (`filter`) | Kiểm tra kết nối hiện tại (online/offline). | Điều kiện: `sessionStatus == "online"` hoặc `offline`. |
| **Send Session Connection message** (`telegram`) | Thông báo trạng thái kết nối hiện tại. | Chọn **Credentials** → `telegramApi`. Nội dung mẫu: `✅ Phiên Telegram đang hoạt động bình thường.` |

> **Lưu ý quan trọng:**  
> - Đảm bảo **Credentials** cho TelePilot và Telegram đều **được kích hoạt** (đánh dấu “Active”).  
> - Kiểm tra lại **API URL** trong `telePilotApi` (địa chỉ endpoint TelePilot của bạn).  
> - Nếu muốn thay đổi lệnh chat, chỉnh sửa **Sticky Note** trên canvas hoặc cập nhật phần “Supported Commands” trong node `When chat message received`.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** một lần để kiểm tra luồng dữ liệu mẫu.  
2. Kiểm tra log trong **Execution Overview** – mọi node phải trả về **Success**.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy theo lịch và phản hồi lệnh chat.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack**: Thêm node Slack để gửi thông báo song song cho đội DevOps.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại lịch sử các lần khởi động/đóng phiên, tiện cho audit.  
- **Báo cáo định kỳ**: Sử dụng node **Email** hoặc **Telegram** để gửi báo cáo tổng hợp mỗi ngày/tuần về trạng thái phiên.  
- **Mở rộng lệnh**: Thêm các lệnh `/stats`, `/restartAll` để quản lý nhiều UserBot cùng lúc.

### 📌 Kết luận
Với workflow **Automated Telegram UserBot Session Monitoring & Recovery**, các sếp sẽ không còn lo lắng về việc mất kết nối bất ngờ của UserBot nữa. Hệ thống tự động giám sát, khởi động lại và thông báo ngay lập tức, giúp duy trì **hiệu suất tối đa** và **tiết kiệm thời gian**. Hãy triển khai ngay hôm nay, để bot của bạn luôn “online” và sẵn sàng phục vụ! 🚀