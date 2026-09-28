---
title: "🚀 Tự động giám sát bài viết viral trên Reddit và tóm tắt bằng GPT-4o-mini gửi Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động quét các bài viết xu hướng trên Reddit theo ngách, dùng GPT-4o-mini tóm tắt và gửi thẳng về Telegram mỗi ngày."
slug: "tu-dong-giam-sat-reddit-va-tom-tat-gpt-4o-mini-telegram"
tags: [n8n, automation, reddit, openai, telegram, ai-summarization]
keywords: [n8n workflow, tự động hóa reddit, tóm tắt bài viết ai, openai gpt-4o-mini, telegram bot n8n]
---

# 🚀 Tự động giám sát bài viết viral trên Reddit và tóm tắt bằng GPT-4o-mini gửi Telegram

Việc cập nhật tin tức, xu hướng công nghệ hay nội dung viral trên Reddit mỗi ngày để nghiên cứu thị trường (Market Research) thường tốn rất nhiều thời gian. Nếu các sếp cứ phải lướt thủ công từng subreddit, chắc chắn sẽ bị "ngợp" trước lượng thông tin khổng lồ. 

Giải pháp hoàn hảo là đây: Workflow n8n tự động hóa 100 giúp quét các bài viết nổi bật trên Reddit, lọc ra những bài thực sự chất lượng, dùng AI (GPT-4o-mini) chắt lọc ý chính và gửi báo cáo gọn gàng thẳng về Telegram của các sếp vào mỗi buổi sáng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối**: Không cần mất hàng giờ lướt Reddit, toàn bộ thông tin "nóng" đã được gom lại một chỗ.
- **Nội dung chắt lọc thông minh**: GPT-4o-mini tự động tóm tắt ngắn gọn, súc tích chuẩn định dạng Telegram.
- **Lọc nhiễu hiệu quả**: Chỉ giữ lại các bài viết thực sự viral (đạt ngưỡng tương tác cao hoặc mới nổi trong 24h).
- **Hoạt động tự động 24/7**: Chạy đều đặn mỗi ngày vào lúc 8 giờ sáng, sẵn sàng báo cáo ngay khi các sếp vừa nhấp ngụm cà phê sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Reddit API / OAuth2**: Để n8n kết nối và lấy dữ liệu bài viết.
- **OpenAI API Key**: Sử dụng mô hình `gpt-4o-mini` tiết kiệm và mạnh mẽ.
- **Telegram Bot Token & Chat ID**: Để bot gửi tin nhắn tóm tắt về tài khoản hoặc nhóm Telegram của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để workflow chạy mượt mà:

- **Daily 8 AM Trigger**: Node lịch chạy mặc định lúc 8:00 sáng mỗi ngày. Các sếp có thể đổi giờ nếu muốn nhận tin vào khung giờ khác.
- **Workflow Configuration**: Node này dùng để thiết lập danh sách các ngách (niches) muốn theo dõi (mặc định là: *technology, programming, science, gaming*) và cấu hình **Telegram Chat ID** của các sếp.
- **Get Reddit Viral Posts**: Kết nối tài khoản thông qua **Reddit OAuth2 API** để n8n có quyền truy cập lấy bài viết.
- **Filter (Quality Filter)**: Node này giúp giữ lại các bài viết viral thực sự đáp ứng điều kiện tương tác (ví dụ: trên 500 upvotes HOẶC trên 70 upvotes trong vòng 24 giờ). Các sếp có thể tùy chỉnh lại con số này cho phù hợp với nhu cầu.
- **AI Summarizer & OpenAI Chat Model**: Chọn model `gpt-4o-mini` và điền **OpenAI API Key** để AI bắt đầu công việc tóm tắt nội dung.
- **Send to Telegram**: Kết nối **Telegram Bot API** và đảm bảo Chat ID đã được truyền xuống từ node cấu hình ban đầu.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu xem tin nhắn có bắn về Telegram ngon lành chưa.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Ngoài Telegram, các sếp có thể gắn thêm node Slack hoặc Discord để team cùng theo dõi xu hướng thị trường.
- **Lưu trữ dữ liệu**: Thêm node Google Sheets hoặc Airtable ngay sau bước tóm tắt để lưu lại lịch sử các bài viết viral phục vụ cho việc nghiên cứu nội dung (Content Ideas) lâu dài.
- **Tùy biến Prompt AI**: Tinh chỉnh lại câu lệnh (prompt) trong AI Agent để mô hình viết tóm tắt theo phong cách hài hước, chuyên nghiệp hoặc tập trung vào một khía cạnh cụ thể mà các sếp quan tâm.

### 📌 Kết luận
Workflow này là một "trợ lý ảo" cực kỳ đắc lực cho những ai làm trong lĩnh vực sáng tạo nội dung, marketing hay nghiên cứu thị trường. Hãy triển khai ngay hôm nay để tối ưu hóa nguồn thông tin mỗi ngày cho các sếp!