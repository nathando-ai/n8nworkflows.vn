---
title: "🚀 Tự động tạo bản tin hàng ngày với Perplexity và Gmail qua n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động tổng hợp tin tức thông minh mỗi ngày từ Perplexity AI theo các chủ đề tùy chỉnh và lưu nháp vào Gmail."
slug: "tu-dong-tao-ban-tin-hang-ngay-voi-perplexity-va-gmail"
tags: [n8n, automation, perplexity, ai, gmail, newsletter]
keywords: [n8n workflow, tu dong hoa ban tin, perplexity ai, gmail automation, lap lich n8n]
---

# 🚀 Tự động tạo bản tin hàng ngày với Perplexity và Gmail qua n8n

Việc cập nhật tin tức chuyên ngành, xu hướng AI hay kiến thức quản trị mỗi ngày ngốn rất nhiều thời gian của các sếp. Thay vì phải lướt web thủ công, tại sao không để AI tự động tổng hợp và soạn sẵn một bản tin chỉn chu gửi thẳng vào hộp thư? 

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: gom nhặt thông tin nóng hổi từ **Perplexity AI**, tổng hợp lại và tạo bản nháp (Draft) trên **Gmail** vào mỗi buổi sáng. Không cần code phức tạp, chỉ cần thiết lập một lần và chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Tự động tra cứu và tổng hợp tin tức chuyên sâu mà không cần đọc nhiều nguồn.
- **Cá nhân hóa nội dung:** Dễ dàng thay đổi chủ đề (Quản trị, AI Automation, Product Management...) theo sở thích cá nhân.
- **Chủ động kiểm soát:** Lưu dưới dạng bản nháp (Draft) trong Gmail để sếp duyệt lại trước khi gửi chính thức.
- **Hoạt động tự động 24/7:** Chạyđều đặn mỗi ngày vào khung giờ cố định mà không cần bận tâm can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt hoặc chạy trên Cloud.
- **Perplexity API Key:** Để gọi mô hình AI `sonar` lấy tin tức.
- **Tài khoản Gmail:** Kết nối với n8n qua OAuth2 để tạo bản nháp email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã nguồn JSON của template và dán trực tiếp vào giao diện (hoặc import file JSON được cung cấp).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node cốt lõi sau đây:

- **Daily Trigger (`scheduleTrigger`):** Thiết lập lịch chạy tự động mỗi ngày (mặc định vào lúc 9:00 sáng). Các sếp có thể đổi giờ nếu muốn nhận tin sớm hơn.
- **Set Dates (`set`):** Node này định dạng ngày tháng để gắn vào tiêu đề bản tin.
- **Các node Perplexity (`MBA News`, `Product Management`, `AI Automation News`):** 
  - Cần thêm **Perplexity API Credentials**.
  - Tùy chỉnh model (`sonar`) và prompt bên trong để lấy thông tin đúng lĩnh vực các sếp quan tâm (ví dụ: Xu hướng AI, Tin tức công nghệ, Kinh tế...).
- **Merge (`merge`) & Combine messages (`code`):** Gộp kết quả từ các luồng tin tức thành một định dạng HTML đẹp mắt, có tiêu đề và link bấm trực quan.
- **Gmail (`gmail`):** 
  - Kết nối tài khoản Gmail cá nhân/doanh nghiệp qua `gmailOAuth2`.
  - Cấu hình node để lưu nội dung email vào mục **Drafts** (Bản nháp) hoặc gửi trực tiếp tùy ý.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem email nháp có được tạo thành công trong Gmail hay không.
- Nếu mọi thứ mượt mà, hãy bật công tắc **Active** ở góc trên bên phải để n8n tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh nhận tin:** Thay vì chỉ lưu vào Gmail Draft, các sếp có thể kết nối thêm node **Telegram** hoặc **Slack** để bắn thông báo nóng vào group chat làm việc.
- **Mở rộng chủ đề:** Thêm các node Perplexity mới nếu muốn theo dõi thêm các lĩnh vực khác như Crypto, Chứng khoán hay Marketing.
- **Lưu trữ lịch sử:** Kết nối thêm Google Sheets để lưu lại các bản tin đã tạo mỗi ngày, phục vụ việc tra cứu về sau.

### 📌 Kết luận
Một bản tin tự động chuẩn hóa từ AI sẽ giúp các sếp luôn đi đầu trong việc cập nhật tri thức và xu hướng mới mà không tốn chút sức lực thủ công nào. Hãy import ngay workflow này và tận hưởng sức mạnh của tự động hóa n8n nhé!