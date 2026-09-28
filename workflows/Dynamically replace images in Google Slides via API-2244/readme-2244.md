---
title: "🚀 Tự Động Thay Thế Hình Ảnh Trong Google Slides Qua API Bằng n8n"
description: "Hướng dẫn xây dựng API tự động thay đổi hình ảnh (logo, background) trong Google Slides thông qua webhook n8n cực kỳ nhanh chóng và không cần code phức tạp."
slug: "tu-dong-thay-the-hinh-anh-trong-google-slides-qua-api-bang-n8n"
tags: [n8n, automation, google-slides, api, no-code, webhook]
keywords: [n8n workflow, tự động hóa google slides, replace image google slides api, n8n webhook, auto presentation]
---

# 🚀 Tự Động Thay Thế Hình Ảnh Trong Google Slides Qua API Bằng n8n

Việc thủ công cập nhật hàng loạt slide thuyết trình, thay đổi logo khách hàng, hay cập nhật hình nền (background) cho các bộ tài liệu kinh doanh thực sự là một "cực hình" tốn thời gian. Thay vì ngồi copy-paste từng tấm hình bằng tay, các sếp hoàn toàn có thể tự động hóa 100% quy trình này thông qua một API endpoint duy nhất được xây dựng bằng n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Cập nhật hình ảnh trong Google Slides chỉ bằng một cú gọi API (POST Request).
- **Linh hoạt & Tái sử dụng:** Dùng một định danh (identifier) duy nhất cho nhiều slide và nhiều presentation khác nhau.
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn các thao tác thủ công lặp đi lặp lại khi làm slide báo cáo, pitch deck.
- **Hoạt động 24/7:** Webhook lắng nghe liên tục, sẵn sàng phục vụ mọi hệ thống tích hợp (CRM, Form, v.v.).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Account** có quyền truy cập Google Slides.
- **Google Slides OAuth2 API Credentials** đã được cấu hình trên n8n để kết nối với Google API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow hoặc sử dụng tính năng import file JSON để đưa 7 nodes vào màn hình làm việc (Canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính phối hợp nhịp nhàng để nhận dữ liệu từ Webhook, kiểm tra tham số, gọi Google Slides API và trả về kết quả:

- **Node `Webhook`**: Lắng nghe phương thức `POST` tại đường dẫn `/path/replace-image-in-slide`. Đây sẽ là endpoint API của các sếp.
- **Node `Check if all params are provided` (IF Node)**: Kiểm tra xem các tham số bắt buộc đã được truyền đầy đủ qua body của request hay chưa.
- **Node `Error Missing Fields` & `Respond to Webhook`**: Xử lý phản hồi về cho client tùy thuộc vào việc request có hợp lệ hay không.
- **Node `Retrieve All Slide Elements` & `Retrieve matching Images ObjectIds` (Code Node)**: Kết nối tới Google Slides API thông qua **Google Slides OAuth2 API Credentials**, lấy danh sách các phần tử trong slide và tìm chính xác `ObjectId` của bức ảnh dựa vào Alt Text mà các sếp đã đánh dấu.
- **Node `Replace Images` (HTTP Request)**: Gửi lệnh yêu cầu Google Slides thực hiện thay thế hình ảnh cũ bằng hình ảnh mới từ URL được cung cấp.

**💡 Hướng dẫn cấu hình Alt Text trong Google Slides:**
1. Click vào bức ảnh các sếp muốn tự động thay thế trong Google Slides.
2. Nhấp chuột phải chọn **Format Options** (Tùy chọn định dạng) -> Chọn mục **Alt Text** (Văn bản thay thế).
3. Nhập mã định danh (Unique Identifier) vào ô **Title** hoặc **Description**, ví dụ: `client_logo` hoặc `background`.

**📤 Cấu trúc Body khi gọi API (POST Request):**
```json
{
  "presentation_id": "ID_cua_Google_Slides_lay_tu_URL",
  "image_key": "client_logo",
  "image_url": "https://example.com/new-image.png"
}
```
*(Lấy `presentation_id` từ URL của Google Slides: `https://docs.google.com/presentation/d/{presentation_id}/edit`)*

#### 3. Kích hoạt ⚡️
- Thực hiện gửi một Test Request bằng Postman hoặc cURL tới Webhook URL của n8n để kiểm tra xem hình ảnh trong slide đã được thay đổi thành công chưa.
- Sau khi test ngon lành, các sếp bật **Active** workflow để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Form/Typeform:** Tạo một landing page hoặc form nội bộ để nhân viên sales nhập thông tin, tự động gọi API này để tạo ra bộ tài liệu giới thiệu khách hàng độc bản trong vài giây.
- **Tích hợp Slack/Telegram:** Thêm node thông báo về kênh chat nhóm khi một tài liệu Google Slides đã được cập nhật thành công hình ảnh.
- **Mở rộng hàng loạt:** Sử dụng vòng lặp (Loop/Split In Batches) để cập nhật hình ảnh cho hàng chục presentation cùng một lúc.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình làm việc với tài liệu và báo cáo tự động. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tiết kiệm hàng giờ thao tác thủ công mỗi tuần!