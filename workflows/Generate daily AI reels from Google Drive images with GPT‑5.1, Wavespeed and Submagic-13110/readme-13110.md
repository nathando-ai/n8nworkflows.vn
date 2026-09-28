---
title: "🚀 Tự động hóa sản xuất video ngắn hàng ngày từ ảnh Google Drive với AI, Wavespeed và Submagic"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn diện quy trình biến ảnh tĩnh thành video Reels/TikTok cinematic, tự động thêm sub, kiểm duyệt qua Gmail và đăng tải tự động."
slug: "tu-dong-hoa-tao-video-reels-tu-google-drive-ai"
tags: [n8n, automation, no-code, ai-video, content-creation, instagram, tiktok]
keywords: [n8n workflow, tự động hóa video, tạo reels bằng ai, wavespeed, submagic, blotato, google drive ai]
---

# 🚀 Tự động hóa sản xuất video ngắn hàng ngày từ ảnh Google Drive với AI

Các sếp có đang cảm thấy kiệt sức vì mỗi ngày phải lọ mọ chọn ảnh, nghĩ ý tưởng viết kịch bản, dựng video ngắn (Reels/TikTok) rồi lại mất hàng giờ chèn phụ đề, kiểm duyệt và đăng thủ công lên hàng loạt nền tảng? Đây là một "nỗi đau" cực kỳ tốn thời gian nhưng lại cực kỳ quan trọng đối với các nhà sáng tạo nội dung, chủ doanh nghiệp hay các social media manager.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tuyệt vời được chia sẻ bởi **Automate With Marc**, giúp tự động hóa 100% quy trình từ một bức ảnh tĩnh trên Google Drive thành một thước phim video ngắn cực kỳ chuyên nghiệp, có chèn sub cuốn hút, có cơ chế gửi email phê duyệt (Human-in-the-loop) và tự động đăng lên Instagram, TikTok!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu hóa nội dung vô hạn:** Biến kho ảnh sản phẩm, ảnh dịch vụ hoặc ảnh stock tĩnh thành hàng trăm video ngắn thu hút tương tác cao.
- **Tiết kiệm 95% thời gian:** Không còn công đoạn dựng hình, viết prompt thủ công hay cắt ghép video mệt mỏi.
- **Kiểm soát thông minh (Human-in-the-loop):** Gửi email xem trước video và chỉ đăng tải khi được các sếp bấm nút phê duyệt.
- **Đa nền tảng:** Tự động phát hành đồng thời lên Instagram Reels và TikTok một cách mượt mà.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Google Drive OAuth:** Thư mục chứa nguồn ảnh gốc.
- **OpenAI API Key:** Dùng cho node `Prompt Generator` (GPT-5.1) để viết câu lệnh tạo video cinematic.
- **Wavespeed API Key:** Dùng để tạo video từ ảnh (Image-to-Video).
- **Submagic API Key:** Công cụ tự động thêm phụ đề (captions) và hiệu ứng chữ thịnh hành.
- **Gmail OAuth:** Gửi email thông báo chờ phê duyệt nội dung.
- **Blotato Account:** Nền tảng trung gian giúp đăng bài tự động lên Instagram và TikTok.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON từ trang chính thức của n8n.
- Mở không gian làm việc n8n của các sếp, chọn **Import from JSON** và dán vào để hiển thị toàn bộ 18 nodes.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thông số quan trọng sau:

- **Schedule Trigger:** Mặc định workflow được lên lịch chạy vào lúc 9:00 AM mỗi ngày. Các sếp có thể chỉnh lại khung giờ phù hợp với chiến lược nội dung của mình.
- **Search files and folders (Google Drive):** Kết nối tài khoản Google Drive và trỏ đến ID của thư mục chứa các bức ảnh nguồn. Node `Randomizer` (Code node) sẽ tự động bốc thăm ngẫu nhiên 1 bức ảnh mỗi ngày để tránh lặp nội dung.
- **Prompt Generator (OpenAI):** Cấu hình OpenAI Credentials và kiểm tra câu lệnh (prompt) để AI tạo ra kịch bản chuyển động (cinematic prompt) tối ưu nhất cho mô hình tạo video.
- **Wavespeed Post Request & GET Result:** Điền API Key của Wavespeed vào HTTP Request nodes để ra lệnh biến ảnh thành video dọc 9:16 dài 8 giây, kết hợp node `Wait` để chờ hệ thống render xong.
- **Submagic Post Request & Submagic Get Result:** Cấu hình API của Submagic để hệ thống tự động nhận diện giọng nói/nội dung và phủ lớp text/captions phong cách viral lên video.
- **Send message and wait for response (Gmail):** Kết nối tài khoản Gmail cá nhân/doanh nghiệp. Node này sẽ gửi link xem trước video kèm trạng thái chờ duyệt tới hộp thư của các sếp.
- **Post to Instagram / Post to Tik Tok (Blotato):** Kết nối tài khoản Blotato đã liên kết sẵn kênh Instagram và TikTok của các sếp để hoàn tất khâu xuất bản tự động khi có lệnh phê duyệt.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công với một dữ liệu mẫu để kiểm tra toàn bộ chuỗi kết nối từ Drive đến Gmail.
- Nếu email phê duyệt về thành công và video render mượt mà, hãy gạt công tắc **Active** góc trên cùng bên phải để hệ thống tự động chạy ngầm mỗi ngày.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack để nhận thông báo duyệt video nhanh chóng ngay trên điện thoại.
- **Lưu trữ kho video:** Thêm một bước phụ lưu trữ các video đã hoàn thiện vào một thư mục Google Drive riêng biệt hoặc Notion Database để dễ dàng làm báo cáo định kỳ.
- **Xử lý ngoại lệ (Error Handling):** Cấu hình thêm Error Trigger để nhận cảnh báo ngay lập tức nếu API của Wavespeed hoặc Submagic gặp sự cố gián đoạn.

---

### 📌 Kết luận
Việc sản xuất video ngắn hàng loạt chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n, OpenAI, Wavespeed và Submagic. Hãy áp dụng ngay template này để giải phóng sức lao động, tối ưu hóa kênh social và bứt phá lượng tiếp cận cho thương hiệu của các sếp ngay hôm nay!