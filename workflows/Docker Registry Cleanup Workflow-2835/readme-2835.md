---
title: "🧹 Tự động hóa dọn dẹp Docker Registry và giải phóng dung lượng ổ cứng với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động liệt kê, lọc, xóa các Docker image tag cũ và thực thi garbage collection trên Docker Registry, giúp tiết kiệm dung lượng VPS."
slug: "docker-registry-cleanup-workflow-n8n"
tags: [n8n, automation, devops, docker, registry, cleanup]
keywords: [n8n workflow, docker registry cleanup, tự động hóa devops, dọn dẹp docker image, quản lý docker registry]
keywords: [n8n workflow, docker registry cleanup, tự động hóa devops, dọn dẹp docker image, quản lý docker registry]
---

# 🧹 Tự động hóa dọn dẹp Docker Registry và giải phóng dung lượng ổ cứng với n8n

Các sếp làm kỹ thuật (DevOps, SysAdmin) chắc hẳn đã quá quen thuộc với cảm giác đau đầu khi dung lượng ổ cứng trên VPS/Server cứ đầy dần lên chỉ vì các Docker image cũ cứ liên tục được đẩy (push) lên Private Registry mà không được dọn dẹp. Việc ngồi kiểm tra thủ công từng tag, gọi API xóa manifest rồi chạy lệnh garbage collection vừa mất thời gian lại vừa dễ sót.

Để giải quyết triệt để vấn đề này, workflow **Docker Registry Cleanup Workflow** ra đời giúp tự động hóa toàn bộ quy trình: từ việc lấy danh sách image, lọc các tag cũ theo chiến lược, tiến hành xóa qua Docker Registry API, kích hoạt garbage collection qua SSH và cuối cùng là gửi báo cáo qua Email cho các sếp. Hoàn toàn tự động 100% không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giải phóng dung lượng tự động:** Không bao giờ còn tình trạng ổ cứng VPS bị đầy bất ngờ do Docker Registry phình to.
- **Tùy biến thông minh:** Dễ dàng cấu hình giữ lại số lượng bản dựng (builds) mới nhất hoặc xóa các tag theo thời gian.
- **Hoạt động định kỳ:** Chạy tự động theo lịch (ví dụ: hàng tuần, hàng tháng) nhờ Scheduled Trigger.
- **Báo cáo minh bạch:** Gửi email thông báo chi tiết danh sách các image/tag đã bị xóa hoặc cảnh báo ngay lập tức nếu có lỗi xảy ra trong quá trình thực thi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Docker Registry:** Đang chạy một Private Docker Registry (hỗ trợ HTTP API v2).
- **SSH Access:** Thông tin đăng nhập SSH vào server đang chạy Docker Registry (để chạy lệnh garbage collection).
- **Email Credentials:** Tài khoản SMTP (Gmail, SendGrid, Resend,...) để nhận email báo cáo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n template (ID: 2835) hoặc copy toàn bộ mã nguồn JSON của workflow và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 16 nodes kết hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình chính xác các điểm sau:

- **Scheduled Trigger:** Cài đặt lịch chạy tự động (ví dụ: chạy vào 02:00 sáng Chủ Nhật hàng tuần để tránh ảnh hưởng hệ thống).
- **List Images & Retrieve Image Tags (HTTP Request Nodes):** Cấu hình URL của Docker Registry (ví dụ: `https://registry.domain.com:5000/v2/_catalog`) cùng với thông tin xác thực (Basic Auth nếu registry của các sếp có bảo vệ bằng mật khẩu).
- **Extract Image Names & Identify Tags to Remove (Code Nodes):** Tùy chỉnh đoạn code JavaScript bên trong các node này nếu các sếp muốn thay đổi logic giữ lại bao nhiêu tag gần nhất (mặc định script sẽ lọc và xác định các tag cũ cần dọn dẹp).
- **Remove Old Tags & Fetch Manifest Digest (HTTP Request Nodes):** Gửi yêu cầu lấy Digest và tiến hành xóa manifest của các tag cũ theo chuẩn API của Docker Registry.
- **Execute Garbage Collection (SSH Node):** Cấu hình thông tin SSH (Host, Port, Username, Private Key/Password) trỏ tới server chạy Registry và điền câu lệnh dọn dẹp rác, ví dụ: `docker exec -it <registry-container-name> bin/registry garbage-collect /etc/docker/registry/config.yml`.
- **Send Notification Email & Send Failure Notification Email (Email Send Nodes):** Điền thông tin SMTP của các sếp để nhận thông báo thành công hoặc cảnh báo thất bại.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test chạy thử với dữ liệu thực tế và kiểm tra xem các tag cũ có được liệt kê chính xác không.
- Sau khi kiểm tra mọi thứ trơn tru, các sếp gạt công tắc sang **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp ChatOps:** Thay vì chỉ nhận thông báo qua Email, các sếp có thể thay thế hoặc bổ sung node `Slack` hoặc `Telegram` để bắn tin nhắn báo cáo trực tiếp vào group chat của team DevOps.
- **Lưu Log vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử các lần dọn dẹp (tên image, tag đã xóa, thời gian, dung lượng giải phóng ước tính) nhằm dễ dàng kiểm toán về sau.
- **Whitelist tag quan trọng:** Bổ sung logic lọc trong node Code để bỏ qua các tag quan trọng như `latest`, `production`, hoặc các tag bắt đầu bằng `v*` nhằm tránh vô tình xóa mất các bản release chính thức.

### 📌 Kết luận
Docker Registry Cleanup Workflow là một công cụ cực kỳ hữu ích giúp tự động hóa khâu vận hành hạ tầng, tiết kiệm chi phí lưu trữ và giữ cho hệ thống luôn gọn gàng, sạch sẽ. Hãy cài đặt ngay hôm nay để tối ưu hóa không gian server của các sếp nhé!