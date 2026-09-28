---
title: "🚀 Tra cứu ngày lễ quốc gia nhanh chóng với Nager.Date API qua Webhook"
description: "Workflow n8n nhận yêu cầu POST chứa năm và mã quốc gia, tự động gọi API Nager.Date và trả về danh sách ngày lễ công cộng chỉ trong vài giây."
slug: "public-holiday-lookup-nager-date"
tags: [n8n, automation, no-code, api, webhook, holiday]
keywords: [n8n workflow, tự động hóa, public holiday, Nager.Date, webhook API]
---

# 🚀 Tra cứu ngày lễ quốc gia nhanh chóng với Nager.Date API qua Webhook

Doanh nghiệp thường phải **tự tay tra cứu ngày lễ quốc gia** để lên lịch làm việc, tính lương, hay gửi thông báo tới khách hàng.  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót khi nhập dữ liệu thủ công hoặc quên cập nhật khi năm mới tới.  

**Public Holiday Lookup** là workflow n8n giải quyết 100 % nhu cầu này mà không cần viết một dòng code nào. Chỉ cần gửi một yêu cầu POST chứa `year` và `countryCode`, hệ thống sẽ gọi Nager.Date API, lấy danh sách ngày lễ và trả về ngay cho bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở trình duyệt, tìm kiếm và sao chép danh sách ngày lễ.  
- **Độ chính xác 100 %**: Dữ liệu được lấy trực tiếp từ API chính thức của Nager.Date.  
- **Tự động hoá hoàn toàn**: Workflow chạy 24/7, trả về kết quả ngay khi nhận yêu cầu.  
- **Dễ tích hợp**: Có thể nhúng vào hệ thống ERP, CRM, hoặc bot chat nội bộ chỉ bằng một endpoint.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Kết nối internet** để gọi Nager.Date API (không cần API key).  
- **Công cụ gửi POST** (Postman, curl, hoặc bất kỳ hệ thống nào có thể thực hiện HTTP POST).  
- **Thông tin đầu vào**:  
  - `year` : Năm muốn tra cứu (vd: `2025`).  
  - `countryCode` : Mã quốc gia ISO 2 ký tự (vd: `US`, `PH`, `DE`). Danh sách mã quốc gia: https://www.nager.at/Country  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n > Workflows**.  
2. Nhấn **Import** → **Upload JSON** và chọn file `public-holiday-lookup.json` (hoặc copy toàn bộ JSON từ trang gốc).  
3. Nhấn **Import** để workflow xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hướng dẫn cấu hình |
|------|-------------------|
| **Receive Holiday Request Webhook** | - **Path**: `public-holidays`  <br> - **HTTP Method**: `POST`  <br> - **Response Mode**: `Respond to webhook` (để node `Respond with Holiday Data` trả về). |
| **Get Public Holidays** (HTTP Request) | - **Method**: `GET`  <br> - **URL**: `https://date.nager.at/api/v3/PublicHolidays/{{ $json["year"] }}/{{ $json["countryCode"] }}`  <br> - **Response Format**: `JSON`  <br> - **Headers**: không cần (API công khai). |
| **Respond with Holiday Data** | - **Response Mode**: `Last Node` (đảm bảo trả về dữ liệu từ node HTTP Request).  <br> - **Response Body**: `{{$node["Get Public Holidays"].json}}` (hoặc để mặc định trả toàn bộ output). |
| **Sticky Note** | Chỉ mang tính mô tả, không cần cấu hình. |

> **Lưu ý:** Đảm bảo **Webhook URL** được công khai (hoặc qua reverse proxy) để các hệ thống bên ngoài có thể gọi được, ví dụ: `https://your-domain.com/webhook/public-holidays`.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** → **Run** để kiểm tra với dữ liệu mẫu:  
   ```json
   {
     "year": 2025,
     "countryCode": "US"
   }
   ```  
2. Kiểm tra phản hồi: danh sách ngày lễ dạng JSON.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi góc trên bên phải) để workflow luôn sẵn sàng nhận yêu cầu.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu log**: Thêm node **Google Sheets** hoặc **Airtable** để ghi lại mỗi lần truy vấn (ngày, quốc gia, số lượng ngày lễ).  
- **Thông báo**: Kết nối **Slack / Telegram** để gửi tin nhắn báo cáo nhanh khi có ngày lễ quan trọng (ví dụ: ngày lễ quốc gia lớn).  
- **Bộ lọc**: Trước node `Respond`, chèn **Function** để lọc chỉ lấy các ngày lễ loại `Public` hoặc `Bank`.  
- **Cache**: Dùng **Redis** hoặc **n8n Cache** để lưu kết quả trong 24 h, giảm số lần gọi API khi cùng một yêu cầu lặp lại.  

### 📌 Kết luận
Với workflow **Public Holiday Lookup**, các sếp có thể **tự động hoá hoàn toàn** quy trình tra cứu ngày lễ quốc gia, giảm thiểu lỗi nhập liệu và tăng tốc độ phản hồi cho các hệ thống nội bộ hay khách hàng. Hãy **import ngay**, cấu hình webhook và để n8n làm việc thay bạn! 🚀