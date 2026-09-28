---
title: "🚀 Tự động hóa Chấm điểm Khách hàng Mục tiêu (ICP) trên LinkedIn với Airtop & Google Sheets"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động cào dữ liệu công ty từ LinkedIn, sử dụng Airtop AI để phân tích và chấm điểm ICP, sau đó cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-cham-diem-icp-linkedin-airtop-google-sheets"
tags: [n8n, automation, no-code, sales, ai, airtop, google-sheets]
keywords: [n8n workflow, linkedin icp scoring, airtop ai, google sheets automation, tu dong hoa sales, ai extraction]
---

# 🚀 Tự động hóa Chấm điểm Khách hàng Mục tiêu (ICP) trên LinkedIn với Airtop & Google Sheets

Việc nghiên cứu và chấm điểm từng công ty mục tiêu (ICP - Ideal Customer Profile) trên LinkedIn để chuẩn bị cho các chiến dịch Outbound Sales là một công việc cực kỳ tẻ nhạt, mất hàng giờ đồng hồ cho mỗi danh sách khách hàng. Thay vì để đội ngũ sales phải "cày cuốc" thủ công, các sếp hoàn toàn có thể tự động hóa 100% quy trình này bằng n8n kết hợp với sức mạnh AI của Airtop.

Workflow này sẽ tự động đọc danh sách công ty từ Google Sheets, sử dụng Airtop để truy cập trang LinkedIn, phân tích thông tin chi tiết và chấm điểm mức độ phù hợp với chân dung khách hàng lý tưởng (ICP), sau đó tự động ghi nhận kết quả trở lại Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh mở hàng chục tab LinkedIn, đọc mô tả công ty và đoán già đoán non điểm số ICP.
- **Chấm điểm khách quan, chuẩn xác:** AI (Airtop) sẽ đọc hiểu sâu sắc nội dung trang LinkedIn của doanh nghiệp để đưa ra phân tích chi tiết dựa trên tiêu chí của các sếp.
- **Đồng bộ hóa dữ liệu thời gian thực:** Kết quả phân tích, tóm tắt và điểm số tự động cập nhật gọn gàng vào Google Sheets để sales team chăm sóc ngay.
- **Vận hành trơn tru không cần code:** Dễ dàng tinh chỉnh prompt cho AI phù hợp với từng ngành hàng hoặc sản phẩm khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản Google và một file Sheets chứa danh sách các đường dẫn (URL) trang LinkedIn công ty cần chấm điểm.
- **Airtop AI Account:** Tài khoản và API Key của Airtop để thực hiện các thao tác trích xuất và phân tích trang web (Web Extraction).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc copy trực tiếp mã nguồn workflow, sau đó dán (Paste) vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Get companies (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Chọn đúng file Spreadsheet và Sheet chứa danh sách URL LinkedIn của các công ty cần chấm điểm.
- **Calculate ICP Scoring (`airtop`):**
  - Kết nối tài khoản sử dụng `airtopApi`.
  - Tại đây, cấu hình `operation` là `query` và `resource` là `extraction`. 
  - Các sếp cần tinh chỉnh lại đoạn `prompt` sao cho phù hợp nhất với tiêu chí ICP của công ty mình (ví dụ: quy mô nhân sự, lĩnh vực hoạt động, từ khóa sản phẩm...).
- **Format response (`code`):**
  - Node này dùng để xử lý dữ liệu trả về từ Airtop, chuyển đổi cấu trúc JSON của AI thành các trường dữ liệu rõ ràng để chuẩn bị ghi vào Google Sheets. Các sếp có thể kiểm tra đoạn code JS bên trong nếu muốn tùy biến thêm các trường dữ liệu.
- **Update row (`googleSheets`):**
  - Kết nối lại tài khoản Google Sheets.
  - Cấu hình `operation` là `update` để ghi đè hoặc bổ sung điểm số ICP, tóm tắt công ty vào đúng dòng tương ứng trong file Sheets ban đầu.

#### 3. Kích hoạt ⚡️
- Bấm vào nút **When clicking ‘Test workflow’** (`manualTrigger`) để chạy thử với một vài dòng dữ liệu mẫu xem kết quả trả về đã đúng ý chưa.
- Sau khi test thành công, bật công tắc **Active** để workflow sẵn sàng hoạt động tự động mỗi khi có danh sách mới hoặc theo lịch trình (nếu các sếp thay đổi trigger).

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình Sales Automation, các sếp có thể mở rộng workflow này bằng cách:
1. **Tích hợp kênh thông báo:** Thêm node Slack hoặc Telegram để bắn thông báo về channel riêng mỗi khi có một công ty đạt điểm ICP cao (ví dụ: > 80 điểm).
2. **Tự động gửi Email/LinkedIn Outreach:** Kết hợp thêm các bước gửi email cá nhân hóa tự động thông qua Gmail hoặc công cụ outreach nếu điểm ICP đạt yêu cầu.
3. **Lưu trữ Log & Báo cáo:** Định kỳ tổng hợp các leads tiềm năng vào một bảng tổng hợp để đội ngũ Sales dễ dàng theo dõi tiến độ.

### 📌 Kết luận
Workflow "LinkedIn Company ICP Scoring Automation with Airtop & Google Sheets" là trợ đắc lực giúp tối ưu hóa khâu nghiên cứu khách hàng, giúp đội ngũ sales tập trung 100% thời gian vào việc chốt deal thay vì tốn thời gian cào dữ liệu thủ công. Hãy áp dụng ngay vào hệ thống của các sếp để thấy sự khác biệt!