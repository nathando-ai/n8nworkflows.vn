---
title: "🚀 Trích xuất Thực thể từ Trang Web tự động với Google Natural Language API"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích và trích xuất thực thể (con người, tổ chức, địa điểm) từ bất kỳ URL nào bằng Google Natural Language API."
slug: "trich-xuat-thuc-the-tu-trang-web-google-natural-language-api"
tags: [n8n, automation, ai, marketing, google-cloud, web-scraping]
keywords: [n8n workflow, google natural language api, trich xuat thuc the, entity extraction, tu dong hoa marketing]
---

# 🚀 Trích xuất Thực thể từ Trang Web tự động với Google Natural Language API

Việc phân tích nội dung từ các trang web đối thủ, bài báo tin tức hoặc blog để thu thập thông tin về con người, tổ chức, địa điểm hay các sự kiện thủ công thường tốn rất nhiều thời gian. Các marketer và đội ngũ nghiên cứu thường phải đọc qua hàng loạt trang web để tổng hợp dữ liệu.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code. Chỉ với một cú gọi API (Webhook), hệ thống sẽ tự động cào nội dung trang web, gửi sang Google Natural Language API để phân tích chuyên sâu và trả về danh sách các thực thể (Named Entities) kèm theo mức độ quan trọng (Salience score) một cách nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận kết quả phân tích cấu trúc chỉ bằng một yêu cầu POST chứa URL.
- **Dữ liệu chuẩn xác:** Sử dụng Google Natural Language API đẳng cấp thế giới để nhận diện chính xác người, tổ chức, địa điểm, sản phẩm...
- **Tối ưu SEO & Content Marketing:** Dễ dàng phân tích từ khóa, thực thể nổi bật trên trang web của đối thủ hoặc bài viết của chính mình.
- **Tích hợp linh hoạt:** Dễ dàng kết nối Webhook này vào các ứng dụng khác như CRM, Google Sheets, hoặc Notion.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt và hoạt động (Cloud hoặc Self-hosted).
- **Google Cloud Account:** Đã tạo Project và kích hoạt **Cloud Natural Language API**.
- **Google API Key:** Khóa API có quyền truy cập vào Natural Language API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON của workflow, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần lưu ý cấu hình kỹ các điểm sau:

- **Get Url (`webhook`):** Node nhận dữ liệu đầu vào. Các sếp sẽ sử dụng URL Webhook này để gửi request POST từ các hệ thống khác.
  - Định dạng JSON gửi lên:
    ```json
    {
      "url": "https://website-to-analyze.com/page"
    }
    ```
- **Get URL Page Contents (`httpRequest`):** Node thực hiện cào nội dung HTML hoặc text từ URL được truyền vào từ Webhook.
- **Google Entities (`httpRequest`):** Node gọi trực tiếp đến Google Natural Language API. 
  - Các sếp cần thay thế `"YOUR-GOOGLE-API-KEY"` bằng Google API Key thực tế của mình trong phần Header hoặc Query Parameters của HTTP Request.
  - Đảm bảo Google Natural Language API đã được bật trên Google Cloud Console.
- **Respond with detected entities (`code`):** Node xử lý dữ liệu JavaScript, lọc và định dạng lại kết quả trả về từ Google thành dạng cấu trúc gọn gàng, dễ đọc.
- **Respond to Webhook (`respondToWebhook`):** Trả kết quả phân tích cuối cùng về cho ứng dụng gọi tới.

#### 3. Kích hoạt ⚡️
- Nhấp nút **Execute Workflow** và gửi một request thử nghiệm bằng Postman hoặc cURL để kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết nối thêm node Google Sheets hoặc Supabase sau node `Respond with detected entities` để lưu lại lịch sử phân tích của từng URL.
- **Tích hợp Chatbot:** Gửi kết quả phân tích tóm tắt về một kênh Slack hoặc nhóm Telegram khi có yêu cầu phân tích bài viết mới.
- **Xử lý hàng loạt (Batch Processing):** Kết hợp thêm một vòng lặp (Loop node) để phân tích danh sách hàng trăm URL từ file Excel/Google Sheets cùng một lúc.

### 📌 Kết luận
Với workflow n8n này, việc trích xuất và phân tích thông tin thực thể từ trang web trở nên đơn giản hơn bao giờ hết. Hãy áp dụng ngay để tiết kiệm hàng giờ đồng hồ nghiên cứu thủ công cho đội ngũ của các sếp!