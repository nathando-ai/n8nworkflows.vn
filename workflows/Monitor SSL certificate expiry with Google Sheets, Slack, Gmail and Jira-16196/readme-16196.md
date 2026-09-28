---
title: "🚀 Tự động giám sát hạn SSL certificate, cảnh báo qua Slack, Gmail và Jira với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra chứng chỉ SSL hàng ngày từ Google Sheets, cảnh báo trước khi hết hạn qua Slack, Gmail và tạo task Jira."
slug: "tu-dong-giam-sat-han-ssl-certificate-voi-n8n"
tags: [n8n, automation, no-code, devops, monitoring, google-sheets, slack, jira]
keywords: [n8n workflow, giám sát ssl, kiểm tra ssl hết hạn, tự động hóa devops, google sheets slack jira n8n]
---

# 🚀 Tự động giám sát hạn SSL certificate, cảnh báo qua Slack, Gmail và Jira

Các sếp có từng gặp cảnh website công ty bỗng nhiên hiển thị cảnh báo bảo mật đỏ rực chỉ vì chứng chỉ **SSL Certificate hết hạn mà không ai hay biết**? Việc quên gia hạn SSL không chỉ làm gián đoạn trải nghiệm khách hàng, tụt hạng SEO mà còn làm sụt giảm nghiêm trọng uy tín thương hiệu. 

Làm thủ công thì dễ bỏ sót, còn thuê dịch vụ bên ngoài thì tốn kém. Giải pháp hoàn hảo nhất là đây: **Workflow n8n tự động hóa 100%** giúp kiểm tra hàng loạt tên miền mỗi ngày, tính toán thời gian chính xác, tự động tạo ticket Jira, bắn tin nhắn cảnh báo qua Slack và gửi email Gmail khi sắp hết hạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bao giờ bỏ lỡ hạn SSL:** Tự động kiểm tra danh sách domain đều đặn mỗi ngày mà không cần con người nhúng tay.
- **Đa kênh cảnh báo:** Lập tức bắn thông báo khẩn cấp qua Slack, gửi Email và tạo Task Jira giao việc cho đội ngũ kỹ thuật khi SSL sắp hết hạn hoặc đã hết hạn.
- **Báo cáo tổng hợp minh bạch (Daily Digest):** Gửi một bản tổng kết toàn bộ tình trạng các domain lên Slack sau khi quét xong.
- **Log dữ liệu tự động:** Ghi nhận trạng thái các chứng chỉ an toàn vào Google Sheets để dễ dàng theo dõi, kiểm toán.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Sheets**: Tài khoản chứa danh sách các domain cần giám sát.
- **SSL Lookup API / HTTP Request**: Endpoint hoặc dịch vụ kiểm tra SSL live.
- **Slack Workspace**: Token/Webhook để gửi thông báo cảnh báo và tổng kết.
- **Gmail Account**: Kết nối OAuth2 để gửi email cảnh báo.
- **Jira Account**: Kết nối API/Token để tự động tạo ticket khi có sự cố.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy toàn bộ mã JSON và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm **13 nodes** được tối ưu hóa toàn diện từ khâu quét, lọc, xử lý logic đến thông báo.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình chính xác các thành phần sau:
- **Daily Schedule (`scheduleTrigger`):** Thiết lập thời gian chạy định kỳ mỗi sáng (ví dụ: 8:00 AM hàng ngày).
- **Read Domain List & Log Healthy Cert (`googleSheets`):** Kết nối tài khoản Google Sheets của các sếp, trỏ tới file quản lý danh sách domain và cột cần đọc/ghi (cột `domain`).
- **Fetch SSL Details (`httpRequest`):** Cấu hình API endpoint để truy vấn thông tin chi tiết chứng chỉ SSL của từng domain.
- **Calculate Days Left & Aggregate Daily Summary (`code`):** Node JavaScript tính toán chính xác số ngày còn lại đến khi hết hạn và phân loại trạng thái (`Expired`, `Critical`, `Warning`, `Healthy`). Các sếp có thể tuỳ chỉnh ngưỡng ngày cảnh báo tại đây.
- **Needs Alert (`if`):** Node điều kiện phân luồng xử lý: domain nào sắp hết hạn sẽ chạy nhánh cảnh báo, domain an toàn sẽ đi qua nhánh ghi log.
- **Create Jira Ticket (`jira`):** Chọn credentials Jira, chọn Project Key để tự động tạo task giao việc xử lý SSL.
- **Slack Alert & Slack Daily Digest (`slack`):** Kết nối Slack Bot Token và chọn Channel ID nhận thông báo khẩn cấp cũng như bản tin tổng hợp cuối ngày.
- **Email Alert (`gmail`):** Kết nối Gmail credentials và cấu hình hòm thư nhận cảnh báo lỗi SSL.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu xem hệ thống bắn tin nhắn và tạo ticket có mượt mà không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc **Active** góc trên bên phải để n8n tự động túc trực bảo vệ hệ thống 24/7 cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Microsoft Teams:** Ngoài Slack và Gmail, các sếp có thể nhân bản node cảnh báo sang Telegram Bot để nhận tin nhắn trên điện thoại nhanh chóng hơn.
- **Bổ sung Auto-Renewal (Nâng cao):** Nếu dùng Let's Encrypt, có thể tích hợp thêm các API tự động gia hạn SSL ngay trong n8n thay vì chỉ cảnh báo.
- **Lưu lịch sử vào Database:** Thay vì chỉ ghi Google Sheets, có thể đẩy log sang PostgreSQL hoặc Supabase để vẽ biểu đồ dashboard theo dõi sức khỏe hạ tầng.

### 📌 Kết luận
Một sự cố nhỏ về SSL cũng có thể làm tổn hại doanh thu và uy tín của doanh nghiệp. Với workflow n8n tự động hóa này, các sếp hoàn toàn có thể yên tâm ngủ ngon vì hệ thống đã có "lính canh" tự động kiểm tra và báo động từ xa trước khi rủi ro xảy ra. Áp dụng ngay thôi các sếp ơi!