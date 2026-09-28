---
title: "🚀 Tự động tạo ảnh kiểu tóc độc đáo bằng AI với n8n và Replicate"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo ảnh kiểu tóc bằng mô hình AI Replicate (barbacoaexpert1), giúp tiết kiệm thời gian và tạo nội dung sáng tạo không giới hạn."
slug: "tu-dong-tao-anh-kieu-toc-ai-replicate-n8n"
tags: [n8n, automation, ai-image-generation, replicate, content-creation]
keywords: [n8n workflow, tạo ảnh ai, replicate api, tự động hóa n8n, ai haircuts]
---

# 🚀 Tự động tạo ảnh kiểu tóc độc đáo bằng AI với n8n và Replicate

Các sếp làm trong ngành làm đẹp, salon tóc hay sáng tạo nội dung chắc hẳn luôn đau đầu mỗi khi cần lên ý tưởng hoặc thiết kế hình ảnh các kiểu tóc mới để chạy quảng cáo hay đăng mạng xã hội. Việc thuê thiết kế hoặc tự làm thủ công vừa tốn kém lại mất rất nhiều thời gian. 

Giải pháp là đây! Hôm nay tôi xin giới thiệu một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia **YaronBeen**. Workflow này sẽ tự động hóa 100% quy trình gọi API đến mô hình AI chuyên dụng trên **Replicate** (`barbacoaexpert1/ai-haircuts`) để tạo ra những bức ảnh kiểu tóc siêu thực, giúp các sếp tối ưu hóa quy trình làm content mà không cần biết lập trình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập câu lệnh (prompt), hệ thống sẽ tự gửi yêu cầu, chờ xử lý và trả về kết quả ảnh kiểu tóc chất lượng cao.
- **Tiết kiệm chi phí & thời gian:** Không cần thuê thiết kế đắt đỏ hay tốn hàng giờ mày mò trên các công cụ chỉnh sửa ảnh phức tạp.
- **Sáng tạo không giới hạn:** Dễ dàng biến hóa hàng trăm kiểu tóc khác nhau chỉ bằng vài thao tác cấu hình câu lệnh.
- **Quy trình thông minh:** Workflow tích hợp sẵn cơ chế kiểm tra trạng thái xử lý của AI (Polling/Wait) để đảm bảo lấy được kết quả thành công một cách mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản trên **Replicate** và **Replicate API Key** để kết nối với mô hình AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào màn hình giao diện n8n Editor của mình, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi "treo", các sếp cần chú ý cấu hình các node quan trọng sau:

- **Set API Key (`Set API Key` node):** 
  - Tại đây, các sếp cần cấu hình biến chứa **Replicate API Key** của mình. Hãy đảm bảo key này có quyền gọi API tạo dự đoán (Prediction) trên Replicate.
- **Create Prediction (`Create Prediction` node - HTTP Request):** 
  - Node này sẽ gửi prompt mô tả kiểu tóc tới model `barbacoaexpert1/ai-haircuts` trên Replicate. Các sếp cần kiểm tra lại phần Body/JSON payload để truyền đúng tham số `prompt` theo mong muốn.
- **Extract Prediction ID (`Extract Prediction ID` node - Code):** 
  - Node này dùng mã nguồn JavaScript nhỏ để bóc tách ID của tiến trình dự đoán vừa được khởi tạo từ phản hồi của Replicate.
- **Wait & Check Prediction Status (`Wait` & `Check Prediction Status` nodes):** 
  - Do việc tạo ảnh bằng AI mất vài giây đến vài phút, node `Wait` sẽ tạm dừng một chút trước khi gọi lại API (`Check Prediction Status`) để kiểm tra xem AI đã vẽ xong chưa.
- **Check If Complete (`If` node):** 
  - Kiểm tra trạng thái trả về. Nếu đã hoàn thành (`succeeded`), luồng sẽ chuyển sang bước xử lý kết quả; nếu chưa, có thể cấu hình vòng lặp chờ tiếp.
- **Process Result (`Process Result` node - Code):** 
  - Lọc và trả về đường dẫn (URL) bức ảnh kiểu tóc hoàn chỉnh cho các sếp sử dụng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`On clicking 'execute'`** để test chạy thử (Manual Trigger) với một prompt mẫu.
- Kiểm tra kết quả đầu ra ở các node cuối. Nếu mọi thứ xanh mướt (success), các sếp có thể đổi Trigger thành Webhook, Schedule (chạy định kỳ) và bật **Active workflow** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Telegram/Slack:** Các sếp có thể nối thêm node Telegram hoặc Slack vào cuối workflow để hệ thống tự động gửi ảnh kiểu tóc vừa tạo thẳng vào nhóm chat của team.
- **Lưu trữ tự động:** Thêm node Google Drive hoặc Airtable để lưu lại lịch sử các prompt đã dùng kèm link ảnh kết quả, phục vụ cho việc quản lý chiến dịch marketing.
- **Mở rộng nguồn Trigger:** Thay vì dùng Manual Trigger, hãy tích hợp Webhook để nhận yêu cầu tạo ảnh từ form đăng ký trên website của salon tóc.

### 📌 Kết luận
Workflow tạo ảnh kiểu tóc bằng AI với Replicate trên n8n là một công cụ cực kỳ mạnh mẽ giúp tự động hóa khâu sản xuất nội dung hình ảnh. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất công việc và mang lại trải nghiệm độc đáo cho khách hàng của các sếp nhé! Chúc các sếp thao tác thành công!