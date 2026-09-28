---
title: "🚀 Tự động hóa bản tin AI chuyên sâu từ RSS Feeds và Reddit bằng n8n, OpenAI & Slack"
description: "Xây dựng hệ thống tự động tổng hợp tin tức AI từ hàng trăm nguồn RSS, Reddit, blog công nghệ, lọc nội dung thông minh bằng LLM và phê duyệt qua Slack."
slug: "tu-dong-hoa-ban-tin-ai-rss-openai-slack"
tags: [n8n, automation, ai-newsletter, openai, slack, content-creation]
keywords: [n8n workflow, tự động hóa bản tin, AI newsletter, RSS automation, OpenAI o3-mini, Slack approval]
---

# 🚀 Tự động hóa bản tin AI chuyên sâu từ RSS Feeds và Reddit bằng n8n, OpenAI & Slack

Việc cập nhật tin tức công nghệ và AI mỗi ngày để viết bản tin (newsletter) hay blog tốn rất nhiều thời gian của các biên tập viên và nhà sáng tạo nội dung. Từ việc đi gom bài từ các trang blog lớn, lướt Reddit, lọc tin trùng lặp, cho đến khâu viết lách và chỉnh sửa. 

Workflow n8n mạnh mẽ này sẽ thay thế hoàn toàn quy trình thủ công đó. Hệ thống tự động thu thập thông tin từ hàng loạt nguồn uy tín, sử dụng AI (OpenAI & Anthropic) để chắt lọc những tin đắt giá nhất, tự động viết bản thảo chi tiết, và gửi thẳng vào Slack để các sếp duyệt hoặc góp ý chỉnh sửa trước khi xuất bản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Tự động gom tin từ hàng chục nguồn RSS, Google News, Hacker News, Reddit và các blog AI hàng đầu (OpenAI, Anthropic, Google, Meta...).
- **Lọc tin thông minh bằng AI**: Sử dụng các mô hình LLM tiên tiến (như OpenAI o3-mini, GPT-4o, Claude) để đánh giá độ liên quan và chọn ra top stories chất lượng nhất.
- **Quy trình Human-in-the-loop mượt mà**: Gửi bản thảo, tiêu đề và lý do chọn tin trực tiếp lên Slack để duyệt (`sendAndWait`). Các sếp có thể phản hồi để AI tự động viết lại.
- **Tạo nội dung đa dạng**: Tự động tạo phần mở đầu (Intro), các đoạn nội dung phân tích chi tiết, danh sách tin ngắn, và thậm chí cả ý tưởng video viral dựa trên nội dung bản tin.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **n8n Instance**: Phiên bản hỗ trợ LangChain (khuyến nghị n8n Cloud hoặc self-hosted bản mới nhất).
- **OpenAI API Key**: Dành cho các node AI (`o3-mini`, `OpenAI Chat Model`, và các chain LLM).
- **Anthropic API Key**: Dành cho `Anthropic Chat Model` (Claude Haiku).
- **Google Sheets API**: Để lưu log và quản lý dữ liệu bài viết.
- **Slack Bot & Workspace**: Để nhận thông báo, duyệt bài và tương tác phản hồi với AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Log to Google Sheets` & `Get Stories`**: Cần kết nối tài khoản Google Sheets của các sếp và điền chính xác **Google Sheet ID** vào tham số của node.
- **Các node Slack (`Share Selected Stories`, `Share Subject Line Approval Feedback`, `Upload Newsletter File`,...)**: Cập nhật lại **Channel ID** của workspace Slack nơi các sếp muốn bot gửi thông báo và nhận phản hồi phê duyệt.
- **Các node AI (OpenAI / Anthropic)**: Chọn đúng credentials API key đã chuẩn bị. Workflow sử dụng các model như `o3-mini` và `chatgpt-4o-latest` (hoặc Claude), hãy đảm bảo tài khoản OpenAI của các sếp có đủQuota/Credits.
- **Node `Stories Prompt`**: Tùy chỉnh lại prompt hệ thống nếu các sếp muốn thay đổi phong cách văn phong, tiêu chí chọn tin cho bản tin của riêng mình.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) từng phần hoặc chạy từng trigger RSS/Schedule để đảm bảo dữ liệu đổ về mượt mà qua các bước `Normalize` và `Merge`.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** để hệ thống tự động chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo**: Thay vì chỉ dùng Slack, các sếp có thể mở rộng thêm node Telegram hoặc Discord để nhận bản thảo phê duyệt linh hoạt hơn trên điện thoại.
- **Tự động đăng bài**: Kết hợp thêm node Webflow, WordPress hoặc Ghost ở cuối workflow để sau khi phê duyệt trên Slack, bản tin sẽ tự động lên sóng website.
- **Lưu trữ lịch sử**: Tận dụng Google Sheets để lưu lại tất cả các chủ đề đã viết, giúp AI kiểm tra trùng lặp nội dung cho các kỳ bản tin sau.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo dành cho các nhà sáng tạo nội dung, marketer hoặc solopreneur muốn xây dựng một kênh tin tức/bản tin AI chuyên nghiệp mà không phải tốn hàng giờ đọc báo mỗi ngày. Hãy thiết lập ngay hôm nay và tối ưu hóa quy trình sản xuất nội dung của các sếp!