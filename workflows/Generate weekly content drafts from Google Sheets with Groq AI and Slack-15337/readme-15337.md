---
title: "🚀 Tự động tạo bản thảo nội dung hàng tuần từ Google Sheets với Groq AI và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy ý tưởng từ Google Sheets, sử dụng Groq AI để viết bài blog, kịch bản video, bài đăng mạng xã hội và gửi báo cáo qua Slack."
slug: "tu-dong-tao-noi-dung-google-sheets-groq-ai-slack"
tags: [n8n, automation, groq, google-sheets, slack, ai-content-creation]
keywords: [n8n workflow, tự động hóa content, Groq AI, Google Sheets automation, Slack bot, content marketing automation]
---

# 🚀 Tự động tạo bản thảo nội dung hàng tuần từ Google Sheets với Groq AI và Slack

Các sếp làm content marketing chắc chắn hiểu cảm giác "cạn kiệt ý tưởng" hoặc ngập đầu trong việc viết dàn ý blog, kịch bản video và bài đăng mạng xã hội mỗi tuần. Việc lên kế hoạch thủ công vừa tốn thời gian, vừa dễ bỏ sót tiến độ. 

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: lấy ý tưởng từ Google Sheets, giao cho các "chuyên gia AI" (Groq AI) viết nội dung chuyên sâu dựa theo từng định dạng (Blog, Video, Social), tổng hợp kết quả gửi về Slack cho team duyệt, đồng thời cập nhật trạng thái trên Google Sheets để tránh trùng lặp. Hoạt động 100% tự động mà không cần tốn một xu tiền thuê server đắt đỏ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không còn phải ngồi viết từng dàn ý hay kịch bản thủ công.
- **Đa dạng hóa định dạng:** Tự động phân loại và tạo nội dung riêng biệt cho Blog, Video (YouTube/TikTok), và Social Media.
- **Cộng đồng làm việc mượt mà:** Báo cáo chi tiết được gửi thẳng vào kênh Slack của team hàng tuần.
- **Quản lý dữ liệu thông minh:** Tự động đồng bộ trạng thái bài viết trên Google Sheets (chuyển sang trạng thái "writing") để tránh xử lý lặp lại.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản Google và file Google Sheets quản lý lịch content.
- **Groq API Key:** Tài khoản Groq (miễn phí) để sử dụng các mô hình AI tốc độ cao.
- **Slack Bot Token / OAuth:** Tài khoản Slack và quyền gửi tin nhắn vào kênh (channel).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **New Workflow**, nhấn tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 19 nodes được chia thành 3 nhóm chính. Các sếp cần cấu hình các điểm quan trọng sau:

- **Fetch Content Backlog & Mark Status as Writing (Google Sheets):** 
  - Kết nối tài khoản Google Sheets thông qua `Credentials`.
  - Điền **Spreadsheet ID** và chọn đúng **Sheet Name** chứa danh sách ý tưởng.
  - Đảm bảo các cột trong sheet bao gồm: `Sr No`, `Topic`, `Type`, `Status`, `Deadline`.
- **SEO Strategist LLM, Video Producer LLM, Growth Expert LLM (Groq AI):**
  - Kết nối `groqApi` credentials.
  - Mô hình mặc định được cấu hình là `openai/gpt-oss-120b` (hoặc các model LLM mạnh mẽ khác do Groq cung cấp). Các sếp có thể tùy chỉnh prompt trong các Agent node tương ứng (`Generate Blog Outline`, `Generate Video Script`, `Generate Social Post`) để AI viết đúng văn phong thương hiệu.
- **Route by Format (Switch):** 
  - Node này sẽ tự động phân loại dựa trên cột `Type` (video, blog, social) để chuyển hướng dữ liệu đến nhánh AI phù hợp.
- **Post Summary to Slack (Slack):**
  - Kết nối tài khoản Slack (`slackOAuth2Api`).
  - Chọn kênh (Channel ID) mà bot sẽ gửi báo cáo tổng hợp hàng tuần.

#### 3. Kích hoạt ⚡️
- **Test run:** Bấm nút **Execute Workflow** thủ công với một vài dòng dữ liệu mẫu trong Google Sheets để kiểm tra luồng chạy từ đầu đến cuối.
- **Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để node `Check for New Ideas (Weekly)` tự động kích hoạt theo lịch hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo:** Ngoài Slack, các sếp có thể thêm node Telegram Bot để gửi bản thảo trực tiếp vào nhóm chat riêng của sếp.
- **Gửi email tự động:** Thêm bước gửi email bản thảo trực tiếp cho khách hàng hoặc biên tập viên duyệt.
- **Lưu trữ mở rộng:** Thay vì chỉ cập nhật Google Sheets, có thể lưu trực tiếp bản thảo AI sinh ra vào Google Docs hoặc Notion.

### 📌 Kết luận
Workflow **Generate weekly content drafts from Google Sheets with Groq AI and Slack** là trợ thủ đắc lực giúp tự động hóa khâu sáng tạo nội dung từ A-Z. Hãy cài đặt ngay hôm nay để giải phóng thời gian và tối ưu hóa hiệu suất làm việc cho đội ngũ marketing của các sếp!