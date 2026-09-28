---
title: "🚀 Tự động hóa bản tin khởi nghiệp hàng ngày từ Crunchbase bằng AI GPT & n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu cập nhật từ Crunchbase, dùng AI tóm tắt thông minh và gửi email tổng hợp mỗi ngày."
slug: "tu-dong-hoa-ban-tin-crunchbase-voi-ai-va-n8n"
tags: [n8n, automation, ai, gpt, crunchbase, marketing]
keywords: [n8n workflow, crunchbase api, ai summarizer, tu dong hoa email, gpt-4o-mini]
---

# 🚀 Tự động hóa bản tin khởi nghiệp hàng ngày từ Crunchbase bằng AI GPT & n8n

Các nhà đầu tư, nhà sáng lập startup hay các marketer luôn phải tốn hàng giờ mỗi ngày để theo dõi các xu hướng thị trường, biến động từ đối thủ hoặc các công ty mới nổi trên **Crunchbase**. Việc tổng hợp thủ công này vừa nhàm chán, tốn thời gian lại rất dễ bỏ lỡ thông tin quan trọng.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: lấy dữ liệu công ty cập nhật từ Crunchbase, sử dụng AI thông minh để chắt lọc, tóm tắt và tự động gửi một bản tin (email digest) gọn gàng, súc tích thẳng vào hòm thư của các sếp mỗi ngày. Hoàn toàn tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm tối đa thời gian:** Không cần tự tay tra cứu dữ liệu hàng ngày.
- **Nắm bắt xu hướng nhanh chóng:** AI phân tích và tóm tắt các điểm nổi bật nhất từ hàng loạt công ty.
- **Cá nhân hóa nội dung:** Bản tin được format sạch sẽ, rõ ràng gửi trực tiếp qua Gmail.
- **Hoạt động tự động 24/7:** Có thể thiết lập chạy tự động mỗi sáng trước khi các sếp bắt đầu ngày làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Crunchbase API Key:** Để lấy dữ liệu tổ chức/công ty.
- **OpenAI API Key:** Cho AI Agent phân tích và tóm tắt dữ liệu.
- **Tài khoản Gmail:** Kết nối qua OAuth2 để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được chia làm 3 phần quan trọng:

* **Trigger Manual Test / Fetch Crunchbase Updates (HTTP Request):**
  - Node này thực hiện câu lệnh `GET` tới API của Crunchbase (`https://api.crunchbase.com/api/v4/entities/organizations`).
  - Các sếp cần điền `user_key` chính là API Key của tài khoản Crunchbase.
  - *Lưu ý sản xuất:* Trong thực tế, các sếp nên thay node `Trigger Manual Test` bằng một **Cron Node** để lịch chạy tự động mỗi ngày (ví dụ: 8 giờ sáng).
* **Extract Company Details (Set):**
  - Node này giúp lọc ra các trường dữ liệu cốt lõi (Tên công ty, mô tả, vị trí, ngành nghề, ngày cập nhật gần nhất) nhằm tối ưu token cho AI.
* **Summarizer Agent & OpenAI Chat Model:**
  - Chọn model `gpt-4o-mini` (hoặc GPT-4 tùy nhu cầu).
  - Kết nối `OpenAI Chat Model` với credential OpenAI của các sếp.
  - Sử dụng kèm **Structured Output Parser** để ép AI trả về đúng cấu trúc JSON gồm 2 thuộc tính: `subject` (tiêu đề email) và `body` (nội dung email).
* **Send Email with Summary (Gmail):**
  - Chọn kết nối Gmail (`gmailOAuth2`).
  - Đưa biểu thức `{{$json.subject}}` vào ô Subject và `{{$json.body}}` vào phần Body của email.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm xem dữ liệu có trả về và email có được gửi đi chính xác hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh thông báo:** Ngoài gửi Gmail, các sếp có thể nối thêm node Telegram Bot hoặc Slack để bắn tin nhắn nhanh vào nhóm làm việc chung.
- **Lưu trữ lịch sử:** Thêm node Google Sheets để ghi lại danh sách các công ty đã được tổng hợp mỗi ngày, tạo cơ sở dữ liệu nghiên cứu thị trường lâu dài.
- **Lọc theo ngành nghề (Industry Filter):** Tùy chỉnh tham số trong HTTP Request của Crunchbase để chỉ lấy các công ty thuộc lĩnh vực AI, SaaS hoặc Fintech mà các sếp quan tâm.

### 📌 Kết luận
Workflow này là một "trợ lý ảo" cực kỳ đắc lực giúp tự động hóa hoàn toàn quy trình nghiên cứu thị trường khởi nghiệp. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc của các sếp!