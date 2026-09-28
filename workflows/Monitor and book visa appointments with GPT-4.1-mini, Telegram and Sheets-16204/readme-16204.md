---
title: "🚀 Tự động săn và đặt lịch hẹn visa 24/7 với GPT-4.1-mini, Telegram và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động quét lịch hẹn visa mỗi 10 phút, đánh giá điểm số bằng AI, gửi cảnh báo qua Telegram và tự động đặt lịch."
slug: "tu-dong-san-dat-lich-hen-visa-n8n-gpt4"
tags: [n8n, automation, no-code, ai-agent, openai, telegram, google-sheets]
keywords: [n8n workflow, săn lịch visa tự động, gpt-4-mini, telegram bot, tự động hóa n8n, visa appointment sniper]
---

# 🚀 Tự động săn và đặt lịch hẹn visa 24/7 với GPT-4.1-mini, Telegram và Google Sheets

Việc canh lịch hẹn visa (Mỹ, Anh, Schengen,...) thủ công là nỗi ám ảnh lớn: cổng thông tin thường xuyên nghẽn, lịch trống vừa hiển thị đã hết, hoặc bạn bỏ lỡ khung giờ đẹp chỉ vì không kịp F5 trang web. 

Bài viết này sẽ hướng dẫn các sếp triển khai một "trợ lý ảo" tự động hóa 100% bằng n8n. Workflow này sẽ thay bạn túc trực 24/7, quét lịch hẹn mỗi 10 phút, nhờ AI chấm điểm mức độ phù hợp, gửi thông báo ngay lập tức qua Telegram và thậm chí tự động book lịch nếu đạt tiêu chuẩn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ khung giờ vàng:** Hệ thống chạy ngầm tự động mỗi 10 phút, nhanh hơn bất kỳ con người nào thao tác thủ công.
- **AI thông minh đánh giá:** GPT-4.1-mini chấm điểm từng slot (từ 0-100) dựa trên tiêu chí ngày tháng và độ khẩn cấp của bạn.
- **Cảnh báo tức thì qua Telegram:** Nhận thông tin chi tiết kèm đề xuất ngay trên điện thoại ngay khi có lịch trống.
- **Tự động hóa toàn diện:** Tự động tiến hành đặt chỗ (auto-book) nếu slot đạt ngưỡng điểm cho phép và lưu log minh bạch vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **OpenAI API Key:** Sử dụng mô hình `gpt-4.1-mini` để phân tích và chấm điểm slot.
- **Telegram Bot:** Bot Token và Chat ID để nhận cảnh báo và tương tác.
- **Google Sheets Credentials:** Tài khoản OAuth2 hoặc Service Account để ghi log kết quả đặt lịch.
- **API/Endpoint cổng visa:** Đường dẫn hoặc API endpoint của cổng thông tin đại sứ quán/trung tâm tiếp nhận visa.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON) và dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 9 nodes chính được chia làm 3 giai đoạn. Các sếp cần cấu hình kỹ các điểm sau:

- **Node `Poll Every 10 Min` (scheduleTrigger):** 
  - Mặc định quét mỗi 10 phút. Các sếp có thể chỉnh lại thời gian (tần suất nhanh hơn hoặc chậm hơn) tùy theo chính sách chống bot của cổng visa.
- **Node `Set User Config` (set):** 
  - Điền các thông tin cá nhân quan trọng: loại visa, số hộ chiếu, khoảng thời gian mong muốn, địa điểm, mức độ khẩn cấp và ngưỡng điểm tự động đặt (`auto-book threshold`, ví dụ: >85 điểm).
- **Node `Code 1 - Fetch & Parse Slots` (code):** 
  - Cập nhật đoạn code JavaScript để kết nối đúng với API hoặc URL của cổng đặt lịch visa mà sếp đang cần săn.
- **Node `OpenAI Chat Model` & `AI - Score Slot` (lmChatOpenAi & agent):** 
  - Kết nối OpenAI Credentials, kiểm tra chắc chắn model đang chọn là `gpt-4.1-mini`.
- **Node `Send Telegram Alert` & `Send Final Status` (telegram):** 
  - Kết nối Telegram API Credentials, điền Chat ID cá nhân hoặc nhóm chat nhận thông báo.
- **Node `Code 2 - Book & Log to Sheets` (code):** 
  - Thay thế endpoint đặt chỗ giả lập bằng API endpoint thực tế của cổng visa. Cấu hình Google Sheet ID để hệ thống tự động ghi log sau khi book thành công.
- **Node `Wait - Confirm Window (15 min)` (wait):** 
  - Khoảng thời gian chờ (15 phút) để sếp có cơ hội xác nhận thủ công trước khi hệ thống tự động tiến hành bước book lịch chính thức (nếu cấu hình yêu cầu).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Execute Workflow**) với dữ liệu mẫu để kiểm tra luồng tin nhắn Telegram và quyền ghi Google Sheets.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm bộ lọc:** Thêm một node `If` hoặc `Filter` ngay sau bước AI Scoring để loại bỏ hoàn toàn các slot bị AI đánh giá điểm thấp (SKIP), tránh làm phiền Telegram bằng những thông báo rác.
- **Mở rộng đa hồ sơ:** Tùy biến node `Code 2` để hỗ trợ săn lịch đồng thời cho nhiều đương đơn (gia đình hoặc nhóm bạn).
- **Báo cáo định kỳ:** Tạo thêm nhánh gửi báo cáo tổng kết cuối ngày vào Telegram để biết hôm nay bot đã quét bao nhiêu lần và tìm được bao nhiêu slot khả dụng.

### 📌 Kết luận
Với workflow n8n thông minh kết hợp sức mạnh của AI GPT-4.1-mini, việc săn lịch visa giờ đây không còn là cuộc chiến F5 mệt mỏi nữa. Hãy triển khai ngay hôm nay để nắm chắc tấm vé trong tay các sếp nhé!