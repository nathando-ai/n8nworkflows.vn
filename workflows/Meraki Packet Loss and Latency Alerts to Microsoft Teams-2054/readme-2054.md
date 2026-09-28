---
title: "🚀 Tự động cảnh báo Packet Loss & Latency từ Cisco Meraki lên Microsoft Teams bằng n8n"
description: "Xây dựng hệ thống giám sát mạng tự động từ Cisco Meraki, lọc lỗi packet loss/latency, chống spam thông báo bằng Redis và gửi cảnh báo trực tiếp qua Microsoft Teams."
slug: "tu-dong-canh-bao-meraki-microsoft-teams-n8n"
tags: [n8n, automation, cisco-meraki, microsoft-teams, redis, it-ops]
keywords: [n8n workflow, meraki monitoring, packet loss alert, microsoft teams integration, redis deduplication, it ops automation]
---

# 🚀 Tự động cảnh báo Packet Loss & Latency từ Cisco Meraki lên Microsoft Teams

Các sếp làm trong ngành IT Ops hoặc SecOps chắc chắn đã quá quen thuộc với cảm giác đau đầu khi hệ thống mạng gặp sự cố rớt gói tin (packet loss) hay độ trễ cao (latency). Việc ngồi dán mắt vào dashboard của Cisco Meraki 24/7 là bất khả thi, còn nếu không cấu hình cảnh báo khéo léo, anh em kỹ thuật sẽ bị "ngập lụt" trong hàng trăm tin nhắn spam mỗi khi mạng chập chờn.

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó! Nó tự động hóa hoàn toàn quy trình: **Lấy dữ liệu từ Meraki ➡️ Phân tích & Lọc ngưỡng cảnh báo ➡️ Kiểm tra trùng lặp qua Redis (tránh spam) ➡️ Bắn thông báo thông minh qua Microsoft Teams kèm log thời gian thực**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với Redis cũng như các API bên ngoài, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát tự động 24/7:** Định kỳ quét thông tin Uplink (Loss & Latency) của tất cả các tổ chức và thiết bị mạng Meraki.
- **Chống spam thông minh:** Sử dụng Redis để lưu trạng thái cảnh báo với TTL (Time-to-Live) 3 tiếng. Nếu lỗi chưa được khắc phục sau 3 tiếng, hệ thống mới gửi tin nhắn nhắc lại.
- **Cảnh báo trúng đích:** Chỉ lọc các site thực sự có vấn đề vượt ngưỡng (ví dụ: độ trễ > 300ms và packet loss > 2%).
- **Tương tác nhanh chóng:** Tin nhắn gửi lên Microsoft Teams có sẵn Direct Link (Hyperlink) dẫn thẳng tới cấu hình thiết bị Meraki đang gặp sự cố.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Bản Self-hosted hoặc Cloud).
- **Cisco Meraki Dashboard API Key** (Tạo key trong phần cài đặt tài khoản Meraki).
- **Redis Database** (Dùng để cache và chống spam thông báo).
- **Microsoft Teams Incoming Webhook** hoặc cấu hình **Microsoft Teams Node** trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n (Template ID: 2054) hoặc copy đoạn JSON tương ứng và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia làm 3 phần chính, các sếp cần chú ý cấu hình các node sau:

* **Phần 1: Thu thập dữ liệu (Pulling in Info)**
  - **Get Meraki Organizations** & **Get Uplink Loss and Latency** (`httpRequest`): Cần cấu hình **Credentials** dạng `httpHeaderAuth` với header `X-Cisco-Meraki-API-Key` chứa API Key của các sếp và header `Accept: application/json`.
  - **Schedule Trigger**: Thiết lập chu kỳ chạy mong muốn (ví dụ: chạy mỗi 5 phút hoặc 10 phút).

* **Phần 2: Xử lý & Lọc dữ liệu (Changing data)**
  - **Filters Problematic sites** (`code` - JavaScript node): Mặc định script đang lọc các site có độ trễ trên **300ms** và packet loss trên **2%**. Các sếp có thể tùy chỉnh ngưỡng này trong đoạn code JavaScript cho phù hợp với hạ tầng thực tế của công ty.
  - **Average Latency & Loss over 5m** (`code`): Gom nhóm và tính trung bình các mốc thời gian để tránh báo động giả do nhiễu tức thời.

* **Phần 3: Xử lý chống spam và Gửi thông báo (Notify)**
  - **Check if Alert Exists** & **Log the Alert** (`redis`): Kết nối tới Redis Server của các sếp để kiểm tra key theo tên Network. Node Log sẽ tự động gán TTL là **3 tiếng (3h)** để tránh việc cứ mỗi 5 phút lại bắn một tin nhắn Teams gây phiền toái.
  - **Message Techs** (`microsoftTeams`): Điền thông tin Chat/Channel ID đích trên Microsoft Teams để nhận tin nhắn cảnh báo. Nội dung tin nhắn đã được viết sẵn kèm hyperlink dẫn trực tiếp tới trang quản trị Meraki của site lỗi.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** chạy thử thủ công với nút `When clicking "Execute Workflow"` để kiểm tra luồng dữ liệu từ Meraki.
- Kiểm tra kết quả trên Microsoft Teams và Redis.
- Bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay thế Teams bằng PSA Ticketing:** Nếu đội ngũ IT của các sếp sử dụng các hệ thống quản lý sự cố như ConnectWise Manage, Jira Service Management hoặc ServiceNow, các sếp có thể thay thế node Microsoft Teams bằng HTTP Request gọi API tạo ticket tự động.
- **Mở rộng kênh nhận tin:** Có thể kết hợp thêm node Telegram hoặc Slack để gửi cảnh báo song song cho đội ngũ quản lý cấp cao.
- **Giám sát Redis:** Đảm bảo Redis server có cấu hình lưu trữ (persistence) ổn định để không bị mất state khi khởi động lại.

### 📌 Kết luận
Workflow Meraki Packet Loss and Latency Alerts to Microsoft Teams là một giải pháp "nhỏ mà có võ", giúp tự động hóa khâu giám sát hạ tầng mạng cốt lõi mà không cần viết code phức tạp. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa thời gian xử lý sự cố mạng nhé!