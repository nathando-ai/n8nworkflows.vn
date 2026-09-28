---
title: "🚀 Xây dựng API trích xuất dữ liệu từ hình ảnh tự động bằng Gemini AI và n8n"
description: "Hướng dẫn tạo API trích xuất dữ liệu thông minh từ ảnh (CCCD, hóa đơn, danh thiếp) bằng Google Gemini AI và n8n, trả về định dạng JSON chuẩn xác."
slug: "api-trich-xuat-du-lieu-tu-hinh-anh-bang-gemini-ai-n8n"
tags: [n8n, automation, no-code, gemini-ai, ocr, api]
keywords: [n8n workflow, trích xuất dữ liệu ảnh, gemini api, ocr tự động, n8n webhook]
---

# 🚀 Biến hình ảnh thành dữ liệu cấu trúc tự động với Gemini AI & n8n

Các sếp có đang đau đầu vì phải nhập liệu thủ công từ hàng trăm hình ảnh, hóa đơn, CCCD hay danh thiếp mỗi ngày? Việc đọc và gõ lại dữ liệu không chỉ tốn thời gian, dễ sai sót mà còn làm chậm trễ quy trình vận hành của doanh nghiệp.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tạo ra một **API endpoint tự động**, nhận đầu vào là URL hình ảnh và yêu cầu trích xuất, sau đó sử dụng sức mạnh của **Google Gemini AI** để đọc hiểu, trích xuất thông tin và trả về kết quả dưới dạng JSON chuẩn xác 100% không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình OCR:** Thay vì dùng các tool OCR truyền thống kém thông minh, Gemini AI hiểu ngữ cảnh và trích xuất đúng trọng tâm.
- **API Endpoint sẵn sàng:** Dễ dàng tích hợp vào website, app di động hoặc các phần mềm quản lý nội bộ (CRM, ERP).
- **Cấu trúc dữ liệu tùy biến linh hoạt:** Các sếp có thể định nghĩa các trường (properties) muốn lấy ngay trong request (ví dụ: Số CCCD, Họ tên, Ngày sinh, Tổng tiền...).
- **Tiết kiệm 90% thời gian:** Xử lý hàng nghìn tài liệu chỉ trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Credentials:** Tài khoản Google AI Studio để lấy API Key kết nối với node Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động mượt mà với nhau. Các sếp cần chú ý các điểm sau:
- **Webhook:** Node này đóng vai trò nhận request từ bên ngoài. Các sếp nhớ copy URL endpoint (Production/Test URL) để gọi API.
- **Get image from URL:** Node `httpRequest` thực hiện tải hình ảnh từ URL được truyền vào trong request body (`image_url`).
- **Transform image to base64:** Node `extractFromFile` chuyển đổi định dạng ảnh sang Base64 để chuẩn bị gửi cho AI.
- **Call Gemini API (Flash Lite) với Image:** Node cốt lõi xử lý AI. Các sếp cần cấu hình **Google Palm/Gemini API Credentials** và chọn model phù hợp (khuyên dùng Gemini Flash Lite để có tốc độ xử lý nhanh và tiết kiệm chi phí).
- **Edit fields to output required data alone:** Node `set` giúp lọc và làm sạch dữ liệu trả về, đảm bảo kết quả gọn gàng đúng yêu cầu.
- **Respond to Webhook:** Trả kết quả dữ liệu JSON về cho ứng dụng gọi API.

#### 3. Test API Call (cURL mẫu) ⚡️
Các sếp có thể kiểm tra nhanh API bằng lệnh cURL sau:

```bash
curl --request GET \
  --url https://your_domain.com/webhook/data-extractor \
  --data '{
  "image_url":"https://www.immihelp.com/nri/images/sample-pan-card-front.jpg",
  "Requirement":"extract the details from the image",
  "properties": {
        "PAN Number": {
          "type": "string"
        },
        "Name": {
          "type": "string"
        },
        "Date of Birth": {
          "type": "string"
        },
        "Valid": {
          "type": "boolean"
        }
      }
}'
```

**Kết quả mẫu nhận được:**
```json
{
  "result": "{\"Date of Birth\":\"23/11/1974\",\"Name\":\"RAHUL GUPTA\",\"PAN Number\":\"ABCDE1234F\",\"Valid\":true}"
}
```

- Sau khi test thành công, bấm **Active** để đưa workflow vào trạng thái hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack Bot:** Nhận ảnh gửi vào nhóm chat, bot tự động gọi API này và trả kết quả ngay lập tức.
- **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Airtable** để lưu lại toàn bộ dữ liệu đã trích xuất thành file báo cáo.
- **Xử lý đa dạng tài liệu:** Áp dụng cho việc quét hóa đơn thanh toán, xử lý đơn hàng tự động hoặc xác thực danh tính khách hàng (KYC).

### 📌 Kết luận
Với workflow n8n kết hợp Gemini AI này, các sếp đã sở hữu ngay một hệ thống OCR thông minh chuẩn doanh nghiệp mà không cần tốn chi phí thuê đội ngũ lập trình phức tạp. Áp dụng ngay để tối ưu hóa quy trình làm việc thôi nào!