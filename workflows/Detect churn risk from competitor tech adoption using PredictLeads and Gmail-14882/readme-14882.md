---
title: "🚀 Tự động phát hiện nguy cơ khách hàng rời bỏ (Churn Risk) bằng PredictLeads và Gmail trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi công nghệ đối thủ mà khách hàng sử dụng qua PredictLeads, kết hợp Google Sheets và Gmail để cảnh báo CSM kịp thời."
slug: "tu-dong-phat-hien-nguy-co-churn-risk-predictleads-gmail"
tags: [n8n, automation, crm, ai-summarization, predictleads, gmail, google-sheets]
keywords: [n8n workflow, churn risk detection, predictleads n8n, tu dong hoa crm, canh bao khach hang roi bo]
---

# 🚀 Tự động phát hiện nguy cơ khách hàng rời bỏ (Churn Risk) bằng PredictLeads và Gmail

Các sếp có bao giờ rơi vào cảnh khách hàng lớn đột ngột hủy dịch vụ (Churn) mà đội ngũ Sales hay Customer Success Manager (CSM) không hề nhận được dấu hiệu cảnh báo trước? Thông thường, trước khi khách hàng "quay xe", họ thường âm thầm thử nghiệm hoặc tích hợp các công cụ của đối thủ vào hệ thống. 

Việc kiểm tra thủ công tech stack của từng khách hàng là bất khả thi nếu doanh nghiệp có hàng trăm, hàng ngàn tài khoản. Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, tự động quét công nghệ mà khách hàng đang sử dụng hàng tuần, phân tích đối thủ cạnh tranh và bắn cảnh báo trực tiếp qua Gmail/Slack khi có rủi ro xuất hiện!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động phòng ngừa (Proactive Churn Management):** Phát hiện sớm việc khách hàng cài cắm công nghệ đối thủ trước khi họ gửi yêu cầu hủy hợp đồng.
- **Tự động hóa 100%:** Lịch trình hàng tuần (`Weekly Workflow Trigger`) tự động quét dữ liệu từ Google Sheets mà không cần nhân sự can thiệp thủ công.
- **Phân loại rủi ro thông minh:** Kết hợp kiểm tra công nghệ đối thủ và thời hạn gia hạn hợp đồng (dưới 90 ngày) để khoanh vùng tài khoản rủi ro cao nhất.
- **Cảnh báo tức thì:** Tự động gửi email chi tiết cho CSM phụ trách qua Gmail hoặc thông báo cho team qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** File chứa danh sách khách hàng (cần các cột: `company_domain`, `renewal_date`, `csm_email`).
- **PredictLeads API:** Tài khoản PredictLeads để lấy API Key (`X-Api-Key` và `X-Api-Token`) phục vụ việc phân tích Tech Stack.
- **Gmail Credentials:** Tài khoản Gmail đã cấu hình OAuth2 để gửi email cảnh báo.
- **Slack Account (Tùy chọn):** Kết nối Slack OAuth2 nếu muốn nhận thông báo chung cho team.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [PredictLeads Churn Detection Workflow](https://n8n.io/workflows/14882)) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 14 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Fetch Customers from Google Sheet:** Kết nối tài khoản Google Drive/Sheets của sếp, chọn đúng file Google Sheet quản lý khách hàng và đảm bảo các tên cột khớp với yêu cầu (`company_domain`, `renewal_date`, `csm_email`).
- **Get Customer Tech Stack (PredictLeads):** Điền thông tin API Key và API Token từ PredictLeads vào phần Credentials của node này để hệ thống có quyền truy xuất dữ liệu công nghệ.
- **Detect Competitor Usage (Code Node):** Node này chứa đoạn code JavaScript dùng để quét tên các công nghệ. Các sếp có thể tùy chỉnh danh sách đối thủ cần theo dõi (ví dụ: HubSpot, Salesforce, Zoho CRM...) trực tiếp trong code cho phù hợp với sản phẩm của mình.
- **Calculate Renewal Risk (90 Days) (Code Node):** Node này tính toán khoảng thời gian từ ngày hiện tại đến ngày gia hạn (`renewal_date`). Mốc 90 ngày có thể được thay đổi trong code tùy thuộc vào chu kỳ sales của doanh nghiệp.
- **Send Churn Risk Alert Email to CSM (Gmail):** Chọn credential Gmail OAuth2, cấu hình người nhận động (`{{ $json.csm_email }}`) để hệ thống tự động gửi email cảnh báo đúng người phụ trách khi tài khoản có rủi ro cao (Vừa dùng công nghệ đối thủ, vừa sắp đến hạn gia hạn dưới 90 ngày).
- **Notify Team (No Competitor - Safe Account) (Slack):** (Tùy chọn) Kết nối Slack workspace để nhận báo cáo hoặc bỏ qua nếu không sử dụng Slack.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với một vài dữ liệu mẫu trên Google Sheets và kiểm tra kết quả trả về ở từng node.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy theo lịch hàng tuần.

### ✍️ Nâng cấp & Gợi ý mở rộng
- **Tích hợp AI Summarization:** Kết hợp thêm node AI (OpenAI/Anthropic) sau bước phát hiện đối thủ để tự động viết nội dung email cảnh báo mang tính cá nhân hóa cao hơn cho CSM.
- **Lưu log rủi ro:** Thêm một node Google Sheets hoặc Airtable phía sau nhánh rủi ro cao để lưu trữ lịch sử biến động tech stack của khách hàng, phục vụ cho việc phân tích dữ liệu dài hạn.
- **Mở rộng kênh thông báo:** Ngoài Gmail, có thể đẩy thông báo khẩn cấp qua Telegram Bot để team Sales/CSM phản ứng nhanh lập tức trên điện thoại.

### 📌 Kết luận
Việc giữ chân khách hàng (Retention) luôn tiết kiệm chi phí hơn rất nhiều so với việc đi tìm khách hàng mới. Với workflow n8n kết hợp PredictLeads và Gmail này, các sếp sẽ luôn đi trước một bước trong việc bảo vệ nguồn doanh thu định kỳ (Recurring Revenue) của doanh nghiệp. Hãy thiết lập ngay hôm nay để không bỏ lỡ bất kỳ tín hiệu cảnh báo nào từ khách hàng nhé!