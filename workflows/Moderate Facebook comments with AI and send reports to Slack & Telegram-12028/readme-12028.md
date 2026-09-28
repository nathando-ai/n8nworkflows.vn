---
title: "🚀 Tự động kiểm duyệt bình luận Facebook bằng AI và gửi báo cáo qua Slack, Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động lọc bình luận rác, độc hại trên trang Facebook bằng OpenAI, lưu log vào Supabase và gửi báo cáo chi tiết đến Slack, Telegram."
slug: "tu-dong-kiem-duyet-binh-luan-facebook-bang-ai-n8n"
tags: [n8n, automation, facebook, ai, openai, supabase, slack, telegram]
keywords: [n8n workflow, kiem duyet binh luan facebook, ai moderation, openai n8n, supabase, telegram slack automation]
---

# 🚀 Tự động kiểm duyệt bình luận Facebook bằng AI và gửi báo cáo qua Slack, Telegram

Các sếp đang quản lý Fanpage chắc chắn sẽ hiểu cảm giác "đau đầu" khi mỗi ngày có hàng trăm bình luận (comment) từ spam, từ ngữ thô tục, công kích cho đến tin nhắn rác làm ảnh hưởng nghiêm trọng đến uy tín thương hiệu. Việc ngồi đọc và xóa thủ công tốn rất nhiều thời gian mà đôi khi vẫn bỏ sót.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa **100%** quy trình quét, phân tích ý định, phát hiện độc hại (toxicity), spam bằng **OpenAI**, lưu trữ lịch sử vào **Supabase** và tổng hợp gửi báo cáo tóm tắt thẳng tới **Slack** và **Telegram** của đội ngũ mà không cần các sếp phải động tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lọc sạch rác & từ ngữ độc hại:** AI tự động phân tích sắc thái (tích cực, trung tính, tiêu cực), phát hiện spam và ngôn từ phản cảm.
- **Lưu trữ dữ liệu minh bạch:** Mọi lịch sử kiểm duyệt được lưu tự động vào cơ sở dữ liệu Supabase phục vụ việc audit và thống kê.
- **Báo cáo định kỳ tự động:** Cập nhật ngay các con số tổng quan, số lượng bình luận vi phạm lên kênh Slack và Telegram nhóm mỗi 6 giờ.
- **Tiết kiệm 90% thời gian:** Đội ngũ không cần túc trực trên Fanpage hay mở dashboard thủ công để kiểm tra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Facebook Graph API Token** (Page Access Token có quyền đọc bài viết/bình luận).
- **OpenAI API Key** (Dùng cho node AI-Based Comment Moderation).
- **Supabase Account & Project** (Tạo bảng lưu log kết quả kiểm duyệt).
- **Telegram Bot Token & Chat ID**.
- **Slack Bot Token & Channel ID**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ JSON từ nguồn gốc hoặc import trực tiếp file JSON của workflow này vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Scheduled Workflow Trigger (`cron`):** 
  - Mặc định workflow được thiết lập chạy định kỳ 6 tiếng/lần. Các sếp có thể cấu hình lại thời gian chạy tùy theo lượng tương tác thực tế của Fanpage.
- **Fetch Facebook Page Comments (`httpRequest`):** 
  - Dán **Facebook Page Access Token** và cấu hình endpoint URL để lấy danh sách bình luận mới nhất từ Page của các sếp.
- **AI-Based Comment Moderation (`openAi`):** 
  - Chọn credentials OpenAI đã chuẩn bị. 
  - Tinh chỉnh system prompt nếu muốn AI chấm điểm, phân loại theo ngôn ngữ hoặc quy chuẩn riêng của doanh nghiệp.
- **Store Moderation Logs in Database (`supabase`):** 
  - Kết nối Supabase API credentials. 
  - Trỏ tới đúng bảng (Table) đã tạo sẵn trong cơ sở dữ liệu để lưu trữ log kết quả quét (bao gồm ID comment, nội dung, điểm độc hại, trạng thái flagged...).
- **Send Moderation Reports to Telegarm & Slack (`telegram`, `slack`):** 
  - Điền Telegram Bot Token và Chat ID của nhóm trực.
  - Cấu hình Slack Webhook/Bot Token và chọn đúng kênh (Channel) nhận báo cáo tóm tắt.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu mẫu xem luồng chạy có lỗi ở node nào không.
- Sau khi test thành công, bật công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp tính năng Auto-hide/Auto-delete:** Có thể nối thêm một HTTP Request gọi trực tiếp Facebook API để tự động ẩn hoặc xóa ngay những bình luận bị AI đánh dấu là "toxic" hoặc "spam" nặng.
- **Thêm cảnh báo khẩn cấp (Emergency Alert):** Nếu phát hiện bình luận có mức độ độc hại cao vượt ngưỡng (high toxicity), có thể gửi tin nhắn riêng hú còi trực tiếp cho nhân viên chăm sóc khách hàng qua Telegram.
- **Xuất file báo cáo tuần:** Kết hợp thêm node Google Sheets để lưu dồn dữ liệu mỗi tuần làm báo cáo hiệu suất xử lý khủng hoảng truyền thông.

### 📌 Kết luận
Việc kiểm duyệt bình luận thủ công giờ đây đã trở thành dĩ vãng. Với sự trợ giúp của AI và n8n, Fanpage của doanh nghiệp sẽ luôn được thanh lọc sạch sẽ, chuyên nghiệp, bảo vệ hình ảnh thương hiệu 24/7 mà không tốn nhiều nguồn lực. Chúc các sếp cài đặt thành công!