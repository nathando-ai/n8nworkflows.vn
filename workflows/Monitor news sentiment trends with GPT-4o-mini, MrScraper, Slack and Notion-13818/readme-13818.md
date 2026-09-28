---
title: "🚀 Tự động theo dõi xu hướng cảm xúc tin tức với AI GPT-4o-mini, MrScraper, Slack và Notion"
description: "Hướng dẫn xây dựng workflow n8n tự động cào tin tức, phân tích tâm lý thị trường bằng AI GPT-4o-mini và lưu trữ kết quả lên Notion, Google Sheets đồng thời cảnh báo qua Slack."
slug: "tu-dong-theo-doi-xu-huong-cam-xuc-tin-tuc-n8n"
tags: [n8n, automation, ai, gpt-4o-mini, notion, slack, mrscraper]
keywords: [n8n workflow, phân tích cảm xúc tin tức, sentiment analysis, ai automation, mrscraper notion slack, gpt-4o-mini n8n]
---

# 🚀 Tự động theo dõi xu hướng cảm xúc tin tức với AI GPT-4o-mini, MrScraper, Slack và Notion

Việc theo dõi tin tức thị trường, đối thủ cạnh tranh hoặc ngành hàng thủ công mỗi ngày ngốn rất nhiều thời gian của các nhà quản lý và đội ngũ Marketing. Bạn phải liên tục lướt web, đọc bài viết, đánh giá xem tin tức đó mang sắc thái tích cực, tiêu cực hay trung lập, rồi lại lọ mọ copy paste vào Google Sheets hay Notion để báo cáo. 

Quá trình thủ công này không chỉ chậm chạp mà còn dễ bỏ lỡ các biến động thị trường quan trọng. Giải pháp tối ưu nhất lúc này là tự động hóa 100% quy trình với **n8n workflow**, kết hợp sức mạnh cào dữ liệu của **MrScraper**, khả năng phân tích đỉnh cao của **GPT-4o-mini**, cùng hệ thống lưu trữ **Notion/Google Sheets** và thông báo tức thời qua **Slack**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Định kỳ quét tin tức mới mà không cần con người nhúng tay vào.
- **Phân tích thông minh bằng AI:** GPT-4o-mini tự động đánh giá sắc thái (Sentiment), tóm tắt nội dung chính và chấm điểm mức độ quan trọng của tin tức.
- **Đồng bộ đa nền tảng:** Dữ liệu được lưu trữ có cấu trúc tại Notion và Google Sheets để tiện tra cứu lịch sử.
- **Cảnh báo thời gian thực:** Nhận ngay thông báo qua Slack khi có các tin tức quan trọng hoặc có xu hướng tiêu cực/tích cực bất thường.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **MrScraper Account:** Tài khoản và API Key để cào dữ liệu web.
- **OpenAI API Key:** Để sử dụng model GPT-4o-mini phân tích ngữ nghĩa.
- **Slack Workspace:** Kênh Slack để nhận cảnh báo tự động.
- **Notion Integration:** Trang Notion đã cấp quyền cho n8n Database.
- **Google Sheets:** File Google Sheets chuẩn bị sẵn các cột lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> **Import from File** và tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger:** Cài đặt mốc thời gian chạy tự động (ví dụ: Chạy 2 lần/ngày vào lúc 8h sáng và 8h tối).
- **MrScraper Node:** Điền API Key của MrScraper và chọn kịch bản (Scraping recipe) đã thiết lập sẵn trên nền tảng MrScraper để quét các trang báo/nguồn tin mong muốn.
- **Split in Batches:** Cấu hình kích thước lô (batch size) phù hợp để xử lý dữ liệu lần lượt, tránh vượt quá giới hạn API rate limit của OpenAI.
- **OpenAI Chat Model (`@n8n/n8n-nodes-langchain.lmChatOpenAi`) & Chain LLM:** 
  - Chọn Credentials OpenAI của bạn.
  - Chọn model: `gpt-4o-mini`.
  - Viết System Prompt hướng dẫn AI phân tích rõ ràng: Đọc nội dung bài viết, phân loại cảm xúc (Tích cực / Tiêu cực / Trung lập), tóm tắt 3 ý chính và đưa ra điểm số tác động.
- **Notion Node:** Kết nối với tài khoản Notion, chọn đúng Database đã tạo sẵn và map các trường dữ liệu (Tiêu đề, Link, Tóm tắt, Cảm xúc, Ngày tháng) từ output của AI.
- **Google Sheets Node:** Map dữ liệu vào các cột tương ứng trong bảng tính Google Sheets để làm báo cáo backup.
- **Slack Node:** Chọn channel nhận tin và soạn nội dung thông báo động (ví dụ: *"📰 Tin mới về [Chủ đề]: [Tiêu đề] - Cảm xúc: [Sentiment] - Xem chi tiết tại [Link]"*).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thủ công với dữ liệu mẫu xem các node có chạy xanh (thành công) hay không.
- Kiểm tra lại kết quả trên Notion, Google Sheets và Slack.
- Nếu mọi thứ ổn định, gạt công tắc sang chế độ **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo:** Thay vì chỉ nhận thông báo qua Slack, các sếp có thể add thêm node Telegram Bot để bắn tin nhắn trực tiếp về điện thoại cá nhân.
- **Bộ lọc thông minh (IF Node):** Thêm node điều kiện để chỉ gửi thông báo Slack với những bài viết có điểm cảm xúc cực đoan (quá tiêu cực hoặc quá tích cực), tránh làm phiền kênh chung bằng các tin tức trung lập.
- **Báo cáo tuần tự động:** Tạo thêm một nhánh chạy vào cuối tuần, tổng hợp tất cả dữ liệu từ Google Sheets/Notion, dùng AI viết bản "Bản tin tuần" và gửi email cho Ban Giám Đốc.

### 📌 Kết luận
Workflow tích hợp MrScraper, GPT-4o-mini, Notion và Slack là một "vũ khí" cực kỳ lợi hại giúp các doanh nghiệp, nhà đầu tư hoặc đội ngũ PR nắm bắt nhanh chóng mạch cảm xúc của thị trường mà không tốn chút sức lực thủ công nào. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của bạn nhé!