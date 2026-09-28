---
title: "🚀 Tự động tạo Snapshot VPS Hostinger và gửi báo cáo qua WhatsApp mỗi ngày"
description: "Hướng dẫn thiết lập workflow n8n tự động sao lưu VPS Hostinger, kiểm tra thông số tài nguyên và gửi thông báo trạng thái qua WhatsApp với Evolution API."
slug: "tu-dong-tao-snapshot-vps-hostinger-va-gui-bao-cao-whatsapp"
tags: [n8n, automation, devops, hostinger, whatsapp, vps, backup]
keywords: [n8n workflow, hostinger vps snapshot, tu dong backup vps, evolution api whatsapp, devops automation n8n]
---

# 🚀 Tự động hóa Snapshot VPS Hostinger & Theo dõi tài nguyên qua WhatsApp

Các sếp đang quản lý nhiều VPS trên Hostinger chắc chắn đã từng trải qua cảm giác "thót tim" khi hệ thống gặp sự cố mà bản backup gần nhất lại từ... tuần trước. Việc vào từng panel, thủ công bấm tạo snapshot và kiểm tra thông số CPU, RAM, ổ cứng mỗi ngày vừa tốn thời gian lại vừa dễ quên.

Giải pháp ở đây là gì? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được tác giả **Leandro Melo** thiết kế riêng cho các DevOps "lười mà hệ thống vẫn cứ mượt". Workflow này sẽ tự động hóa 100% quy trình tạo snapshot cho toàn bộ VPS, đo đạc thông số tài nguyên và báo cáo trực tiếp về điện thoại qua WhatsApp mỗi sáng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Định kỳ hàng ngày vào 4:00 sáng, hệ thống tự kích hoạt sao lưu mà không cần con người nhúng tay.
- **An toàn dữ liệu:** Tự động tạo Snapshot cho toàn bộ VPS đang hoạt động. *(Lưu ý: Hostinger cho phép 1 snapshot mỗi VPS và bản mới sẽ ghi đè bản cũ)*.
- **Giám sát thời gian thực:** Thu thập các thông số cốt lõi gồm: Số vCPU, RAM (đang dùng/tổng), Ổ cứng (dung lượng sử dụng), Hệ điều hành, Uptime, IP và Status.
- **Cảnh báo tức thì:** Gửi tin nhắn thành công hoặc lỗi chi tiết qua WhatsApp ngay sau khi quá trình hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted trên VPS).
- **Hostinger API Key:** Lấy tại [Hostinger API Profile](https://hpanel.hostinger.com/profile/api).
- **Evolution API (WhatsApp):** Dùng để gửi tin nhắn thông báo (Hoặc các sếp có thể thay thế bằng Telegram/Slack node nếu muốn).
- **Community Nodes cần cài đặt trước:**
  - `n8n-nodes-hostinger-api`
  - `n8n-nodes-evolution-api`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy mã JSON của workflow từ nguồn hoặc tải file về, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau:
- **Cài đặt Community Nodes:** Vào mục *Settings > Community Nodes* trong n8n và cài đặt hai gói `n8n-nodes-hostinger-api` và `n8n-nodes-evolution-api`.
- **Node `Hostinger API list VPS`, `Get VPS Metrics`, `Create Snapshot`:** Tạo credential mới bằng Hostinger API Key đã lấy từ hPanel của Hostinger và áp dụng chung cho các node này.
- **Node `WhatsApp Message (success)` và `WhatsApp Message (error)`:** Cấu hình credential kết nối với Evolution API, điền số điện thoại nhận thông báo và tùy chỉnh nội dung mẫu báo cáo các thông số như:
  - 🔹 **Status:** Trạng thái snapshot
  - 🔹 **Server:** Tên server & IP ngoài
  - ⚙️ **Metrics:** Số vCPU, RAM, Ổ cứng, OS và thời gian Uptime.
- **Node `Every day 4:00am` (Schedule Trigger):** Kiểm tra lại múi giờ của hệ thống n8n để đảm bảo lịch chạy đúng 4 giờ sáng hàng ngày.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Test workflow’** tại node `When clicking ‘Test workflow’` để chạy thử nghiệm xem thông tin VPS có được kéo về và tin nhắn WhatsApp có bắn đi thành công không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Nếu không dùng WhatsApp, các sếp có thể thay thế bằng node Telegram Bot để nhận cảnh báo qua Telegram hoàn toàn miễn phí và nhanh chóng.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để ghi lại log dung lượng RAM, ổ cứng theo ngày, phục vụ việc phân tích xu hướng tài nguyên (Capacity Planning).
- **Xử lý lỗi thông minh:** Kết hợp thêm node điều kiện để nếu snapshot lỗi quá 3 lần, hệ thống sẽ ưu tiên ping thẳng vào nhóm chat kỹ thuật để xử lý khẩn cấp.

### 📌 Kết luận
Việc tự động hóa sao lưu VPS và theo dõi tài nguyên chưa bao giờ dễ dàng đến thế với n8n và Hostinger API. Hãy cài đặt ngay để bảo vệ dữ liệu doanh nghiệp của các sếp khỏi những rủi ro bất ngờ! Chúc các sếp thao tác thành công.