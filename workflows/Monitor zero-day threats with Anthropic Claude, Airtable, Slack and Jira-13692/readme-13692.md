---
title: "🚀 Giám sát mối đe dọa Zero-Day tự động với Claude AI, Airtable, Slack và Jira"
description: "Xây dựng hệ thống SecOps tự động 24/7 quét lỗ hổng zero-day từ các nguồn uy tín, đối chiếu tài sản nội bộ và dùng Claude AI đánh giá rủi ro, tạo ticket Jira và cảnh báo Slack."
slug: "giam-sat-moi-de-doa-zero-day-tu-dong-claude-ai-airtable-jira"
tags: [n8n, automation, no-code, SecOps, AI Summarization, Cybersecurity]
keywords: [n8n workflow, zero-day threat monitoring, Claude AI security, tự động hóa bảo mật, Jira Slack security alerts]
keywords: [n8n workflow, tự động hóa, zero-day threat monitoring, SecOps automation, Claude AI security]
---

# 🚀 Giám sát mối đe dọa Zero-Day tự động với Claude AI, Airtable, Slack và Jira

Trong bối cảnh an ninh mạng phức tạp hiện nay, các lỗ hổng zero-day và mã độc xuất hiện liên tục khiến đội ngũ bảo mật (SOC) luôn ở trạng thái "chạy đua với thời gian". Việc kiểm tra thủ công các cơ sở dữ liệu CVE, đối chiếu với tài sản công ty và đánh giá mức độ nguy hiểm ngốn rất nhiều thời gian và dễ bỏ sót.

Workflow này giải quyết triệt để vấn đề trên bằng cách **tự động hóa 100% quy trình SecOps**: liên tục quét các nguồn threat intelligence toàn cầu, đối chiếu với danh mục tài sản thực tế, sử dụng **Claude AI** để phân tích độ nguy hiểm, từ đó tự động bắn cảnh báo qua Slack, tạo ticket Jira và kích hoạt hệ thống vá lỗi trước khi kẻ tấn công kịp khai thác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Quét định kỳ hàng giờ hoặc kích hoạt khẩn cấp qua Webhook mà không cần nhân sự can thiệp thủ công.
- **AI Thông minh:** Claude AI phân tích chính xác blast radius (vùng ảnh hưởng), điểm số EPSS và đưa ra hành động khắc phục cụ thể.
- **Phản ứng tức thì:** Tự động định tuyến mức độ nguy hiểm (Critical/High/Medium), bắn alert lên Slack và mở ticket trên Jira/ServiceNow ngay lập tức.
- **Log đầy đủ & Minh bạch:** Lưu trữ toàn bộ lịch sử threat intelligence vào Google Sheets để phục vụ kiểm toán và báo cáo SIEM/SOAR.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Anthropic API Key** (cho Claude AI đánh giá rủi ro)
- **NVD API Key** (NIST National Vulnerability Database)
- **AlienVault OTX API** & **Shodan API** (Thu thập OSINT threat feeds)
- **Airtable Account** (Quản lý danh mục tài sản & phần mềm)
- **Slack App / Bot Token** (Gửi cảnh báo SOC)
- **Jira Software API** (Tự động tạo incident tickets)
- **SMTP / SendGrid** (Gửi email báo cáo chi tiết cho đội ngũ an ninh)
- **Google Sheets OAuth** (Lưu log threat intelligence)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện quản trị n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Load Asset & Software Inventory (Airtable):** Kết nối tài khoản Airtable của các sếp, chọn đúng Base và Table chứa danh sách hạ tầng, IP, hostname và phiên bản phần mềm.
- **Claude AI Model (lmChatAnthropic):** Chọn đúng credential Anthropic và model `=claude-sonnet-4-20250514` để AI thực hiện nhiệm vụ đánh giá lỗ hổng.
- **Filter Above Risk Threshold:** Cấu hình điểm số ngưỡng rủi ro tối thiểu (mặc định là `65`) để lọc các mối đe dọa thực sự nguy hiểm trước khi đẩy xuống các bước tiếp theo.
- **Alert SOC Team on Slack:** Điền channel ID của nhóm SOC trên Slack để nhận thông báo tức thời.
- **Submit Jira Issues via API:** Kết nối Jira Cloud API, cấu hình Project Key và Issue Type phù hợp (ví dụ: Bug hoặc Task).
- **Append to Threat Intelligence Log (Google Sheets):** Trỏ tới file Google Sheets dùng làm sổ nhật ký ghi nhận các mối đe dọa.

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (Test run) với dữ liệu mẫu qua node `On-Demand Scan Webhook` hoặc chạy thủ công node lịch trình.
- Sau khi kiểm tra dữ liệu trả về chính xác ở các nhánh, gạt công tắc sang **Active** để hệ thống tự động túc trực 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Microsoft Teams:** Thay thế hoặc bổ sung node Slack bằng node Telegram để nhận cảnh báo ngay trên điện thoại cá nhân của sysadmin.
- **Tự động hóa bản vá (Patch Management):** Kết nối node `Trigger Patch Management System` với Ansible Tower hoặc bash script qua SSH để tự động vá các lỗ hổng cấp độ Critical.
- **Báo cáo định kỳ:** Thêm một Schedule Trigger chạy vào cuối tuần để tổng hợp log từ Google Sheets và gửi email báo cáo tuần cho ban quản lý.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp tự động hóa khâu giám sát bảo mật, tiết kiệm hàng chục giờ phân tích thủ công mỗi tuần và bịt kín các lỗ hổng zero-day trước khi tin tặc kịp lợi dụng. Hãy áp dụng ngay vào hệ thống của các sếp để nâng tầm bảo mật doanh nghiệp lên mức chuyên nghiệp!