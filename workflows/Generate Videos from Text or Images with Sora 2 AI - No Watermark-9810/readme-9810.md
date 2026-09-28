---
title: "🚀 Hướng dẫn tạo video AI từ Text hoặc Ảnh không có watermark với Sora 2 trên n8n"
description: "Tự động hóa hoàn toàn quy trình tạo video chất lượng cao từ văn bản hoặc hình ảnh sử dụng Sora 2 AI (Kie.AI) không dính watermark, tích hợp form nhận yêu cầu và gửi kết quả qua Telegram."
slug: "tao-video-ai-sora-2-khong-watermark-n8n"
tags: [n8n, automation, ai-video, sora-2, telegram, content-creation]
keywords: [n8n workflow, sora 2 ai, tạo video ai, text to video, image to video, kie ai, tự động hóa n8n]
---

# 🚀 Tự động hóa quy trình tạo video AI với Sora 2 (Không Watermark) bằng n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mất hàng giờ tạo, render và chỉnh sửa video thủ công cho các chiến dịch marketing, TikTok hay Reels? Việc sử dụng các công cụ AI thông thường đôi khi gặp rắc rối với watermark hoặc quy trình thủ công tốn kém thời gian.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó! Nó cho phép các sếp xây dựng một hệ thống tạo video tự động 100% từ văn bản (Text-to-Video) hoặc từ hình ảnh có sẵn (Image-to-Video) sử dụng sức mạnh của **Sora 2 AI (thông qua Kie.AI)** hoàn toàn không có watermark, kèm theo giao diện Form thân thiện và tự động gửi video về Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần điền Form hoặc gửi ảnh, hệ thống tự lo phần còn lại từ xử lý API, chờ đợi đến tải về.
- **Video chất lượng cao, không Watermark:** Nhận ngay file MP4 chuyên nghiệp, sẵn sàng sử dụng cho các chiến dịch nội dung.
- **Hỗ trợ đa phương thức (Multimodal):** Vừa có thể tạo video từ câu lệnh văn bản (Text-to-Video), vừa có thể làm sống động hình ảnh tĩnh (Image-to-Video).
- **Thông báo tức thì:** Tự động gửi thành phẩm video trực tiếp về tài khoản Telegram cá nhân hoặc nhóm ngay khi hoàn tất.
:::

### 📦 Các Nodes chính trong Workflow
- **`formTrigger`**: Giao diện thu thập yêu cầu (prompt văn bản và ảnh tùy chọn) từ người dùng.
- **`switch`**: Bộ định tuyến thông minh phân tách luồng Text-to-Video hay Image-to-Video dựa trên việc có ảnh đính kèm hay không.
- **`httpRequest`**: Giao tiếp với API của ImgBB (upload ảnh) và Kie.AI (gửi yêu cầu tạo video, kiểm tra trạng thái, tải video).
- **`wait` & `if`**: Cơ chế polling thông minh, tự động kiểm tra tiến độ render của AI sau mỗi khoảng thời gian định sẵn mà không làm nghẽn hệ thống.
- **`telegram`**: Gửi file video hoàn chỉnh về Telegram cho người dùng.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Self-hosted hoặc n8n Cloud).
- **Kie.AI API Key:** Tài khoản tại [Kie.AI](https://kie.ai) để gọi API Sora 2.
- **ImgBB API Key:** Tài khoản miễn phí tại [ImgBB](https://api.imgbb.com/) (Dùng cho luồng Image-to-Video).
- **Telegram Bot (Tùy chọn):** Tạo bot qua `@BotFather` và lấy Chat ID từ `@get_id_bot` nếu muốn nhận video qua Telegram.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thông số sau để workflow hoạt động trơn tru:

- **Cấu hình Credentials cho Kie.AI:**
  - Đi tới `Credentials` -> `New Credential` -> Chọn **HTTP Header Auth**.
  - Đặt tên: `Kie Ai(Veo and more)`
  - Header Name: `Authorization`
  - Header Value: `Bearer YOUR_TOKEN_HERE` (Thay bằng API Key của sếp từ Kie.AI).
  - Áp dụng cho các node: `TEXT TO VIDEO`, `IMAGE TO VIDEO`, `Check Status (Text)`, `Check Status (Image)`.

- **Cấu hình ImgBB API (`Upload to ImgBB` node):**
  - Mở node `Upload to ImgBB` và thay thế tham số API Key mặc định bằng ImgBB API Key của các sếp để hệ thống có thể upload ảnh nguồn lên cloud.

- **Cấu hình Telegram (`Send Text to Video` & `Send Image to Video` nodes):**
  - Tạo kết nối `Telegram API` bằng Bot Token lấy từ `@BotFather`.
  - Thay thế `YOUR_CHAT_ID` bằng Chat ID thực tế của các sếp. *(Nếu không dùng Telegram, các sếp có thể xóa 2 node này và nối trực tiếp Download nodes sang dịch vụ lưu trữ khác).*

#### 3. Kích hoạt ⚡️
- Click vào node `On form submission` để lấy Test URL, mở trên trình duyệt và thử điền prompt/tải ảnh lên để test run.
- Sau khi test thành công, bật công tắc **Active** góc trên bên phải để đưa workflow vào vận hành 24/7.

---

## 🔄 Cơ chế hoạt động thông minh (Polling Mechanism)

Việc tạo video AI không diễn ra tức thì (thường mất từ 30 đến 120 giây tùy độ phân giải). Workflow này sử dụng vòng lặp thông minh:
1. **Gửi yêu cầu:** `TEXT TO VIDEO` hoặc `IMAGE TO VIDEO` đẩy request lên hệ thống Sora 2.
2. **Chờ đợi thông minh:** Node `Wait` tạm dừng 30 giây để tránh spam API và cho phép AI render.
3. **Kiểm tra trạng thái:** Node `Check Status` gọi API kiểm tra tiến độ.
4. **Đánh giá:** Node `Is Ready?` kiểm tra trạng thái (`success`). Nếu chưa xong, vòng lặp tự động quay lại chờ tiếp; nếu xong, tiến hành tải video về qua node `Download Video` và gửi về Telegram.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tối ưu Prompt:** Hãy sử dụng câu lệnh chi tiết (bao gồm chuyển động camera, ánh sáng, phong cách nghệ thuật) để Sora 2 trả về kết quả mãn nhãn nhất.
- **Mở rộng kênh lưu trữ:** Thay vì chỉ gửi qua Telegram, các sếp có thể nối thêm node Google Drive, OneDrive hoặc Airtable để lưu trữ toàn bộ video tự động tạo ra.
- **Báo cáo định kỳ:** Thêm node gửi thông báo tổng kết số lượng video đã tạo thành công vào cuối ngày qua Slack hoặc Email.

### 📌 Kết luận
Workflow tạo video AI Sora 2 không watermark này là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp tối ưu hóa quy trình sáng tạo nội dung của các sếp. Hãy cài đặt ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!