---
title: "🚀 Tự Động Hóa Viết Bài WordPress Hàng Tuần Từ Chủ Đề SharePoint Kèm Ảnh AI"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy chủ đề từ SharePoint, sử dụng AI viết bài, tạo hình ảnh minh họa và đăng bản nháp lên WordPress một cách mượt mà."
slug: "tu-dong-hoa-viet-bai-wordpress-tu-sharepoint"
tags: [n8n, automation, wordpress, sharepoint, ai-content-creation, openai, google-gemini]
keywords: [n8n workflow, tự động viết bài wordpress, sharepoint to wordpress, ai content creator n8n, tao anh ai wordpress]
---

# 🚀 Tự Động Hóa Viết Bài WordPress Hàng Tuần Từ Chủ Đề SharePoint Kèm Ảnh AI

Các sếp có đang đau đầu vì việc lên lịch, nghiên cứu chủ đề, viết bài chuẩn SEO và tìm hình ảnh minh họa cho website WordPress mỗi tuần ngốn quá nhiều thời gian? Việc tạo nội dung thủ công không chỉ chậm chạp mà còn dễ gây gián đoạn lịch xuất bản, ảnh hưởng lớn đến SEO vàtraffic của website.

Giải pháp ở đây chính là quy trình tự động hóa 100% không cần code (No-code) bằng n8n. Workflow này sẽ thay đội ngũ content làm toàn bộ các bước: lấy ý tưởng từ **SharePoint**, phân loại chuyên mục tự động nhờ AI, viết bài hoàn chỉnh, vẽ ảnh minh họa bằng AI, đăng bản nháp lên **WordPress** và cuối cùng là gửi email thông báo qua **Microsoft Outlook**. Các sếp chỉ việc kiểm duyệt và bấm xuất bản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Bỏ qua hoàn toàn các bước lên ý tưởng, phác thảo và tìm kiếm hình ảnh thủ công.
- **Tự động hóa toàn diện**: Định kỳ hàng tuần, hệ thống tự động quét danh sách chủ đề trên SharePoint và xử lý tuần tự.
- **Chất lượng nội dung cao & Đa phương tiện**: Sử dụng các mô hình AI mạnh mẽ (OpenAI GPT, Google Gemini) để viết bài chuyên sâu và tạo hình ảnh độc quyền, kèm theo khớp nối danh mục tự động.
- **Quy trình kiểm duyệt an toàn**: Bài viết được lưu dưới dạng **Draft (Bản nháp)** trên WordPress và gửi email thông báo để các sếp kiểm tra trước khi công khai.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Microsoft 365 Account**: Truy cập vào SharePoint (chứa danh sách chủ đề bài viết) và Microsoft Outlook (để nhận thông báo).
- **WordPress Website**: Tài khoản quản trị kèm ứng dụng mật khẩu (Application Passwords) hoặc kết nối REST API/OAuth.
- **AI API Keys**: 
  - OpenAI API Key (cho GPT viết bài và tạo tiêu đề).
  - Google Gemini API Key (cho việc tạo prompt và vẽ ảnh minh họa).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n.io (hoặc file mẫu), sau đó tại giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc dán trực tiếp mã JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 20 nodes phối hợp nhịp nhàng. Các sếp cần tập trung cấu hình kỹ các node sau:

- **Schedule Trigger**: Thiết lập lịch chạy định kỳ (ví dụ: Chạy vào mỗi thứ Hai hàng tuần lúc 8:00 sáng).
- **Get Topics (microsoftSharePoint)**: Kết nối tài khoản Microsoft 365, trỏ đến site SharePoint và danh sách (List) chứa các chủ đề bài viết.
- **Fetch WP Categories & Format Categories**: Cấu hình URL trang WordPress của các sếp để lấy danh sách Category hiện có, giúp AI biết cách phân loại bài viết chính xác.
- **Match Categories AI (openAi)**: Cấu hình credentials OpenAI và kiểm tra Prompt để AI map đúng chủ đề với danh mục có sẵn trên website.
- **Write Article & Generate Title (agent & lmChatOpenAi)**: Cấu hình OpenAI Chat Model để tinh chỉnh giọng văn (tone of voice), độ dài và cấu trúc bài viết theo đúng ý muốn.
- **Generate Feature Image (googleGemini)**: Cấu hình node Google Gemini để tạo hình ảnh đại diện ấn tượng dựa trên tiêu đề bài viết.
- **Add Draft to WP (wordpress)**: Điền thông tin kết nối WordPress (URL, Username, Application Password) để hệ thống tự động đẩy bài viết về trạng thái *Draft*.
- **Send Notification (microsoftOutlook)**: Cấu hình email nhận thông báo sau khi bài viết đã được tạo thành công trên WordPress.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với một dòng dữ liệu mẫu từ SharePoint và kiểm tra kết quả trên WordPress Drafts.
- Nếu mọi thứ hoạt động trơn tru, hãy gạt công tắc sang trạng thái **Active** để hệ thống tự động hóa làm việc thay các sếp!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ nhận email qua Microsoft Outlook, các sếp có thể gắn thêm node **Telegram** hoặc **Slack** để nhận tin nhắn tức thời ngay khi bài viết nháp vừa được tạo xong.
- **Lưu lịch sử vào Google Sheets / Airtable**: Thêm một bước lưu lại trạng thái bài viết (Tiêu đề, Link bản nháp, Ngày tạo) vào Google Sheets để dễ dàng theo dõi tiến độ content hàng tháng.
- **Tích hợp Sub-workflow**: Tách phần xử lý hình ảnh hoặc viết bài thành các sub-workflow riêng biệt nếu các sếp muốn tái sử dụng cho các chiến dịch mạng xã hội khác (Facebook, LinkedIn).

### 📌 Kết luận
Với workflow n8n cực kỳ thông minh này, việc vận hành một trang web WordPress với lượng nội dung đều đặn hàng tuần chưa bao giờ dễ dàng đến thế. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm việc và bứt phá lượng traffic cho website của các sếp!