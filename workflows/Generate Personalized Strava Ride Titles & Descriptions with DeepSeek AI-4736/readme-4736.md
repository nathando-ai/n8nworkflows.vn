---
title: "🚀 Tự động tạo Tiêu đề và Mô tả buổi đạp xe Strava cực chất với DeepSeek AI trong n8n"
description: "Biến các buổi đạp xe trên Strava trở nên sinh động và cuốn hút hơn bao giờ hết với workflow tự động phân tích dữ liệu và tạo nội dung bằng DeepSeek AI."
slug: "tu-dong-tao-tieu-de-mo-ta-strava-voi-deepseek-ai"
tags: [n8n, automation, no-code, strava, ai, deepseek]
keywords: [n8n workflow, tự động hóa strava, deepseek ai, tạo tiêu đề strava tự động, openrouter]
---

# 🚀 Tự động tạo Tiêu đề và Mô tả buổi đạp xe Strava cực chất với DeepSeek AI

Các sếp là những tín đồ của môn đạp xe và thường xuyên sử dụng Strava? Việc phải nghĩ ra một tiêu đề thật kêu hay một mô tả chi tiết, hài hước cho mỗi buổi đạp xe (Ride) đôi khi tốn không ít thời gian sau khi đã kiệt sức trên đường đua. 

Nỗi đau này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh này. Nó sẽ tự động bắt sự kiện khi các sếp vừa kết thúc chuyến đi, phân tích toàn bộ dữ liệu (quãng đường, thời gian, độ cao...) và nhờ **DeepSeek AI** (thông qua OpenRouter) viết giùm một chiếc tiêu đề cực "bốc" cùng đoạn mô tả chuẩn "dân chuyên nghiệp". 100% tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Không còn phải đau đầu nghĩ caption hay tiêu đề mỗi khi upload bài lên Strava.
- **Cá nhân hóa độc đáo:** AI tự động dựa vào thông số thực tế (tốc độ, cung đường, độ dốc) để tạo ra nội dung sinh động, mang đậm dấu ấn cá nhân.
- **Hoạt động ngầm 24/7:** Vừa bấm nút "Finish" trên đồng hồ/App Strava là vài giây sau bài đăng đã được AI trau chuốt lại tự động.
- **Tối ưu chi phí:** Sử dụng mô hình DeepSeek R1 miễn phí qua OpenRouter, tiết kiệm tuyệt đối.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Strava & Strava Developer App** (để lấy Client ID và Client Secret cấu hình OAuth2).
- **Tài khoản OpenRouter** (để lấy API Key kết nối với DeepSeek AI).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON tương ứng, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính được cấu hình mượt mà, các sếp cần lưu ý các điểm sau khi kết nối:

- **Strava Trigger & Strava Node:** 
  - Vào phần **Credentials** > chọn **Strava OAuth2 API**.
  - Điền `Client ID` và `Client Secret` từ cổng lập trình viên Strava Developer Portal.
  - Cấp quyền (scopes): `activity:read_all` và `activity:write` để n8n có quyền đọc và chỉnh sửa bài đăng của các sếp.
- **OpenRouter Chat Model:**
  - Chọn credential kết nối OpenRouter.
  - Đảm bảo tham số model được trỏ chính xác đến `deepseek/deepseek-r1:free` (hoặc model tùy chọn khác của DeepSeek).
- **Các node xử lý dữ liệu (Code & Edit Fields):**
  - Node `Code` và `Combine Everything` sẽ tự động gom nhặt và biến đổi dữ liệu JSON phức tạp của Strava thành một đoạn text gọn gàng để AI dễ dàng đọc hiểu ngữ cảnh.
  - Node `Edit Fields` làm nhiệm vụ bóc tách kết quả trả về từ AI thành tiêu đề (`name`) và mô tả (`description`) trước khi đẩy ngược lại lên Strava.

#### 3. Kích hoạt ⚡️
- Thử nghiệm bằng cách tạo một hoạt động mẫu hoặc đợi chuyến đi thực tế tiếp theo.
- Sau khi kiểm tra thấy mọi thứ hoạt động trơn tru, hãy gạt công tắc sang chế độ **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo về Telegram/Slack:** Các sếp có thể bổ sung thêm node Telegram ở cuối workflow để bot gửi một tin nhắn báo cáo kèm thông tin buổi đạp xe và nội dung AI vừa tạo vào nhóm chat riêng.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets để lưu trữ toàn bộ các thông số và nội dung bài viết AI làm kỷ niệm, tiện theo dõi tiến độ tập luyện theo tuần/tháng.
- **Tùy chỉnh Prompt cho AI:** Trong node `Strava Social Manager` (Agent), các sếp có thể tinh chỉnh lại câu lệnh (prompt) theo văn phong cá nhân: hài hước, truyền động lực, hay chuyên nghiệp kiểu vận động viên đua xe đạp.

### 📌 Kết luận
Một workflow cực kỳ thú vị và hữu ích cho anh em đam mê đạp xe công nghệ. Hãy cài đặt ngay để những chuyến "núp gió", "kéo tua" của các sếp trên Strava trở nên chuyên nghiệp và thú vị hơn bao giờ hết! Chúc các sếp thao tác thành công!