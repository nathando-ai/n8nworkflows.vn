---
title: "🚀 Tự động hóa tạo hình ảnh siêu đỉnh với Adamantiamable Lumi AI qua Replicate trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tích hợp Replicate API để tự động hóa quy trình tạo ảnh nghệ thuật với mô hình Adamantiamable Lumi AI."
slug: "tao-anh-tu-dong-voi-adamantiamable-lumi-ai-replicate-n8n"
tags: [n8n, automation, replicate, ai-image-generation, no-code, multimodal-ai]
keywords: [n8n workflow, tạo ảnh ai tự động, replicate api, adamantiamable lumi ai, n8n image generation]
---

# 🚀 Tự động hóa tạo hình ảnh đỉnh cao với Adamantiamable Lumi AI qua Replicate

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thao tác thủ công trên các nền tảng tạo ảnh AI, copy-paste prompt liên tục và chờ đợi kết quả rồi mới tải về? Việc sản xuất nội dung hình ảnh hàng loạt cho marketing hay mạng xã hội bằng tay thực sự tốn rất nhiều thời gian và làm giảm năng suất sáng tạo.

Giải pháp là gì? Hãy để n8n lo! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow tự động hóa hoàn toàn để gọi API **Replicate**, sử dụng mô hình **Adamantiamable Lumi AI** để sinh ảnh tự động chỉ bằng một cú click hoặc kích hoạt từ hệ thống khác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gửi yêu cầu prompt đến Replicate và nhận lại link hình ảnh hoàn thiện mà không cần thao tác thủ công trên web.
- **Tối ưu thời gian:** Xử lý việc gọi API, kiểm tra trạng thái (polling) và trích xuất kết quả một cách mượt mà.
- **Dễ dàng mở rộng:** Dễ dàng kết hợp thêm các bước lưu ảnh vào Google Drive, gửi về Telegram/Slack hoặc đăng bài tự động lên mạng xã hội.
- **Linh hoạt:** Dễ dàng thay đổi prompt và các thông số cấu hình hình ảnh theo nhu cầu chiến dịch.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn n8n (Cloud hoặc Self-hosted).
- **Replicate Account:** Tài khoản Replicate và **API Token** để có quyền gọi mô hình AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 8 nodes cơ bản được thiết kế sẵn sàng hoạt động.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Set API Key (Node loại: `set`):** 
  - Tại đây, các sếp cần cấu hình biến chứa Replicate API Key của mình. Đảm bảo thay thế giá trị mẫu bằng API token thật từ tài khoản Replicate.
- **Create Prediction (Node loại: `httpRequest`):** 
  - Node này sẽ gửi POST request đến endpoint của Replicate để khởi tạo quá trình tạo ảnh bằng mô hình `adamantiamable/lumi`.
  - Kiểm tra lại phần Header để đảm bảo đã truyền Authorization Bearer Token chính xác từ node `Set API Key`.
  - Cấu hình Body JSON với câu lệnh `prompt` mong muốn của các sếp.
- **Extract Prediction ID (Node loại: `code`):** 
  - Sử dụng đoạn mã Javascript ngắn để bóc tách `Prediction ID` trả về từ Replicate, phục vụ cho việc kiểm tra trạng thái ở các bước sau.
- **Wait & Check Prediction Status (Nodes `wait` & `httpRequest`):** 
  - Do AI mất một khoảng thời gian ngắn để render ảnh, node `Wait` sẽ tạm dừng một vài giây, sau đó node `Check Prediction Status` sẽ gọi lại API của Replicate để kiểm tra tiến độ.
- **Check If Complete (Node loại: `if`):** 
  - Kiểm tra xem trạng thái xử lý của Replicate đã hoàn thành (`succeeded`) hay chưa. Nếu chưa, workflow có thể quay lại vòng lặp chờ; nếu rồi, chuyển sang bước xử lý kết quả.
- **Process Result (Node loại: `code`):** 
  - Lọc và trích xuất đường dẫn URL của bức ảnh hoàn chỉnh để các sếp có thể sử dụng ngay lập tức cho các tác vụ tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** trên node `On clicking 'execute'` (hoặc nút Test) để chạy thử nghiệm lần đầu.
- Kiểm tra kết quả trả về ở node `Process Result` xem ảnh đã được sinh ra thành công chưa.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên bên phải để kích hoạt workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho công việc thực tế, các sếp có thể mở rộng thêm:
1. **Kết hợp Webhook/Form:** Thay vì dùng `Manual Trigger`, hãy thay bằng n8n Form hoặc Webhook để người dùng nhập prompt trực tiếp qua giao diện web.
2. **Lưu trữ tự động:** Thêm node **Google Drive** hoặc **Supabase/Airtable** để tải và lưu trữ vĩnh viễn hình ảnh vừa tạo (vì link gốc của Replicate có thời hạn).
3. **Thông báo kết quả:** Tích hợp node **Telegram** hoặc **Slack** để gửi hình ảnh vừa tạo trực tiếp về nhóm làm việc ngay khi hoàn tất.

### 📌 Kết luận
Workflow tích hợp Replicate AI với mô hình Adamantiamable Lumi trên n8n là một "vũ khí" cực kỳ lợi hại giúp các sếp tự động hóa quy trình sáng tạo nội dung hình ảnh. Hãy áp dụng ngay vào hệ thống của mình để tiết kiệm hàng giờ làm việc thủ công mỗi ngày!