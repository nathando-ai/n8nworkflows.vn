---
title: "🛡️ Tự Động Hoàn Hảo: Scan Link Gmail Bằng VirusTotal & Gửi Cảnh Báo Tự Động Đến WhatsApp, Teams & Google Sheets"
description: "Workflow này tự động quét tất cả link trong email Gmail bằng VirusTotal, lọc ra các link nguy hiểm (đặc biệt là từ domain google.com), và gửi cảnh báo tức thời đến WhatsApp, Microsoft Teams, đồng thời ghi log chi tiết vào Google Sheets. Giúp các sếp bảo mật email 24/7 mà không cần code."
slug: "tieu-dong-scan-link-gmail-bang-virustotal"
tags: [n8n, automation, no-code, secops, virus-total, whatsapp, microsoft-teams, google-sheets]
keywords: [tự động hóa an ninh email, scan link nguy hiểm, virus total api, cảnh báo whatsapp teams, lưu log google sheets, bảo mật email doanh nghiệp]
---

# 🚀 **Tự Động Quét Link Gmail Bằng VirusTotal & Gửi Cảnh Báo Tự Động**

### **Nỗi Đau Của Các Sếp: Email Là Mặt Trận Đầu Tiên Của Cyber Attack**
Hàng ngày, các sếp phải mở hàng trăm email, trong đó có thể ẩn chứa **link độc hại** từ phishing, malware, hoặc spam. Thời gian và công sức để kiểm tra từng link thủ công là một **thiệt hại lớn**, đặc biệt khi:
- **Link từ domain google.com** (đặc biệt là liên kết chứa mã độc) có thể trốn qua bộ lọc spam.
- **Các cuộc tấn công zero-day** không được phát hiện kịp thời.
- **Không có hệ thống cảnh báo tự động**, các sếp phải phụ thuộc vào phản ứng chậm trễ của nhân viên IT.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Quét tự động** tất cả link trong email bằng **VirusTotal API** (một trong những công cụ quét an ninh uy tín nhất thế giới).
✅ **Lọc ra link nguy hiểm** (đặc biệt là từ domain `google.com` hoặc chứa mã độc).
✅ **Gửi cảnh báo tức thời** đến **WhatsApp, Microsoft Teams** (để các sếp phản ứng ngay).
✅ **Ghi log chi tiết** vào **Google Sheets** để theo dõi lịch sử và phân tích sau này.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra từng email thủ công, hệ thống làm việc tự động.
- **Bảo mật cao**: Phát hiện **tất cả link nguy hiểm**, kể cả từ domain `google.com` (thường bị bỏ qua).
- **Cảnh báo tức thời**: Nhận thông báo trên **WhatsApp/Teams** ngay khi có link độc hại.
- **Lưu trữ log chi tiết**: Dữ liệu phân tích được ghi vào **Google Sheets**, giúp theo dõi và báo cáo.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
- **Tích hợp đa nền tảng**: WhatsApp, Teams, và Google Sheets trong một hệ thống.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy email cần quét).
2. **API Key VirusTotal** (miễn phí hoặc premium).
   - Đăng ký tại: [https://www.virustotal.com/](https://www.virustotal.com/)
   - **Lưu ý**: Đăng ký tài khoản **premium** nếu muốn quét nhiều link hơn.
3. **Tài khoản WhatsApp Business API** (để gửi cảnh báo).
   - Sử dụng **Rapiwa** (n8n có node hỗ trợ).
   - Đăng ký tại: [https://rapiwa.com/](https://rapiwa.com/)
4. **Tài khoản Microsoft Teams** (để gửi thông báo).
5. **Google Sheets** (để lưu log phân tích).
6. **Credentials cho n8n**:
   - **Gmail**: Cấu hình OAuth 2.0.
   - **VirusTotal**: API Key.
   - **Rapiwa**: Phone Number và API Key.
   - **Microsoft Teams**: Webhook URL.
   - **Google Sheets**: Credentials để truy cập sheet.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/13581) (nếu có quyền).
- **Hoặc copy toàn bộ JSON** từ trang workflow và dán vào **n8n Editor** → **Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **12 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

##### **A. Node "Gmail Trigger" (n8n-nodes-base.gmailTrigger)**
- **Cấu hình**:
  - Chọn **event type**: `Inbox` (hoặc `Sent` nếu muốn quét email đã gửi).
  - **Labels**: Chọn `unread` (để quét email chưa đọc) hoặc bỏ trống để quét tất cả.
  - **Credentials**: Chọn tài khoản Gmail đã cấu hình OAuth 2.0.

##### **B. Node "Code (Extracts URLs from email content)" (n8n-nodes-base.code)**
- **Mã JavaScript mặc định**:
  ```javascript
  // Lấy tất cả link trong nội dung email
  const content = $input.all()[0].payload.data.content;
  const links = content.match(/https?:\/\/[^\s]+/g) || [];
  return { json: { links: links } };
  ```
- **Lưu ý**:
  - Nếu email có **đính kèm HTML**, cần sử dụng `content` thay vì `plainText`.
  - **Test run** với email mẫu để đảm bảo trích xuất đúng link.

##### **C. Node "If (Checks if URLs contain 'google.com')" (n8n-nodes-base.if)**
- **Cấu hình điều kiện**:
  - **Condition**: `$.json.links.includes('https://google.com')` (hoặc sử dụng regex để kiểm tra domain).
  - **Lưu ý**: Nếu muốn **lọc ra link nguy hiểm**, có thể thay đổi điều kiện thành:
    ```json
    $.json.links.some(link => link.includes('google.com') && !link.includes('docs.google.com') && !link.includes('drive.google.com'))
    ```

##### **D. Node "If (Checks if URLs are not empty)" (n8n-nodes-base.if)**
- **Cấu hình điều kiện**:
  - **Condition**: `$.json.links.length > 0` (đảm bảo có link để quét).

##### **E. Node "VirusTotal (Submits URLs for analysis)" (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://www.virustotal.com/api/v3/urls`
  - **Headers**:
    ```json
    {
      "x-apikey": "YOUR_VIRUSTOTAL_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "urls": [
        "LINK_FROM_EMAIL"
      ]
    }
    ```
  - **Lưu ý**:
    - **VirusTotal API** có giới hạn free tier (5 requests/minute).
    - Nếu muốn quét nhiều link, **upgrade tài khoản premium**.

##### **F. Node "Code (VirusTotal report to extract relevant information)" (n8n-nodes-base.code)**
- **Mã JavaScript mặc định**:
  ```javascript
  // Trích xuất thông tin từ VirusTotal
  const report = $input.all()[0].json.data.attributes;
  const isMalicious = report.last_analysis_stats.malicious > 0;
  const threatLevel = report.last_analysis_stats.suspicious > 0 ? "Suspicious" : "Clean";

  return {
    json: {
      isMalicious: isMalicious,
      threatLevel: threatLevel,
      url: report.url,
      description: report.description
    }
  };
  ```
- **Lưu ý**:
  - **Thay đổi logic** nếu muốn **lọc ra các link nguy hiểm** (ví dụ: `malicious > 0`).

##### **G. Node "Rapiwa (WhatsApp notification)" (n8n-nodes-rapiwa.rapiwa)**
- **Cấu hình**:
  - **Phone Number**: Số điện thoại WhatsApp của các sếp.
  - **Message Template**:
    ```json
    {
      "text": "🚨 ALERT: Link nguy hiểm phát hiện trong email!\n\nURL: {{ $node["Code (VirusTotal report to extract relevant information)"].json.url }}\n\nTrạng thái: {{ $node["Code (VirusTotal report to extract relevant information)"].json.threatLevel }}\n\nChi tiết: {{ $node["Code (VirusTotal report to extract relevant information)"].json.description }}"
    }
    ```
  - **Lưu ý**:
    - **Test run** trước khi kích hoạt để đảm bảo tin nhắn gửi được.

##### **H. Node "Sends a Microsoft Teams notification" (n8n-nodes-base.microsoftTeams)**
- **Cấu hình**:
  - **Webhook URL**: URL từ Teams (cấu hình trong **Teams → Connectors → Incoming Webhook**).
  - **Message Template**:
    ```json
    {
      "text": "🚨 Cảnh báo link nguy hiểm từ email!\n\nURL: {{ $node["Code (VirusTotal report to extract relevant information)"].json.url }}\n\nTrạng thái: {{ $node["Code (VirusTotal report to extract relevant information)"].json.threatLevel }}"
    }
    ```
  - **Lưu ý**:
    - **Kiểm tra quyền** để đảm bảo webhook hoạt động.

##### **I. Node "Logs the analysis results to a Google Sheet" (n8n-nodes-base.googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google đã cấu hình.
  - **Sheet Name**: Tên sheet muốn ghi log (ví dụ: `VirusTotal_Logs`).
  - **Range**: `A1` (để ghi dữ liệu từ ô A1).
  - **Data**:
    ```json
    {
      "email": $input.all()[0].payload.data.email,
      "url": $node["Code (VirusTotal report to extract relevant information)"].json.url,
      "threatLevel": $node["Code (VirusTotal report to extract relevant information)"].json.threatLevel,
      "timestamp": new Date().toISOString()
    }
    ```
  - **Lưu ý**:
    - **Tạo sheet mới** nếu chưa có.
    - **Cấu trúc cột**: `Email | URL | Threat Level | Timestamp`.

#### **3. Kích Hoạt ⚡️**
- **Test run** với **email mẫu** (có link nguy hiểm) để kiểm tra workflow.
- **Bật Active workflow** khi đã cấu hình xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack**:
   - Thêm node **Slack** để gửi cảnh báo đến kênh #security-alerts.
   - **Cấu hình**:
     ```json
     {
       "text": "🚨 Link nguy hiểm phát hiện!\nURL: {{ $node["Code"].json.url }}"
     }
     ```

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.schedule** để gửi **báo cáo tuần/Tháng** về số lượng link nguy hiểm qua email.

3. **Lọc ra các domain nguy hiểm nhất**:
   - Thêm node **Code** để phân tích **tần suất xuất hiện** của các domain nguy hiểm và gửi cảnh báo ưu tiên.

4. **Tích hợp với SIEM (Security Information & Event Management)**:
   - Gửi dữ liệu log đến **Splunk, ELK, hoặc Graylog** để phân tích sâu hơn.

5. **Tự động xóa email có link nguy hiểm**:
   - Sử dụng **Gmail API** để **xóa email** sau khi phát hiện link độc hại.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **bảo mật email 24/7** mà không cần code. Bằng cách **quét tự động, cảnh báo tức thời, và lưu log chi tiết**, các sếp có thể:
✔ **Ngăn chặn tấn công phishing** trước khi nó xảy ra.
✔ **Tiết kiệm thời gian** và tập trung vào công việc chính.
✔ **Có hệ thống báo cáo** để phân tích và cải thiện an ninh.

**Hãy import workflow ngay hôm nay và bảo vệ email của doanh nghiệp!** 🚀

---
**🔗 [Tải workflow từ nguồn gốc](https://n8n.io/workflows/13581)**
**📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**