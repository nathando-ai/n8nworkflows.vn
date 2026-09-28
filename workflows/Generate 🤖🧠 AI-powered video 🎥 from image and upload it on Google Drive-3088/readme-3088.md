---
title: "🚀 Tự động tạo video bằng AI từ hình ảnh và lưu trữ trực tiếp lên Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video từ hình ảnh sử dụng AI, kiểm tra trạng thái render và lưu trữ thành phẩm an toàn trên Google Drive."
slug: "tu-dong-tao-video-ai-tu-hinh-anh-google-drive-n8n"
tags: [n8n, automation, no-code, AI video, Google Drive, HTTP Request]
keywords: [n8n workflow, tạo video AI từ ảnh, automation n8n, google drive upload, AI video generator]
---

# 🚀 Tự động tạo video bằng AI từ hình ảnh và lưu trữ trực tiếp lên Google Drive

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ đồng hồ để tạo video thủ công từ hình ảnh cho các chiến dịch marketing, sau đó lại phải tải xuống và upload thủ công lên Google Drive chưa? Quy trình này vừa tốn thời gian, vừa dễ sai sót và làm gián đoạn cảm sáng tạo.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ thông minh, tự động hóa 100% quy trình: **Nhận yêu cầu qua form 👉 Gọi AI tạo video từ ảnh 👉 Kiểm tra tiến độ 👉 Tải về và lưu trữ gọn gàng trên Google Drive**. Tất cả diễn ra hoàn toàn tự động mà không cần một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh canh chừng thời gian render video hay tải đi tải lại giữa các nền tảng.
- **Tự động hóa toàn diện:** Từ khâu nhận input (hình ảnh, prompt) qua Form cho đến khi file video nằm gọn trong Google Drive.
- **Vận hành mượt mà 24/7:** Workflow tích hợp cơ chế chờ (Wait) và kiểm tra trạng thái (If/Loop) thông minh để xử lý các tác vụ render nặng của AI.
- **Lưu trữ khoa học:** File video tạo ra được phân loại và cất giữ an toàn trên Google Drive cá nhân hoặc doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hệ thống n8n:** Đã được cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Google Drive:** Để lấy OAuth2 Credentials cấu hình node upload video.
- **API Key/Tài khoản dịch vụ AI Video:** Dịch vụ bên thứ ba cung cấp API tạo video từ ảnh (được gọi thông qua node HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc (hoặc copy đoạn JSON tương ứng) và dán trực tiếp vào n8n Editor của mình thông qua tính năng `Import from Clipboard`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `On form submission` (Form Trigger):** 
  - Nơi khởi tạo quy trình. Các sếp cần cấu hình giao diện form để người dùng (hoặc chính các sếp) tải ảnh lên và nhập các thông tin cần thiết cho AI.
- **Node `Create Video` (HTTP Request):** 
  - Điền chính xác Endpoint API của dịch vụ tạo video AI. 
  - Đảm bảo truyền đúng Headers chứa API Key và Body chứa dữ liệu ảnh/prompt lấy từ Form Trigger.
- **Node `Get status` & `Wait 60 sec.` & `Completed?` (HTTP Request, Wait, If):**
  - Vì quá trình render video của AI mất thời gian, workflow sử dụng node `Wait 60 sec.` để chờ và `Get status` để gọi lại kiểm tra.
  - Node `Completed?` (If node) sẽ kiểm tra xem trạng thái trả về đã hoàn thành hay chưa (`status === 'completed'`). Nếu chưa, vòng lặp tiếp tục chờ; nếu rồi, chuyển sang bước lấy file.
- **Node `Get Url Video` & `Get File Video` (HTTP Request):**
  - Lấy đường dẫn download video từ kết quả trả về của AI và tải tệp video nhị phân (binary) về bộ nhớ tạm của n8n.
- **Node `Upload Video` (Google Drive):**
  - Chọn tài khoản Google Drive (Credentials OAuth2).
  - Chọn thư mục đích (`Parent Folder`) trên Google Drive để lưu video thành phẩm.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một bản test thông qua Form Trigger để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công và không báo lỗi, các sếp nhớ gạt công tắc sang chế độ **Active** để hệ thống tự động hoạt động nhé!

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau node `Upload Video` để bot bắn thông báo kèm đường dẫn Google Drive ngay khi video render xong.
- **Lưu log vào Google Sheets:** Thêm node Google Sheets để ghi lại lịch sử tạo video (thời gian, tên file, link Drive) phục vụ việc quản lý và thống kê.
- **Xử lý hàng loạt (Batch Processing):** Có thể mở rộng form để nhận nhiều ảnh cùng lúc, xử lý danh sách hàng đợi (Queue) chuyên nghiệp hơn.

### 📌 Kết luận
Việc tích hợp AI vào quy trình sản xuất nội dung video chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất làm việc và giải phóng thời gian cho các sếp tập trung vào chiến lược kinh doanh lớn hơn!