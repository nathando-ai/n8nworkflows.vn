---
title: "🚀 Tự động săn việc làm Reddit, phân tích với GPT-4o và gửi cảnh báo qua Telegram bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài đăng tuyển dụng trên Reddit, sử dụng Azure OpenAI phân tích và lọc trùng lặp qua Google Sheets trước khi gửi thông báo tức thì về Telegram."
slug: "tu-dong-san-viec-lam-reddit-gpt4o-telegram-n8n"
tags: [n8n, automation, ai-summarization, reddit, telegram, google-sheets, azure-openai]
keywords: [n8n workflow, tự động hóa reddit, gpt-4o phân tích việc làm, telegram alert, google sheets n8n]
---

# 🚀 Tự động săn việc làm Reddit, phân tích với GPT-4o & Bắn thông báo qua Telegram

Việc thủ công lướt các subreddit tìm kiếm cơ hội việc làm hay đối tác (như r/n8n, r/freelance, r/forhire) tốn rất nhiều thời gian mà lại dễ bỏ lỡ các tin đăng mới. Các sếp có bao giờ tự hỏi làm sao để không bao giờ bỏ lỡ một bài tuyển dụng nào phù hợp với kỹ năng của mình không? 

Bài viết này sẽ hướng dẫn các sếp cách triển khai một workflow n8n cực kỳ mạnh mẽ giúp tự động quét Reddit, nhờ AI (GPT-4o qua Azure) phân tích, lưu trữ và lọc trùng lặp qua Google Sheets, sau đó bắn tin nhắn cảnh báo thẳng vào Telegram của các sếp ngay khi có bài đăng mới!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 săn deal liên tục không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Quét các bài tuyển dụng theo lịch trình (Schedule) mà không cần động tay.
- **AI thông minh:** Sử dụng GPT-4o-mini phân tích, tóm tắt và đánh giá bài đăng chuẩn xác theo yêu cầu.
- **Không sợ trùng lặp:** Tự động kiểm tra Google Sheets để chắc chắn các sếp không nhận 1 thông báo 2 lần cho cùng một bài đăng.
- **Nhận tin tức thì:** Bắn tin nhắn trực tiếp qua Telegram cá nhân hoặc nhóm làm việc để ứng tuyển đầu tiên.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Reddit App Info:** Tạo một Script App miễn phí tại [Reddit Developers Apps](https://reddit.com/prefs/apps).
- **Azure OpenAI API:** Credentials kết nối với Azure OpenAI để dùng mô hình `gpt-4o-mini`.
- **Google Sheets:** Một file Google Sheet làm cơ sở dữ liệu lưu các bài đã quét.
- **Telegram Bot Token:** Tạo bot thông qua [@BotFather](https://t.me/BotFather) trên Telegram.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn cung cấp, sau đó paste trực tiếp vào n8n Editor hoặc import file JSON vào không gian làm việc của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy lần lượt cấu hình các node cốt lõi sau:

- **Schedule Trigger:** Cài đặt chu kỳ thời gian quét bài đăng tùy ý các sếp (ví dụ: mỗi 30 phút hoặc 1 tiếng chạy 1 lần).
- **Generate Token - Reddit & Search N8N (HTTP Request):** 
  - Tại node tạo token, cấu hình cURL command với Client ID và Secret lấy từ tài khoản Reddit Developer của các sếp theo định dạng:
    ```bash
    curl -X POST \
      -u "script_app_id:script_app_secret" \
      -A "YOUR_APP_NAME/0.1 by YOUR_USERNAME" \
      -d 'grant_type=password&username=YOUR_USERNAME&password=YOUR_PASSWORD' \
      https://www.reddit.com/api/v1/access_token
    ```
  - Tại node `Search N8N`, tùy chỉnh lại Sub-reddit muốn quét (ví dụ: `r/n8n` hoặc `r/forhire`), chọn từ khóa hoặc flair cần tìm kiếm và giới hạn số lượng bài trả về.
- **Azure OpenAI Chat Model & Basic LLM Chain:** Chọn credentials Azure OpenAI, kiểm tra lại model (`gpt-4o-mini`) và tinh chỉnh System Prompt của AI nếu muốn nó tập trung phân tích kỹ năng cụ thể nào đó.
- **Get Rows That Match & Append Data In Sheet (Google Sheets):** Kết nối tài khoản Google Sheets thông qua OAuth2, trỏ tới file Google Sheet lưu log bài đăng để hệ thống đối chiếu xem tiêu đề bài viết đã tồn tại chưa.
- **Telegram Trigger & Send a Text Message:** 
  - Kích hoạt `Telegram Trigger` và gửi 1 tin nhắn cho Bot của các sếp để lấy Chat ID cá nhân.
  - Cập nhật Chat ID đó vào node `Send a Text Message` để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test workflow) bằng dữ liệu giả lập hoặc bấm nút **Execute Workflow** để kiểm tra dòng dữ liệu qua từng node (`If It Doesn't Exist`, `Split Out Code`,...).
- Nếu mọi thứ xanh mướt, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Telegram, các sếp có thể nối thêm node Slack hoặc Discord để gửi thông báo vào kênh chung của team dev/freelance.
- **Lưu trữ nâng cao:** Thay vì dùng Google Sheets, có thể thay thế bằng Airtable hoặc Notion Database để quản lý danh sách việc làm trực quan hơn.
- **Lọc thông minh hơn:** Tùy chỉnh đoạn code ở node `Split Out Code` để chỉ lọc ra các bài đăng có mức ngân sách hoặc công nghệ cụ thể (ví dụ: Python, n8n, AI Agents).

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" giúp các freelancer, developer hayAgency tự động hóa hoàn toàn quy trình tìm kiếm khách hàng và việc làm trên Reddit. Hãy setup ngay hôm nay để không bỏ lỡ bất kỳ cơ hội kiếm tiền tiềm năng nào các sếp nhé!