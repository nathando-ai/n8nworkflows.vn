---
title: "🚀 Tự động hóa tạo Moodboard Nội thất chuyên nghiệp bằng AI, Claude, Gemini & Hugging Face trong n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa toàn diện quy trình thiết kế nội thất: từ ý tưởng form nhập liệu, AI tạo prompt/layout, tạo ảnh Hugging Face, lưu trữ Nextcloud đến xuất file PDF chuyên nghiệp và gửi email cho khách hàng."
slug: "tao-moodboard-noi-that-tu-dong-voi-ai-n8n"
tags: [n8n, automation, ai-agent, claude, gemini, huggingface, nextcloud]
keywords: [n8n workflow, tạo moodboard nội thất, ai thiết kế nội thất, hugging face image generation, gotenberg pdf, tự động hóa n8n]
---

# 🚀 Tự động hóa tạo Moodboard Nội thất chuyên nghiệp bằng AI & n8n

Các sếp làm trong ngành thiết kế nội thất chắc hẳn đều hiểu cảm giác "đau đầu" khi phải ngồi hàng giờ để lên ý tưởng concept, tìm kiếm hoặc tự tạo hình ảnh minh họa, sắp xếp bố cục và xuất file PDF gửi khách hàng. Quá trình thủ công này vừa tốn thời gian, vừa thiếu tính nhất quán.

Hiểu được nỗi đau đó, workflow n8n này ra đời như một giải pháp **tự động hóa 100% không cần code**, kết hợp sức mạnh của các mô hình AI hàng đầu (Claude, Gemini), Hugging Face Image Generation và Nextcloud để biến một biểu mẫu yêu cầu đơn giản thành một bộ Moodboard 2 trang chuẩn chỉnh, sắc nét và chuyên nghiệp dưới dạng file PDF gửi thẳng vào email khách hàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ AI nặng và lưu trữ file mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Khách hàng điền form 👉 AI phân tích 👉 Tạo 12 ảnh thiết kế chi tiết 👉 Lưu trữ cloud 👉 Xuất PDF 2 trang 👉 Gửi email tự động.
- **Tiết kiệm 95% thời gian:** Thay vì mất vài ngày, hệ thống chỉ mất vài phút để hoàn thành một bộ hồ sơ moodboard chỉn chu.
- **Chất lượng chuyên nghiệp:** Sử dụng AI tạo ảnh qua Hugging Face kết hợp bố cục HTML/PDF chuẩn A4 (bao gồm phối cảnh 3D, mã màu Hex, bảng vật liệu...).
- **Cá nhân hóa tự động:** Tự động tạo thư mục riêng theo tên email người dùng trên Nextcloud để lưu trữ file gọn gàng.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Google Gemini API Key** (cho Google Gemini Chat Model).
3. **OpenRouter API Key** (truy cập Claude Sonnet qua OpenRouter).
4. **Hugging Face API Token** (để gọi Image Generator).
5. **Nextcloud Account** (để tạo thư mục và chia sẻ link ảnh).
6. **Gotenberg Service** (hoặc endpoint tương thích để convert HTML sang PDF).
7. **Gmail Credentials / OAuth2** (để gửi email đính kèm PDF).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ JSON).
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 21 nodes được chia thành 3 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Moodbaord Form (`formTrigger`):** Nơi khách hàng nhập yêu cầu (tiêu đề concept, màu sắc, vật liệu, ánh sáng, email...). Hãy tùy chỉnh các trường form theo nhu cầu thực tế của công ty.
- **Email extractor (`code`):** Node trích xuất tên người dùng từ email (bỏ phần `@` và dấu `+`) để tạo cấu trúc thư mục lưu trữ.
- **Create a folder & Upload Image & Share a file (`nextCloud`):** Kết nối tài khoản Nextcloud của các sếp. Node sẽ tự động tạo thư mục `/moodboard/{username}` và lưu trữ 12 ảnh được tạo ra, sau đó tạo public link.
- **Conceptualization Agent & Moodboard Generator Agent (`agent`):** 
  - Cấu hình **Google Gemini Chat Model1** (`googlePalmApi`) và **OpenRouter Chat Model** (`openRouterApi` - dùng model `anthropic/claude-sonnet-4`).
  - Các agent này chịu trách nhiệm phân tích brief thành 12 prompt chi tiết (từ 1-11 là góc nhìn vật liệu/nội thất, 12 là phối cảnh 3D) và sinh HTML 2 trang cho moodboard.
- **Image Generator (`httpRequest`):** Kết nối với Hugging Face API (`httpHeaderAuth`) để nhận các prompt dài 300-500 từ và trả về hình ảnh chất lượng cao.
- **PDF creator (`httpRequest`):** Gửi mã nguồn HTML hoàn chỉnh qua dịch vụ Gotenberg (`httpBasicAuth`) để render thành file PDF A4 sắc nét.
- **Send PDF (`gmail`):** Cấu hình tài khoản Gmail OAuth2 để gửi email tự động đính kèm file PDF moodboard cho khách hàng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền form mẫu.
- Kiểm tra xem ảnh đã được đẩy lên Nextcloud, file PDF đã được tạo và email đã gửi thành công chưa.
- Sau khi test ngon lành, bật công tắc **Active** góc trên cùng bên phải để đưa workflow vào vận hành thực tế 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm một node Telegram hoặc Slack sau bước "Send PDF" để thông báo cho đội ngũ Sales/Designer ngay khi có khách hàng hoàn thành form yêu cầu.
- **Lưu trữ Google Drive / Notion:** Ngoài Nextcloud, các sếp có thể mở rộng lưu trữ thêm vào Google Drive hoặc tạo một dòng dữ liệu (Row) trên Notion để quản lý khách hàng dễ dàng hơn.
- **Tùy biến Email Template:** Viết lại nội dung email trong node Gmail với văn phong thương hiệu riêng để tăng tỷ lệ chuyển đổi và uy tín chuyên nghiệp.

---

### 📌 Kết luận
Workflow tự động hóa tạo Moodboard nội thất bằng AI này là một vũ khí cực kỳ lợi hại cho các studio thiết kế, kiến trúc sư tự do hoặc các công ty nội thất muốn tối ưu hóa quy trình làm việc và gây ấn tượng mạnh với khách hàng ngay từ cái nhìn đầu tiên. Chúc các sếp cài đặt thành công và tự động hóa thành công công việc kinh doanh của mình!