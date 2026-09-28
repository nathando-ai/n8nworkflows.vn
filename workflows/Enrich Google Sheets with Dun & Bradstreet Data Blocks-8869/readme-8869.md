---
title: "🚀 Tự động hóa làm giàu dữ liệu doanh nghiệp từ Dun & Bradstreet vào Google Sheets với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để tự động lấy mã Bearer Token từ Dun & Bradstreet, gọi API Data Blocks, trích xuất điểm Paydex và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-du-lieu-dun-bradstreet-google-sheets-n8n"
tags: [n8n, automation, no-code, google-sheets, api-integration, dun-bradstreet]
keywords: [n8n workflow, tự động hóa google sheets, dun and bradstreet api, làm giàu dữ liệu doanh nghiệp, paydex score n8n]
---

# 🚀 Tự động hóa làm giàu dữ liệu doanh nghiệp từ Dun & Bradstreet vào Google Sheets

Việc thu thập và cập nhật thông tin tài chính, điểm tín dụng (Paydex) của các đối tác hay khách hàng doanh nghiệp từ **Dun & Bradstreet (D&B)** theo cách thủ công thường tốn rất nhiều thời gian, dễ xảy ra sai sót khi copy-paste dữ liệu hàng loạt. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên: tự động đọc danh sách mã DUNS từ Google Sheets, xác thực tài khoản lấy Bearer Token, gọi API D&B Data Blocks để lấy các thông tin tài chính quan trọng, và tự động ghi đè hoặc thêm mới (`Upsert`) kết quả trở lại Google Sheets mà không cần động đến một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ qua thao tác tra cứu thủ công từng mã DUNS trên hệ thống D&B.
- **Cập nhật thông minh:** Tự động lọc các dòng chưa xử lý và chỉ cập nhật (`Upsert`) những dữ liệu mới, tránh trùng lặp.
- **Dữ liệu thời gian thực:** Lấy chính xác điểm số tín dụng Paydex và các chỉ số kinh doanh mới nhất từ D&B đưa thẳng vào Google Sheets.
- **Tối ưu vận hành:** Tiết kiệm hàng chục giờ làm việc mỗi tuần cho đội ngũ Sales, Mua hàng (Procurement) hoặc Quản trị rủi ro.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Dun & Bradstreet (API Access):** Cần có `Username` và `Password` để gọi API lấy Token.
- **Google Sheets:** Chuẩn bị sẵn một trang tính có các cột cơ bản như: `duns`, `paydex`, `Complete` (hoặc tương tự).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (ID: `8869`) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Node `Get Companies` & `Append to g-sheets` (Google Sheets):**
  - Vào **Credentials**, tạo mới kết nối **Google Sheets (OAuth2)** và đăng nhập bằng tài khoản Google của các sếp.
  - Trỏ đúng tới File Google Sheets và Sheet Tab chứa danh sách doanh nghiệp cần làm giàu dữ liệu.

- **Node `Get Token1` (HTTP Request):**
  - Cấu hình phương thức `POST` tới URL: `https://plus.dnb.com/v3/token`.
  - Thiết lập **Authentication** là *Basic Auth*, điền **D&B Username** và **Password** của các sếp.
  - Thêm Body Parameter: `grant_type = client_credentials` và Header `Accept = application/json`.

- **Node `D&B Info` (HTTP Request):**
  - Cấu hình phương thức `GET` tới URL lấy dữ liệu Data Blocks động theo từng dòng:
    ```text
    https://plus.dnb.com/v1/data/duns/{{ $json.duns }}?blockIDs=paymentinsight_L4_v1&tradeUp=hq&customerReference=customer%20reference%20text&orderReason=6332
    ```
  - Thêm Header `Authorization` lấy động token từ bước trước: `Bearer {{$node["Get Token1"].json["access_token"]}}`.

- **Node `Only New Rows` (Filter) & `Keep Score` (Set):**
  - Node Filter giúp lọc các dòng dữ liệu chưa được xử lý (ví dụ: cột `Complete` chưa đánh dấu `Yes`).
  - Node Set trích xuất chính xác đường dẫn JSON trả về từ D&B để lấy điểm số Paydex:
    ```text
    {{$json.organization.businessTrading[0].summary[0].paydexScoreHistory[0].paydexScore}}
    ```

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài dòng dữ liệu mẫu để kiểm tra kết quả trả về trong Google Sheets.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động hoạt động theo lịch trình hoặc sự kiện kích hoạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** để gửi báo cáo tóm tắt về các doanh nghiệp vừa được làm giàu dữ liệu mỗi ngày.
- **Lưu trữ báo cáo PDF:** Sử dụng thêm HTTP Request gọi D&B Report kết hợp với node **Google Drive** để lưu tự động hồ sơ pháp lý/tài chính của doanh nghiệp dưới dạng PDF phục vụ công tác kiểm toán.
- **Xử lý lỗi (Error Handling):** Bổ sung nhánh Error Trigger để ghi log vào Slack khi API D&B gặp sự cố hoặc mã DUNS không tồn tại.

### 📌 Kết luận
Workflow tích hợp Dun & Bradstreet và Google Sheets này là trợ thủ đắc lực giúp tự động hóa toàn bộ quy trình thẩm định đối tác và nghiên cứu thị trường. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp!