---
title: "🚀 Tự động tạo và lên lịch đăng bài mạng xã hội X (Twitter) & LinkedIn với AI"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa quy trình sáng tạo nội dung, đăng bài đa nền tảng X và LinkedIn sử dụng Gemini và OpenAI."
slug: "tu-dong-tao-va-len-lich-dang-bai-mang-xa-hoi-x-va-linkedin"
tags: [n8n, automation, no-code, social-media, ai, gemini, openai]
keywords: [n8n workflow, tu dong hoa mang xã hội, dang bai linkedin twitter ai, google gemini openAi n8n]
---

# 🚀 Tự động hóa quy trình sáng tạo và đăng bài X, LinkedIn với AI

Việc duy trì sự hiện diện thường xuyên trên các nền tảng mạng xã hội như X (Twitter) và LinkedIn là chìa khóa sống còn để xây dựng thương hiệu cá nhân hoặc doanh nghiệp. Tuy nhiên, việc phải nghĩ ý tưởng, viết nội dung riêng cho từng nền tảng, lên lịch và đăng thủ công ngốn rất nhiều thời gian quý báu của các sếp.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: từ việc tiếp nhận chủ đề qua form, sử dụng sức mạnh của **Google Gemini** và **OpenAI** để sáng tạo nội dung, tự động đăng lên X & LinkedIn, cho đến việc phân tích bài viết tương tác cao để gợi ý ý tưởng mới và lưu trữ vào Google Sheets. Tất cả diễn ra hoàn toàn tự động mà không cần tốn một giọt mồ hôi viết lách thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Chỉ cần nhập tiêu đề/chủ đề ngắn gọn, AI sẽ tự động viết nội dung chuẩn SEO, tối ưu hóa riêng cho cả X và LinkedIn.
- **Đa kênh đồng bộ:** Đăng bài đồng thời lên X và LinkedIn chỉ trong một nốt nhạc, kết quả được tổng hợp trực quan qua Form xác nhận.
- **Nuôi dưỡng ý tưởng liên tục:** Tự động quét các bài viết có lượng tương tác cao trên LinkedIn, kết hợp OpenAI để sinh ra ý tưởng nội dung mới và lưu thẳng vào Google Sheets.
- **Kiểm soát chặt chẽ:** Thông báo tức thì qua Slack để đội ngũ duyệt nội dung hoặc theo dõi tiến độ dễ dàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Gemini API Key** (cho node Google Gemini Chat Model).
- **OpenAI API Key** (cho node Generate Post Ideas - GPT-4o-mini).
- **Tài khoản Twitter (X) & LinkedIn** (đã cấp quyền API/OAuth).
- **Google Sheets** (tạo sẵn file chứa bảng nháp nội dung).
- **Slack Workspace & Webhook** (để nhận thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node cốt lõi sau để hệ thống chạy đúng ý đồ:
- **Receive Post Title (`formTrigger`):** Thiết lập giao diện form đầu vào để người dùng nhập tiêu đề hoặc chủ đề bài viết.
- **Generate AI Content (`agent` kết hợp `Google Gemini Chat Model` & `Format AI Output`):** Điền `Google Gemini API Key` và viết system prompt rõ ràng để AI phân tách rõ nội dung dành riêng cho X (ngắn gọn, hashtag) và LinkedIn (chuyên nghiệp, sâu sắc).
- **Post to X (`twitter`) & Post to LinkedIn (`linkedIn`):** Kết nối tài khoản mạng xã hội tương ứng qua OAuth để cấp quyền đăng bài tự động.
- **Schedule Trigger (`scheduleTrigger`):** Cài đặt thời gian biểu (ví dụ: chạy định kỳ mỗi tuần/tháng) để tự động quét nội dung.
- **Fetch LinkedIn Posts (`httpRequest`):** Điền API Endpoint của LinkedIn để lấy danh sách bài viết cũ.
- **Filter High Engagement (`function`):** Tùy chỉnh đoạn code JavaScript lọc bài viết có lượt like/comment vượt ngưỡng mong muốn.
- **Generate Post Ideas OpenAI (`openAi`):** Chọn model `gpt-4o-mini` và truyền dữ liệu bài viết tương tác cao vào Prompt để OpenAI gợi ý ý tưởng mới.
- **Save Drafts to Google Sheets (`googleSheets`):** Chọn file Google Sheet và mapping chính xác các cột (Tiêu đề, Nội dung nháp, Nền tảng...).
- **Notify Reviewer (`slack`):** Cấu hình kênh Slack nhận thông báo khi có bài viết mới được tạo hoặc lưu nháp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách nhập một chủ đề bất kỳ vào `Receive Post Title`.
- Kiểm tra kết quả trên X, LinkedIn, Google Sheets và Slack.
- Nếu mọi thứ mượt mà, bật công tắc **Active** góc trên bên phải để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước duyệt qua Telegram/Slack:** Thay vì tự động đăng ngay lập tức, các sếp có thể thêm nút "Approve / Reject" qua Telegram để kiểm duyệt nội dung AI viết trước khi cho lên sóng.
- **Tích hợp thêm Notion hoặc Airtable:** Thay vì Google Sheets, các sếp có thể lưu trữ ý tưởng bài viết vào Notion Database để quản lý trực quan hơn theo dạng Kanban.
- **Thêm AI Image Generation:** Tích hợp thêm node OpenAI (DALL-E 3) hoặc Midjourney để tự động tạo hình ảnh minh họa đi kèm bài đăng mạng xã hội.

### 📌 Kết luận
Với workflow n8n này, việc sáng tạo nội dung đa nền tảng không còn là gánh nặng mà trở thành một cỗ máy tự động hóa hoàn hảo. Hãy "lên đồ" ngay cho hệ thống của các sếp để tối ưu hóa hiệu suất truyền thông ngay hôm nay!