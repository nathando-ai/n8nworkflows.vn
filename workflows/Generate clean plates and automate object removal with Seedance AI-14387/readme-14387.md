---
title: "🚀 Tự động hóa tạo Clean Plate & Xóa vật thể VFX bằng AI với n8n và Seedance"
description: "Hướng dẫn cấu hình workflow n8n giúp tự động hóa quá trình tạo clean plate cho dự án VFX, tích hợp Seedance AI, Google Drive, Notion và Slack/Telegram."
slug: "tu-dong-hoa-tao-clean-plate-vfx-voi-seedance-ai-n8n"
tags: [n8n, automation, vfx, seedance-ai, google-drive, slack]
keywords: [n8n workflow, tự động hóa vfx, clean plate ai, seedance ai, n8n telegram slack]
---

# 🚀 Tự động hóa tạo Clean Plate & Xóa vật thể VFX với Seedance AI

Trong quy trình sản xuất kỹ xảo (VFX), việc tạo ra các *clean plate* (khung hình nền sạch không có diễn viên hoặc vật thể) thường ngốn rất nhiều thời gian của các nghệ sĩ Paint và Comp. Quy trình thủ công này đòi hỏi nhiều công đoạn rườm rà và dễ gây chậm trễ tiến độ dự án.

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n toàn diện, tự động hóa hoàn toàn quy trình nhận yêu cầu, gọi AI render, kiểm tra chất lượng (QC), lưu trữ file và thông báo cho đội ngũ kỹ thuật mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 4 luồng render song song:** Tạo ra primary clean plate, bản thay thế, pass xóa tiền cảnh và difference map chỉ bằng một yêu cầu qua Webhook.
- **Kiểm tra chất lượng thông minh (QC):** Tự động chấm điểm các pass theo ngưỡng cài đặt, tự động tạo script Nuke sẵn sàng cho họa sĩ comp.
- **Đồng bộ dữ liệu tập trung:** Tự động lưu video kết quả lên Google Drive và ghi log chi tiết vào Notion database.
- **Thông báo thời gian thực:** Gửi báo cáo chi tiết kèm link và điểm số QC trực tiếp qua Slack và Telegram cho team Paint/Comp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt phiên bản n8n (Self-hosted hoặc Cloud).
- **Seedance AI API Key:** Tài khoản và API key dịch vụ render video của Seedance.
- **Google Drive:** Tài khoản Google với OAuth2 Credentials đã cấu hình.
- **Notion Integration:** Notion API Key và một Database được thiết lập sẵn để lưu log.
- **Slack & Telegram Bot:** Slack App/Token và Telegram Bot Token để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ kho lưu trữ n8n (Link gốc: [Seedance AI Clean Plate Generator](https://n8n.io/workflows/14387)) và thực hiện import trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để workflow nhận diện đúng hệ thống:

- **Webhook: Clean Plate Request:** Sao chép URL từ node này và tích hợp vào công cụ quản lý shot hoặc script pipeline của các sếp để gửi request dạng POST chứa (`plateImageUrl`, `removalBrief`, `shotCode`).
- **Seedance API (Nodes: `Seedance: Generate Clean Pass`, `Poll: Check Job Status`):** Cập nhật Header `Authorization` bằng Seedance API Key chính chủ thông qua n8n Credentials.
- **Google Drive: Upload Clean Plate:** Kết nối credential Google Drive OAuth2 và điền ID thư mục đích (Folder ID) trên Drive để lưu trữ video.
- **Create a database page (Notion):** Kết nối Notion API và chọn đúng Database ID chuyên dùng quản lý log clean plate.
- **Slack & Telegram (Nodes thông báo):** Kết nối tài khoản Slack/Telegram, sau đó cấu hình lại `Channel ID` hoặc `Chat ID` cho đúng nhóm làm việc của team VFX.
- **Ngưỡng QC (`qcThreshold`):** Mặc định là `0.85` (từ 0 đến 1), có thể truyền trực tiếp trong payload của webhook để tinh chỉnh độ nhạy tự động phê duyệt.

#### 3. Kích hoạt ⚡️
- Thực hiện test thử bằng cách bắn một POST request mẫu qua Postman hoặc script nội bộ vào Webhook URL.
- Kiểm tra kết quả trả về ở từng node, sau đó gạt công tắc sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kho lưu trữ:** Có thể bổ sung thêm node lưu trữ phụ như Airtable hoặc AWS S3 bên cạnh Notion và Google Drive.
- **Tích hợp Jira / ShotGrid (Flow):** Tự động chuyển trạng thái task trên hệ thống quản lý dự án (Jira/ShotGrid) sang "Review" ngay khi QC thành công.
- **Xử lý lỗi thông minh:** Đã có sẵn Error Trigger gắn với Slack Error Alert, giúp các sếp phát hiện ngay lập tức nếu API bên thứ ba gặp sự cố.

### 📌 Kết luận
Workflow tự động hóa tạo Clean Plate kết hợp Seedance AI này sẽ giải phóng toàn bộ thời gian cho team Paint/Comp khỏi các công đoạn lặp đi lặp lại. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất cho studio VFX của các sếp!