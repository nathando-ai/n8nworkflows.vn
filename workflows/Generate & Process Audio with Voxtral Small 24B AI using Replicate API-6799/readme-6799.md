---
title: "🚀 Tự động hóa xử lý và tạo âm thanh thông minh với Voxtral Small 24B AI qua Replicate API trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Replicate API sử dụng mô hình Voxtral Small 24B để xử lý, chuyển đổi và tạo nội dung âm thanh tự động."
slug: "tu-dong-hoa-tao-va-xu-ly-am-thanh-voxtral-small-24b-replicate-n8n"
tags: [n8n, automation, no-code, replicate, ai-audio]
keywords: [n8n workflow, voxtral small 24b, replicate api, ai audio generation, tu dong hoa am thanh]
keywords: [n8n workflow, voxtral small 24b, replicate api, ai audio generation, tự động hóa âm thanh]
---

# 🚀 Tự động hóa xử lý và tạo âm thanh thông minh với Voxtral Small 24B AI qua Replicate API trong n8n

Việc xử lý, chuyển mã hoặc tạo nội dung âm thanh thủ công thường tốn rất nhiều thời gian và đòi hỏi nhiều công cụ phức tạp. Đối với các nhà sáng tạo nội dung và doanh nghiệp, việc phải thao tác qua lại giữa nhiều nền tảng làm giảm đi hiệu suất vận hành đáng kể. Giải pháp tuyệt vời cho các sếp chính là workflow n8n tự động hóa 100% kết hợp sức mạnh của mô hình **Voxtral Small 24B** thông qua **Replicate API**, giúp xử lý các tác vụ về âm thanh (transcription, translation, audio understanding) một cách nhanh chóng, mượt mà và hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Loại bỏ hoàn toàn các thao tác thủ công khi làm việc với các file âm thanh lớn.
- **Tích hợp AI đỉnh cao:** Khai thác tối đa khả năng xử lý âm thanh xuất sắc từ mô hình Voxtral Small 24B (`notdaniel/voxtral-small-24b-2507`).
- **Cơ chế vòng lặp thông minh:** Tự động kiểm tra trạng thái xử lý (Polling loop) với độ trễ tối ưu, đảm bảo nhận kết quả chính xác mà không bị quá tải API.
- **Xử lý lỗi mượt mà:** Hệ thống tự động bắt lỗi và trả về phản hồi chi tiết khi có sự cố xảy ra trong quá trình xử lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Replicate Account:** Tài khoản tại [Replicate](https://replicate.com) cùng với **API Token** cá nhân và một chút số dư khả dụng.
- **File âm thanh đầu vào:** Chuẩn bị sẵn đường dẫn hoặc file audio để hệ thống tiến hành xử lý.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON.
- Mở giao diện n8n của các sếp, chọn **Workflows** -> Nhấp vào dấu **+** (Add workflow) -> Chọn **Import from File/Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 13 nodes được sắp xếp logic từ bước kích hoạt đến xử lý vòng lặp và trả kết quả. Các sếp cần chú ý cấu hình các điểm sau:

- **Set API Token (Node `set`):** 
  - Điền Replicate API Token của các sếp vào biến cấu hình. Thay thế đoạn `'YOUR_REPLICATE_API_TOKEN'` bằng token thực tế để xác thực quyền gọi API.
- **Set Audio Parameters (Node `set`):**
  - Cấu hình các tham số đầu vào cho mô hình như: đường dẫn file `audio`, mã ngôn ngữ `language` (mặc định là `en`), và `max_new_tokens` (mặc định là `1024`).
- **Create Audio Prediction & Check Status (Nodes `httpRequest`):**
  - Đảm bảo endpoint gọi API chính xác tới Replicate (`https://api.replicate.com/v1/predictions`).
- **Wait 5s & Wait 10s (Nodes `wait`):**
  - Các node này quản lý thời gian chờ giữa các lần gọi kiểm tra tiến độ (polling). Các sếp có thể tinh chỉnh thời gian này nếu thời gian xử lý của file audio dài hơn bình thường.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** sau khi chọn **Manual Trigger** để test thử với dữ liệu mẫu.
- Theo dõi các kết quả trả về ở nhánh **Success Response** hoặc **Error Response**.
- Khi mọi thứ đã chạy trơn tru, hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Tích hợp thêm node Slack hoặc Telegram ở nhánh **Success Response** để nhận thông báo trực tiếp khi file audio được xử lý xong.
- **Lưu trữ kết quả:** Kết nối kết quả trả về với Google Sheets hoặc cơ sở dữ liệu (Supabase, PostgreSQL) để lưu lại lịch sử xử lý.
- **Mở rộng đầu vào:** Thay thế **Manual Trigger** bằng Webhook hoặc Trigger từ Google Drive/Email để hệ thống tự động bắt file audio mới tải lên và xử lý ngay lập tức.

### 📌 Kết luận
Với workflow n8n tích hợp Voxtral Small 24B AI này, các sếp đã có trong tay một hệ thống tự động hóa xử lý âm thanh cực kỳ mạnh mẽ, tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình làm việc của mình!