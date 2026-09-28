---
title: "🚀 Tự động quét và thu thập URL bài viết từ mọi website với AI và Google Sheets"
description: "Xây dựng hệ thống tự động hóa trích xuất URL bài viết thông minh sử dụng AI Agent, GPT-5-mini, chuyển đổi HTML sang Markdown và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-quet-va-thu-thap-url-bai-viet-voi-ai-google-sheets"
tags: [n8n, automation, ai-agent, google-sheets, openai, web-scraping]
keywords: [n8n workflow, ai url extractor, tu dong cao du lieu, gpt-5-mini, google sheets automation]
---

# 🚀 Tự động quét và thu thập URL bài viết từ mọi website với AI và Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công lướt qua hàng loạt trang tin tức, blog hoặc website đối thủ mỗi ngày để tìm kiếm các bài viết mới phục vụ cho việc nghiên cứu thị trường (Market Research) hay làm Content Marketing không? Công việc copy-paste thủ công này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ sót thông tin quan trọng.

Giải pháp là đây! Workflow n8n siêu việt này sẽ giúp các sếp tự động hóa 100% quy trình: Đọc danh sách website nguồn từ Google Sheets $\rightarrow$ Tải mã nguồn trang web $\rightarrow$ Chuyển hóa HTML sang Markdown gọn gàng $\rightarrow$ Sử dụng AI thông minh (**GPT-5-mini**) để lọc và bóc tách chính xác các URL bài viết chất lượng $\rightarrow$ Tự động lưu ngược lại Google Sheets kèm theo chống trùng lặp. Hoàn toàn không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ lướt web thủ công, hệ thống tự động thu thập hàng trăm URL bài viết mỗi ngày.
- **AI thông minh lọc nhiễu:** AI Agent tự động nhận diện bài viết chuẩn, loại bỏ các trang điều hướng (navigation), trang danh mục (category), quảng cáo hay file PDF rác.
- **Chống trùng lặp thông minh:** Dữ liệu tự động đồng bộ vào Google Sheets, tự động bỏ qua các URL đã quét trước đó.
- **Hoạt động 24/7 tự động:** Chạy định kỳ mỗi 6 giờ sáng hoặc kích hoạt thủ công bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets Credentials** (OAuth2 API) để đọc/ghi dữ liệu.
- **OpenAI API Key** (Hỗ trợ mô hình `gpt-5-mini`).
- **File Google Sheets** chuẩn bị sẵn các cột: `URL`, `Source`, `Status`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, sau đó dán trực tiếp vào giao diện n8n Editor (hoặc Import file JSON từ nguồn gốc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes được thiết kế tối ưu, các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Node `Read Seed URLs` (Google Sheets):** 
  - Chọn Credentials Google Sheets của các sếp.
  - Trỏ đến file Google Sheet chứa danh sách các website nguồn (Seed URLs).
- **Node `Rate Limit (3s)` (Wait):** 
  - Đảm bảo độ trễ giữa các request (mặc định 3 giây) để tránh việc website mục tiêu chặn IP do quét quá nhanh.
- **Node `Fetch Webpage HTML` (HTTP Request):** 
  - Kiểm tra phần Header để đảm bảo đã thêm Custom User-Agent (giúp giả lập trình duyệt, vượt qua các lớp bảo mật cơ bản).
- **Node `AI URL Extractor` & `OpenAI Chat Model`:** 
  - Chọn đúng Credentials OpenAI.
  - Đảm bảo model được chọn là `gpt-5-mini` theo cấu hình tối ưu sẵn.
- **Node `Save Discovered URLs` (Google Sheets):** 
  - Cấu hình chế độ hoạt động `appendOrUpdate` (Thêm mới hoặc cập nhật).
  - Sử dụng URL làm khóa khớp dữ liệu (Match Key) để chống trùng lặp.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thử với một vài URL mẫu trên Google Sheets.
- Kiểm tra kết quả trả về trong Google Sheets xem các URL bài viết đã được bóc tách chuẩn xác chưa.
- Gạt công tắc sang **Active** để hệ thống tự động chạy theo lịch hẹn (Daily Schedule vào 6 giờ sáng hàng ngày).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào cuối quy trình để mỗi khi quét xong, bot sẽ gửi tin nhắn báo cáo số lượng bài viết mới tìm được về máy cho các sếp.
- **Kết hợp cào nội dung chi tiết:** Sau khi lấy được danh sách URL bài viết, các sếp có thể mở rộng workflow để tự động tóm tắt nội dung bài viết đó bằng AI và lưu vào Notion hoặc WordPress.
- **Quản lý trạng thái:** Tận dụng cột `Status` (mặc định là "Pending") để phát triển thêm các bước xử lý nội dung tiếp theo trong tương lai.

### 📌 Kết luận
Một công cụ tự động hóa cực kỳ mạnh mẽ giúp các sếp xây dựng cơ sở dữ liệu nội dung, nghiên cứu từ khóa đối thủ hoặc cập nhật tin tức ngành tự động mỗi ngày. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc!