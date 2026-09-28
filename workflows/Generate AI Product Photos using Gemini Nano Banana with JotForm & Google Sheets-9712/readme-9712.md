---
title: "🚀 Tự động tạo ảnh sản phẩm bằng AI với Gemini Nano Banana, JotForm & Google Sheets trên n8n"
description: "Xây dựng hệ thống tự động hóa 100% giúp tạo hình ảnh sản phẩm chất lượng cao bằng AI Gemini kết hợp JotForm và Google Sheets, tiết kiệm hàng giờ chỉnh sửa thủ công."
slug: "tu-dong-tao-anh-san-pham-ai-gemini-jotform-google-sheets-n8n"
tags: [n8n, automation, ai-images, google-gemini, jotform, google-sheets]
keywords: [n8n workflow, tạo ảnh sản phẩm ai, gemini nano banana, jotform automation, google sheets n8n, tự động hóa marketing]
---

# 🚀 Tự động tạo ảnh sản phẩm bằng AI với Gemini Nano Banana, JotForm & Google Sheets

Các sếp làm thương mại điện tử, marketing hay thiết kế chắc hẳn đều hiểu cảm giác "đau đầu" mỗi khi cần sản xuất hàng loạt ảnh sản phẩm. Việc thuê studio chụp ảnh, hoặc ngồi hàng giờ đồng hồ để blend màu, tách nền, tạo bối cảnh bằng tay vừa tốn kém chi phí lại vừa chậm tiến độ. 

Giải pháp là gì? Hãy để công nghệ tự động hóa lo! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia Zain Khan. Workflow này sẽ tự động nhận thông tin sản phẩm từ **JotForm**, xử lý hình ảnh qua AI **Google Gemini**, lưu trữ file vào **Google Drive** và đồng thời cập nhật toàn bộ trạng thái, lịch sử lên **Google Sheets** mà không cần đụng tay vào một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Từ lúc khách hàng/nhân viên điền form đến khi hoàn thành bức ảnh sản phẩm AI.
- **Tiết kiệm chi phí studio:** Tận dụng sức mạnh của Google Gemini để tạo ra các bối cảnh sản phẩm đa dạng, bắt mắt.
- **Quản lý tập trung:** Mọi dữ liệu, link ảnh kết quả đều được đồng bộ tự động vào Google Sheets và Google Drive một cách ngăn nắp.
- **Linh hoạt kích hoạt:** Hỗ trợ cả kích hoạt tức thì qua JotForm, chạy định kỳ với Schedule Trigger hoặc chạy thủ công khi cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- Tài khoản **n8n** (Self-hosted hoặc Cloud).
- Tài khoản **JotForm** để tạo form nhận yêu cầu/ảnh sản phẩm gốc.
- Tài khoản **Google Workspace** (Google Sheets, Google Drive).
- **Google Gemini API Key** (hoặc cấu hình Credential cho node Google Gemini).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua tuỳ chọn **Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **JotForm Trigger**: Kết nối tài khoản JotForm của các sếp và chọn đúng Form ID nhận yêu cầu tạo ảnh sản phẩm.
- **Get row(s) in sheet / Add row in sheet / Update row in sheet**: Trỏ các node Google Sheets này tới file Google Sheet quản lý của sếp, map đúng tên cột cho các trường thông tin sản phẩm, link ảnh gốc và link ảnh kết quả AI.
- **Message a model (Google Gemini)**: Cấu hình Gemini API Credential và kiểm tra lại System Prompt để AI hiểu rõ cách tạo mô tả/bối cảnh ảnh sản phẩm theo ý muốn.
- **Gemini Nano Banana (HTTP Request)**: Điền đúng Endpoint và Header/API Key của dịch vụ AI tạo ảnh mà workflow đang tích hợp.
- **Upload to Drive**: Chọn thư mục đích trên Google Drive để lưu trữ các bức ảnh sản phẩm do AI xuất ra.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng node `When clicking ‘Execute workflow’` hoặc gửi một bản ghi mẫu từ JotForm để kiểm tra luồng chạy của dữ liệu.
- Sau khi chắc chắn không còn lỗi, hãy gạt công tắc sang chế độ **Active** để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** vào cuối workflow để gửi thông báo ngay lập tức về máy điện thoại của sếp hoặc đội ngũ thiết kế mỗi khi có một bức ảnh sản phẩm mới được tạo thành công.
- **Xử lý hàng loạt (Batch Processing):** Kết hợp với `Schedule Trigger` để tự động quét Google Sheets và tạo hàng loạt ảnh sản phẩm theo lịch hẹn vào ban đêm, giúp tối ưu băng thông và tài nguyên.
- **Lưu log lỗi:** Thiết lập nhánh Error Trigger để bắt lỗi trong quá trình gọi API Gemini và ghi log lại vào một sheet riêng, giúp dễ dàng kiểm tra khi có sự cố.

### 📌 Kết luận
Việc ứng dụng AI vào quy trình sản xuất nội dung hình ảnh chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa năng suất, tiết kiệm chi phí và bứt phá doanh số cho cửa hàng trực tuyến của các sếp ngay hôm nay!