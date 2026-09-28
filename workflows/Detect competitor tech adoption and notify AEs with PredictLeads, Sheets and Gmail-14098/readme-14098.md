---
title: "🚀 Tự động phát hiện đối thủ cạnh tranh áp dụng công nghệ mới và cảnh báo Sales với PredictLeads, Google Sheets và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động quét danh sách khách hàng tiềm năng qua PredictLeads API, phát hiện khi họ sử dụng công nghệ của đối thủ và gửi email cảnh báo tức thì cho Account Executive (AE)."
slug: "tu-dong-phat-hien-doi-thu-canh-tranh-cong-nghe-predictleads-gmail"
tags: [n8n, automation, no-code, sales-automation, predictleads, market-research]
keywords: [n8n workflow, tự động hóa sales, predictleads api, google sheets n8n, gmail automation, market research automation]
---

# 🚀 Tự động phát hiện đối thủ cạnh tranh áp dụng công nghệ mới và cảnh báo Sales

Trong thị trường cạnh tranh khốc liệt, thời gian chính là tiền bạc. Việc biết được khi nào một khách hàng tiềm năng bắt đầu sử dụng giải pháp của đối thủ (ví dụ: họ vừa cài đặt Salesforce, HubSpot hay một CRM khác) sẽ giúp đội ngũ Sales của các sếp nhảy vào "đánh phủ đầu" trước khi khách hàng kịp ký hợp đồng dài hạn.

Tuy nhiên, việc kiểm tra thủ công website của hàng trăm công ty mỗi ngày là điều bất khả thi. Đó là lý do workflow n8n này ra đời — tự động hóa 100% quy trình theo dõi công nghệ của đối thủ qua **PredictLeads API**, đối chiếu danh sách và bắn email cảnh báo trực tiếp cho Account Executive (AE) phụ trách thông qua **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt sóng kịp thời:** Đội ngũ Sales nhận được thông báo ngay lập tức khi khách hàng tiềm năng cài đặt công nghệ của đối thủ để có phương án tiếp cận.
- **Tự động hóa hoàn toàn:** Chạy ngầm mỗi ngày nhờ lịch trình tự động (Daily Schedule), loại bỏ hoàn toàn việc tra cứu thủ công.
- **Cá nhân hóa người nhận:** Tự động định vị đúng Account Executive (AE) phụ trách từng tài khoản để gửi email thông báo chính xác.
- **Tối ưu tỷ lệ chuyển đổi:** Tiếp cận đúng thời điểm khách hàng có nhu cầu hoặc đang dịch chuyển hạ tầng công nghệ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** Tạo sẵn 1 file Google Sheet chứa danh sách domain công ty cần theo dõi và email của AE phụ trách tương ứng.
- **PredictLeads Account & API Key:** Tài khoản PredictLeads để truy vấn dữ liệu công nghệ (https://predictleads.com).
- **Google Account (Gmail):** Kết nối OAuth2 với n8n để workflow có quyền gửi email thay mặt các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, sau đó vào giao diện n8n Editor, chọn **Import from JSON** và dán vào là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes chính, các sếp cần cấu hình kỹ các điểm sau để chạy mượt mà:

- **⏰ Daily Schedule Trigger:** 
  - Mặc định chạy định kỳ hàng ngày. Các sếp có thể cấu hình lại khung giờ chạy phù hợp với múi giờ và nhu cầu của đội ngũ.
- **📂 Read Company Watchlist (Google Sheets):** 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Chọn đúng File ID và Sheet Name chứa danh sách domain công ty và email AE.
- **🔄 Loop Over Companies & 🔍 Fetch Tech Detections (HTTP Request):** 
  - Node HTTP Request sẽ gọi tới PredictLeads API (`https://predictleads.com`). 
  - Các sếp cần cấu hình Header chứa API Key của PredictLeads và truyền biến `domain` lấy từ Google Sheets vào endpoint API.
- **⚙️ Check Competitor Tech & ❓ Competitor Tech Found? (Code & IF):** 
  - Node Code chứa logic JavaScript để so sánh danh sách công nghệ mà PredictLeads quét được với danh sách công nghệ đối thủ mà các sếp đang muốn "canh chừng" (ví dụ: Salesforce).
  - Node IF sẽ lọc ra các bản ghi khớp (True) để tiến hành gửi cảnh báo.
- **⚙️ Extract AE Email & 📧 Gmail Alert to AE (Gmail):** 
  - Kết nối tài khoản Gmail qua `gmailOAuth2`.
  - Node Code giúp bóc tách đúng email của AE từ hàng đợi, sau đó node Gmail sẽ soạn sẵn nội dung (Tên công ty, domain, công nghệ phát hiện, ngày giờ) và gửi đi tự động.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với dữ liệu mẫu (Test run) để kiểm tra xem API trả về và email có gửi đi thành công không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Thay vì chỉ gửi Gmail, các sếp có thể nối thêm node **Slack** hoặc **Telegram** để bắn tin nhắn alert thẳng vào group chat chung của sales team.
- **Lưu lịch sử vào CRM:** Thêm node cập nhật trạng thái vào Google Sheets hoặc HubSpot CRM để đánh dấu công ty nào đã được Sales tiếp cận, tránh spam.
- **Mở rộng danh sách đối thủ:** Chỉnh sửa đoạn code check công nghệ để theo dõi đồng thời nhiều đối thủ khác nhau (Ví dụ: HubSpot, Salesforce, Marketo...).

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một "trợ lý tình báo thị trường" cực kỳ sắc bén, giúp đội ngũ sales luôn đi trước một bước so với đối thủ. Cài đặt ngay hôm nay và tối ưu hóa quy trình sales automation của doanh nghiệp thôi nào!