---
title: "🚀 Tự động tạo danh tính giả lập chân thực cho UX/UI Mockup với AI và n8n"
description: "Hướng dẫn xây dựng API tự động tạo tên người dùng đa dạng, chân thực bằng OpenAI LLM phục vụ thiết kế UX/UI, prototype và kiểm thử hệ thống."
slug: "tao-ten-ux-ui-mockup-openai-n8n"
tags: [n8n, automation, openai, ux-ui, ai-agent, no-code]
keywords: [n8n workflow, tạo tên mockup, ai name generator, openai gpt, tu dong hoa ux ui]
---

# 🚀 Tự động tạo danh tính giả lập chân thực cho UX/UI Mockup với AI và n8n

Khi làm các sản phẩm thiết kế UX/UI, dựng prototype trong Figma, hay phát triển các ứng dụng demo trên Bubble, việc nghĩ ra danh sách tên người dùng (User Persona) sao cho tự nhiên, đa dạng vùng miền và phù hợp với ngữ cảnh luôn tốn rất nhiều thời gian. Việc lặp đi lặp lại những cái tên quen thuộc như "John Doe" hay "Nguyễn Văn A" sẽ làm giảm tính chuyên nghiệp của bản thiết kế.

Giải pháp là gì? Hãy để AI lo! Workflow n8n này sẽ giúp các sếp xây dựng một API endpoint chuyên dụng để tự động sinh ra danh sách tên chân thực dựa trên giới tính, số lượng và tên mẫu (reference name) tùy chỉnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu thời gian thiết kế:** Cung cấp ngay lập tức hàng loạt tên người dùng chuẩn xác cho mockup, prototype mà không cần nghĩ thủ công.
- **Đa dạng hóa danh tính:** Hỗ trợ linh hoạt tùy chỉnh theo giới tính (nam, nữ, trung tính), số lượng từ 1 đến 20 tên và khả năng học theo phong cách tên mẫu (reference name).
- **Đầu chuẩn JSON:** Dữ liệu trả về qua Webhook được format sạch sẽ, sẵn sàng tích hợp trực tiếp vào các No-Code app (Bubble, Webflow) hoặc công cụ thiết kế.
- **Hoạt động 24/7:** Biến n8n thành một Microservice API nội bộ phục vụ mọi dự án thiết kế của đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Tài khoản OpenAI có quyền truy cập vào các mô hình GPT (workflow sử dụng mặc định `gpt-4.1-mini`).
- **HTTP Client:** Postman, cURL hoặc ứng dụng bất kỳ có khả năng bắn HTTP POST Request tới webhook của n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy toàn bộ mã JSON của workflow và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ trang quản trị n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Webhook Trigger (Name Request):** Node này nhận request phương thức `POST` tại đường dẫn `/generate-names`. Các sếp có thể thay đổi path nếu muốn, đồng thời cấu hình authentication (Header Auth hoặc Basic Auth) nếu cần bảo mật endpoint.
- **OpenAI GPT-4.1 Mini:** Node xử lý trí tuệ nhân tạo. Các sếp cần tạo Credentials mới bằng cách điền **OpenAI API Key** của mình. Có thể đổi model sang các dòng GPT khác nếu muốn tối ưu chi phí hoặc tốc độ.
- **AI Name Generator Agent & Format Name Results:** Các node này đã được cấu hình sẵn Prompt và logic xử lý code JavaScript để bóc tách kết quả trả về từ LLM thành mảng JSON chuẩn chỉnh.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và dùng Postman gửi một đoạn JSON mẫu lên Webhook URL để test thử:
```json
{
  "gender": "masculine",
  "count": 5,
  "reference_name": "Alex Chen"
}
```
- Nếu nhận về kết quả JSON thành công chứa danh sách tên, các sếp hãy bật **Active** workflow để đưa vào sử dụng thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thẳng vào Figma / Bubble:** Gọi trực tiếp Webhook URL này từ ứng dụng No-Code hoặc Plugin để lấy tên người dùng động ngay trong lúc thiết kế giao diện.
- **Mở rộng tham số đầu vào:** Tùy chỉnh thêm các biến trong prompt AI như độ tuổi, nghề nghiệp hoặc văn hóa/quốc tịch (ví dụ: tên tiếng Nhật, tên Châu Âu...) để mockup thêm phần sinh động.
- **Lưu trữ dữ liệu:** Kết nối thêm một node Google Sheets hoặc Database (Supabase/Postgres) để lưu lại lịch sử các tên đã tạo nếu dự án có nhu cầu quản lý lớn.

### 📌 Kết luận
Workflow tạo tên giả lập bằng AI này là một "vũ khí bí mật" giúp các designer và developer tiết kiệm hàng giờ đồng hồ mỗi tuần. Hãy cài đặt ngay vào hệ thống n8n của các sếp để tự động hóa trọn gói khâu chuẩn bị dữ liệu mẫu cho các dự án sắp tới!