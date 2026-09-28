---
title: "🚀 Tự Động Cào Profile LinkedIn Với Apify Và Đồng Bộ CRM Google Sheets Bằng n8n"
description: "Hướng dẫn xây dựng hệ thống tự động hóa khai thác thông tin profile LinkedIn qua Apify, xử lý dữ liệu và lưu trữ trực tiếp vào Google Sheets CRM với n8n."
slug: "tu-dong-cao-linkedin-apify-google-sheets-crm"
tags: [n8n, automation, lead-generation, apify, google-sheets, crm, linkedin]
keywords: [n8n workflow, cào linkedin tự động, apify linkedin scraper, đồng bộ google sheets, tự động hóa lead generation]
keywords: [n8n workflow, cào linkedin tự động, apify linkedin scraper, đồng bộ google sheets, tự động hóa lead generation]
---

# 🚀 Tự Động Cào Profile LinkedIn Với Apify Và Đồng Bộ CRM Google Sheets Bằng n8n

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) trên LinkedIn thủ công đang ngốn của đội ngũ sales hàng đống thời gian: từ việc copy URL từng profile, bóc tách thông tin công việc, kinh nghiệm, cho đến việc nhập liệu thủ công vào Google Sheets CRM. Quá trình này không chỉ chậm chạp, dễ sai sót mà còn làm lỡ nhịp cơ hội tiếp cận khách hàng nóng.

Được thiết kế bởi chuyên gia tự động hóa David Olusola, workflow n8n này sẽ thay thế toàn bộ quy trình thủ công đó. Hệ thống tự động nhận diện danh sách URL, kết hợp với Apify để cào dữ liệu chuyên sâu từ LinkedIn, xử lý và tự động cập nhật vào Google Sheets CRM một cách mượt mà, chính xác 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Tự động hóa hoàn toàn khâu thu thập dữ liệu profile LinkedIn mà không cần copy/paste thủ công.
- **Dữ liệu CRM luôn sạch và đồng bộ:** Thông tin chi tiết của lead (Họ tên, chức vụ, công ty, lịch sử làm việc...) được đẩy thẳng vào Google Sheets theo từng batch gọn gàng.
- **Linh hoạt kích hoạt:** Hỗ trợ nhiều nguồn trigger khác nhau như chạy lịch trình tự động (Schedule), kích hoạt thủ công (Manual) hoặc nhận dữ liệu qua Webhook từ bên thứ ba.
- **Hoạt động 24/7:** Vận hành trơn tru trên hạ tầng n8n tự chủ, sẵn sàng phục vụ đội ngũ sales bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Apify** kèm API Token (để sử dụng dịch vụ cào dữ liệu LinkedIn Actor).
- Tài khoản **Google Sheets** đã chuẩn bị sẵn một file trang tính làm CRM lưu danh sách URL và nhận thông tin lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy nội dung JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống cào và đẩy dữ liệu chạy mượt, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Check New Entries (`scheduleTrigger`):** Thiết lập lịch trình thời gian chạy (ví dụ: chạy mỗi giờ hoặc mỗi ngày một lần) nếu muốn hệ thống tự động quét định kỳ.
- **Webhook Input (`webhook`) & Respond Success (`respondToWebhook`):** Cấu hình nếu các sếp muốn nhận danh sách URL từ hệ thống bên ngoài (như CRM khác, Typeform, hoặc Landing Page).
- **Read LinkedIn URLs (`googleSheets`):** Kết nối tài khoản Google của bạn, trỏ đến file Google Sheets CRM và chọn đúng Sheet chứa danh sách URL LinkedIn cần cào.
- **Scrape LinkedIn Profile (`httpRequest`):** Điền API Endpoint của Apify Actor cào LinkedIn và đính kèm Apify API Token của các sếp vào phần Header để xác thực.
- **Add to Google Sheets CRM (`googleSheets`):** Cấu hình map dữ liệu đã qua xử lý từ node `Process Profile Data` (như Tên, Tiêu đề, Công ty, URL...) vào các cột tương ứng trong Google Sheets CRM.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với node `Manual Trigger` để test thử nghiệm với một vài URL mẫu.
- Kiểm tra lại dữ liệu trả về trong Google Sheets CRM xem đã khớp các cột chưa.
- Khi mọi thứ đã chuẩn chỉnh, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack vào nhánh hoàn thành để hệ thống bắn tin nhắn báo cáo mỗi khi cào xong một batch lead mới.
- **Lọc trùng tự động:** Thêm một bước Code hoặc If node để kiểm tra xem URL LinkedIn đã tồn tại trong Google Sheets CRM hay chưa trước khi gọi API Apify, giúp tiết kiệm chi phí gọi API.
- **Kết hợp AI Scoring:** Sau bước lấy dữ liệu profile, các sếp có thể chèn một node AI (OpenAI/Anthropic) để chấm điểm chất lượng khách hàng (Lead Scoring) dựa trên chức vụ và quy mô công ty trước khi lưu vào CRM.

### 📌 Kết luận
Tự động hóa quy trình thu thập lead từ LinkedIn bằng Apify và Google Sheets là bước đi chiến lược giúp đội ngũ sales tối ưu hóa năng suất, tập trung hoàn toàn vào việc chốt sale thay vì làm việc chân tay. Hãy cài đặt ngay workflow này để bứt phá doanh số trong quý này các sếp nhé!