---
title: "🚀 Tự động chấm điểm chân dung khách hàng LinkedIn (ICP Scoring) với Airtop & Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu profile LinkedIn, chấm điểm ICP bằng AI và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-cham-diem-icp-linkedin-airtop-google-sheets"
tags: [n8n, automation, no-code, linkedin, ai, airtop, google-sheets]
keywords: [n8n workflow, chấm điểm icp linkedin, airtop ai, tự động hóa google sheets, cào linkedin bằng ai]
---

# 🚀 Tự động chấm điểm chân dung khách hàng LinkedIn (ICP Scoring) với Airtop & Google Sheets

Việc phân loại và đánh giá khách hàng tiềm năng (Lead Scoring) trên LinkedIn thủ công đang ngốn quá nhiều thời gian của đội ngũ Sales và Marketing. Các sếp thường phải mất hàng giờ để mở từng profile, đọc kinh nghiệm làm việc, chức danh và tự phỏng đoán xem họ có khớp với chân dung khách hàng lý tưởng (ICP) hay không.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100%: Lấy dữ liệu từ Google Sheets, sử dụng AI (thông qua **Airtop**) để truy cập profile LinkedIn, trích xuất thông tin, chấm điểm ICP và tự động cập nhật kết quả ngược lại vào Google Sheets. Không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần duyệt tay từng profile LinkedIn hay copy/paste thủ công vào file Excel.
- **Đánh giá chuẩn xác:** AI phân tích sâu chức danh, công ty hiện tại và profile để chấm điểm ICP khách quan theo đúng tiêu chí doanh nghiệp đặt ra.
- **Đồng bộ thời gian thực:** Mọi thông tin trích xuất và điểm số được cập nhật tức thì vào Google Sheets để đội Sales chủ động tiếp cận.
- **Vận hành tự động:** Có thể mở rộng kết nối với trigger lịch trình (Schedule) để chạy tự động hàng ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets** (chứa sẵn danh sách các đường link profile LinkedIn cần chấm điểm).
- **Tài khoản Airtop AI** (để cấu hình node Airtop trích xuất dữ liệu web thông minh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này (ID gốc trên n8n: `3476`) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Get person` (Google Sheets):** 
  - Chọn tài khoản Google Sheets credentials.
  - Chỉ định đúng **Document** và **Sheet Name** chứa danh sách lead có kèm cột chứa link profile LinkedIn.
- **Node `Calculate ICP PersonScoring` (Airtop):** 
  - Cấu hình kết nối API của Airtop.
  - Kiểm tra lại phần `Prompt` để đảm bảo AI trích xuất đúng các trường thông tin cần thiết như *Full Name*, *Job Title*, *Employer* và đưa ra điểm số (Scoring) dựa trên tiêu chí ICP của công ty các sếp.
- **Node `Format response` (Code):** 
  - Node này dùng ngôn ngữ JavaScript cơ bản để chuẩn hóa dữ liệu đầu ra từ AI trước khi đẩy về Google Sheets. Các sếp chỉ cần giữ nguyên nếu cấu trúc dữ liệu không thay đổi.
- **Node `Update row` (Google Sheets):** 
  - Map lại các trường dữ liệu (Họ tên, Chức danh, Điểm ICP...) từ node trước vào đúng các cột tương ứng trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm với 1-2 dòng dữ liệu đầu tiên.
- Kiểm tra lại Google Sheets xem dữ liệu đã được cập nhật chính xác chưa.
- Chuyển công tắc sang **Active** để đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Webhook/Trigger mới:** Thay vì dùng nút `When clicking ‘Test workflow’`, các sếp có thể đổi thành **Webhook** hoặc **Google Sheets Trigger** để mỗi khi thêm một link LinkedIn mới vào bảng, hệ thống sẽ tự động chấm điểm ngay lập tức.
- **Tích hợp kênh thông báo:** Nối thêm node **Slack** hoặc **Telegram** để gửi thông báo về máy khi có một "High-value Lead" (khách hàng tiềm năng điểm ICP cao) xuất hiện.
- **Lưu log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để đề phòng trường hợp link LinkedIn bị lỗi hoặc tài khoản Airtop hết hạn mức.

### 📌 Kết luận
Việc tự động hóa quy trình đánh giá khách hàng tiềm năng trên LinkedIn chưa bao giờ dễ dàng đến thế với sự kết hợp của n8n và Airtop AI. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho đội ngũ sales và tối ưu hóa tỷ lệ chuyển đổi khách hàng!