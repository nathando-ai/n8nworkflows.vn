---
title: "🚀 Giám sát Website, Lên lịch Kiểm tra & Gửi Cảnh báo Email tự động"
description: "Tự động kiểm tra trạng thái website theo lịch, phát hiện downtime và gửi email cảnh báo ngay lập tức, không cần viết code."
slug: "giamsat-website-lich-trinh-email-can-canh"
tags: [n8n, automation, no-code, devops, monitoring, email]
keywords: [n8n workflow, tự động hóa, website monitoring, email alerts, schedule]
---

# 🚀 Giám sát Website, Lên lịch Kiểm tra & Gửi Cảnh báo Email tự động

Doanh nghiệp thường phải **giám sát liên tục** các website quan trọng để tránh mất khách hàng và uy tín khi có sự cố downtime.  
Việc kiểm tra thủ công mỗi giờ, mỗi ngày không chỉ tốn thời gian mà còn dễ bỏ sót những giây phút quan trọng.  

**Website Monitoring, Scheduling, and Email Alerts Template** là workflow n8n giúp bạn **tự động kiểm tra trạng thái website** theo lịch định sẵn, **phát hiện ngay khi website ngừng hoạt động** và **gửi email cảnh báo** tới người chịu trách nhiệm – tất cả mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở trình duyệt kiểm tra thủ công.  
- **Phát hiện nhanh**: Khi website down, email cảnh báo được gửi trong vòng vài giây.  
- **Độ chính xác 100 %**: Kiểm tra dựa trên mã trạng thái HTTP, không phụ thuộc vào mắt người.  
- **Hoạt động liên tục 24/7**: Workflow chạy trên server riêng, không bị gián đoạn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **URL website** muốn giám sát (ví dụ: `https://example.com`).  
- **Tài khoản email SMTP** (Gmail, Outlook, SendGrid, …) để gửi cảnh báo.  
- **API credentials** cho n8n (nếu chạy trên server tự host).  
- **Quyền truy cập** vào n8n editor để import và chỉnh sửa workflow.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n.  
2. Vào **Workflows → Import**.  
3. Chọn **Upload JSON** và tải file `website-monitoring.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
4. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là mô tả chi tiết từng node và các tham số cần cấu hình:

| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **Schedule Website Check** (`scheduleTrigger`) | Kích hoạt workflow theo lịch định kỳ. | - **Cron Expression**: Đặt tần suất mong muốn (ví dụ: `0 */5 * * * *` → mỗi 5 phút). <br> - **Timezone**: Chọn múi giờ phù hợp với doanh nghiệp. |
| **Check Website Status** (`httpRequest`) | Gửi yêu cầu GET tới website để lấy mã trạng thái. | - **Method**: `GET` <br> - **URL**: Điền URL website cần giám sát. <br> - **Response Format**: `JSON` (không quan trọng nếu chỉ kiểm tra status code). |
| **Website Down?** (`if`) | Kiểm tra xem website có trả về mã 200 hay không. | - **Condition**: `{{ $json["statusCode"] !== 200 }}` (hoặc sử dụng **Number** → **!=** → **200**). |
| **Send Downtime Email Alert** (`emailSend`) | Gửi email cảnh báo khi website down. | - **Credentials**: Chọn **SMTP** credentials đã tạo. <br> - **To**: Địa chỉ email nhận cảnh báo (có thể là danh sách, cách nhau bằng `,`). <br> - **Subject**: Ví dụ `⚠️ Website Down Alert – {{ $json["url"] }}`. <br> - **Body**: Nội dung chi tiết, ví dụ: <br>```text\nWebsite {{ $json["url"] }} đã trả về status code {{ $json["statusCode"] }} vào lúc {{ $now }}.\nVui lòng kiểm tra ngay!\n``` |

> **Lưu ý:** Nếu website trả về redirect (3xx) hoặc lỗi client (4xx) mà vẫn được coi là “down”, bạn có thể mở rộng điều kiện trong node **if**.

#### 3. Kích hoạt ⚡️
1. Nhấn **Save** → **Activate** ở góc trên bên phải.  
2. Chạy **Test Run** một lần với dữ liệu mẫu để xác nhận email được gửi đúng.  
3. Kiểm tra hộp thư nhận cảnh báo; nếu mọi thứ ổn, workflow đã sẵn sàng hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo tổng hợp**: Thêm một node `Google Sheets` hoặc `Airtable` để lưu lịch sử downtime, sau đó dùng `Cron` khác để gửi báo cáo hàng tuần.  
- **Kết nối Slack/Telegram**: Thay node `emailSend` bằng `Slack` hoặc `Telegram` để nhận thông báo nhanh hơn trên kênh làm việc.  
- **Giám sát nhiều website**: Sử dụng **SplitInBatches** hoặc **Loop** để lặp qua danh sách URL trong một Google Sheet.  
- **Alert mức độ nghiêm trọng**: Thêm node `IF` thứ hai để phân biệt giữa “downtime ngắn” (<5 phút) và “downtime dài” (>5 phút), gửi email với mức ưu tiên khác nhau.

### 📌 Kết luận
Với workflow **Website Monitoring, Scheduling, and Email Alerts**, các sếp có thể **đảm bảo website luôn hoạt động**, nhận cảnh báo ngay khi có sự cố và **giảm thiểu rủi ro mất khách hàng**. Hãy import ngay, cấu hình các tham số cơ bản và để n8n làm việc thay bạn 24/7! 🚀