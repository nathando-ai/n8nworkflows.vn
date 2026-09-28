---
title: "🚀 Tự động tạo YouTube Chapter Timestamps & Community Post với WayinVideo và GPT-4o-mini"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc phân tích video YouTube, trích xuất khoảnh khắc quan trọng, tạo timestamp chuẩn và viết bài đăng cộng đồng."
slug: "tu-dong-hoa-youtube-chapter-timestamps-wayinvideo-gpt4o-mini"
tags: [n8n, automation, youtube, ai-agent, openai, googlesheets, content-creation]
keywords: [n8n workflow, tự động hóa youtube, wayinvideo, gpt-4o-mini, tạo timestamp youtube tự động, ai content creator]
---

# 🚀 Tự động tạo YouTube Chapter Timestamps & Community Post với WayinVideo và GPT-4o-mini

Đối với các nhà sáng tạo nội dung YouTube, giảng viên và các đội ngũ marketing, việc tạo thủ công các mốc thời gian (chapter timestamps) cho video dài và viết bài đăng cộng đồng (Community post) quảng bá là một công việc cực kỳ tốn thời gian. 

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: phân tích video, tìm kiếm các khoảnh khắc quan trọng qua API, sử dụng AI (GPT-4o-mini) để viết nội dung, và lưu trữ gọn gàng vào Google Sheets chỉ qua một biểu mẫu (Form) duy nhất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần phải xem lại video và bấm giờ thủ công từng phân đoạn nữa.
- **Chapter chuẩn xác:** Tự động sắp xếp thời gian theo thứ tự thời gian (bắt đầu từ 0:00 Introduction).
- **Cá nhân hóa nội dung đa kênh:** Tự động tạo cả đoạn mô tả video (description block) và bài đăng YouTube Community cực kỳ thu hút.
- **Lưu trữ khoa học:** Mọi dữ liệu được gom gọn vào Google Sheets, sẵn sàng copy-paste bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WayinVideo API Key:** Tài khoản và API key để gọi dịch vụ Find Moments API.
- **OpenAI API Key:** Để kết nối với mô hình `gpt-4o-mini`.
- **Google Account:** Tài khoản Google Sheets để lưu trữ dữ liệu đầu ra.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã JSON, sau đó dán (paste) vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số sau trong các nodes tương ứng:
- **`2. WayinVideo — Submit Find Moments`** & **`4. WayinVideo — Get Moments Results`**: Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API key thật của các sếp trong phần Header/Auth.
- **`9. OpenAI — GPT-4o-mini Model`**: Kết nối credential OpenAI của các sếp và đảm bảo model đang chọn là `gpt-4o-mini`.
- **`11. Google Sheets — Save Timestamp Library`**: Kết nối OAuth2 credential của Google Sheets và thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID bảng tính của các sếp.
- **Chuẩn bị Google Sheet**: Tạo một Sheet tab tên là `Timestamp Library` với các cột: `Video URL`, `Video Title`, `Channel Name`, `Video Category`, `Total Chapters`, `Total Moments Found`, `Video Duration (min)`, `Formatted Timestamps`, `Video Description Block`, `Community Post`, `Hashtags`, `Generated On`, `Status`.

#### 3. Kích hoạt ⚡️
- Điền thử thông tin vào node **`1. Form — Video URL + Details`** để test run xem dữ liệu trả về có mượt mà không.
- Nếu mọi thứ chạy trơn tru, hãy bật công tắc **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về điện thoại cho các sếp khi video đã được xử lý xong.
- **Tối ưu câu lệnh tìm kiếm (Query):** Nên dùng các từ khóa cụ thể như `'step by step section transition'` thay vì chỉ search `'steps'` để WayinVideo bắt trúng các khoảnh khắc đắt giá nhất.
- **Khắc phục rủi ro vòng lặp:** Lưu ý rằng workflow gốc chưa có bộ đếm vòng lặp (poll counter). Nếu video bị lỗi hoặc riêng tư, nó có thể loop liên tục. Các sếp có thể bổ sung biến đếm `pollCount` giới hạn 15 lần thử để an toàn hơn.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các content creator tự động hóa khâu hậu kỳ video YouTube một cách chuyên nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp nhé!