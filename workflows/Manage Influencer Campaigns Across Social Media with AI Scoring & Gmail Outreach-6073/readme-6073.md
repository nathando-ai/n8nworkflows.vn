---
title: "🚀 Tự động hóa chiến dịch Influencer Marketing đa nền tảng với AI Scoring và Gmail Outreach"
description: "Hướng dẫn xây dựng hệ thống n8n tự động tìm kiếm, chấm điểm AI, gửi email outreach và follow-up influencer trên Instagram, TikTok, YouTube cực kỳ chuyên nghiệp."
slug: "quan-ly-chien-dich-influencer-ai-gmail-n8n"
tags: [n8n, automation, influencer-marketing, ai-scoring, gmail, google-sheets]
keywords: [n8n workflow, tự động hóa influencer marketing, AI scoring influencer, gửi email tự động gmail n8n, quản lý chiến dịch KOL]
---

# 🚀 Tự động hóa chiến dịch Influencer Marketing đa nền tảng với AI Scoring và Gmail Outreach

Các sếp có đang cảm thấy đau đầu mỗi khi chạy chiến dịch Influencer/KOL Marketing không? Việc phải thủ công lên Instagram, TikTok, YouTube để tìm kiếm profile, lọc hàng trăm kênh, chấm điểm độ phù hợp, rồi lại soạn email, gửi tay và theo dõi lịch trình follow-up thực sự ngốn quá nhiều thời gian và nhân lực.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh: tự động tiếp nhận brief, tìm kiếm influencer đa nền tảng, sử dụng AI để chấm điểm chất lượng, tự động gửi email chào hàng (outreach), lên lịch follow-up và lưu trữ toàn bộ tiến độ vào Google Sheets hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình:** Từ khâu tìm kiếm, lọc, chấm điểm đến gửi email và theo dõi mà không cần thao tác thủ công.
- **AI Scoring thông minh:** Đánh giá chính xác mức độ phù hợp của KOL/Influencer dựa trên brief chiến dịch, loại bỏ các kênh kém chất lượng.
- **Cá nhân hóa nội dung:** Tự động tạo nội dung email outreach và follow-up riêng biệt cho từng influencer.
- **Đồng bộ dữ liệu thời gian thực:** Mọi tiến độ chiến dịch được ghi nhận tự động vào Google Sheets để dễ dàng báo cáo, tối ưu ROI.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **API Access:** Tài khoản API tìm kiếm Influencer (Instagram, TikTok, YouTube APIs hoặc các dịch vụ bên thứ ba tương ứng kết nối qua node `httpRequest`).
- **Google Account:** Tài khoản Google Sheets để lưu log chiến dịch.
- **Google Workspace / Gmail Account:** Tài khoản Gmail đã kết nối Credential với n8n để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc tải file từ nguồn gốc (`https://n8n.io/workflows/6073`), sau đó mở n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Campaign Brief Webhook (`webhook`):** Node này nhận dữ liệu đầu vào (brief chiến dịch). Các sếp cần copy URL của webhook này để bắn dữ liệu (JSON) từ hệ thống CRM, form đăng ký hoặc Postman vào.
- **Campaign Settings (`set`):** Nơi cấu hình các tham số mặc định cho chiến dịch như đối tượng mục tiêu, ngân sách, yêu cầu nội dung và timeline (như ghi chú trên canvas của tác giả).
- **Search Instagram / TikTok / YouTube Influencers (`httpRequest`):** Cấu hình API Endpoint và Header xác thực cho từng nền tảng mạng xã hội để hệ thống tiến hành quét dữ liệu influencer dựa theo brief.
- **Score & Qualify Influencers & Generate Outreach Content (`code`):** Các node xử lý code JavaScript (hoặc tích hợp LLM Node nếu muốn AI chấm điểm sâu hơn). Các sếp cần kiểm tra lại logic chấm điểm (độ tương tác, số lượng followers, lĩnh vực) cho phù hợp với tiêu chí doanh nghiệp.
- **Send Outreach Email & Send Follow-up Email (`gmail`):** Kết nối tài khoản Gmail của doanh nghiệp. Thiết lập tiêu đề và nội dung email được tạo tự động từ bước trước.
- **Wait 3 Days (`wait`):** Thiết lập thời gian chờ (mặc định 3 ngày) trước khi hệ thống tự động kích hoạt email follow-up.
- **Track Campaign Progress (`googleSheets`):** Kết nối tài khoản Google Drive/Sheets, chọn file bảng tính và chỉ định sheet tương ứng để node `appendRow` ghi nhận lại thông tin influencer, điểm số và trạng thái gửi email.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request mẫu vào **Campaign Brief Webhook** để test toàn bộ luồng chạy.
- Kiểm tra kết quả trả về ở Gmail, Google Sheets xem dữ liệu đã chính xác chưa.
- Nếu mọi thứ xanh mướt, hãy bật nút **Active** ở góc trên bên phải để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm ChatOps:** Thêm node Telegram hoặc Slack vào sau node `Filter Top Influencers` để nhận thông báo ngay lập tức mỗi khi hệ thống tìm được một Influencer "chất lượng cao".
- **Quản lý trạng thái phản hồi:** Thêm một nhánh check email phản hồi (Gmail Trigger) để tự động chuyển trạng thái trong Google Sheets từ "Đã gửi email" sang "Đã phản hồi" nhằm dừng lịch follow-up không cần thiết.
- **Nâng cấp AI Prompt:** Tùy biến đoạn code sinh nội dung email bằng cách tích hợp OpenAI/Anthropic Node để câu chữ outreach trở nên tự nhiên, uy tín và có tỷ lệ hồi đáp cao hơn.

### 📌 Kết luận
Hệ thống quản lý chiến dịch Influencer tự động này sẽ giúp đội ngũ Marketing tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần, đồng thời tối ưu hóa tỷ lệ chuyển đổi nhờ sự hỗ trợ đắc lực của AI Scoring. Chúc các sếp cài đặt thành công và chạy chiến dịch bùng nổ!