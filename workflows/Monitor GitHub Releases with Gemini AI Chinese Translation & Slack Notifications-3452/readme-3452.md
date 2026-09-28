---
title: "🚀 Tự động giám sát GitHub Releases bằng Gemini AI và Slack Notifications"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi các bản phát hành GitHub, sử dụng Gemini AI để tóm tắt, dịch thuật và gửi thông báo qua Slack."
slug: "giam-sat-github-releases-gemini-ai-slack"
tags: [n8n, automation, github, ai, slack, gemini]
keywords: [n8n workflow, gitHub releases, gemini AI, slack notifications, tự động hóa github, dịch bản phát hành]
---

# 🚀 Tự động giám sát GitHub Releases bằng Gemini AI và Slack Notifications

Các sếp làm kỹ sư phần mềm hay quản lý dự án chắc hẳn đều hiểu cảm giác "ngợp thở" khi phải theo dõi hàng tá kho lưu trữ (repositories) trên GitHub để cập nhật các bản phát hành (Releases) mới nhất. Việc F5 liên tục hoặc đọc changelog dài dằng dặc bằng tiếng Anh (hoặc ngôn ngữ gốc) tốn rất nhiều thời gian và dễ bỏ sót thông tin quan trọng.

Giải pháp là gì? Workflow n8n này sẽ "thầu" trọn gói công việc đó cho các sếp: Tự động quét RSS release từ danh sách GitHub, nhờ **Google Gemini AI** tóm tắt và dịch thuật (mặc định sang tiếng Trung hoặc bất kỳ ngôn ngữ nào các sếp muốn), sau đó đẩy thông báo đẹp mắt thẳng vào **Slack**. Toàn bộ quá trình hoàn toàn tự động 100% không cần tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cập nhật tức thì:** Tự động kiểm tra release mới theo lịch trình (Cron Trigger) mà không bỏ sót bất kỳ phiên bản nào.
- **AI thông minh:** Sử dụng **Gemini AI** thông qua node `Information Extractor` để tự động chắt lọc thông tin cốt lõi và dịch nội dung sang ngôn ngữ mong muốn.
- **Chống trùng lặp thông minh:** Lưu trạng thái đã kiểm tra vào **Redis**, đảm bảo mỗi release mới chỉ gửi thông báo đúng 1 lần duy nhất.
- **Cảnh báo lỗi tự động:** Nếu có sự cố (ví dụ lỗi gọi API, lỗi AI), node `Send Error` sẽ lập tức bắn tin nhắn cảnh báo vào Slack để các sếp xử lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản mới nhất).
- **Redis Service:** Có sẵn một database Redis để lưu trữ state/ID các release đã đọc.
- **Google Gemini API Key:** Tài khoản hoặc API Key của Google AI / Gemini.
- **Slack Bot App:** Bot Slack đã được cấp quyền cấu hình đầy đủ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và dán trực tiếp vào n8n Editor của các sếp, hoặc import file JSON thông qua giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Cron Trigger:** Điều chỉnh quy tắc (Rule) thời gian chạy tùy ý. Mặc định workflow đang cấu hình chạy 10 phút một lần trong khung giờ từ 9 giờ sáng đến 11 giờ tối (`0 */10 9-23 * * *`).
- **GitHub Config (Node Code):** Mở node này và chỉnh sửa mảng JavaScript chứa danh sách các repo các sếp muốn theo dõi. Cấu trúc mỗi phần tử gồm `name` (tên hiển thị tùy ý) và `github` (đường dẫn dạng `owner/repo`).
   ```javascript
   [
     {
       "name": "n8n", 
       "github": "n8n-io/n8n"
     },
     {
       "name": "LobeChat",
       "github": "lobehub/lobe-chat"
     }
   ]
   ```
- **Gemini (Node lmChatGoogleGemini):** Chọn thông tin xác thực Google Gemini API của các sếp.
- **Information Extractor:** Kiểm tra `System Prompt`. Mặc định AI được yêu cầu trích xuất thông tin và dịch sang tiếng Trung. Các sếp có thể đổi prompt thành tiếng Việt hoặc ngôn ngữ khác nếu thích.
- **Redis Get / Redis Set Id:** Cấu hình thông tin kết nối Redis (Host, Port, Password) để workflow ghi nhận các release đã thông báo.
- **Send Message & Send Error (Node Slack):** 
  - Chọn Slack Credentials cho cả 2 node này.
  - Điền Channel ID nơi muốn nhận thông báo release và thông báo lỗi.
  - *Lưu ý cấu hình Slack App:* Trong phần `Bot Token Scopes` của Slack App, nhớ cấp quyền `chat:write` và `chat:write.customize`, sau đó tiến hành Install/Reinstall App để lấy `Bot User OAuth Token`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test workflow) bằng cách nhấn nút **Execute Workflow** để kiểm tra luồng dữ liệu.
- Sau khi mọi thứ chạy mượt mà, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản nhánh gửi tin nhắn để bắn song song sang Telegram, Discord hoặc Microsoft Teams.
- **Lưu trữ lịch sử:** Kết hợp thêm node Google Sheets hoặc Notion để lưu lại toàn bộ lịch sử các bản release quan trọng phục vụ việc tra cứu sau này.
- **Tùy biến Prompt AI:** Yêu cầu Gemini phân loại mức độ quan trọng của bản release (Major, Minor, Patch, Security Fix) để gắn nhãn màu sắc (Color tag) khác nhau trên Slack.

### 📌 Kết luận
Với workflow n8n này, các sếp sẽ tiết kiệm được hàng giờ mỗi tuần trong việc theo dõi tiến độ công nghệ của các bên thứ ba. Hãy cài đặt ngay lên hệ thống tự động hóa của mình và tối ưu hóa thời gian cho các công việc chiến lược hơn!