---
title: "🚀 Tự động hóa bản tin công nghệ hàng ngày với RSS, GPT-4o-Mini và Gmail trong n8n"
description: "Xây dựng hệ thống tổng hợp tin tức công nghệ tự động từ 14+ nguồn uy tín, lọc và tóm tắt thông minh bằng AI và gửi bản tin chuyên nghiệp qua Gmail mỗi ngày."
slug: "tu-dong-hoa-ban-tin-cong-nghe-rss-gpt-4o-mini-gmail"
tags: [n8n, automation, no-code, ai, openai, rss, gmail]
keywords: [n8n workflow, tự động hóa bản tin, AI tech news, tóm tắt tin tức tự động, OpenAI GPT-4o-Mini, Gmail automation]
---

# 🚀 Tự động hóa bản tin công nghệ hàng ngày với RSS, GPT-4o-Mini và Gmail

Việc cập nhật các xu hướng công nghệ mới nhất từ hàng chục trang báo chí uy tín mỗi ngày là một "cực hình" tốn rất nhiều thời gian. Các sếp thường phải mất hàng giờ lướt web, đọc bài, tổng hợp và viết báo cáo thủ công để gửi cho đội ngũ hoặc khách hàng. 

Giải pháp tuyệt vời nhất là đây: Một hệ thống tự động hóa 100% không cần code bằng **n8n**, giúp thu thập tin tức từ các nguồn hàng đầu, sử dụng trí tuệ nhân tạo (AI) để chọn lọc, tóm tắt thông minh và tự động gửi một bản tin (newsletter) chuẩn HTML đẹp mắt thẳng vào hộp thư Gmail của các sếp mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công lướt 10-15 trang tin công nghệ mỗi ngày.
- **AI chọn lọc & tóm tắt thông minh:** GPT-4o-Mini giúp phân tích, loại bỏ tin rác và tổng hợp những bài viết đắt giá nhất, cân bằng nguồn tin tránh thiên vị.
- **Bản tin chuyên nghiệp:** Định dạng HTML sạch sẽ, trình bày khoa học, đọc cực mượt trên cả máy tính lẫn điện thoại.
- **Hoạt động tự động 24/7:** Chạy đúng giờ hẹn mỗi ngày mà không cần con người nhúng tay vào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **OpenAI API Key:** Tài khoản OpenAI để sử dụng mô hình GPT-4o-Mini.
- **Gmail Account:** Kết nối tài khoản Gmail qua OAuth2 để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n (hoặc copy toàn bộ JSON từ nguồn) và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau đây:

- **Daily Newsletter Trigger (`scheduleTrigger`):** Thiết lập khung giờ gửi bản tin mong muốn hàng ngày (mặc định là 8:00 AM UTC).
- **Configure RSS Sources (`set`):** Nơi chứa danh sách 14 nguồn tin công nghệ hàng đầu (TechCrunch, The Verge, MIT Technology Review, Wired, VentureBeat, v.v.). Các sếp có thể thêm/bớt URL tùy thích.
- **Filter Articles (`code`):** Node code JavaScript giúp lọc các bài viết chất lượng và giới hạn số lượng bài từ mỗi nguồn (mặc định tối đa 5 bài/nguồn) nhằm tránh bị tràn dữ liệu.
- **AI Newsletter Creator (`openAi`):** 
  - Chọn Credentials OpenAI của các sếp.
  - Kiểm tra lại prompt điều phối AI để định hình phong cách bản tin, ngôn ngữ (tiếng Việt hoặc tiếng Anh) và định dạng HTML đầu ra.
- **Send Newsletter (`gmail`):** 
  - Kết nối Credentials Gmail OAuth2.
  - Điền địa chỉ email nhận bản tin của các sếp (hoặc danh sách email nhóm).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm thủ công xem bản tin có đến Gmail suôn sẻ không.
- Kiểm tra nội dung AI tổng hợp xem đã chuẩn chỉnh chưa.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì chỉ gửi qua Gmail, các sếp có thể gắn thêm node Telegram Bot hoặc Slack để bắn thông báo tóm tắt tin tức lên nhóm chat nội bộ công ty.
- **Lưu trữ lịch sử:** Thêm node Google Sheets ở cuối workflow để lưu lại toàn bộ các bản tin đã gửi, tiện cho việc tra cứu sau này.
- **Tùy chỉnh chủ đề:** Thay đổi prompt trong node AI nếu các sếp chỉ muốn tập trung sâu vào một ngách cụ thể như *AI Startups*, *Web3*, hoặc *Cybersecurity*.

### 📌 Kết luận
Workflow Daily Tech News Curation là một "trợ lý ảo" hoàn hảo giúp các sếp luôn đi đầu xu thế công nghệ mà không tốn một chút công sức thủ công nào. Hãy "lên đồ" ngay cho hệ thống n8n của mình và tận hưởng thành quả nhé!