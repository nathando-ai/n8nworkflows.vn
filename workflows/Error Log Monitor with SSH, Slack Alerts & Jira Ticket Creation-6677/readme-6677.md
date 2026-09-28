---
title: "🚀 Tự động giám sát lỗi hệ thống qua SSH, cảnh báo Slack và tạo Jira Ticket với n8n"
description: "Xây dựng hệ thống DevOps tự động hóa: định kỳ đọc error logs từ server qua SSH, phân loại lỗi thông minh, cảnh báo ngay lập tức trên Slack và tạo task Jira cho lỗi nghiêm trọng."
slug: "giam-sat-loi-he-thong-ssh-slack-jira-n8n"
tags: [n8n, automation, devops, ssh, slack, jira, monitoring]
keywords: [n8n workflow, giám sát log server, ssh n8n, slack alert, jira automation, devops automation]
---

# 🚀 Tự động giám sát lỗi hệ thống qua SSH, cảnh báo Slack và tạo Jira Ticket

Các sếp làm DevOps hay quản trị hệ thống chắc hẳn đã quá quen thuộc với cảm giác "đau tim" khi hệ thống gặp sự cố giữa đêm nhưng không biết sớm, hoặc việc kiểm tra log thủ công trên server tốn hàng giờ đồng hồ mỗi ngày. Việc phát hiện lỗi chậm trễ không chỉ làm gián đoạn trải nghiệm người dùng mà còn ảnh hưởng trực tiếp đến uy tín doanh nghiệp.

Giải pháp là đây! Workflow n8n này từ **Oneclick AI Squad** sẽ giúp các sếp tự động hóa 100% quy trình: định kỳ truy cập server đọc log qua SSH, phân loại mức độ nghiêm trọng, bắn cảnh báo nóng hổi lên Slack và tự động tạo ticket trên Jira để đội ngũ dev xử lý ngay lập tức mà không cần con người can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố 24/7:** Hệ thống tự động quét log mỗi 5 phút, không bỏ sót bất kỳ lỗi nào.
- **Phân loại thông minh:** Tự động lọc lỗi Critical (nghiêm trọng) và Non-Critical để có hướng xử lý phù hợp.
- **Tương tác đa nền tảng:** Bắn thông báo chi tiết tức thì qua Slack giúp team nắm bắt thông tin ngay lập tức.
- **Tự động hóa quản lý công việc:** Tự khởi tạo bug ticket trên Jira cho các lỗi nghiêm trọng, tiết kiệm thời gian tạo task thủ công cho kỹ sư.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **SSH Access:** Thông tin kết nối SSH (Host, Port, Username, SSH Private Key) tới server cần giám sát log.
- **Slack Workspace:** Bot Token hoặc Webhook để gửi tin nhắn cảnh báo.
- **Jira Software Account:** API Token và thông tin dự án (Project Key) để tự động tạo ticket.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình thông qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru trên môi trường thực tế, các sếp cần cấu hình kỹ các node sau:

- **Schedule Every 5min & Manual Trigger:** Xác định tần suất quét log tự động (mặc định 5 phút/lần) hoặc chạy thử thủ công bằng nút `Manual Trigger`.
- **Set Config:** Nơi cấu hình các tham số cơ bản ban đầu cho hệ thống như đường dẫn file log trên server (`/var/log/...`).
- **Read Error Logs (SSH Node):** 
  - Chọn credentials `sshPrivateKey` đã thiết lập.
  - Điền địa chỉ IP server, cổng SSH và câu lệnh đọc file log.
- **Parse Logs (Code Node):** Chạy đoạn code JavaScript để bóc tách, đọc và phân loại các dòng lỗi từ kết quả trả về của SSH.
- **IF Critical Error:** Thiết lập điều kiện rẽ nhánh dựa trên mức độ lỗi (Lỗi nghiêm trọng vs. Lỗi thông thường).
- **Send Slack Alert & Send Non-Critical Alert (Slack Node):** Kết nối tài khoản `slackApi`, chọn kênh (channel) nhận thông báo tương ứng cho từng mức độ lỗi.
- **Create Jira Ticket (Jira Node):** Kết nối với `jiraSoftwareCloudApi`, cấu hình Project Key và loại Issue (Bug) để hệ thống tự động tạo ticket khi gặp lỗi Critical.
- **Wait For All Logs (Wait Node):** Đảm bảo đồng bộ hóa luồng dữ liệu xử lý log từ server trước khi chuyển sang các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** chạy thử công đoạn `Manual Trigger` để kiểm tra toàn bộ kết nối SSH, Slack và Jira có hoạt động chính xác không.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm AI:** Có thể tích hợp thêm các node OpenAI/Anthropic vào giữa bước *Parse Logs* và *IF Critical Error* để AI phân tích nguyên nhân gốc rễ (Root Cause Analysis) và đề xuất hướng fix lỗi ngay trong thông báo Slack.
- **Lưu lịch sử lỗi:** Kết nối thêm Google Sheets hoặc Airtable để lưu lại toàn bộ lịch sử lỗi phục vụ việc báo cáo tổng hợp hàng tuần/tháng cho sếp lớn.
- **Mở rộng kênh thông báo:** Ngoài Slack, có thể duplicate node để bắn thêm thông báo qua Telegram hoặc Zalo OA cho các kỹ sư trực đêm.

### 📌 Kết luận
Với workflow **Error Log Monitor with SSH, Slack Alerts & Jira Ticket Creation**, các sếp đã sở hữu ngay một "hệ thống cảnh báo sớm" chuẩn DevOps chỉ với vài cú click thiết lập. Không còn cảnh phải ngồi soi log thủ công hay bị khách hàng phàn nàn mới biết hệ thống sập. Triển khai ngay thôi các sếp ơi!