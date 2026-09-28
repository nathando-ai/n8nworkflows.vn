---
title: "🚀 Tự động gửi email cảnh báo bảo mật khi Secret và Certificate của Microsoft Entra ID sắp hết hạn"
description: "Hướng dẫn sử dụng n8n workflow để quét định kỳ các ứng dụng trên Microsoft Entra ID, lọc credential sắp hết hạn và gửi báo cáo HTML chi tiết qua email hoàn toàn tự động."
slug: "tu-dong-canh-bao-secret-certificate-entra-id-microsoft-graph"
tags: [n8n, automation, microsoft-graph, entra-id, devops, security]
keywords: [n8n workflow, microsoft entra id, azure ad secret expiration, graph api automation, tu dong hoa devops]
---

# 🚀 Tự động gửi email cảnh báo bảo mật khi Secret và Certificate của Microsoft Entra ID sắp hết hạn

Trong môi trường doanh nghiệp sử dụng hệ sinh thái Microsoft, việc quản lý các Client Secrets và Certificates của ứng dụng trên **Microsoft Entra ID (Azure AD)** là cực kỳ quan trọng. Nếu một secret hết hạn mà không được gia hạn kịp thời, hệ thống tích hợp hoặc ứng dụng nội bộ sẽ ngừng hoạt động đột ngột, gây gián đoạn kinh doanh. 

Việc kiểm tra thủ công bằng mắt thường là một ác mộng đối với đội ngũ IT và DevOps khi số lượng ứng dụng ngày càng tăng. Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động kết nối qua Microsoft Graph API, quét toàn bộ metadata, lọc ra các credential sắp hết hạn và gửi bảng báo cáo HTML trực quan qua email.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phòng ngừa gián đoạn hệ thống:** Phát hiện sớm các secret/certificate sắp hết hạn trước khi chúng gây ra sự cố downtime.
- **Tự động hóa 100%:** Thay vì kiểm tra thủ công trên Azure Portal, hệ thống tự động quét định kỳ theo lịch trình.
- **Báo cáo trực quan:** Tổng hợp danh sách thành một bảng HTML chuyên nghiệp gửi thẳng đến hòm thư của quản trị viên.
- **Tiết kiệm thời gian:** Giúp đội ngũ DevOps tập trung vào các nhiệm vụ cốt lõi thay vì theo dõi lịch hết hạn thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Microsoft Entra ID App Registration** với quyền API:
  - `Application.Read.All` (Microsoft Graph)
- **OAuth2 Credentials** đã được cấu hình trong n8n (sử dụng loại *Client Credentials grant type*).
- **SMTP Server / Email Account** cấu hình trong node `Send email` để gửi báo cáo.
- **n8n Instance** (Khuyến nghị dùng bản Self-hosted hoặc n8n Cloud).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ n8n.io và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, hãy chú ý cấu hình kỹ các node sau:

- **Get EntraID Applications and Secrets (Node `httpRequest`):**
  - Kết nối với tài khoản **OAuth2 API** đã tạo sẵn (sử dụng Client Credentials).
  - Endpoint trỏ đến Microsoft Graph API để lấy thông tin applications và credentials.
- **Set Variables (Node `set`):**
  - Tinh chỉnh khoảng thời gian cảnh báo (ví dụ: số ngày trước khi hết hạn để đưa vào danh sách cần chú ý).
- **Filter Client Secrets & Filter Client Certificates (Node `filter`):**
  - Thiết lập điều kiện lọc dựa trên ngày hết hạn (`endDateTime`) so với biến thời gian hiện tại.
- **HTML Table with Expiring Secrets (Node `html`):**
  - Tùy chỉnh định dạng giao diện bảng HTML theo sở thích hiển thị của doanh nghiệp.
- **Send email (Node `emailSend`):**
  - Điền thông tin người nhận (IT Admin, DevOps Team) và cấu hình SMTP credentials để gửi mail cảnh báo.

#### 3. Kích hoạt ⚡️
- Thay thế node `When clicking ‘Execute workflow’` (Manual Trigger) bằng **Schedule Trigger** (ví dụ: chạy 1 lần mỗi tuần vào sáng thứ Hai).
- Nhấn **Test Step** từng node để kiểm tra dữ liệu trả về từ Microsoft Graph.
- Bật **Active workflow** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thay vì chỉ gửi email, các sếp có thể nối thêm node **Slack** hoặc **Telegram** để bắn thông báo trực tiếp vào group chat của đội ngũ DevOps.
- **Lưu lịch sử vào Database:** Lưu kết quả quét vào **Google Sheets** hoặc **PostgreSQL** để theo dõi xu hướng quản lý bảo mật theo thời gian.
- **Tự động gia hạn (Nâng cao):** Kết hợp thêm API gọi để tự động tạo secret mới (nếu chính sách bảo mật cho phép).

### 📌 Kết luận
Một giải pháp DevOps nhỏ gọn nhưng cực kỳ thiết thực để bảo vệ hệ thống khỏi những cú "sập nguồn" bất ngờ do quên gia hạn credential. Hãy setup ngay hôm nay để tối ưu hóa quy trình quản lý hạ tầng của doanh nghiệp các sếp nhé!