---
title: "🚀 Tự động làm giàu dữ liệu và chống trùng lặp công ty từ Slack lên HubSpot bằng Coresignal"
description: "Hướng dẫn tự động hóa quy trình xử lý danh sách công ty tải lên Slack, làm giàu dữ liệu qua Coresignal, kiểm tra trùng lặp và đồng bộ vào HubSpot một cách thông minh."
slug: "tu-dong-lam-giau-du-lieu-cong-ty-slack-hubspot-coresignal"
tags: [n8n, automation, no-code, slack, hubspot, coresignal, lead-generation]
keywords: [n8n workflow, tự động hóa slack hubspot, coresignal enrich data, chong trung lap hubspot, b2b data pipeline]
---

# 🚀 Tự động làm giàu dữ liệu và chống trùng lặp công ty từ Slack lên HubSpot bằng Coresignal

Các sếp làm Sales và RevOps chắc chắn hiểu được nỗi đau khi đội ngũ gửi một file danh sách công ty (CSV/Excel) lên Slack, sau đó nhân sự phải thủ công tra cứu từng domain, kiểm tra xem công ty đã có trên HubSpot chưa, rồi mới cập nhật hoặc tạo mới. Quá trình này vừa tốn thời gian, dễ xảy ra sai sót, lại cực kỳ nhàm chán.

Workflow n8n tuyệt vời này sinh ra để giải quyết triệt để vấn đề đó. Chỉ với một thao tác kéo thả file danh sách công ty lên Slack, hệ thống sẽ tự động trích xuất, đối soát dữ liệu chống trùng lặp (deduplication), xin phê duyệt qua Slack, làm giàu thông tin (enrichment) bằng **Coresignal** và tự động cập nhật/tạo mới dữ liệu trên **HubSpot**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình nhập liệu:** Không cần copy-paste thủ công từ file Excel lên CRM nữa.
- **Chống trùng lặp thông minh:** Kiểm tra domain trên HubSpot trước khi tạo mới, tránh làm ô nhiễm CRM.
- **Tích hợp kiểm duyệt (Human-in-the-loop):** Gửi thông báo và chờ người dùng phê duyệt qua Slack trước khi tiến hành cập nhật dữ liệu nhạy cảm.
- **Làm giàu dữ liệu mạnh mẽ:** Bổ sung thông tin chi tiết về doanh nghiệp thông qua API của Coresignal.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Slack App / Bot Token** với quyền đọc/ghi file và gửi tin nhắn (Interactive/Send and Wait).
- **HubSpot Account** kèm theo API Key hoặc OAuth2 Credentials.
- **Coresignal API Key** để thực hiện việc enrich dữ liệu công ty.
- **n8n Data Table** được thiết lập sẵn cột `Domain` để lưu trữ tạm thời.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công 27 nodes, các sếp cần cấu hình các thông số quan trọng sau:

- **When Slack File Uploaded (`slackTrigger`):** Kết nối với tài khoản Slack và chọn channel nhận file upload.
- **Download Slack File & Fetch File Contents (`slack` & `httpRequest`):** Đảm bảo quyền truy cập file của Slack Bot được cấp đầy đủ để tải file xuống hệ thống.
- **Insert File Data into Table & Retrieve Current Table Rows (`dataTable`):** Cấu hình Data Table trong n8n để khớp với cấu trúc cột (đặc biệt là cột `Domain`) của file tải lên.
- **Search Company by Domain & Create/Update HubSpot Nodes (`hubspot`):** Chọn HubSpot Credentials (OAuth2 hoặc Private App Token). Kiểm tra lại mapping giữa các trường dữ liệu tùy chỉnh (custom fields) của HubSpot.
- **Await Slack User Approval (`slack` - `sendAndWait`):** Cấu hình channel Slack để hệ thống gửi yêu cầu xác nhận và chờ phản hồi từ người quản lý.
- **Enrich Existing company & Enrich new company (`n8n-nodes-coresignal-api.coresignal`):** Nhập Coresignal API Key và map thông tin trả về với cấu trúc dữ liệu công ty.
- **Process Company Fields (`code`):** Kiểm tra đoạn code JavaScript xử lý logic tùy chỉnh các trường dữ liệu trước khi đẩy vào CRM.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng một file mẫu chứa vài dòng domain công ty để kiểm tra luồng chạy từ Slack -> HubSpot.
- Sau khi chắc chắn không có lỗi, bật công tắc **Active** để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Kết hợp thêm node gửi tin nhắn sang một kênh Telegram riêng để đội ngũ Leadership theo dõi số lượng lead được enrich mỗi ngày.
- **Lưu log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để tự động thông báo về Slack nếu Coresignal hoặc HubSpot trả về mã lỗi API.
- **Báo cáo định kỳ:** Tạo thêm một lịch chạy cron job mỗi tuần tổng hợp số liệu công ty mới được thêm vào HubSpot và gửi báo cáo qua email.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp tự động hóa khâu làm sạch và làm giàu dữ liệu khách hàng doanh nghiệp, giúp đội ngũ Sales tiết kiệm hàng chục giờ làm việc mỗi tuần. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình CRM của doanh nghiệp các sếp nhé!