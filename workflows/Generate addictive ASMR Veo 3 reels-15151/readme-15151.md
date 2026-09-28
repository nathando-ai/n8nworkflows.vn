---
title: "🚀 Tự động hóa sản xuất Reels ASMR vạn view với AI và n8n"
description: "Xây dựng hệ thống tự động hóa hoàn toàn quy trình tạo ý tưởng, render video ASMR tỷ lệ 9:16 và đăng tải lên YouTube, TikTok, Instagram bằng n8n và AI."
slug: "tu-dong-hoa-san-xuat-reels-asmr-ai-n8n"
tags: [n8n, automation, no-code, ai, content-creation, asmr-reels]
keywords: [n8n workflow, tự động hóa asmr reels, ai video generation, tao video tu dong n8n, postiz automation]
---

# 🚀 Tự động hóa sản xuất Reels ASMR vạn view với AI và n8n

Việc sản xuất video ngắn (Reels, TikTok, Shorts) theo phong cách ASMR cuốn hút đòi hỏi rất nhiều thời gian từ khâu lên ý tưởng, viết kịch bản, tạo hình ảnh/video cho đến bước dựng hình tỷ lệ 9:16 và đăng tải đa nền tảng. Nếu làm thủ công, các sếp sẽ mất hàng giờ mỗi ngày chỉ để duy trì kênh.

Hiểu được nỗi đau đó, workflow được thiết kế bởi **Koulikas Giannis** (Coreflow Automation) sẽ giúp các sếp tự động hóa **100%** từ A-Z quy trình này mà không cần tốn một giọt mồ hôi viết code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Hệ thống tự động kích hoạt định kỳ mỗi 8 giờ hoặc chạy thủ công để sản xuất nội dung liên tục.
- **AI thông minh:** Tận dụng sức mạnh của OpenAI GPT-4.1 Mini để sáng tạo kịch bản và ý tưởng ASMR siêu dính, kích thích người xem.
- **Xử lý đồ họa chuyên nghiệp:** Tự động gọi API tạo video, render chuẩn tỷ lệ 9:16, lưu trữ Cloud và đồng bộ hóa URL truy cập.
- **Đa kênh mạng xã hội:** Tự động phân phối và đăng tải video hoàn chỉnh lên các nền tảng YouTube, TikTok, và Instagram thông qua Postiz API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Khuyên dùng bản self-hosted để không bị giới hạn thời gian chạy).
- **Google Sheets & Google Cloud Storage (GCS)**: Để lưu trữ dữ liệu nguồn và upload video trung gian.
- **OpenAI API Key**: Cung cấp năng lượng cho các Agent AI (OpenAI GPT-4.1 Mini).
- **Video Generation API & Postiz API**: Cấu hình tài khoản dịch vụ render video và công cụ quản lý mạng xã hội Postiz để tự động publish bài viết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn dấu ba chấm ở góc trên bên phải -> **Import from File** và tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Read Sheet1 Data (Google Sheets):** Kết nối tài khoản Google của bạn, trỏ tới file Google Sheets chứa danh sách từ khóa, chủ đề hoặc thông tin nguồn cho video ASMR.
- **OpenAI GPT-4.1 Mini & Định nghĩa Agent (Define Prompt Agent / Idea Generation Agent):** Nhập OpenAI API Key để kích hoạt các Agent phân tích ý tưởng và cấu trúc caption tự động.
- **Set API Credentials & Generate JWT:** Nhập thông tin xác thực API tạo video của bạn để hệ thống tự động tạo token truy cập (`Acquire Access Token`).
- **Setup Postiz API Config & Fetch Postiz Integrations:** Điền cấu hình API của Postiz để hệ thống nhận diện các kênh mạng xã hội đích (YouTube, TikTok, Instagram).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm bằng node **Manual Trigger Start** để kiểm tra luồng dữ liệu chạy qua các bước `Route by Status`, `Wait 20 Seconds`, `Render Video to 9:16`.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** tại node **When Every 8 Hours** để hệ thống tự động cày cuốc thay cho bạn!

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước kiểm duyệt (Human-in-the-loop):** Chèn thêm node gửi thông báo về Telegram hoặc Slack trước khi video được đăng lên mạng xã hội để các sếp có thể duyệt lại lần cuối.
- **Lưu log chi tiết:** Kết nối thêm một node Google Sheets ở cuối luồng để ghi lại trạng thái đăng bài (Thành công/Thất bại, Link video trên từng nền tảng).
- **Mở rộng nền tảng:** Tích hợp thêm các kênh mạng xã hội khác hỗ trợ bởi Postiz để tối đa hóa độ phủ sóng thương hiệu.

### 📌 Kết luận
Workflow tạo Reels ASMR tự động này là một cỗ máy kiếm traffic thực thụ cho các nhà sáng tạo nội dung và agency marketing. Hãy cài đặt ngay hôm nay để giải phóng thời gian và để AI làm thay những công việc nặng nhọc nhất!