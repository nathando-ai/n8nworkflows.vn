---
title: "🚀 Tự động quét và tìm kiếm Email từ Website với n8n, Google Sheets & EmailListVerify"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất email từ danh sách website hoặc sử dụng EmailListVerify API để dự đoán email doanh nghiệp cực nhanh."
slug: "tu-dong-quet-va-tim-kiem-email-tu-website-n8n"
tags: [n8n, automation, lead-generation, google-sheets, email-verification, api]
keywords: [n8n workflow, trích xuất email website, email list verify, lead generation tự động, google sheets n8n]
---

# 🚀 Tự động quét và tìm kiếm Email từ Website với n8n, Google Sheets & EmailListVerify

Việc tìm kiếm thông tin liên hệ (lead generation) thủ công từ hàng trăm website là một ác mộng tốn cực nhiều thời gian của đội ngũ sales và marketing. Các sếp thường phải mất hàng giờ lướt web, vào mục "Liên hệ" (Contact Us) để copy từng chiếc email. 

Giải pháp ư? Workflow n8n này sẽ tự động hóa 100% quy trình: cào dữ liệu (scrape) từ website để tìm email có sẵn, và nếu không tìm thấy, hệ thống sẽ thông minh gọi qua **EmailListVerify API** để dự đoán các email dạng chung (generic email như `contact@`, `info@`) cực kỳ hiệu quả cho việc tiếp cận các doanh nghiệp vừa và nhỏ (SMB).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhập danh sách website vào Google Sheets, workflow tự lo phần còn lại.
- **Giải pháp kép thông minh:** Vừa quét trực tiếp mã nguồn website, vừa có phương án dự phòng (fallback) dùng API chuyên nghiệp khi website không public email.
- **Đồng bộ hóa tức thì:** Kết quả bao gồm email tìm được, website và độ tin cậy được cập nhật thẳng vào Google Sheets.
- **Tối ưu hóa chiến dịch Sales:** Giúp đội ngũ tiếp cận nhanh chóng với các chủ doanh nghiệp nhỏ, nơi các email chung (`contact@`) thường xuyên được chủ doanh nghiệp trực tiếp theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản Google để kết nối với n8n qua OAuth2.
- **EmailListVerify Account:** Tài khoản tại [EmailListVerify](https://emaillistverify.com/) để lấy API Key (có chương trình dùng thử miễn phí).
- **Google Sheets Template:** Bản sao của [Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1VOTFM8UeWHhJbtBM7SRca6vsVJlRUXzX71kjJ8n2jUY/edit?gid=1538095319#gid=1538095319) (cần có các cột: `email`, `website`, và `confidence`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Sao chép đoạn mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File/Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình chính xác các node sau:
- **Node `Get input Data` (Google Sheets):** 
  - Chọn Credentials loại `googleSheetsOAuth2Api`.
  - Trỏ tới file Google Sheet mẫu mà các sếp vừa sao chép, chọn đúng Sheet chứa danh sách URL website đầu vào.
- **Node `Use EmailListVerify API to find generic emails` (HTTP Request):**
  - Cấu hình API Key lấy từ tài khoản EmailListVerify của các sếp vào phần Header hoặc Query Authentication tùy theo tài liệu API của họ.
- **Node `Add result to google` (Google Sheets):**
  - Cấu hình `operation` là `appendOrUpdate` để ghi đè hoặc thêm mới kết quả trả về (`email`, `website`, `confidence`) vào bảng tính Google Sheets một cách ngăn nắp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute workflow** thủ công với một vài dòng dữ liệu mẫu trong Google Sheets để kiểm tra luồng dữ liệu chạy qua các node `Add http to url if missing`, `Get the website data`, `Email found?`,...
- Sau khi test thành công và dữ liệu đổ về Google Sheets chuẩn chỉnh, hãy bật nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay lập tức mỗi khi hệ thống quét và tìm được một lead chất lượng mới.
- **Lọc domain rác:** Thêm một node `If` hoặc `Code` trung gian để loại bỏ các website lỗi, website chết (404) trước khi gọi API để tiết kiệm credit của EmailListVerify.
- **Chia mẻ (Batching):** Nếu danh sách website của các sếp có tới hàng nghìn dòng, hãy sử dụng node `SplitInBatches` để cào dữ liệu theo từng đợt, tránh việc quá tải timeout.

### 📌 Kết luận
Workflow tích hợp n8n, Google Sheets và EmailListVerify chính là vũ khí bí mật giúp tự động hóa khâu tìm kiếm khách hàng tiềm năng mà không tốn nhiều nhân lực. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất cho đội ngũ Sales của các sếp!