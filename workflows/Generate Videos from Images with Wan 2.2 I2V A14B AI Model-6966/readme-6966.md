---
title: "🚀 Tự động tạo video chuyển động từ hình ảnh tĩnh bằng AI Wan 2.2 I2V"
description: "Hướng dẫn xây dựng workflow n8n tích hợp AI Wan 2.2 I2V trên Replicate để biến ảnh tĩnh thành video sinh động hoàn toàn tự động."
slug: "tao-video-tu-anh-voi-wan-2-2-i2v-ai-model-n8n"
tags: [n8n, automation, ai-video, wan-2.2, replicate, content-creation]
keywords: [n8n workflow, wan 2.2 i2v, tạo video từ ảnh ai, replicate api, tự động hóa n8n]
keywords: [n8n workflow, wan 2.2 i2v, tạo video từ ảnh ai, replicate api, tự động hóa n8n]
---

# 🚀 Tự động tạo video chuyển động từ hình ảnh tĩnh bằng AI Wan 2.2 I2V

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ đồng hồ để animate (làm chuyển động) từng bức ảnh sản phẩm, ảnh chân dung hay hình minh họa thủ công trên các công cụ phức tạp? Việc sản xuất nội dung video ngắn (Shorts, Reels, TikTok) đòi hỏi lượng tài nguyên hình ảnh chuyển động cực lớn, khiến đội ngũ marketing luôn rơi vào tình trạng quá tải.

Giải pháp là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình gọi mô hình AI **Wan 2.2 I2V A14B** thông qua Replicate API. Chỉ với một hình ảnh tĩnh và một đoạn mô tả (prompt), hệ thống sẽ tự động tạo ra những thước phim chuyển động mượt mà, chuyên nghiệp mà không cần bất kỳ thao tác thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến ảnh tĩnh thành video chỉ bằng vài cú click hoặc tích hợp vào hệ thống lớn.
- **Tiết kiệm thời gian & chi phí:** Không cần thuê dựng phim chuyên nghiệp hay tốn thời gian thao tác thủ công trên các web tool rời rạc.
- **Chất lượng AI hàng đầu:** Sử dụng mô hình Wan 2.2 I2V A14B mạnh mẽ từ Replicate, cho ra video có độ chi tiết và chuyển động chân thực.
- **Hoạt động liên tục:** Xử lý bất kỳ lúc nào, dễ dàng scale-up thành dây chuyền sản xuất nội dung hàng loạt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản Replicate:** Cần có tài khoản trên [Replicate](https://replicate.com/) và lấy **API Token**.
- **Tài nguyên đầu vào:** Hình ảnh gốc (URL hoặc file) và câu lệnh (Prompt) mô tả chuyển động mong muốn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n.io (Link gốc: `https://n8n.io/workflows/6966`), sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes được thiết kế tối ưu cho việc gọi API, chờ kết quả và xử lý trả về. Các sếp cần chú ý cấu hình các điểm sau:

- **Node "Set API Key":** 
  - Điền Replicate API Token của các sếp vào biến cấu hình trong node này để các node HTTP Request đằng sau có quyền gọi API.
- **Node "Create Prediction" (HTTP Request):** 
  - Kiểm tra endpoint gọi đến mô hình `wan-video/wan-2.2-i2v-a14b` trên Replicate.
  - Đảm bảo phần Body truyền đúng tham số yêu cầu của mô hình bao gồm: `prompt` (mô tả chuyển động) và `image` (đường dẫn hình ảnh đầu vào).
- **Node "Extract Prediction ID" & Node "Wait":** 
  - Node Code sẽ bóc tách lấy `prediction_id` từ kết quả trả về. Node Wait sẽ làm nhiệm vụ tạm dừng một khoảng thời gian (ví dụ: 10-15 giây) trước khi kiểm tra lại tiến độ render video của AI.
- **Node "Check Prediction Status" & Node "Check If Complete":** 
  - Kiểm tra xem AI đã render xong video hay chưa. Nếu chưa hoàn thành, vòng lặp (hoặc cơ chế chờ) sẽ tiếp tục; nếu hoàn thành, chuyển sang bước xử lý kết quả.
- **Node "Process Result":** 
  - Bóc tách lấy đường dẫn URL video hoàn chỉnh để các sếp có thể tải về hoặc gửi tiếp đến Telegram, Google Drive, Slack,...

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** ở node **On clicking 'execute'** để chạy thử với dữ liệu mẫu.
- Kiểm tra kết quả trả về ở node cuối cùng để đảm bảo video đã được tạo thành công.
- Bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái chạy tự động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau node "Process Result" để nhận thông báo kèm video ngay khi AI render xong.
- **Lưu trữ tự động:** Kết hợp thêm node Google Drive hoặc AWS S3 để tự động lưu trữ các video được tạo ra nhằm tránh link nguồn trên Replicate bị hết hạn.
- **Mở rộng hàng loạt (Batch Processing):** Đọc danh sách ảnh từ Google Sheets, sau đó dùng vòng lặp để tạo hàng loạt video tự động mỗi ngày.

### 📌 Kết luận
Workflow tạo video từ ảnh bằng mô hình Wan 2.2 I2V này là trợ thủ đắc lực giúp các nhà sáng tạo nội dung và marketer tối ưu hóa 100% thời gian sản xuất video ngắn. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để bứt phá hiệu suất công việc ngay hôm nay!