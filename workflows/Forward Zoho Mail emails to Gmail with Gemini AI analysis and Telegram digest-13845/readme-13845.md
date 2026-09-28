---
title: "🚀 Tự động chuyển tiếp email Zoho Mail sang Gmail, phân tích bằng Gemini AI và gửi báo cáo Telegram"
description: "Tối ưu hóa quản lý email doanh nghiệp với n8n: Tự động gom email từ Zoho Mail, sử dụng Google Gemini AI để phân tích, tóm tắt và đồng bộ sang Gmail kèm thông báo Telegram."
slug: "chuyen-tiep-zoho-mail-sang-gmail-gemini-ai-telegram"
tags: [n8n, automation, zoho-mail, gmail, google-gemini, ai-agent, telegram]
keywords: [n8n workflow, zoho mail to gmail, gemini ai tóm tắt email, tự động hóa email, telegram digest]
---

# 🚀 Tự động chuyển tiếp email Zoho Mail sang Gmail, phân tích bằng Gemini AI và báo cáo qua Telegram

Các sếp có đang gặp tình trạng mỗi ngày phải mở hàng chục, thậm chí hàng trăm email từ Zoho Mail, đọc từng cái để lọc thông tin quan trọng, sau đó thủ công chuyển tiếp hoặc phân loại sang Gmail? Việc này không chỉ tốn thời gian, dễ bỏ sót các email khẩn cấp mà còn làm gián đoạn sự tập trung của đội ngũ.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ thay các sếp làm toàn bộ công việc tẻ nhạt đó: tự động bắt email mới từ Zoho Mail, sử dụng sức mạnh của **Google Gemini AI** để phân tích, trích xuất thông tin cốt lõi, chuyển tiếp mượt mà sang Gmail và gửi bản tóm tắt (digest) trực quan thẳng vào Telegram của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian xử lý email:** Không cần đọc dài dòng, AI đã thay mặt tóm tắt ý chính.
- **Không bỏ lỡ tin quan trọng:** Email từ Zoho được phân loại thông minh và chuyển thẳng tới Gmail cá nhân/công việc.
- **Báo cáo nhanh qua Telegram:** Nhận ngay thông tin tóm tắt các email mới dạng bản tin (digest) ngay trên điện thoại mọi lúc mọi nơi.
- **Vận hành tự động 24/7:** Hệ thống chạy ngầm mượt mà không cần con người nhúng tay vào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp nhớ chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Zoho Mail Account** & Credentials để cấu hình node `Zoho Mail Trigger`.
- **Google Gmail Account** để gửi/nhận email chuyển tiếp.
- **Google Gemini API Key** để kết nối với mô hình AI (`Google Gemini Chat Model`).
- **Telegram Bot Token & Chat ID** để gửi tin nhắn báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, vào giao diện n8n chọn **Add Workflow** -> Dấu ba chấm (...) ở góc trên bên phải -> **Import from File** và tải file lên là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp nhớ cấu hình kỹ các node trọng điểm sau:
- **Zoho Mail Trigger (`@zohomail/n8n-nodes-zohomail.zohoMailTrigger`)**: Kết nối tài khoản Zoho Mail của các sếp để hệ thống lắng nghe sự kiện có email đến (New Email).
- **Google Gemini AI Agent & Chat Model (`@n8n/n8n-nodes-langchain.agent`, `Google Gemini`)**: Điền Google Gemini API Key và cấu hình prompt cho AI biết cách đọc nội dung email, tóm tắt và phân loại theo định dạng chuẩn (sử dụng cấu trúc `Structured Output Parser`).
- **Gmail Node (`n8n-nodes-base.gmail`)**: Chọn tài khoản Gmail đích để chuyển tiếp nội dung email đã được làm sạch và tối ưu.
- **Telegram Node (`n8n-nodes-base.telegram`)**: Điền Bot Token và Chat ID của nhóm hoặc cá nhân để nhận bản tin tóm tắt (digest).
- Các node phụ trợ như **Code**, **If**, **Set**, **Split Out**, **Aggregate** sẽ tự động xử lý logic dữ liệu mà không cần chỉnh sửa gì thêm nếu các sếp giữ nguyên cấu trúc gốc.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email test vào Zoho Mail để kiểm tra xem dữ liệu có chảy qua Gemini AI, đổ về Gmail và bắn tin nhắn Telegram thành công hay không.
- Sau khi test xanh mướt, các sếp bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức gác cổng 24/7 cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Google Sheets:** Lưu lại lịch sử toàn bộ email đã phân tích vào Google Sheets để làm báo cáo thống kê cuối tuần.
- **Phân loại độ ưu tiên:** Tinh chỉnh prompt của Gemini AI để gắn nhãn (Khẩn cấp, Bình thường, Spam) và đổi màu thông báo trên Telegram.
- **Gửi thông báo qua Slack/Microsoft Teams:** Thay vì chỉ Telegram, các sếp có thể nhân bản nhánh tin nhắn sang kênh chat nội bộ công ty để team cùng nắm bắt.

### 📌 Kết luận
Workflow tự động hóa Zoho Mail kết hợp Gemini AI và Telegram này là một vũ khí cực kỳ lợi hại giúp các sếp tối ưu hóa dòng chảy thông tin trong công việc hàng ngày. Hãy cài đặt ngay hôm nay để giải phóng bản thân khỏi biển email rác và tin nhắn thủ công!