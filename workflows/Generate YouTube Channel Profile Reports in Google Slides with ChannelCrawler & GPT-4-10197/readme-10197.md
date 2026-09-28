---
title: "🚀 Tự động tạo báo cáo hồ sơ kênh YouTube vào Google Slides với ChannelCrawler & GPT-4"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động trích xuất dữ liệu kênh YouTube bằng ChannelCrawler, tổng hợp bằng GPT-4 và tạo slide báo cáo chuyên nghiệp."
slug: "tao-bao-cao-kenh-youtube-google-slides-n8n-gpt4"
tags: [n8n, automation, no-code, youtube, google-slides, open-ai]
keywords: [n8n workflow, channelcrawler, google slides automation, gpt-4 youtube summary, tu dong hoa no-code]
---

# 🚀 Tự động tạo báo cáo hồ sơ kênh YouTube vào Google Slides với GPT-4

Việc nghiên cứu thị trường, đánh giá các nhà sáng tạo nội dung (influencer/creator) hoặc đối thủ cạnh tranh trên YouTube thường đòi hỏi hàng giờ đồng hồ thủ công: từ việc thu thập dữ liệu, phân tích số liệu thống kê, tóm tắt thông tin cho đến việc thiết kế từng slide báo cáo. Điều này vừa tốn thời gian vừa dễ xảy ra sai sót khi làm với số lượng lớn.

Bài viết này sẽ hướng dẫn các sếp cách thiết lập một **n8n workflow hoàn toàn tự động** kết hợp giữa **ChannelCrawler API**, **OpenAI GPT-4** và **Google Slides**. Chỉ cần nhập một hoặc nhiều link kênh YouTube, hệ thống sẽ tự động bóc tách dữ liệu, viết tóm tắt thông minh và tạo ra các slide báo cáo đẹp mắt, chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công thông tin kênh YouTube vào slide.
- **Dữ liệu phân tích sâu sắc:** Tự động gọi API ChannelCrawler để lấy lượng view, sub, tốc độ tăng trưởng, video nổi bật... và được GPT-4 tinh chỉnh thành văn bản tóm tắt hấp dẫn.
- **Báo cáo chuẩn hóa:** Tự động nhân bản (duplicate) template slide sẵn có, thay thế avatar và chèn dữ liệu mượt mà qua API.
- **Hoạt động liền mạch:** Chạy thông qua một Form giao diện trực quan, xử lý từng kênh theo lô (batch) tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt và hoạt động tốt (Self-hosted hoặc n8n Cloud).
- **Tài khoản ChannelCrawler:** Cần đăng ký tài khoản và lấy API Key (có hình thức Pay-as-you-go rất tiết kiệm).
- **Tài khoản OpenAI:** Cần có API Key của OpenAI (GPT-4/GPT-3.5) để xử lý ngôn ngữ tự nhiên và tóm tắt.
- **Tài khoản Google Workspace:** Tài khoản Google có quyền truy cập Google Slides để tạo và chỉnh sửa slide báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ mã JSON của workflow.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes được liên kết chặt chẽ. Các sếp cần chú ý cấu hình các điểm sau:

- **On form submission (Form Trigger):** Node này tạo một giao diện nhập liệu pop-up. Các sếp có thể tùy chỉnh thêm các trường input nếu muốn thu thập thêm thông tin.
- **Clean Form Submission (Code Node):** Xử lý danh sách URL kênh YouTube do người dùng nhập thành định dạng mảng (array) để đưa vào vòng lặp.
- **Channel Crawler (HTTP Request Node):** Cần cấu hình Header để truyền ChannelCrawler API Key của sếp và endpoint gọi dữ liệu kênh YouTube.
- **Title the profile & Profile Summary (OpenAI Nodes):** 
  - Chọn Credentials OpenAI của sếp.
  - Tinh chỉnh `Prompt` bên trong node để AI tạo tiêu đề và tóm tắt theo đúng văn phong/nhu cầu báo cáo của doanh nghiệp.
- **Get Presentation & các Google Slides Nodes:** 
  - Kết nối Google OAuth2 credentials.
  - Lấy **Presentation ID** của file Google Slides mẫu (Template) và dán vào tham số của các node liên quan (như *Get Presentation*, *Create a new page*, *Replace Profile image*, *Replace text in Page*).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền một URL kênh YouTube bất kỳ vào Form.
- Kiểm tra kết quả trả về trong Google Slides xem hình ảnh, tiêu đề và văn bản đã khớp chưa.
- Sau khi kiểm tra ổn thỏa, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình làm việc hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
1. **Gửi thông báo qua Slack/Telegram:** Thêm node gửi tin nhắn kèm link Google Slides vừa tạo ngay khi workflow chạy xong để team sales/marketing kịp thời nắm bắt.
2. **Lưu lịch sử vào Google Sheets / Airtable:** Lưu lại danh sách các kênh đã báo cáo kèm thời gian thực hiện để quản lý database creator hiệu quả.
3. **Báo cáo định kỳ tự động:** Thay vì dùng Form Trigger, có thể kết hợp Trigger theo lịch (Schedule) để tự động quét danh sách kênh cần đánh giá hàng tuần/tháng.

### 📌 Kết luận
Workflow tự động hóa kết hợp ChannelCrawler, GPT-4 và Google Slides này là một "vũ khí" cực kỳ lợi hại cho các agency, đội ngũ marketing hoặc nhà sáng lập trong việc nghiên cứu đối thủ và Influencer Marketing. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất công việc của đội ngũ nhé các sếp!