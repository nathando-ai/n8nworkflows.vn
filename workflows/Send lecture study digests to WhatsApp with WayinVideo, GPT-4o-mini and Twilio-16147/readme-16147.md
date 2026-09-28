---
title: "🚀 Tự động hóa tóm tắt video bài giảng gửi thẳng vào WhatsApp với n8n, WayinVideo, GPT-4o-mini & Twilio"
description: "Hướng dẫn xây dựng workflow n8n tự động tiếp nhận video bài giảng, tóm tắt thông minh bằng AI và gửi bản tóm tắt ôn tập qua WhatsApp cho học sinh, sinh viên."
slug: "tu-dong-hoa-tom-tat-video-bai-giang-whatsapp-n8n"
tags: [n8n, automation, ai, openai, twilio, whatsapp, google-sheets]
keywords: [n8n workflow, tóm tắt video bài giảng, wayinvideo, gpt-4o-mini, twilio whatsapp, tự động hóa n8n]
---

# 🚀 Tự động hóa tóm tắt video bài giảng gửi thẳng vào WhatsApp với n8n, WayinVideo, GPT-4o-mini & Twilio

Các sếp làm trong lĩnh vực giáo dục, đào tạo hay các bạn học sinh, sinh viên có bao giờ cảm thấy ngợp trước hàng giờ video bài giảng dài dằng dặc? Việc ngồi xem lại từng phút video để ghi chép bài học hoặc ôn thi cực kỳ tốn thời gian và dễ bỏ sót ý chính.

Bài viết này sẽ hướng dẫn các sếp triển khai một trợ lý tự động hóa đỉnh cao trên **n8n**: Sinh viên chỉ cần điền form (gửi link video bài giảng, số điện thoại WhatsApp và môn học), hệ thống sẽ tự động băm nhỏ video, tóm tắt nội dung cốt lõi nhờ công nghệ AI (GPT-4o-mini), và bắn thẳng kết quả ôn tập qua WhatsApp trong tích tắc, đồng thời lưu lại log trên Google Sheets!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ khâu nhận yêu cầu qua form đến lúc gửi tin nhắn WhatsApp mà không cần con người nhúng tay.
- **Tóm tắt siêu thông minh:** Sử dụng WayinVideo để xử lý video từ YouTube, Zoom, Vimeo, Loom và GPT-4o-mini để chắt lọc 5 ý chính, 3 khái niệm trọng tâm ôn thi và 1 câu thần chú "nhớ đời".
- **Giao hàng tận nơi:** Gửi trực tiếp bản tóm tắt đẹp mắt tới số WhatsApp của học viên.
- **Lưu trữ minh bạch:** Tự động ghi nhận toàn bộ lịch sử tóm tắt vào Google Sheets để tra cứu bất cứ lúc nào.
:::

### yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **WayinVideo API Key:** Đăng ký tại `wayin.ai` để lấy API Key xử lý video.
- **OpenAI API Key:** Kết nối mô hình `gpt-4o-mini`.
- **Twilio Account:** Tài khoản Twilio kèm WhatsApp Sandbox hoặc số điện thoại chính thức đã kích hoạt WhatsApp API.
- **Google Sheets:** Tài khoản Google để kết nối OAuth2 và lưu trữ log.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện (hoặc import file JSON tương ứng).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node 3 & 5 (HTTP — WayinVideo Submit / Get Results):** Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API key thực tế lấy từ tài khoản WayinVideo của các sếp. Node này hỗ trợ các nguồn video từ YouTube, Zoom, Vimeo, Loom.
- **Node OpenAI — GPT-4o-mini Model:** Kết nối credential OpenAI của các sếp và đảm bảo model được chọn là `gpt-4o-mini`.
- **Node 10 (HTTP — Send WhatsApp via Twilio):** Thay thế `YOUR_TWILIO_ACCOUNT_SID`, `YOUR_TWILIO_AUTH_TOKEN`, và `YOUR_TWILIO_WHATSAPP_NUMBER` (định dạng `+1234567890`). *(Lưu ý: Nếu dùng Twilio Sandbox để test, học viên cần gửi mã join code qua WhatsApp trước).*
- **Node 11 (Google Sheets — Save Digest):** Kết nối tài khoản Google Sheets OAuth2, điền `YOUR_GOOGLE_SHEET_ID` và tạo một sheet tab tên là `Lecture Digests` với các cột: `Student`, `Phone`, `Subject`, `Video URL`, `Key Points`, `Exam Concepts`, `Exam Tag`, `Date`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách submit một form mẫu để kiểm tra toàn bộ luồng từ lúc nhận video đến khi nhận tin nhắn WhatsApp.
- Nếu mọi thứ xanh mướt, hãy bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh phụ:** Kết hợp thêm node Telegram hoặc Slack để gửi bản tóm tắt vào nhóm học tập của lớp.
- **Hệ thống cảnh báo lỗi:** Thêm node bắt lỗi (Error Trigger) để thông báo về Zalo/Telegram cá nhân nếu quá trình xử lý video của WayinVideo gặp sự cố.
- **Cá nhân hóa nội dung:** Tinh chỉnh Prompt trong AI Agent để tạo ra giọng điệu tóm tắt phù hợp hơn với từng cấp học (Đại học, THPT hoặc ôn thi chứng chỉ quốc tế).

### 📌 Kết luận
Workflow tóm tắt bài giảng tự động này là một ứng dụng tuyệt vời tận dụng sức mạnh của No-Code kết hợp AI, giúp tiết kiệm thời gian tối đa cho việc học tập và nghiên cứu. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp thôi nào!