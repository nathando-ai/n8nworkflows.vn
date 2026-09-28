---
title: "🚀 Tự động hóa sản xuất video quảng cáo UGC bằng AI (OpenAI & Kie.ai) trên n8n"
description: "Hướng dẫn chi tiết xây dựng hệ thống n8n workflow tự động phân tích hình ảnh sản phẩm, tạo kịch bản, gọi API sinh ảnh/video UGC và lưu trữ mây mượt mà."
slug: "tu-dong-hoa-tao-video-ugc-ai-openai-kie-ai-n8n"
tags: [n8n, automation, ai, openai, video-generation, content-creation]
keywords: [n8n workflow, tao video ugc tự động, openai gpt-4, kie.ai, ai marketing automation]
---

# 🚀 Tự động hóa sản xuất video quảng cáo UGC bằng AI với OpenAI & Kie.ai

Các sếp làm trong ngành Performance Marketing chắc chắn đều hiểu "nỗi đau" khi sản xuất video UGC (User Generated Content): tốn kém thời gian thuê reviewer, chi phí dựng video lớn, và cực kỳ khó scale số lượng lớn biến thể (variations) để chạy ads A/B testing liên tục. 

Giải pháp thủ công đã lỗi thời! Bài viết này sẽ hướng dẫn các sếp triển khai một siêu workflow n8n tự động hóa 100% quy trình: **Phân tích hình ảnh sản phẩm gốc ➡️ Tạo kịch bản & prompt AI ➡️ Gọi API sinh ảnh/video UGC ➡️ Lưu trữ Google Drive/Box và tracking qua Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ AI nặng và gọi API liên tục, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Sản xuất hàng loạt (Scale-up):** Biến 1 hình ảnh sản phẩm đơn lẻ thành hàng loạt video UGC độc đáo chỉ với vài cú click.
- **Tối ưu chi phí & thời gian:** Cắt giảm 90% thời gian lên ý tưởng kịch bản, prompt và dựng hình ảnh/video thủ công.
- **Quy trình khép kín (End-to-End):** Tự động từ khâu phân tích thị giác bằng OpenAI Vision, gọi API sinh media, kiểm tra trạng thái (polling loop), cho đến lưu trữ đám mây và đồng bộ Google Sheets.
- **Quản lý tập trung:** Dễ dàng theo dõi lịch sử sinh video, trạng thái thành công/thất bại ngay trên Google Sheets và Google Drive/Box.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Phiên bản khuyến nghị: v1.0+).
- **Tài khoản OpenAI API:** Để sử dụng GPT-4 và tính năng phân tích hình ảnh (Vision).
- **Kie.ai API Credentials:** Tài khoản và API key để gọi dịch vụ sinh ảnh và video.
- **Google Drive & Box Credentials:** Tài khoản lưu trữ file video thành phẩm.
- **Google Sheets:** File Google Sheets chuẩn bị sẵn để ghi log trạng thái và kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn cung cấp.
- Vào n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và paste trực tiếp vào màn hình workflow).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà không gặp lỗi "Unauthorized" hay thiếu tham số, các sếp cần cấu hình chính xác các node sau:

- **Analyze image & OpenAI Chat Model:** Kết nối tài khoản OpenAI của các sếp. Node này dùng model `gpt-4.1` để phân tích màu sắc, thương hiệu và bối cảnh từ ảnh sản phẩm gốc.
- **Setup (Image & Video settings) & Video script:** Điền link hình ảnh sản phẩm gốc cần làm quảng cáo và thiết lập số lượng video/biến thể muốn tạo.
- **Generate UGC prompts with AI agent1:** Đảm bảo Agent kết nối đúng với `Structured Output Parser` và `OpenAI Chat Model` để trả về định dạng prompt chuẩn xác cho các API sinh ảnh/video phía sau.
- **Call image generation API1 / Call video generation API1:** Nhập API Key của Kie.ai (hoặc dịch vụ AI media tương ứng mà các sếp tích hợp vào HTTP Request nodes).
- **Google Drive (Upload file) & Box (Upload a file):** Kết nối OAuth2 để hệ thống tự động đẩy file video hoàn thiện lên kho lưu trữ chung của team.
- **Google Sheets nodes (Fetch video generation logs1, Log image/video status1, Update final results1):** Trỏ tới file Google Sheets quản lý của các sếp và map đúng tên cột (Columns) để hệ thống ghi log trạng thái chạy tự động.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Execute workflow’** bằng tay (hoặc kích hoạt `When clicking ‘Execute workflow’`) để chạy thử nghiệm với 1 sản phẩm mẫu.
- Theo dõi các vòng lặp (Loops) qua các node `Wait`, `If` xem quá trình polling media diễn ra thành công chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để chính thức tự động hóa quy trình!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để bot tự động gửi thông báo *"Đã tạo xong video UGC cho sản phẩm X"* kèm link Google Drive cho team Content/Marketing.
- **Mở rộng nguồn input:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Webhook` hoặc kết nối với một Google Form để đội ngũ Sale/Marketing tự submit ảnh sản phẩm lên là workflow tự chạy.
- **Tự động đăng TikTok/Reels:** Kết nối thêm n8n node của TikTok Marketing API hoặc Meta Graph API để tự động lên lịch đăng tải các video UGC vừa tạo.

### 📌 Kết luận
Việc ứng dụng AI và tự động hóa vào sản xuất nội dung không chỉ là xu hướng mà là chìa khóa giúp doanh nghiệp bứt phá doanh thu với chi phí tối ưu nhất. Hãy áp dụng ngay workflow này để nâng tầm chiến dịch performance marketing của các sếp lên một đẳng cấp mới!