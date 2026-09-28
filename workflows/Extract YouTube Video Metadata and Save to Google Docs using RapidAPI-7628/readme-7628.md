---
title: "🚀 Tự động trích xuất thông tin video YouTube và lưu vào Google Docs qua RapidAPI"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy thông tin chi tiết từ URL YouTube bằng RapidAPI và lưu trữ trực tiếp vào Google Docs một cách chuyên nghiệp."
slug: "trich-xuat-youtube-metadata-luu-google-docs-n8n"
tags: [n8n, automation, youtube, google-docs, rapidapi, no-code]
keywords: [n8n workflow, tự động hóa youtube, trích xuất metadata youtube, rapidapi n8n, lưu google docs tự động]
---

# 🚀 Tự động trích xuất thông tin video YouTube và lưu vào Google Docs

Việc tổng hợp thông tin, nghiên cứu nội dung hoặc làm báo cáo từ các video YouTube thủ công thường ngốn rất nhiều thời gian của các sếp. Việc phải copy thủ công tiêu đề, mô tả, số liệu thống kê rồi dán vào tài liệu khiến quy trình làm việc bị chậm lại.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code bằng **n8n** giúp các sếp nhận URL video qua biểu mẫu, tự động bóc tách dữ liệu qua RapidAPI và lưu thẳng vào Google Docs chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công copy-paste thông tin từ từng video YouTube.
- **Dữ liệu chuẩn hóa:** Tự động lọc và trình bày tiêu đề, mô tả, số liệu, thumbnail một cách gọn gàng, dễ đọc.
- **Lưu trữ tập trung:** Toàn bộ thông tin được cập nhật trực tiếp vào Google Docs phục vụ nghiên cứu và làm nội dung.
- **Vận hành liên tục 24/7:** Kích hoạt tức thì ngay khi có người dùng gửi URL qua form.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **RapidAPI** và đăng ký một gói dịch vụ YouTube Metadata API bất kỳ.
- Tài khoản **Google Account** để kết nối Google Docs.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trong n8n, sau đó copy toàn bộ JSON của workflow hoặc import file JSON tương ứng để hệ thống tự động dựng các node.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **On form submission (`formTrigger`):** 
  - Node này tạo một giao diện form đơn giản để nhập URL video YouTube. Các sếp có thể tùy chỉnh lại tiêu đề form hoặc chia sẻ đường dẫn form này cho team sử dụng.
- **YouTube Metadata (`httpRequest`):** 
  - Cấu hình endpoint API của RapidAPI trỏ đến dịch vụ YouTube Metadata.
  - Thêm các Header xác thực cần thiết như `X-RapidAPI-Key` và `X-RapidAPI-Host` lấy từ tài khoản RapidAPI của các sếp.
  - Truyền tham số URL video nhận được từ form vào request API.
- **Reformat (`code`):** 
  - Node JavaScript này có nhiệm vụ bóc tách các trường dữ liệu thô (tiêu đề, mô tả, lượt xem, thống kê, hình ảnh...) từ kết quả trả về của API và định dạng lại thành một đoạn văn bản sạch sẽ, dễ đọc.
- **Append Data in Google Docs (`googleDocs`):** 
  - Kết nối tài khoản Google của các sếp (chọn Credentials `googleApi`).
  - Chọn thao tác là `update` (hoặc append tùy theo cấu trúc tài liệu mong muốn).
  - Chọn file Google Docs đích và trỏ dữ liệu đã được định dạng từ node *Reformat* vào nội dung cần ghi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách gửi một URL video YouTube bất kỳ qua form.
- Kiểm tra lại tài liệu Google Docs xem dữ liệu đã được đẩy vào chuẩn xác chưa.
- Gạt nút **Active** để chính thức đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node chatwork ngay sau bước ghi Google Docs để bắn thông báo về nhóm chat rằng tài liệu video mới đã được cập nhật thành công.
- **Lưu trữ song song:** Ngoài Google Docs, các sếp có thể kết nối thêm Google Sheets để lưu trữ dạng bảng, tiện cho việc lọc và thống kê số liệu sau này.
- **Tích hợp AI tóm tắt:** Kết hợp thêm các node AI (OpenAI/Anthropic) trước bước ghi tài liệu để tự động viết tóm tắt ngắn gọn nội dung video thay vì giữ nguyên mô tả dài.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho các Content Creator, Marketer hoặc Researcher thường xuyên phải tổng hợp tài nguyên từ YouTube. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc của các sếp!