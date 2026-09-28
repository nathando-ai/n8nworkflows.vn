---
title: "🚀 Phát hiện kiệt sức nhân sự (Team Burnout) tự động qua GitHub Activity và Groq AI"
description: "Hướng dẫn sử dụng n8n workflow tự động phân tích mã nguồn GitHub, phát hiện dấu hiệu kiệt sức của lập trình viên bằng Groq AI và gửi báo cáo wellness qua Email & GitHub Issues."
slug: "phat-hien-kien-suckinh-nhan-su-github-groq-ai"
tags: [n8n, automation, ai-agent, github, groq, wellness, hr-tech]
keywords: [n8n workflow, phát hiện kiệt sức, team burnout detector, groq ai, github activity, tự động hóa hr]
keywords: [n8n workflow, phat hien kiet suc, team burnout detector, groq ai, github activity]
---

# 🚀 Phát hiện kiệt sức nhân sự (Team Burnout) tự động qua GitHub Activity và Groq AI

Trong môi trường làm việc từ xa hoặc agile hiện đại, việc quản lý sức khỏe tinh thần (wellness) và phát hiện sớm tình trạng kiệt sức (burnout) của đội ngũ kỹ thuật là một thách thức lớn đối với các Quản lý (Engineering Manager) và Trưởng nhóm. Việc kiểm tra thủ công các commit lúc nửa đêm hay ngày cuối tuần thường tốn kém thời gian và dễ bỏ sót.

Workflow n8n này do chuyên gia **Sean Lon** thiết kế sẽ tự động hóa hoàn toàn quy trình: định kỳ quét hoạt động GitHub (Commits, PRs, Workflows), giao cho **Groq AI Agent** phân tích cường độ làm việc, phát hiện các pattern nguy hiểm (thức khuya code, commit cuối tuần, build fail liên tục) và tự động tạo GitHub Issue hoặc gửi báo cáo qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sớm rủi ro:** AI tự động chỉ ra các lập trình viên đang ôm đồm công việc, làm việc quá sức (thức khuya, làm cuối tuần).
- **Báo cáo định kỳ tự động:** Cung cấp báo cáo wellness chi tiết trực tiếp qua Gmail và GitHub Issues mà không cần tốn công tổng hợp thủ công.
- **Duy trì văn hóa lành mạnh:** Giúp nhà quản lý kịp thời điều chỉnh tải công việc (workload) để bảo vệ sức khỏe nhân sự.
- **Vận hành 24/7 tự động:** Kích hoạt theo lịch trình (Schedule Trigger) hoàn toàn rảnh tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản GitHub & Personal Access Token (API):** Để truy cập repository, lấy thông tin PRs, Commits và Workflows.
- **Groq API Key:** Để sử dụng mô hình AI tốc độ cao phân tích dữ liệu.
- **Tài khoản Gmail (OAuth2):** Để gửi email cảnh báo/báo cáo wellness.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (ID: 9517) hoặc copy toàn bộ mã nguồn JSON và paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thông số sau trong các node quan trọng:
- **Schedule Trigger:** Cấu hình mốc thời gian chạy định kỳ (ví dụ: chạy hàng tuần vào sáng thứ Hai).
- **Config:** Cập nhật các biến cấu hình cơ bản như tên Repository GitHub cần theo dõi, khoảng thời gian quét dữ liệu.
- **Get Prs & Github Get Commits & Github Get Workflows:** Thiết lập thông tin kết nối `githubApi` credentials để lấy dữ liệu từ kho lưu trữ mã nguồn.
- **Groq Chat Model Report:** Chọn model AI (mặc định cấu hình `openai/gpt-oss-120b` hoặc thay đổi theo tài nguyên Groq API của sếp) và kết nối `groqApi` credentials.
- **AI Agent & Analyze Patterns Developer:** Node code xử lý và AI Agent sẽ tổng hợp dữ liệu, đánh giá pattern làm việc.
- **Send a message in Gmail & Update Github Issue:** Kết nối tài khoản Gmail (`gmailOAuth2`) và GitHub (`githubApi`) để gửi email báo cáo chi tiết và tự động tạo Issue cảnh báo trên GitHub.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để kiểm tra dữ liệu mẫu chạy qua các node.
- Sau khi kiểm tra thành công, bật nút **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc nội bộ:** Thêm node Slack hoặc Telegram để bắn thông báo trực tiếp vào channel của Engineering Team mỗi khi phát hiện chỉ số burnout cao.
- **Lưu trữ lịch sử:** Kết nối thêm Google Sheets hoặc Notion để lưu trữ lịch sử báo cáo wellness theo từng tuần/tháng, giúp theo dõi sức khỏe đội ngũ lâu dài.
- **Tùy chỉnh Prompt cho AI:** Tinh chỉnh system prompt trong AI Agent để Groq AI đưa ra các lời khuyên wellness phù hợp hơn với văn hóa công ty của sếp.

### 📌 Kết luận
Việc chăm sóc sức khỏe tinh thần cho lập trình viên chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy áp dụng ngay workflow này để xây dựng một đội ngũ kỹ thuật bền vững, hạnh phúc và năng suất cao!