---
title: "🎨 Tạo API Endpoint Tự Động Cải Tiến Hình Ảnh Bằng Nero AI (Không Code)"
description: "Hướng dẫn tự động hóa API endpoint cải tiến hình ảnh bằng API Nero AI, giúp các sếp tiết kiệm thời gian và nâng cao chất lượng hình ảnh chỉ với một cú nhấp chuột. Kết quả đạt được: hình ảnh sắc nét, tự động hóa hoàn toàn, không cần code."
slug: tao-api-endpoint-cai-tien-hinh-anh-nero-ai
tags: [n8n, automation, ai, api, nero-ai, no-code, tự động hóa hình ảnh]
keywords: [n8n workflow ai, tự động hóa cải tiến hình ảnh, api nero ai, tự động hóa không code, cải tiến hình ảnh tự động]
---

# 🎨 **Tạo API Endpoint Tự Động Cải Tiến Hình Ảnh Bằng Nero AI (Không Code)**

Hình ảnh mờ, mất sắc nét hay không đáp ứng tiêu chuẩn chất lượng là vấn đề thường gặp trong công việc của các sếp, đặc biệt khi phải xử lý hàng loạt hình ảnh cho dự án, marketing hoặc nội dung số. Thay vì phải tải lên các công cụ online và chờ đợi kết quả, **workflow này giúp bạn tự động hóa toàn bộ quy trình cải tiến hình ảnh chỉ với một API endpoint đơn giản**, kết hợp với công nghệ AI tiên tiến của **Nero AI**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7 và xử lý nhiều yêu cầu đồng thời, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng loạt hình ảnh chỉ trong vài giây thay vì thủ công.
- **Chất lượng cao**: Sử dụng AI để tự động cải tiến sắc nét, độ tương phản, và màu sắc.
- **Tự động hóa hoàn toàn**: Không cần can thiệp người dùng giữa quá trình xử lý.
- **Kết nối API**: Sử dụng endpoint riêng để tích hợp với các hệ thống khác (WordPress, Shopify, CRM...).
- **Không cần code**: Cấu hình đơn giản, phù hợp cho người mới bắt đầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Nero AI Business**:
   - Đăng ký API key từ [trang web Nero AI](https://ai.nero.com/business).
   - Lưu ý: API key này sẽ được sử dụng trong hai node `Create task` và `Query task status`.
2. **Dịch vụ n8n Self-hosted**:
   - Cài đặt n8n trên máy chủ riêng hoặc VPS (hướng dẫn cài đặt [tại đây](https://docs.n8n.io/hosting/installation/)).
3. **Công cụ test API** (tùy chọn):
   - Postman, Insomnia, hoặc cURL để gửi yêu cầu test đến endpoint.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io](https://n8n.io/workflows/4682) hoặc sao chép JSON từ trang này.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (icon "..." > Import).
- **Bước 3**: Dán JSON vào và nhấn **Import**.

:::note[Lưu ý]
Nếu import từ file JSON, các sếp có thể tải file từ [đây](https://n8n.io/workflows/4682/export) (chọn "Export" trên trang workflow).
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **6 node chính**, các sếp cần cấu hình như sau:

| **Node**               | **Lưu ý cấu hình**                                                                                                                                                                                                 |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Webhook**            | - **Path**: Giá trị mặc định là `c9795945-7dbb-45cb-9082-d3629f15504a` (không thay đổi).                                                                                                                     |
|                        | - **HTTP Method**: Đặt là `POST`.                                                                                                                                                                           |
| **Respond to Webhook** | Node này tự động phản hồi yêu cầu khi nhận được dữ liệu. Không cần cấu hình thêm.                                                                                                                      |
| **Wait**               | Thời gian chờ mặc định là **5 giây** (có thể điều chỉnh nếu cần).                                                                                                                                           |
| **If**                 | Node này kiểm tra xem yêu cầu có hợp lệ hay không. Các sếp không cần thay đổi cấu hình mặc định.                                                                                                      |
| **Create task**        | - **URL**: `https://api.nero.com/v1/tasks` (URL chính thức của Nero AI).                                                                                                                                   |
|                        | - **Headers**: Thêm `Authorization: Bearer <API_KEY>` (điền API key từ Nero AI).                                                                                                                          |
|                        | - **Body**: Chọn `JSON` và điền payload như sau (thay `image_url` bằng URL hình ảnh cần cải tiến):
  ```json
  {
    "service": "enhance",
    "input": {
      "image_url": "https://example.com/image.jpg"
    }
  }
  ```
| **Query task status**  | - **URL**: `https://api.nero.com/v1/tasks/{task_id}` (thay `{task_id}` bằng ID task từ response của `Create task`).                                                                                     |
|                        | - **Headers**: Thêm `Authorization: Bearer <API_KEY>`.                                                                                                                                                 |
|                        | - **Query Parameters**: Thêm `task_id` từ response của node `Create task`.                                                                                                                               |

#### **3. Kích hoạt ⚡️**
- **Bước 1**: Nhấn **Active** để bật workflow.
- **Bước 2**: Test với một URL hình ảnh bằng Postman:
  ```http
  POST https://<n8n-domain>/c9795945-7dbb-45cb-9082-d3629f15504a
  Headers:
    Content-Type: application/json
  Body:
    {
      "image_url": "https://example.com/image.jpg"
    }
  ```
- **Bước 3**: Kiểm tra response trong **n8n Editor** để xác nhận hình ảnh đã được cải tiến.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với WordPress/Shopify**:
   - Sử dụng plugin REST API để gửi yêu cầu cải tiến hình ảnh từ WordPress hoặc Shopify.
   - Ví dụ: Khi người dùng tải lên hình ảnh, hệ thống tự động gửi yêu cầu đến endpoint này và trả về URL hình ảnh cải tiến.

2. **Lưu log kết quả**:
   - Thêm node **Google Sheets** hoặc **Slack** để lưu hoặc thông báo kết quả cải tiến.
   - Cấu hình node `Respond to Webhook` để trả về URL hình ảnh cải tiến trong response.

3. **Xử lý lỗi tự động**:
   - Thêm node **Set** sau `Query task status` để kiểm tra trạng thái task và gửi thông báo lỗi nếu cần.

4. **Tối ưu hóa API key**:
   - Sử dụng **Environment Variables** trong n8n để lưu trữ API key an toàn thay vì hardcode.

---

### 📌 **Kết luận**
Với workflow này, các sếp đã có một **API endpoint tự động cải tiến hình ảnh** chỉ với vài bước cấu hình. Không cần viết code, không cần quản lý nhiều công cụ online, và nhất là **tự động hóa hoàn toàn** quy trình cải tiến hình ảnh. Hãy **áp dụng ngay** và nâng cao chất lượng hình ảnh cho dự án của mình!

👉 **Bắt đầu ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/4682) và cài đặt trên VPS của bạn!