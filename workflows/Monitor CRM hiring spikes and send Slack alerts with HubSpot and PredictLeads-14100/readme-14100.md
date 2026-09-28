---
title: "🚀 Tự động phát hiện biến động tuyển dụng từ CRM và cảnh báo qua Slack với HubSpot & PredictLeads"
description: "Workflow n8n giúp tự động theo dõi danh sách công ty trên HubSpot CRM, kiểm tra dữ liệu tuyển dụng qua PredictLeads, phát hiện đột biến nhân sự và gửi cảnh báo tức thì đến Slack."
slug: "tu-dong-theo-doi-tuyen-dung-hubspot-predictleads-slack"
tags: [n8n, automation, crm, hubspot, slack, lead-generation]
keywords: [n8n workflow, tự động hóa tuyển dụng, hubspot crm, predictleads api, slack alert, sales automation]
---

# 🚀 Tự động phát hiện biến động tuyển dụng từ CRM và cảnh báo qua Slack với HubSpot & PredictLeads

Trong kinh doanh B2B, việc nắm bắt thời điểm khách hàng mục tiêu đang mở rộng quy mô (tuyển dụng ồ ạt) là "chìa khóa vàng" để đội ngũ Sales tiếp cận đúng thời điểm có ngân sách. Tuy nhiên, việc thủ công kiểm tra hàng trăm công ty mỗi ngày là bất khả thi. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa 100% giúp quét danh sách công ty từ HubSpot, đối chiếu dữ liệu tuyển dụng từ PredictLeads, so sánh với lịch sử qua Google Sheets và bắn thông báo cảnh báo qua Slack ngay khi phát hiện tín hiệu tăng trưởng nóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt sóng khách hàng kịp thời:** Phát hiện ngay các công ty tăng trưởng tuyển dụng trên 50%, giúp sales tiếp cận đúng lúc họ có nhu cầu và ngân sách mới.
- **Tự động hóa hoàn toàn:** Không cần tốn nhân sự thủ công lướt LinkedIn hay kiểm tra website từng công ty mục tiêu.
- **Cập nhật dữ liệu thông minh:** Tự động đồng bộ trạng thái mới nhất về HubSpot CRM và lưu lịch sử tracking trên Google Sheets.
- **Cảnh báo tức thì:** Đội ngũ kinh doanh nhận thông báo chi tiết ngay trên kênh Slack chung để chủ động lên phương án outreach.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **HubSpot CRM:** Tài khoản có quyền truy cập API để lấy và cập nhật danh sách Công ty (Companies).
- **PredictLeads API:** Tài khoản và API Key từ [PredictLeads](https://predictleads.com) để lấy dữ liệu tin tuyển dụng.
- **Google Sheets:** File Google Sheet để lưu trữ và đối chiếu dữ liệu lịch sử tuyển dụng.
- **Slack Workspace:** Bot hoặc quyền kết nối để gửi tin nhắn cảnh báo (Slack App/OAuth).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc sao chép toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **⏰ Daily 9AM Trigger:** 
  - Mặc định lịch chạy là 9 giờ sáng mỗi ngày. Các sếp có thể thay đổi thời gian chạy tùy theo múi giờ và nhu cầu của đội ngũ kinh doanh.
- **🏢 HubSpot Get Companies & 🏢 HubSpot Update Company:** 
  - Chọn `hubspotOAuth2Api` credentials. 
  - Đảm bảo các trường dữ liệu (properties) như Domain, Company Name và các trường tùy chỉnh (custom properties nếu có để lưu tín hiệu tuyển dụng) được map chính xác.
- **🔍 Fetch Job Openings (HTTP Request):** 
  - Cấu hình endpoint API của PredictLeads đi kèm với API Key của các sếp để lấy dữ liệu việc làm dựa trên domain công ty.
- **📂 Read Historical Counts, 📝 Update Google Sheets & 📝 Update Sheets (No Spike):** 
  - Chọn `googleSheetsOAuth2Api` credentials.
  - Trỏ đúng đến file Google Sheet và Sheet Name dùng để lưu trữ số liệu lịch sử tuyển dụng của từng công ty.
- **⚙️ Filter Target Roles & 📊 Compare vs Historical (Code Nodes):** 
  - Node Code sẽ lọc các vị trí chiến lược (Sales, Engineering, Marketing, Product...) và tính toán tỷ lệ % biến động so với lịch sử. Đảm bảo ngưỡng so sánh (ví dụ: >50%) phù hợp với chiến lược của doanh nghiệp.
- **💬 Slack Spike Alert:** 
  - Chọn `slackOAuth2Api` credentials.
  - Chọn Channel nhận thông báo (ví dụ: `#sales-alerts` hoặc `#growth-signals`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu test của một vài công ty để kiểm tra luồng chạy từ HubSpot -> PredictLeads -> Google Sheets -> Slack.
- Sau khi test thành công không báo lỗi, gạt công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể kết hợp thêm node Telegram hoặc gửi email tự động cho account manager phụ trách khách hàng đó.
- **Tạo Task tự động trên CRM:** Thay vì chỉ báo Slack, có thể bổ sung node tạo Deal hoặc tạo Task trong HubSpot để Sales bắt buộc phải xử lý lead.
- **Tùy chỉnh ngưỡng cảnh báo:** Thay vì mức mặc định 50%, có thể tách các ngành nghề khác nhau với mức độ nhạy cảm về nhân sự khác nhau (Ví dụ: IT chỉ cần tăng 30% là báo, Sales cần tăng 70%).

### 📌 Kết luận
Workflow tích hợp HubSpot, PredictLeads và Slack này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ Growth và Sales B2B thời đại AI. Thay vì chờ khách hàng tìm đến hoặc mò mẫm thủ công, giờ đây hệ thống sẽ tự động "gõ cửa" báo cáo ngay khi khách hàng có dấu hiệu mở rộng. Hãy cài đặt ngay để tối ưu hóa phễu bán hàng của các sếp!