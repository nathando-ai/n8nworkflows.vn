---
title: "🚀 Tự động giám sát Uptime website & Cảnh báo thông minh qua Claude AI, Telegram, Email"
description: "Hướng dẫn cài đặt workflow n8n giám sát hệ thống website 24/7 với Uptime Robot, phân tích lỗi tự động bằng Claude AI và gửi cảnh báo đa kênh (Telegram, Gmail, WhatsApp)."
slug: "tu-dong-giam-sat-uptime-website-va-canh-bao-ai-n8n"
tags: [n8n, automation, devops, uptimerobot, ai, claude, telegram]
keywords: [n8n workflow, giám sát uptime website, cảnh báo lỗi website, uptimerobot n8n, claude ai n8n, tự động hóa devops]
---

# 🚀 Tự động giám sát Uptime website & Cảnh báo thông minh qua Claude AI, Telegram, Email

Các sếp có bao giờ gặp cảnh website khách hàng hoặc hệ thống SaaS của mình sập giữa đêm, đến sáng hôm sau mới tá hỏa nhận ra vì khách khiếu nại chưa? Việc kiểm tra thủ công hay dùng các công cụ cảnh báo khô khan (chỉ báo "Down" chung chung) khiến chúng ta mất rất nhiều thời gian để phỏng đoán nguyên nhân.

Đừng lo, workflow n8n được thiết kế bởi **SpaGreen Creative** này chính là "vũ khí tối thượng" giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động quét trạng thái website định kỳ, kết hợp sức mạnh của **Claude AI (Anthropic)** để phân tích thông minh, đo lường tốc độ qua **PageSpeed Test**, ghi nhận log vào **Google Sheets** và bắn cảnh báo chi tiết đến tận răng qua **Telegram, Gmail, và WhatsApp**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát tự động 24/7:** Không bỏ sót bất kỳ sự cố sập nguồn hay gián đoạn dịch vụ nào từ Uptime Robot.
- **Phân tích thông minh bằng AI:** Claude AI sẽ biên tập lại nội dung cảnh báo kèm theo phân tích chuyên sâu thay vì những dòng mã lỗi khó hiểu.
- **Cảnh báo đa kênh tức thì:** Thông báo đổ về Telegram, WhatsApp và Email ngay lập tức khi phát hiện sự cố (hoặc khi website phục hồi trở lại).
- **Lưu lịch sử minh bạch:** Tự động đồng bộ trạng thái và ghi log chi tiết vào Google Sheets để tiện thống kê, báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản Uptime Robot:** Lấy API Key để lấy danh sách các monitor đang chạy.
- **Tài khoản Anthropic (Claude):** API Key để AI định dạng và phân tích tin nhắn cảnh báo.
- **Google Sheets:** File trang tính mẫu để lưu log trạng thái website.
- **Telegram Bot Token:** Để gửi tin nhắn cảnh báo qua Telegram.
- **Gmail / Rapiwa (WhatsApp):** Credentials để gửi email và tin nhắn WhatsApp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy toàn bộ mã JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau để hệ thống chạy mượt mà:

- **Schedule Trigger:** Thiết lập chu kỳ thời gian quét (ví dụ: cứ mỗi 5 phút hoặc 15 phút chạy 1 lần).
- **Uptime Robot (Get Monitors):** Nhập Uptime Robot API Key của các sếp để hệ thống lấy danh sách các website đang quản lý.
- **Anthropic Chat Model & ChainLlm (LLM Message Format):** Kết nối API Key của Anthropic (Claude) để node AI có thể hoạt động và tạo nội dung thông báo thông minh.
- **Google Sheets (Append or update row in sheet):** Chọn file Google Sheet và Sheet Name phù hợp để lưu trữ nhật ký trạng thái (Uptime/Downtime log).
- **Telegram, Gmail, Rapiwa Nodes:** Cấu hình Chat ID (Telegram), tài khoản gửi email (Gmail) và số điện thoại nhận tin nhắn WhatsApp để nhận cảnh báo.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thử nghiệm thủ công xem các node đã kết nối mượt mà chưa.
- Kiểm tra xem Telegram/Email có nhận được tin nhắn test không.
- Nếu mọi thứ xanh mướt, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chiến đấu 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Discord:** Các sếp có thể nhân bản node Telegram và nối thêm node Slack hoặc Discord để đội ngũ kỹ thuật nhận thông báo ngay trên kênh chat chung của công ty.
- **Kết hợp Google Looker Studio:** Lấy dữ liệu từ Google Sheets được ghi log bởi workflow để vẽ biểu đồ đo lường độ ổn định (Uptime SLA) theo tháng gửi cho sếp lớn hoặc khách hàng.
- **Bổ sung Webhook tùy chỉnh:** Thêm một node HTTP Request để gọi tới hệ thống quảniticket nội bộ (Jira, Zendesk) mỗi khi website sập để tạo task tự động cho đội DevOps.

### 📌 Kết luận
Một hệ thống DevOps chuyên nghiệp không chỉ là hệ thống biết kêu cứu khi sập, mà phải là hệ thống thông minh tự phân tích và báo cáo nhanh gọn. Hãy cài ngay workflow này vào n8n của các sếp để có những giấc ngủ ngon ban đêm mà không sợ website "tạch" bất ngờ nhé!