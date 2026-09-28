---
title: "🚀 Tự động quét tuyển dụng trên X (Twitter) bằng Apify, AI Agent và Telegram Alerts"
description: "Hướng dẫn xây dựng workflow n8n tự động cào bài đăng tuyển dụng trên X/Twitter, lọc thông minh bằng OpenAI, chống trùng lặp qua Google Sheets và cảnh báo ngay lập tức qua Telegram."
slug: "tu-dong-quet-tuyen-dung-x-twitter-apify-ai-telegram"
tags: [n8n, automation, no-code, apify, openai, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa tuyển dụng, cào twitter apify, ai agent lọc việc làm, telegram alert n8n]
---

# 🚀 Tự động quét tuyển dụng trên X (Twitter) bằng Apify, AI Agent và Telegram Alerts

Các sếp làm freelancer, agency hay đang tìm kiếm khách hàng/việc làm chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải lướt X (Twitter) hàng giờ đồng hồ để tìm các bài đăng tuyển dụng (hiring posts). Đa phần kết quả trả về toàn là bài tự quảng cáo (self-promo) hoặc không đúng trọng tâm. 

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: Quét bài đăng trên X bằng **Apify**, dùng **AI Agent** phân tích ý định tuyển dụng thực sự, lọc trùng qua **Google Sheets** và bắn thông báo nóng hổi về **Telegram** cho các sếp. Không cần viết code phức tạp, chỉ cần thiết lập một lần và chạy 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần canh, lướt Twitter thủ công mỗi ngày.
- **Lọc nhiễu cực chuẩn bằng AI:** AI Agent tự động loại bỏ các bài đăng tự PR bản thân, chỉ giữ lại đúng tin tuyển dụng thực tế.
- **Không bao giờ bị làm phiền bởi tin trùng lặp:** Tự động kiểm tra URL trong Google Sheets trước khi gửi thông báo.
- **Phản hồi chớp nhoáng:** Nhận ngay thông tin chi tiết (link bài viết, tác giả, nội dung, địa điểm) qua Telegram ngay khi có cơ hội mới xuất hiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Apify** kèm API Token và Actor phù hợp (ví dụ: `apidojo/tweet-scraper`).
- **Tài khoản OpenAI** kèm API Key để chạy AI Agent (Model `gpt-4.1-mini`).
- **Google Sheets API / Credentials** để lưu trữ và chống trùng lặp dữ liệu.
- **Telegram Bot Token và Chat ID** để nhận tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:
- **6 hours (scheduleTrigger):** Định thời gian quét tự động (mặc định 6-12 tiếng chạy một lần, có thể tùy chỉnh theo nhu cầu).
- **HTTP Request:** Cấu hình kết nối tới Apify API (sử dụng Actor `apidojo/tweet-scraper`) với các từ khóa tìm kiếm mong muốn (ví dụ: *n8n developer, looking for n8n, hire AI automation*). Nhớ gắn Apify API key.
- **Edit Fields:** Chuẩn hóa các trường dữ liệu đầu ra như `url`, `text`, `author.userName`, `author.url`, `author.location`.
- **OpenAI Chat Model1 & AI Agent1:** Chọn model `gpt-4.1-mini` và thiết lập prompt cho AI Agent để nhận diện chính xác ý định tuyển dụng, loại bỏ bài đăng tự PR.
- **Get row(s) in sheet in Google Sheets1 & Append or update row in sheet1:** Kết nối tài khoản Google Sheets, trỏ tới file Sheet quản lý để kiểm tra trùng lặp qua URL và lưu thông tin lead mới.
- **Code1:** Node JavaScript xử lý và trích xuất dữ liệu JSON an toàn từ kết quả trả về của AI.
- **Send a text message1 (Telegram):** Điền Telegram Bot Token và Chat ID để nhận thông báo công việc.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test step / Execute workflow**) với một vài từ khóa mẫu để kiểm tra dữ liệu chảy qua các node.
- Sau khi thấy thông báo bắn về Telegram chuẩn chỉnh, các sếp bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa từ khóa:** Thay đổi từ khóa tìm kiếm trong HTTP Request để săn các vị trí khác như *video editor, graphic designer, copywriter*...
- **Mở rộng kênh thông báo:** Kết nối thêm node Slack hoặc Discord để đẩy lead về nhóm team cùng xử lý.
- **Nâng cấp Google Sheets thành CRM mini:** Bổ sung thêm các cột trạng thái (*Status: New, Contacted, Interview*), ngày tháng outreach để quản lý khách hàng chuyên nghiệp hơn.

### 📌 Kết luận
Workflow này là một vũ khí cực kỳ lợi hại cho các freelancer và agency muốn chủ động tìm kiếm khách hàng trên mạng xã hội mà không tốn sức. Hãy áp dụng ngay để không bỏ lỡ bất kỳ cơ hội việc làm giá trị nào nhé các sếp!