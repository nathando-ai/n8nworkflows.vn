---
title: "🚀 Tự Động Hóa Tìm Việc Online: Scrap Job + AI Lọc + Email Thông Báo (N8N + SerpAPI + Gemini)"
description: "Workflow tự động hóa tìm kiếm và lọc tin tuyển dụng từ nhiều nguồn, sử dụng AI Gemini để đánh giá phù hợp, sau đó gửi email thông báo ngay cho các sếp. Giúp tiết kiệm 10+ giờ/tuần và tránh bỏ lỡ cơ hội việc làm chất lượng."
slug: "tieu-dong-hoa-tim-viec-online-serpapi-gemini-email"
tags: [n8n, automation, no-code, ai-summarization, serpapi, google-gemini, email-notification]
keywords: [tự động hóa tìm việc, scrap job online, n8n workflow, gemini ai lọc cv, email thông báo việc làm, tự động hóa tuyển dụng]
---

# 🚀 **Tự Động Hóa Tìm Việc Online: Scrap Job + AI Lọc + Email Thông Báo (N8N + SerpAPI + Gemini)**

### **🔍 Nỗi Đau Của Các Sếp Khi Tìm Việc Online**
Hàng ngày, các sếp phải:
- **Quét thủ công** trên LinkedIn, Indeed, VietnamWorks, hay các trang tuyển dụng khác để tìm kiếm tin tuyển dụng phù hợp.
- **Lọc thủ công** hàng trăm tin tuyển dụng, mất thời gian để đánh giá xem có phù hợp với yêu cầu kỹ năng, mức lương, hoặc vị trí mong muốn.
- **Bỏ lỡ cơ hội** vì không được thông báo kịp thời khi có tin tuyển dụng mới xuất hiện.
- **Phải nhớ ghi chép** các tin tuyển dụng phù hợp vào Google Sheets hoặc Excel, dẫn đến rủi ro mất mát dữ liệu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động scrap** tin tuyển dụng từ nhiều nguồn (LinkedIn, Indeed, VietnamWorks,...) mỗi ngày.
✅ **Sử dụng AI Gemini** để đánh giá và lọc tin tuyển dụng phù hợp với tiêu chí của các sếp (lương, kỹ năng, vị trí, địa điểm,...).
✅ **Gửi email tự động** các tin tuyển dụng phù hợp đến email cá nhân hoặc nhóm.
✅ **Lưu trữ dữ liệu** vào Google Sheets để theo dõi và quản lý lâu dài.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** so với cách làm thủ công.
- **Không bỏ lỡ bất kỳ tin tuyển dụng nào** phù hợp với tiêu chí của mình.
- **AI Gemini tự động lọc** tin tuyển dụng chất lượng, giảm thiểu sự mệt mỏi trong quá trình tìm kiếm.
- **Dữ liệu được lưu trữ sẵn** trên Google Sheets, dễ dàng theo dõi và chia sẻ với đồng nghiệp.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản SerpAPI** (để scrap tin tuyển dụng):
   - Đăng ký tại [SerpAPI](https://serpapi.com/) và lấy **API Key**.
   - Miễn phí 10.000 request/tháng (đủ cho việc scrap cơ bản).
2. **Tài khoản Google Workspace** (để sử dụng Google Sheets và Gmail):
   - Tạo một **Google Sheet** để lưu trữ tin tuyển dụng (các sếp có thể tạo 3 sheet riêng biệt như trong workflow: `sheet1`, `sheet2`, `sheet3`).
   - Cấu hình **Gmail API** để gửi email tự động (cần **OAuth 2.0 Client ID**).
3. **Tài khoản Microsoft 365** (nếu sử dụng Outlook để gửi email):
   - Cần **API Key** hoặc **OAuth 2.0 Credentials** cho Microsoft Outlook.
4. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
5. **Tham số cấu hình cho workflow**:
   - **Keywords** (từ khóa tìm kiếm việc làm, ví dụ: "Fullstack Developer", "Data Analyst").
   - **Location** (địa điểm, ví dụ: "Hà Nội", "TP.HCM").
   - **Salary range** (mức lương mong muốn, ví dụ: "50M-100M").
   - **Sheet Name** (tên sheet trong Google Sheets để lưu tin tuyển dụng).
   - **Email recipients** (địa chỉ email nhận thông báo).
---

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/10363](https://n8n.io/workflows/10363).
- **Copy JSON** và dán vào **n8n Editor** (n8n.io) hoặc **n8n Self-hosted**.
- **Chọn "Import"** để thêm workflow vào dự án của mình.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **26 nodes** và cần cấu hình chi tiết như sau:

##### **A. Cấu Hình SerpAPI (Scrap Tin Tuyển Dụng)**
- **Nodes liên quan**: `HTTP Request5`, `HTTP Request6`, `HTTP Request7`, `HTTP Request8`, `HTTP Request9`.
- **Cách cấu hình**:
  1. Mở mỗi node `HTTP Request` và chọn **Method = GET**.
  2. Điền **URL** của SerpAPI theo mẫu:
     ```
     https://serpapi.com/search?q=keyword&location=location&engine=linkedin&api_key=YOUR_SERPAPI_KEY
     ```
     Ví dụ:
     ```
     https://serpapi.com/search?q=Fullstack+Developer&location=Hà+Nội&engine=linkedin&api_key=sk_your_api_key_here
     ```
  3. Thêm **Headers**:
     ```
     Accept: application/json
     ```
  4. **Thêm các từ khóa** (keywords) vào node `Edit Fields` trước khi scrap:
     - Ví dụ: `["Fullstack Developer", "Data Analyst", "DevOps Engineer"]`.

##### **B. Cấu Hình Google Sheets (Lưu Trữ Dữ Liệu)**
- **Nodes liên quan**: `Append or update row in sheet1`, `Get row(s) in sheet2`, `Get row(s) in sheet3`.
- **Cách cấu hình**:
  1. Tạo **3 sheet** trong Google Sheets với tên:
     - `sheet1` (lưu tin tuyển dụng mới).
     - `sheet2` (lưu tin tuyển dụng đã lọc).
     - `sheet3` (lưu tin tuyển dụng đã gửi email).
  2. Trong node `Append or update row in sheet1`:
     - Chọn **Credentials** (OAuth 2.0 Client ID).
     - Điền **Sheet Name = sheet1**.
     - Chọn **Range** = `A1` (hoặc tùy chỉnh).
  3. Trong node `Get row(s) in sheet2` và `Get row(s) in sheet3`:
     - Chọn **Credentials** tương ứng.
     - Điền **Sheet Name** và **Range** tương ứng.

##### **C. Cấu Hình AI Gemini (Lọc Tin Tuyển Dụng)**
- **Nodes liên quan**: `Google Gemini Chat Model`, `AI Agent`.
- **Cách cấu hình**:
  1. Đăng ký tài khoản **Google Cloud AI** và lấy **API Key** cho Gemini.
  2. Trong node `Google Gemini Chat Model`:
     - Chọn **Credentials** (API Key).
     - Điền **Prompt** để AI đánh giá tin tuyển dụng:
       ```
       "Analyze the following job posting and determine if it matches the following criteria:
       - Salary: 50M-100M
       - Location: Hà Nội
       - Skills: Fullstack Developer, Node.js, React, MongoDB
       Return YES/NO and a brief reason."
       ```
  3. Trong node `AI Agent`:
     - Chọn **Model** = `Google Gemini`.
     - Điền **Prompt** tương tự như trên.

##### **D. Cấu Hình Email Thông Báo (Outlook/Gmail)**
- **Nodes liên quan**: `Send a message1`, `Call sub workflow`.
- **Cách cấu hình**:
  1. **Nếu sử dụng Gmail**:
     - Cần cấu hình **OAuth 2.0 Client ID** trong Google Cloud Console.
     - Trong node `Send a message1`:
       - Chọn **Credentials** (OAuth 2.0).
       - Điền **To**, **Subject**, và **Body** của email.
  2. **Nếu sử dụng Outlook**:
     - Cần **API Key** hoặc **OAuth 2.0 Credentials** cho Microsoft 365.
     - Trong node `Send a message1`:
       - Chọn **Credentials** (Microsoft Outlook).
       - Điền **To**, **Subject**, và **Body** tương tự.

##### **E. Cấu Hình Schedule Trigger (Chạy Hàng Ngày)**
- **Node liên quan**: `Schedule Trigger`.
- **Cách cấu hình**:
  - Chọn **Cron Expression** = `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - Hoặc tùy chỉnh theo thời gian mong muốn.

##### **F. Cấu Hình Sub Workflow (Nếu Có)**
- **Node liên quan**: `Call sub workflow`.
- **Cách cấu hình**:
  - Tạo một **sub workflow** riêng để xử lý logic phức tạp (nếu cần).
  - Trong node `Call sub workflow`, chọn **Workflow Name** và **Credentials**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chạy workflow với **data mẫu** để kiểm tra tính năng.
  - Kiểm tra email nhận được và dữ liệu trong Google Sheets.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng ngày.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[MỘT SỐ Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `webhook` để gửi thông báo tin tuyển dụng mới vào Slack hoặc Telegram.
2. **Lưu Log Hoạt Động**:
   - Sử dụng node `stickyNote` để ghi lại lịch sử hoạt động của workflow.
3. **Báo Cáo Định Kỳ**:
   - Tạo một **sub workflow** để gửi báo cáo tuần/month về số lượng tin tuyển dụng đã lọc và gửi email.
4. **Tùy Chỉnh AI Gemini**:
   - Cập nhật **prompt** của AI để phù hợp với yêu cầu kỹ năng mới của các sếp.
5. **Dùng Multiple Keywords**:
   - Thêm nhiều từ khóa khác nhau để tăng cơ hội tìm thấy tin tuyển dụng phù hợp.
:::

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình tìm việc online, tiết kiệm thời gian và tránh bỏ lỡ cơ hội. Với **SerpAPI** để scrap tin tuyển dụng, **Gemini AI** để lọc tin phù hợp, và **email tự động**, các sếp có thể tập trung vào việc ứng tuyển và phát triển sự nghiệp mà không lo bỏ lỡ bất kỳ cơ hội nào.

**🚀 Hãy áp dụng ngay workflow này và bắt đầu tự động hóa tìm việc của mình!**
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn trong quá trình cấu hình, các sếp có thể tham khảo [YouTube của Louis](https://linktr.ee/cashflows.routine) hoặc liên hệ với tôi qua [AI Agency](https://agence-alain.fr).

---
**💡 Lưu ý cuối cùng**:
- **N8n Self-hosted** là lựa chọn tối ưu để workflow chạy 24/7 mà không bị giới hạn.
- **Monitoring** workflow thường xuyên để đảm bảo không có lỗi xảy ra.