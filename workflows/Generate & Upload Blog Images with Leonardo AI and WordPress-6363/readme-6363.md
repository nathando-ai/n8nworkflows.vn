---
title: "🚀 Tự Động Tạo Ảnh Bằng Leonardo AI và Upload Lên WordPress với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình tạo hình ảnh minh họa bài viết bằng Leonardo AI và đăng tải trực tiếp lên WordPress."
slug: "tu-dong-tao-anh-leonardo-ai-va-wordpress-n8n"
tags: [n8n, automation, no-code, leonardo-ai, wordpress, ai-content]
keywords: [n8n workflow, tạo ảnh leonardo ai, upload ảnh wordpress tự động, n8n wordpress integration, ai automation]
---

# 🚀 Tự Động Tạo Ảnh Bằng Leonardo AI và Upload Lên WordPress với n8n

Các sếp có thấy mệt mỏi khi mỗi lần viết bài blog xong lại phảiì hì hục lên Midjourney hay Leonardo AI gõ prompt, tải ảnh về máy, rồi lại mò vào WordPress upload, chèn ảnh đại diện thủ công không? Công việc lặp đi lặp lại này ngốn không ít thời gian quý báu mà lẽ ra các sếp nên dành cho chiến lược nội dung.

Đừng lo, giải pháp ở đây rồi! Bài viết này sẽ hướng dẫn các sếp cách thiết lập workflow n8n tự động hóa 100%: từ việc gọi API tạo ảnh đỉnh cao từ Leonardo AI, chờ đợi xử lý, cho đến việc tự động đẩy thẳng bức ảnh đó lên thư viện media của WordPress. Không một dòng code phức tạp, chạy mượt mà 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn thao tác thủ công tải xuống và tải lên giữa các nền tảng.
- **Tự động hóa hoàn toàn:** Nhận yêu cầu từ bài viết mới hoặc kích hoạt thủ công, ảnh tự động xuất hiện trên WordPress.
- **Chất lượng đỉnh cao:** Tận dụng sức mạnh tạo hình ảnh sắc nét từ Leonardo AI phù hợp với mọi chủ đề blog.
- **Hoạt động không ngừng nghỉ:** Workflow chạy ổn định trên n8n, sẵn sàng scale-up cho hệ thống content lớn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hệ thống n8n:** Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **Tài khoản Leonardo AI:** Lấy API Key để gọi lệnh tạo ảnh.
- **Website WordPress:** Cần có tài khoản quản trị và cấu hình Application Passwords (hoặc plugin hỗ trợ REST API) để n8n có quyền upload ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/6363](https://n8n.io/workflows/6363)), sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON dán trực tiếp vào Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp nhớ cấu hình kỹ các node trọng điểm sau:
- **Node `HTTP Request1`, `HTTP Request2`, `HTTP Request3` (Leonardo AI):** 
  - Cấu hình Authentication dạng Header Auth hoặc Bearer Auth sử dụng API Key của Leonardo AI.
  - Tinh chỉnh các tham số prompt, kích thước ảnh, kiểu dáng theo ý muốn trong phần body của request.
- **Node `Wait`:** 
  - Do Leonardo AI cần thời gian để render ảnh, node này đóng vai trò tạm dừng workflow trong một khoảng thời gian nhất định (thường từ 15-30 giây) trước khi gọi lệnh lấy kết quả ảnh về.
- **Node `Upload image2` (WordPress):** 
  - Chọn Credentials loại `wordpressApi` (điền URL trang WordPress, Username và Application Password).
  - Đảm bảo endpoint upload ảnh của WordPress REST API (`/wp-json/wp/v2/media`) được cấu hình chính xác để nhận file nhị phân (binary data) từ các node trước truyền sang.
- **Node `Code` & `Code1`:** 
  - Các đoạn mã JavaScript ngắn gọn dùng để xử lý dữ liệu JSON trả về từ Leonardo AI (lọc lấy URL ảnh gốc) và chuẩn bị cấu trúc dữ liệu trước khi gửi sang WordPress.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** tại node `When clicking ‘Execute workflow’` hoặc kích hoạt qua node `When Executed by Another Workflow` nếu gọi từ một hệ thống n8n khác (ví dụ: workflow sinh bài viết bằng ChatGPT).
- Kiểm tra kết quả trả về, nếu ảnh đã nằm trên thư viện WordPress thì các sếp tiến hành gạt công tắc sang **Active** để chạy tự động nhé!

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối với AI Writer:** Kết hợp workflow này phía sau một workflow tạo nội dung bài viết bằng AI (OpenAI/Claude). Khi bài viết hoàn thành, tiêu đề hoặc mô tả sẽ được tự động truyền vào Leonardo AI để sinh ảnh minh họa phù hợp nhất.
- **Gửi thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bot báo cáo ngay: *"Đã tạo và upload ảnh thành công cho bài viết X!"* kèm link ảnh trực tiếp.
- **Lưu log vào Google Sheets:** Ghi lại lịch sử tạo ảnh, prompt đã dùng và URL ảnh trên WordPress để dễ dàng quản lý và kiểm tra lại khi cần.

### 📌 Kết luận
Tự động hóa quy trình sản xuất nội dung chưa bao giờ dễ dàng đến thế với n8n và các mô hình AI như Leonardo. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa hiệu suất làm việc và bứt phá lượng traffic cho blog ngay hôm nay!