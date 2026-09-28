---
title: "🚀 Tự động tạo video quảng cáo sản phẩm dựa trên ẩn dụ với AI và n8n"
description: "Khám phá cách tự động hóa quy trình sáng tạo video quảng cáo sản phẩm đỉnh cao sử dụng Google Gemini, DeepSeek, Creatomate và n8n."
slug: "tu-dong-tao-video-quang-cao-san-pham-ai-n8n"
tags: [n8n, automation, no-code, ai-video, content-creation, google-gemini, deepseek]
keywords: [n8n workflow, tạo video quảng cáo ai, tự động hóa n8n, google gemini, deepseek ai, creatomate, video marketing]
---

# 🚀 Tự động tạo video quảng cáo sản phẩm dựa trên ẩn dụ với AI và n8n

Việc sáng tạo nội dung video quảng cáo (video ads) độc đáo, mang tính nghệ thuật và ẩn dụ cao thường đòi hỏi rất nhiều thời gian lên ý tưởng, viết kịch bản, dựng hình và render. Nếu làm thủ công, các sếp sẽ mất hàng giờ liền cho mỗi chiến dịch mà chưa chắc đã tìm được góc nhìn sáng tạo đột phá.

Được phát triển bởi chuyên gia Koulikas Giannis, workflow n8n này sẽ giải quyết triệt để bài toán trên. Hệ thống kết hợp sức mạnh của các mô hình AI hàng đầu như **Google Gemini** và **DeepSeek** để tự động lên ý tưởng ẩn dụ, tối ưu prompt, render video qua **Creatomate**, lưu trữ trên **Google Cloud Storage** và tự động gửi thành phẩm hoàn chỉnh về **Telegram** cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Debian/Ubuntu VPS 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ khâu brainstorm ý tưởng ẩn dụ, viết kịch bản đến render và trả kết quả.
- **Sáng tạo không giới hạn:** Ứng dụng tư duy ẩn dụ (metaphor-based) độc đáo từ AI giúp quảng cáo bắt mắt và thu hút khách hàng hơn.
- **Tiết kiệm thời gian & chi phí:** Thay vì thuê đội ngũ dựng phim mất hàng tuần, hệ thống trả về video chỉ trong vài phút.
- **Nhận file tức thì:** Video hoàn thiện được gửi trực tiếp qua Telegram, sẵn sàng đăng tải lên các nền tảng TikTok, Reels, YouTube Shorts.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (phiên bản Cloud hoặc Self-hosted).
- **Google Gemini API Key** (dùng cho các node `Google Gemini Brainstormer`, `Google Gemini Creative Session`,...).
- **DeepSeek API Key** (dùng cho node `DeepSeek Conversational AI`).
- **Creatomate Account & API Key** (nền tảng tạo và render video tự động).
- **Google Cloud Storage (GCS)** bucket để lưu trữ file video.
- **Telegram Bot Token & Chat ID** để nhận thông báo và video trả về.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy toàn bộ JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp thông qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hệ thống gồm 34 nodes tích hợp đa dịch vụ, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Set Input Variables & Configure API Settings:** Điền thông tin thông số đầu vào cho sản phẩm của các sếp (tên sản phẩm, mô tả, tệp khách hàng mục tiêu) và cấu hình các biến môi trường cần thiết.
- **Các node AI (Google Gemini & DeepSeek):** Kết nối tài khoản thông qua phần **Credentials**, đảm bảo API key còn hạn mức sử dụng (quota).
- **Post to Creatomate API & HTTP Request nodes:** Cấu hình API Endpoint và Token của tài khoản Creatomate để hệ thống có thể gửi yêu cầu render video chính và video bổ trợ.
- **Upload Ad to Cloud Storage & Upload Complementary File:** Cấu hình kết nối Google Cloud Storage (Service Account JSON) để lưu trữ file video render thành công.
- **Send Video via Telegram:** Nhập `Bot Token` và `Chat ID` chính xác để nhận video báo cáo ngay trên điện thoại.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Manual Workflow Trigger`) với một sản phẩm mẫu để kiểm tra toàn bộ luồng từ AI brainstorm đến khi nhận video trên Telegram.
- Sau khi test thành công không báo lỗi, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể kết nối thêm node Slack hoặc Discord để đội ngũ Marketing cùng theo dõi ý tưởng video mới.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các kịch bản ẩn dụ và link video đã tạo nhằm phục vụ việc phân tích hiệu suất chiến dịch sau này.
- **Tích hợp Webhook:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Webhook Trigger` để kết nối với Google Forms hoặc Landing Page, khách hàng điền tên sản phẩm là hệ thống tự động sinh video quảng cáo.

### 📌 Kết luận
Workflow tạo video quảng cáo dựa trên ẩn dụ với AI này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình sản xuất nội dung video ngắn cho các nhà sáng tạo và doanh nghiệp. Hãy thiết lập ngay hôm nay để bứt phá doanh số và tối ưu hiệu suất marketing!