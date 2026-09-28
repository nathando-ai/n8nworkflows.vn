---
title: "🚀 Tự Động Hóa & Tăng Cường Lead với GPT-4 + Dữ Liệu LinkedIn: Chuyển Dữ Liêu Thô Sang Khách Hàng Chất Lượng"
description: "Workflow tự động hóa hoàn toàn không cần code để bắt lead từ form, phân loại và enrich dữ liệu LinkedIn, sử dụng AI GPT-4 để đánh giá lead (0-100 điểm), phân loại Hot/Warm/Cold, và tự động gửi email cá nhân hóa qua Gmail, đồng thời ghi log vào Google Sheets và báo cáo trên Slack. Giúp doanh nghiệp tiết kiệm 90% thời gian theo dõi lead thủ công."
slug: "tieu-dong-hoa-lead-gpt4-linkedin"
tags: [n8n, automation, lead-generation, ai-summarization, gpt-4, linkedin-data, hubspot, slack, google-sheets]
keywords: [n8n workflow lead generation, tự động hóa lead với GPT-4, enrich lead bằng LinkedIn, phân loại lead Hot/Warm/Cold, tự động hóa bán hàng không code]
---

# 🚀 **Tự Động Hóa & Tăng Cường Lead với GPT-4 + Dữ Liệu LinkedIn**

## **💡 Bạn vẫn phải theo dõi lead thủ công hay phụ thuộc vào nhân viên để trả lời mỗi cuộc gọi?**
Hãy tưởng tượng một hệ thống **tự động hóa 100% không cần code**, giúp bạn:
✅ **Bắt lead** từ form trực tuyến
✅ **Phân tích và enrich** dữ liệu từ LinkedIn (thông tin công ty, vị trí, ngành nghề)
✅ **Đánh giá lead** bằng GPT-4 (điểm 0-100) và phân loại **Hot/Warm/Cold**
✅ **Tự động gửi email cá nhân hóa** qua Gmail
✅ **Ghi log vào Google Sheets** và báo cáo trên Slack
✅ **Tạo contact trên HubSpot** với thông tin chi tiết
✅ **Tiết kiệm 90% thời gian** theo dõi lead thủ công

Workflow này **giúp doanh nghiệp tự động hóa quy trình bán hàng**, giảm thiểu công việc lặp lại và tăng hiệu quả chuyển đổi lead thành khách hàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa việc theo dõi và phân loại lead, giảm thiểu công việc thủ công.
- **Chính xác cao**: AI GPT-4 đánh giá lead với độ chính xác cao (điểm 0-100) và phân loại tự động.
- **Cá nhân hóa tối đa**: Email và thông báo Slack được tự động sinh ra dựa trên dữ liệu lead.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào nhân viên.
- **Tích hợp đa nền tảng**: Kết nối với **Slack, HubSpot, Gmail, Google Sheets** để quản lý lead toàn diện.
- **Giảm chi phí**: Tiết kiệm ngân sách marketing bằng cách tập trung vào lead có tiềm năng cao.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:

| **Dịch vụ**       | **Thông tin cần thiết**                                                                 | **Lưu ý**                                                                 |
|-------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **OpenAI (GPT-4)** | API Key từ [OpenAI](https://platform.openai.com/account/api-keys)                          | Cần chọn mô hình **gpt-4o** hoặc **gpt-4** cho kết quả tốt nhất.          |
| **Apify**         | API Key từ [Apify](https://apify.com/platform/credentials) (để enrich LinkedIn)          | Cần tạo **HTTP Query Auth** với `token` là API Key của bạn.               |
| **Slack**         | OAuth2 Credential từ [Slack API](https://api.slack.com/apps)                              | Chọn quyền `chat:write`, `files:write` để gửi thông báo.                |
| **HubSpot**       | App Token từ [HubSpot Developer](https://developers.hubspot.com/docs/api/private-apps)   | Cần quyền `contacts:read`, `contacts:create`.                           |
| **Gmail**         | OAuth2 Credential từ [Google Cloud Console](https://console.cloud.google.com/)           | Chọn quyền `Gmail API` và `Google Drive API`.                             |
| **Google Sheets** | OAuth2 Credential từ [Google Cloud Console](https://console.cloud.google.com/)           | Chọn quyền `Google Sheets API`.                                          |
| **Google Search** | Không cần API Key (sử dụng API Google miễn phí)                                         | Cần kích hoạt **Google Search JSON API** trong Google Cloud Console.     |
| **LinkedIn**      | Không cần API Key (sử dụng Apify để scrape)                                              | Apify sẽ tự động lấy dữ liệu từ LinkedIn thông qua các actor đã cấu hình. |

---
---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấn **Create Workflow** → **Import Workflow**.
3. Chọn file JSON hoặc paste JSON từ [link gốc](https://n8n.io/workflows/11493).
4. Nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **🔹 Node "Extract LinkedIn URL" (Code)**
- **Mục đích**: Trích xuất URL LinkedIn từ email hoặc thông tin công ty.
- **Lưu ý**:
  - Nếu lead không có LinkedIn, workflow sẽ **bỏ qua bước enrich** nhưng vẫn tiến hành AI qualification.
  - Cần kiểm tra logic trong node **Code** để đảm bảo trích xuất đúng định dạng.

##### **🔹 Node "AI Lead Qualification" (OpenAI)**
- **Mục đích**: AI đánh giá lead với điểm từ 0-100 và phân loại **Hot/Warm/Cold**.
- **Cấu hình**:
  - Chọn **OpenAI API Key** trong credentials.
  - **Prompt**: Cần chỉnh sửa để phù hợp với tiêu chí đánh giá của doanh nghiệp (ví dụ: ưu tiên lead từ ngành nào, có nhu cầu cụ thể gì).
  - **Mô hình**: Chọn **gpt-4o** hoặc **gpt-4** cho kết quả chính xác nhất.

##### **🔹 Node "Google Search (Find LinkedIn URL)" (HTTP Request)**
- **Mục đích**: Tìm kiếm LinkedIn URL của công ty từ tên công ty trong lead.
- **Lưu ý**:
  - Cần kích hoạt **Google Search JSON API** trong [Google Cloud Console](https://console.cloud.google.com/).
  - Tham số `cx` (Custom Search Engine ID) cần được cấu hình trong **HTTP Request**.

##### **🔹 Node "LinkedIn Company Scraper" (HTTP Request)**
- **Mục đích**: Trích xuất dữ liệu công ty từ LinkedIn (sử dụng Apify).
- **Lưu ý**:
  - Cần tạo **HTTP Query Auth** trong Apify với `token` là API Key của bạn.
  - Apify sẽ sử dụng **Google Search Scraper PPR** và **LinkedIn Company Scraper PPR** để lấy dữ liệu.

##### **🔹 Node "Create HubSpot Contact" (HubSpot)**
- **Mục đích**: Tạo contact trên HubSpot với thông tin lead đã enrich.
- **Cấu hình**:
  - Chọn **HubSpot App Token** trong credentials.
  - Cần kiểm tra trường dữ liệu được gửi (ví dụ: `properties` trong payload).

##### **🔹 Node "Send Personalized Email" (Gmail)**
- **Mục đích**: Gửi email cá nhân hóa cho lead **Hot/Warm**.
- **Cấu hình**:
  - Chọn **Gmail OAuth2** trong credentials.
  - **Thân email**: Cần chỉnh sửa template email trong node **Code** trước khi gửi.

##### **🔹 Node "Log to Google Sheets" (Google Sheets)**
- **Mục đích**: Ghi log tất cả lead vào Google Sheets.
- **Cấu hình**:
  - Chọn **Google Sheets OAuth2** trong credentials.
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
  - **Operation**: Chọn **Append** để thêm dữ liệu mới vào cuối bảng.

##### **🔹 Node "Slack Hot Lead Alert" / "Slack Warm Lead Notification" (Slack)**
- **Mục đích**: Gửi thông báo Slack cho team khi có lead **Hot/Warm**.
- **Cấu hình**:
  - Chọn **Slack OAuth2** trong credentials.
  - **Channel**: Chọn channel Slack cần gửi thông báo.
  - **Message Format**: Cần chỉnh sửa template thông báo để hiển thị thông tin lead chi tiết.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và nhập thông tin lead mẫu (ví dụ: email `lead@example.com`, tên công ty `ABC Corp`).
   - Kiểm tra kết quả ở các node quan trọng như **AI Qualification**, **HubSpot**, **Gmail**, **Slack**.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH TIẾP CẬN THÊM]
1. **Kết nối với CRM khác**:
   - Thay thế HubSpot bằng **Salesforce** hoặc **Zoho CRM** bằng cách thêm node tương ứng.

2. **Lưu log chi tiết hơn**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi log tất cả hoạt động (ví dụ: thời gian gửi email, phản hồi của lead).

3. **Báo cáo định kỳ**:
   - Sử dụng **n8n + Google Sheets** để tự động tạo báo cáo hàng tuần về số lượng lead Hot/Warm/Cold.

4. **Tích hợp với Zoom/Calendly**:
   - Thêm node **Zoom API** hoặc **Calendly** để tự động tạo cuộc họp với lead Hot.

5. **Chỉnh sửa AI Prompt**:
   - Tùy chỉnh **prompt** trong node **OpenAI** để phù hợp với ngành nghề của doanh nghiệp (ví dụ: ưu tiên lead từ ngành tech, finance...).

6. **Báo lỗi tự động**:
   - Thêm node **Email Notification** để thông báo khi workflow gặp lỗi (ví dụ: không tìm thấy LinkedIn URL).

7. **Tích hợp với Telegram**:
   - Thay thế Slack bằng **Telegram Bot** để gửi thông báo lead.

---

### 📌 **Kết luận**
Workflow **"Tự Động Hóa & Tăng Cường Lead với GPT-4 + Dữ Liệu LinkedIn"** là giải pháp **tự động hóa hoàn toàn không cần code**, giúp doanh nghiệp:
✔ **Tiết kiệm thời gian** theo dõi lead thủ công.
✔ **Tăng hiệu quả chuyển đổi** bằng cách tự động phân loại và enrich lead.
✔ **Cá nhân hóa tương tác** với lead qua email và Slack.
✔ **Quản lý lead toàn diện** trên HubSpot và Google Sheets.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình các credentials.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động chính xác.
3. **Bật Active** và bắt đầu tự động hóa quy trình bán hàng của bạn!

---
**🚀 Cần hỗ trợ thêm?**
- **n8n Discord**: [https://discord.gg/n8n](https://discord.gg/n8n)
- **Agentical AI** (tác giả workflow): [https://agenticalai.com](https://agenticalai.com)