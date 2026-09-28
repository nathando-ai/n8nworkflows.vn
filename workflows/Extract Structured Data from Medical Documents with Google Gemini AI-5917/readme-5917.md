---
title: "🚀 Tự động trích xuất dữ liệu y tế từ tài liệu bằng Google Gemini AI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động phân loại, đọc hiểu và trích xuất dữ liệu cấu trúc từ tài liệu y tế, hóa đơn, đơn thuốc bằng sức mạnh của Google Gemini AI."
slug: "trich-xuat-du-lieu-y-te-google-gemini-ai-n8n"
tags: [n8n, automation, google-gemini, ai-extraction, medical-document, workflow]
keywords: [n8n workflow, trích xuất tài liệu y tế, google gemini ai, automation hóa đơn, OCR y tế n8n]
---

# 🚀 Tự động trích xuất dữ liệu y tế từ tài liệu bằng Google Gemini AI

Các sếp trong ngành y tế, bảo hiểm hay tài chính chắc hẳn luôn cảm thấy đau đầu với hàng núi hóa đơn, đơn thuốc, và báo cáo y tế dạng ảnh hoặc PDF cần xử lý thủ công mỗi ngày. Việc gõ lại dữ liệu vừa tốn thời gian, dễ sai sót lại gây chậm trễ quy trình vận hành. 

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, tự động hóa 100% quy trình tiếp nhận, phân loại và trích xuất dữ liệu cấu trúc từ tài liệu y tế thông qua **Google Gemini AI** mà không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Loại bỏ hoàn toàn việc nhập liệu thủ công, tự động hóa khâu đọc tài liệu.
- **Độ chính xác cao (>95%):** Nhờ sức mạnh của mô hình Google Gemini (Flash 2.0), AI hiểu ngữ cảnh y tế và trích xuất chuẩn xác.
- **Định dạng chuẩn hóa:** Trả về kết quả dạng JSON cấu trúc sạch sẽ, dễ dàng tích hợp vào phần mềm quản lý phòng khám, bảo hiểm.
- **Hoạt động 24/7:** Xử lý tài liệu ngay lập tức thông qua Webhook bất cứ khi nào có request gửi đến.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Self-hosted hoặc n8n Cloud).
- **Google Gemini API Key** (lấy miễn phí hoặc trả phí từ [Google AI Studio](https://aistudio.google.com/)).
- Một endpoint hoặc URL chứa file ảnh/tài liệu y tế để test.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này và Paste trực tiếp vào n8n Editor là toàn bộ 10 nodes sẽ tự động xuất hiện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:

- **Webhook Input**: Node này nhận request phương thức `POST` tại đường dẫn `/webhook/analyze-medical-document`. Các sếp có thể đổi path nếu muốn.
- **Download Image**: Node `httpRequest` có nhiệm vụ tải file hình ảnh từ `image_url` được truyền vào từ payload của webhook.
- **Extract to Base64**: Node loại `extractFromFile` giúp chuyển đổi dữ liệu nhị phân của ảnh sang định dạng Base64 để gửi lên AI.
- **Gemini Classify Extract & Gemini Structure Data**: Đây là 2 node cốt lõi sử dụng `googlePalmApi` credentials. 
  - Các sếp cần tạo một Credentials mới trong n8n mang tên **Google Gemini(PaLM) API**, sau đó điền **Gemini API Key** lấy từ Google AI Studio vào đây.
  - Các node này sẽ gọi mô hình Google Gemini để tiến hành phân loại loại tài liệu (hóa đơn, đơn thuốc, báo cáo...) và trích xuất cấu trúc dữ liệu mong muốn.
- **API Response**: Trả về kết quả JSON cuối cùng cho client gọi webhook.

Cấu trúc JSON đầu vào mẫu (`POST /webhook/analyze-medical-document`):
```json
{
  "image_url": "https://example.com/medical-receipt.jpg"
}
```

Cấu trúc JSON đầu ra mẫu:
```json
{
  "documentType": "financial",
  "content": {
    "amount": 150.00
  },
  "confidence": 0.95
}
```

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và gửi một request test bằng Postman hoặc cURL để kiểm tra dữ liệu trả về.
- Sau khi test thành công, gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp thực tế, các sếp có thể mở rộng thêm:
- **Lưu trữ tự động:** Thêm node Google Sheets hoặc Airtable ngay sau bước `Finalize Track` để lưu toàn bộ dữ liệu trích xuất thành file báo cáo quản lý tài chính/y tế.
- **Cảnh báo lỗi qua Slack/Telegram:** Thêm nhánh Error Trigger để nếu ảnh mờ hoặc AI không đọc được, hệ thống sẽ tự động báo cáo về nhóm chat của nhân sự.
- **Xử lý hàng loạt (Batch Processing):** Kết hợp thêm một vòng lặp (Loop node) nếu các sếp cần xử lý danh sách hàng trăm hóa đơn cùng một lúc từ thư mục Google Drive.

### 📌 Kết luận
Việc tự động hóa trích xuất tài liệu y tế chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n và Google Gemini AI. Hãy áp dụng ngay vào doanh nghiệp của mình để tối ưu hóa chi phí vận hành và giải phóng sức lao động cho đội ngũ nhân sự ngay hôm nay các sếp nhé!