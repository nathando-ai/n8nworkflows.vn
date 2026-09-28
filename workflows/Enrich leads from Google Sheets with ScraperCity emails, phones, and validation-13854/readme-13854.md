---
title: "🚀 Tự động làm giàu dữ liệu khách hàng tiềm năng từ Google Sheets với ScraperCity"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy email, số điện thoại và xác thực contact từ Google Sheets sử dụng ScraperCity API của chuyên gia Alex Berman."
slug: "tu-dong-lam-giau-leads-google-sheets-scrapercity-n8n"
tags: [n8n, automation, lead-generation, scrapercity, google-sheets, b2b]
keywords: [n8n workflow, enrich leads, scrapercity, alex berman, tự động hóa lead generation, google sheets n8n]
---

# 🚀 Tự động làm giàu dữ liệu khách hàng tiềm năng từ Google Sheets với ScraperCity

Trong quy trình B2B Sales, việc sở hữu danh sách khách hàng tiềm năng (leads) chất lượng với email chính xác và số điện thoại còn hoạt động là chìa khóa sống còn của chiến dịch Cold Email hay Telesales. Tuy nhiên, việc thủ công tra cứu từng dòng trên Google Sheets rồi tìm kiếm thông tin liên hệ là một "nỗi đau" tốn hàng tá thời gian mà hiệu quả lại thấp.

Được thiết kế bởi **Alex Berman** (Chuyên gia Serial Entrepreneur, tác giả cuốn *The Cold Email Manifesto*), workflow n8n này sẽ giải quyết triệt để bài toán trên. Hệ thống sẽ tự động quét, bổ sung email, số điện thoại và xác thực độ uy tín của contact trực tiếp từ Google Sheets bằng sức mạnh của ScraperCity API mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quên đi cảnh copy-paste thủ công từng dòng dữ liệu từ Google Sheets sang các công cụ tra cứu.
- **Dữ liệu siêu sạch (Enriched Leads):** Tự động bổ sung email công việc, số điện thoại cá nhân/công ty và trạng thái xác thực (validation) chính xác.
- **Tối ưu chi phí & thời gian:** Xử lý dữ liệu hàng loạt theo lô (batch processing), giúp vượt qua giới hạn API và tiết kiệm tối đa thời gian cho đội ngũ Sales.
- **Hoạt động không nghỉ:** Chạy tự động ngầm 24/7, sẵn sàng cung cấp nguồn lead chất lượng bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Google Sheets:** File chứa danh sách leads thô (ít nhất cần có tên công ty, tên người cần tìm hoặc website).
- **ScraperCity Account & API Key:** Dịch vụ web scraping và B2B lead generation của Alex Berman để lấy dữ liệu email/phone.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chủ n8n (Link gốc: [ScraperCity Leads Enrichment Workflow](https://n8n.io/workflows/13854)), sau đó chọn **Import from File** hoặc copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Google Sheets Node:** Kết nối tài khoản Google của các sếp, trỏ đúng đến file Google Sheets chứa danh sách leads và chọn chính xác Sheet Name cần đọc/ghi dữ liệu.
- **HTTP Request Node (ScraperCity API):** Cấu hình API Endpoint của ScraperCity và điền API Key cá nhân vào phần Header để xác thực. Đảm bảo ánh xạ (mapping) đúng các trường dữ liệu đầu vào từ Google Sheets như tên miền (domain), tên công ty, hoặc họ tên.
- **Code & Set Nodes:** Kiểm tra lại các biến trung gian để đảm bảo dữ liệu trả về từ API (email, phone, validation status) được format gọn gàng trước khi ghi ngược lại Google Sheets.
- **Split In Batches & Wait Nodes:** Rất quan trọng khi xử lý danh sách lớn (hàng ngàn leads). Cấu hình số lượng mỗi mẻ (batch size) và thời gian chờ (wait) phù hợp để tránh bị nghẽn API (Rate Limit).
- **If / Filter / RemoveDuplicates Nodes:** Tinh chỉnh các điều kiện lọc để loại bỏ các email không hợp lệ, email rác hoặc các dòng dữ liệu bị trùng lặp (duplicates) trước khi lưu trữ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu (1-2 dòng) để kiểm tra xem hệ thống đã lấy được email/phone và cập nhật ngược lại Google Sheets thành công chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay cho đội ngũ Sales mỗi khi một batch leads mới được làm giàu thành công.
- **Tự động đẩy vào CRM:** Thay vì chỉ ghi lại Google Sheets, các sếp có thể đẩy thẳng danh sách leads sạch này vào HubSpot, Close CRM hoặc ActiveCampaign để tiến hành chạy chiến dịch Cold Email lập tức.
- **Lưu Log lỗi:** Sử dụng nhánh Error Trigger để bắt các trường hợp API lỗi và ghi nhận lại vào một sheet riêng để dễ dàng kiểm tra.

### 📌 Kết luận
Workflow tự động làm giàu leads từ ScraperCity và Google Sheets chính là vũ khí bí mật giúp tối ưu hóa phễu bán hàng B2B, tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để tăng tốc độ tiếp cận khách hàng tiềm năng cho doanh nghiệp của các sếp!