---
title: "🚀 Tự Động Gửi Tóm Tắt Họp Trước 15 Phút: Kết Hợp Google Calendar, Notion, GitHub & Jira"
description: "Workflow n8n tự động thu thập ghi chú từ Notion, PR từ GitHub và ticket từ Jira, sau đó gửi tin nhắn Slack cá nhân hóa cho từng thành viên tham dự trước cuộc họp 15 phút."
slug: "tu-dong-gui-tom-tat-hop-slack-n8n"
tags: [n8n, automation, project-management, slack, google-calendar]
keywords: [n8n workflow, tự động hóa họp, slack integration, google calendar automation, notion to slack]
---

# 🚀 Tự Động Gửi Tóm Tắt Họp Trước 15 Phút: Kết Hợp Google Calendar, Notion, GitHub & Jira

Bạn có bao giờ bước vào cuộc họp mà quên mất những quyết định quan trọng đã được chốt ở lần họp trước? Hoặc cảm thấy bối rối vì không biết chính xác những Pull Request (PR) nào đang chờ review liên quan đến chủ đề hôm nay?

Làm thủ công việc tổng hợp thông tin từ 4 hệ thống khác nhau (Calendar, Notion, GitHub, Jira) trước mỗi cuộc họp là một gánh nặng lớn, tốn thời gian và dễ gây sai sót. Workflow n8n này giải quyết triệt để vấn đề đó bằng cách **tự động hóa 100%** quy trình chuẩn bị bối cảnh họp.

Ngay khi một cuộc họp mới được tạo trên Google Calendar, hệ thống sẽ "đi trước đón đầu":
1. Tìm kiếm ghi chú từ cuộc họp gần nhất trên Notion.
2. Chờ đến đúng 15 phút trước giờ họp.
3. Quét GitHub và Jira để tìm các PR và Ticket liên quan đến từ khóa trong tiêu đề cuộc họp.
4. Gửi tin nhắn Slack trực tiếp (DM) cho từng thành viên tham dự với đầy đủ thông tin cần thiết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là với cơ chế `Wait` (chờ thời gian) và trigger từ Calendar, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian chuẩn bị:** Không cần tốn 10-15 phút mỗi cuộc họp để lục lọi thông tin từ các tool khác nhau.
- **Tăng hiệu quả họp:** Thành viên tham dự đã có sẵn bối cảnh (context) về các task đang chạy và quyết định trước đó, giúp cuộc họp đi thẳng vào vấn đề.
- **Cá nhân hóa thông tin:** Mỗi người nhận tin nhắn riêng trên Slack, đảm bảo tính riêng tư và tập trung.
- **Hoạt động liên tục & Chính xác:** Workflow xử lý logic lọc từ khóa và đối chiếu email/Slack user tự động, loại bỏ lỗi con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các credentials (thông tin đăng nhập) sau:
1. **Google Calendar:** Tài khoản Google có quyền tạo/đọc lịch.
2. **Notion:** API Key và ID Database chứa ghi chú cuộc họp (Meeting Notes).
3. **GitHub:** Personal Access Token (PAT) hoặc OAuth2 có quyền đọc Repository.
4. **Jira:** API Token cho Jira Software Cloud.
5. **Slack:** Bot Token hoặc App Token có quyền `users:read` (để tìm user qua email) và `chat:write` (để gửi tin nhắn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n của mình bằng cách:
- Tải file JSON từ link gốc [n8n.io/workflows/13224](https://n8n.io/workflows/13224).
- Hoặc copy toàn bộ code JSON và dán vào n8n Editor (chọn `Import from URL` hoặc `Import from Clipboard`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node chính sau để khớp với hạ tầng của mình:

**A. Trigger & Dữ liệu đầu vào**
- **Node `Capture New Google Calendar Event`:** Chọn credentials Google Calendar của bạn. Đảm bảo calendar này là nơi các sếp thường đặt lịch họp.
- **Node `Get Last Meeting Notes`:**
  - Chọn credentials Notion.
  - Trong phần `Database ID`, điền ID của database Notion nơi các sếp lưu ghi chú họp.
  - *Lưu ý:* Workflow giả định database có cấu trúc nhất định để lấy ghi chú gần nhất.

**B. Nguồn dữ liệu kỹ thuật (GitHub & Jira)**
- **Node `Get PRs from Repo`:**
  - Chọn credentials GitHub.
  - Điền `Repository` (định dạng: `owner/repo-name`).
- **Node `Get Jira Issues Related to Meeting`:**
  - Chọn credentials Jira.
  - Kiểm tra JQL query (nếu có) để đảm bảo nó fetch đúng các ticket liên quan. Workflow sử dụng từ khóa từ tiêu đề cuộc họp để lọc.

**C. Xử lý & Gửi tin nhắn Slack**
- **Node `Get User Slack Info from Email`:**
  - Đây là node `httpRequest`. Các sếp cần đảm bảo Slack App của mình đã được cấp quyền `users:read.email` hoặc tương đương để API có thể tra cứu user qua email.
  - Kiểm tra URL API endpoint nếu cần (thường là `https://slack.com/api/users.lookupByEmail`).
- **Node `Send Meeting Context in Slack DM`:**
  - Chọn credentials Slack.
  - Đảm bảo Bot/Token có quyền gửi tin nhắn DM.

**D. Logic xử lý (Code Nodes)**
- Các node như `Extract Meeting Keywords`, `Filter PRs Related to Meeting`, `Build Message for Slack` chứa logic JavaScript.
- *Mẹo:* Nếu team các sếp có quy ước đặt tên cuộc họp khác (ví dụ: `[Project] Topic`), các sếp có thể chỉnh sửa logic trong node `Extract Meeting Keywords` để tách từ khóa chính xác hơn.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Tạo một cuộc họp giả lập trên Google Calendar (ví dụ: "Review Feature X").
   - Đảm bảo trong Notion có ghi chú của cuộc họp "Review Feature X" ở lần trước.
   - Đảm bảo GitHub có PR và Jira có ticket chứa từ khóa "Feature X".
   - Chạy workflow thủ công hoặc chờ trigger.
   - Kiểm tra xem tin nhắn có được gửi đến Slack của các thành viên tham dự không.
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n.
   - Workflow sẽ tự động chạy mỗi khi có cuộc họp mới được tạo.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI để tóm tắt:** Thay vì chỉ gửi link PR/Ticket, các sếp có thể thêm một node `OpenAI` hoặc `Anthropic` để tóm tắt nội dung các PR/Ticket đó thành 3-5 gạch đầu dòng ngắn gọn trước khi gửi Slack.
- **Gửi vào Channel thay vì DM:** Nếu cuộc họp là của cả team, thay vì gửi DM riêng lẻ, các sếp có thể chỉnh node `Send Meeting Context in Slack DM` để gửi vào một Channel Slack cụ thể (ví dụ: `#dev-team`).
- **Cảnh báo nếu thiếu thông tin:** Thêm một node `If` để kiểm tra xem có tìm thấy PR/Ticket nào không. Nếu không có, gửi một thông báo nhẹ nhàng rằng "Không có task kỹ thuật nào liên quan đến cuộc họp này" để tránh gây nhầm lẫn.
- **Lưu log hoạt động:** Thêm một node `Google Sheets` hoặc `Notion` để ghi lại lịch sử các cuộc họp đã được gửi briefing, giúp audit và theo dõi hiệu quả.

### 📌 Kết luận
Việc chuẩn bị bối cảnh cho cuộc họp là yếu tố quyết định đến chất lượng thảo luận. Với workflow n8n này, các sếp không chỉ tiết kiệm thời gian mà còn nâng tầm chuyên nghiệp cho đội ngũ kỹ thuật và quản lý. Hãy import, cấu hình và trải nghiệm ngay sự khác biệt mà tự động hóa mang lại!