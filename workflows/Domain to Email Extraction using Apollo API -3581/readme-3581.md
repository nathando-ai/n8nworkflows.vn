---
title: "🚀 Tự động trích xuất Email và thông tin Leads từ Domain bằng Apollo API"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tìm kiếm email, thông tin nhân sự từ danh sách domain doanh nghiệp thông qua Apollo API và Google Sheets."
slug: "tu-dong-trich-xuat-email-tu-domain-apollo-api"
tags: [n8n, automation, sales, apollo-api, google-sheets, lead-generation]
keywords: [n8n workflow, apollo api, trích xuất email, lead generation tự động, tìm kiếm khách hàng b2b]
keywords: [n8n workflow, apollo api, trích xuất email, lead generation tự động, tìm kiếm khách hàng b2b]
---

# 🚀 Tự động trích xuất Email và thông tin Leads từ Domain bằng Apollo API

Trong các chiến dịch Sales và Cold Email B2B, việc tốn hàng giờ đồng hồ để truy cập từng website doanh nghiệp, tìm kiếm thông tin nhân sự (CEO, Marketing Manager, Sales Director...) rồi mò mẫm tìm email là một nỗi đau cực kỳ lớn. Công việc thủ công này vừa nhàm chán, tốn nhân lực lại mang lại hiệu quả cực kỳ thấp.

Được phát triển bởi **Hueston**, workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp quét toàn bộ danh sách domain, gọi Apollo API để bóc tách thông tin nhân sự, lấy email và tự động lưu thẳng kết quả vào Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần đưa danh sách domain vào Google Sheets, phần việc còn lại để n8n và Apollo lo.
- **Tiết kiệm 90% thời gian:** Thay vì tra cứu thủ công từng người, hệ thống quét hàng loạt dữ liệu trong chớp mắt.
- **Dữ liệu chuẩn xác, sạch sẽ:** Các node xử lý code giúp làm sạch, chuẩn hóa kết quả trước khi đẩy về kho lưu trữ.
- **Mở rộng quy mô dễ dàng:** Hoạt động bền bỉ, không lo giới hạn thao tác tay của con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Apollo.io:** Cần có API Key để gọi dữ liệu từ nền tảng Apollo.
- **Google Sheets:** 
  - 1 Sheet chứa danh sách domain đầu vào (Node `Pull Target Domains`).
  - 1 Sheet lưu kết quả trả về (Node `Results To Results Sheet`).
- **Credentials:** Kết nối Google Sheets OAuth2 và API Key của Apollo trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n, sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào giao diện làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Pull Target Domains (Google Sheets):** 
  - Chọn tài khoản Google Sheets Credentials.
  - Trỏ đúng đến file Google Sheets chứa danh sách domain cần quét khách hàng.
- **Loop Targets & Loop Over Results (Split in Batches):** 
  - Các node này giúp chia nhỏ dữ liệu thành từng batch để tránh vượt quá giới hạn gọi API (Rate limit) từ phía Apollo. Các sếp có thể giữ nguyên kích thước batch theo mặc định hoặc tinh chỉnh tùy theo gói API của mình.
- **Get People By Domain & Get Person Info (HTTP Request):** 
  - Cấu hình phương thức gọi API chính xác tới endpoint của Apollo.io.
  - Thêm Apollo API Key vào phần Header xác thực (Authentication/Headers).
- **Clean Up Results & Clean Up (Code):** 
  - Các node JavaScript/Python này thực hiện nhiệm vụ lọc bỏ các trường dữ liệu rác, chỉ giữ lại thông tin quan trọng như Tên, Chức vụ, Email, Công ty, LinkedIn...
- **Results To Results Sheet (Google Sheets):** 
  - Trỏ đến file Google Sheets lưu kết quả đầu ra.
  - Đảm bảo mapping đúng các cột dữ liệu đã được làm sạch từ node trước vào đúng các cột trong Sheet.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với 1-2 domain mẫu đầu tiên, kiểm tra xem dữ liệu có đổ về Google Sheets chuẩn chỉnh hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động hóa vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để gửi thông báo về máy mỗi khi quét xong một danh sách domain hoặc khi có lead VIP xuất hiện.
- **Gửi Email tự động:** Kết nối tiếp kết quả từ Google Sheets sang các công cụ gửi email như Gmail, Resend hoặc Hubspot để triển khai chiến dịch Cold Email ngay lập tức.
- **Lưu trữ nâng cao:** Thay vì Google Sheets, các sếp có thể đổi thành Airtable, Notion hoặc PostgreSQL để quản lý cơ sở dữ liệu leads quy mô lớn hơn.

### 📌 Kết luận
Workflow "Domain to Email Extraction using Apollo API" là một thứ vũ khí hạng nặng giúp các đội ngũ Sales, Marketing tối ưu hóa quy trình tìm kiếm khách hàng tiềm năng B2B. Hãy cài đặt ngay lên hệ thống n8n của các sếp để giải phóng sức lao động và bứt phá doanh số ngay hôm nay!