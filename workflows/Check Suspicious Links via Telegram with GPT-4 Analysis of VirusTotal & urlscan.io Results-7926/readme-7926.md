---
title: "🚨 Kiểm Tra Liên Kết Ảnh Hưởng qua Telegram với Phân Tích GPT-4 & VirusTotal/urlscan.io - Tự Động Hóa An Toàn Mạng"
description: "Workflow tự động hóa 100% không code giúp các sếp nhanh chóng kiểm tra tính an toàn của liên kết nguy hiểm nhận được qua Telegram, Telegram Bot hoặc email, với kết quả phân tích chi tiết từ GPT-4, VirusTotal và urlscan.io - chỉ trong vài giây!"
slug: kiem-tra-lien-ket-anh-huong-qua-telegram
tags: [n8n, automation, no-code, secops, ai, url-scanner, telegram-bot, urlscan-io, virus-total, gpt-4]
keywords: [tự động hóa kiểm tra liên kết nguy hiểm, n8n workflow an toàn mạng, phân tích URL bằng GPT-4, urlscan.io và VirusTotal, Telegram Bot an toàn, tự động hóa SecOps]
---

# 🚨 **Kiểm Tra Liên Kết Ảnh Hưởng qua Telegram với Phân Tích AI & Công Cụ An Toàn Mạng**

### **🔍 Nỗi Đau Của Các Sếp: "Liên Kết Nào An Toàn? Tôi Không Có Thời Gian Để Kiểm Tra Mỗi Link!"**
Trong môi trường làm việc hiện đại, các sếp thường phải đối mặt với hàng trăm liên kết được gửi qua Telegram, email hoặc tin nhắn cá nhân hàng ngày. Kiểm tra thủ công từng liên kết không chỉ tốn thời gian mà còn dễ gây lỗi nhầm lẫn, đặc biệt khi phải phân biệt giữa liên kết an toàn và nguy hiểm. **Workflow này giải quyết vấn đề này bằng cách tự động hóa toàn bộ quy trình kiểm tra an toàn URL chỉ trong vài giây**, với kết quả phân tích chi tiết từ hai công cụ an toàn mạng hàng đầu (VirusTotal và urlscan.io) và tổng kết bởi trí tuệ nhân tạo GPT-4.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết Kiệm Thời Gian**: Không cần phải mở nhiều tab browser hoặc sử dụng công cụ kiểm tra thủ công.
- **Kết Quả Chỉnh Xác**: Phân tích từ hai nguồn dữ liệu độc lập (VirusTotal + urlscan.io) và tổng kết bởi GPT-4.
- **Tương Tác Đơn Giản**: Gửi liên kết qua Telegram Bot và nhận kết quả ngay lập tức.
- **Lưu Lịch Sử Kiểm Tra**: Tất cả kết quả được ghi lại trên Google Sheets để tra cứu sau này.
- **Hoạt Động 24/7**: Workflow hoạt động liên tục, không phụ thuộc vào giờ làm việc của bạn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow hoạt động, các sếp cần chuẩn bị các thông tin sau:
1. **Telegram Bot**:
   - Tạo một bot Telegram mới và lấy **API Token** từ [@BotFather](https://t.me/BotFather).
   - Cấu hình bot để nhận và gửi tin nhắn (cần quyền admin trong nhóm hoặc chat cá nhân).
2. **API Keys**:
   - **VirusTotal API Key**: [Đăng ký miễn phí](https://www.virustotal.com/) (có giới hạn 4 request/phút với tài khoản miễn phí).
   - **urlscan.io API Key**: [Đăng ký miễn phí](https://urlscan.io/) (có giới hạn 100 scan/tháng).
   - **OpenAI API Key**: [Đăng ký](https://platform.openai.com/) để sử dụng GPT-4 (giá cao, nên sử dụng tài khoản miễn phí nếu có thể).
3. **Google Sheets**:
   - Tạo một bảng Google Sheets và chia sẻ với n8n bằng OAuth 2.0.
   - Cấu hình **Sheet Name** và **Tab Name** trong node Google Sheets.
4. **n8n Self-Hosted**:
   - Workflow này yêu cầu n8n được cài đặt trên máy chủ riêng (Self-hosted) để hoạt động 24/7. **Không thể chạy trên n8n Cloud** do giới hạn API và thời gian chạy dài.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/7926) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** (hoặc **Create New Workflow** và paste JSON).
- **Lưu workflow** với tên **"Malicious URL Scanner via Telegram"**.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflows này bao gồm **11 node** quan trọng, mỗi node cần cấu hình kỹ lưỡng. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu Hình Credentials**
1. **Telegram Trigger & Send Message**:
   - Đi đến **Credentials** trong n8n và thêm:
     - **Telegram API**: Điền **API Token** từ BotFather.
     - **Chat ID**: Lấy từ bot `@getidsbot` (gửi tin nhắn `/start` để bot trả về Chat ID).
   - **Lưu ý**: Node **Telegram Trigger** cần được cấu hình để chỉ kích hoạt khi nhận tin nhắn chứa **liên kết (URL)**. Thêm **filter** trong node này:
     ```json
     "jsonPath": "$[*]?.text?.includes('http')"
     ```

2. **VirusTotal HTTP Request**:
   - Đi đến **Credentials** và thêm:
     - **virusTotalApi**: Điền **API Key** từ VirusTotal.
   - **Request URL**: `https://www.virustotal.com/api/v3/urls/{url}`
   - **Headers**:
     ```json
     {
       "x-apikey": "{{ $credentials.virusTotalApi }}"
     }
     ```
   - **Query Parameters**:
     ```json
     {
       "limit": 1
     }
     ```

3. **urlscan.io**:
   - Thêm **credentials** `urlScanIoApi` với **API Key** từ urlscan.io.
   - **Request URL**: `https://urlscan.io/api/v1/scan/`
   - **Body**:
     ```json
     {
       "url": "{{ $node["Telegram Trigger"].json["$.text"] }}"
     }
     ```

4. **OpenAI (GPT-4)**:
   - Thêm **credentials** `openAiApi` với **API Key** từ OpenAI.
   - **Model**: Chọn **gpt-4** (hoặc gpt-3.5-turbo nếu không đủ budget).
   - **Prompt Template** (node **Prepare Summary Data**):
     ```javascript
     // Node "Prepare Summary Data" (Code Node)
     const url = $input.all()[0].json["$.text"];
     const virusTotalResult = $input.all()[1].json;
     const urlscanResult = $input.all()[2].json;

     const summaryPrompt = `
     Analyze the following URL scan results from VirusTotal and urlscan.io.
     Provide a concise summary (max 3 sentences) of whether the URL is malicious or safe.
     Include key findings such as:
     - Any detected malware or phishing indicators.
     - Suspicious domains or subdomains.
     - Behavioral analysis from urlscan.io (e.g., connections to known malicious IPs).
     - Overall risk level (High/Medium/Low).

     VirusTotal Results:
     ${JSON.stringify(virusTotalResult, null, 2)}

     urlscan.io Results:
     ${JSON.stringify(urlscanResult, null, 2)}

     Summary:
     `;

     return {
       prompt: summaryPrompt,
       model: "gpt-4",
       temperature: 0.5,
     };
     ```

5. **Google Sheets (URL Logging)**:
   - Thêm **credentials** `googleSheetsOAuth2Api`.
   - **Spreadsheet ID**: Lấy từ liên kết Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
   - **Sheet Name**: Đặt tên sheet (ví dụ: `URL_Scans`).
   - **Tab Name**: Đặt tên tab (ví dụ: `Logs`).
   - **Data Format**:
     ```json
     {
       "url": "{{ $node["Telegram Trigger"].json["$.text"] }}",
       "virusTotalResult": "{{ $node["VirusTotal HTTP Request"].json }}",
       "urlscanResult": "{{ $node["urlscan Perform Scan"].json }}",
       "summary": "{{ $node["Malicious URL Summary Agent"].json }}",
       "timestamp": "{{ $node["Prepare Summary Data"].json["$.timestamp"] }}"
     }
     ```

##### **B. Cấu Hình Node Quá Trình**
1. **Merge Node**:
   - Kết hợp kết quả từ **VirusTotal** và **urlscan.io** trước khi gửi cho AI.
   - **Merge Strategy**: Chọn **"Array"** và chọn các trường cần ghép (ví dụ: `virusTotalResult`, `urlscanResult`).

2. **Limit Node**:
   - Đảm bảo chỉ **1 tin nhắn tổng kết** được gửi cho mỗi URL.
   - **Limit**: Đặt số lượng là **1**.

3. **AI Agent (Malicious URL Summary Agent)**:
   - Node này sử dụng **LangChain Agent** kết hợp với **Memory Buffer Window** để phân tích kết quả.
   - **Prompt**: Được định nghĩa trong node **Prepare Summary Data** (xem trên).

4. **Telegram Send Message**:
   - **Message Format**: Sử dụng **template** để gửi kết quả tổng kết:
     ```json
     {
       "text": `🔍 **URL Scan Results for: {{ $node["Telegram Trigger"].json["$.text"] }}**

       **VirusTotal**: {{ $node["VirusTotal HTTP Request"].json["$.attributes"]?.malicious ?? "No data" }}
       **urlscan.io**: {{ $node["urlscan Perform Scan"].json["$.status"] }}

       **Summary**:
       {{ $node["Malicious URL Summary Agent"].json["$.summary"] }}

       📊 **Full Log**: [Google Sheets Link]`
     }
     ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một URL mẫu qua Telegram Bot (ví dụ: `https://example.com`).
   - Kiểm tra **n8n Dashboard** để xác nhận workflow chạy thành công.
   - Mở **Google Sheets** để xác nhận dữ liệu đã được ghi lại.

2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Tối Ưu Hóa Workflow**]
1. **Kết Nối với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để thông báo kết quả cho nhóm hoặc quản lý.
   - Ví dụ: Sử dụng node **n8n-nodes-base.slack** để gửi tin nhắn khi URL nguy hiểm được phát hiện.

2. **Lưu Log vào Database**:
   - Thay vì Google Sheets, các sếp có thể kết nối với **PostgreSQL** hoặc **MongoDB** để lưu trữ dữ liệu dài hạn.

3. **Cảnh Báo Thông Qua Email**:
   - Sử dụng node **n8n-nodes-base.email** để gửi báo cáo định kỳ (ví dụ: hàng tuần) về các URL nguy hiểm đã phát hiện.

4. **Phân Loại URL theo Độ Nguy Hiểm**:
   - Sử dụng **Conditional Node** để phân loại URL thành **High Risk**, **Medium Risk**, **Low Risk** và gửi tin nhắn khác nhau cho từng loại.

5. **Tích Hợp với Microsoft Teams**:
   - Thay vì Telegram, các sếp có thể sử dụng **Microsoft Teams** để nhận kết quả phân tích.
   - Sử dụng node **n8n-nodes-base.microsoftTeams**.

6. **Sử Dụng Tài Khoản Miễn Phí**:
   - Nếu không muốn trả tiền cho OpenAI, các sếp có thể thử **GPT-3.5-turbo** (rẻ hơn) hoặc **Mistral AI** (nếu có API key).
   - Thay đổi model trong node **OpenAI Model**:
     ```json
     {
       "model": "gpt-3.5-turbo"
     }
     ```

---

### 📌 **Kết Luận: Tự Động Hóa An Toàn Mạng - Không Cần Code!**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc kiểm tra an toàn URL mà không cần viết một dòng code nào. Với sự kết hợp giữa **Telegram Bot**, **AI GPT-4**, và **hai công cụ an toàn mạng hàng đầu**, bạn có thể:
✅ **Nhanh chóng phát hiện URL nguy hiểm** trong vài giây.
✅ **Tiết kiệm thời gian** so với việc kiểm tra thủ công.
✅ **Lưu trữ lịch sử** để tra cứu sau này.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-Hosted** trên VPS (đăng ký [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test với URL mẫu** và bắt đầu sử dụng!

**Chú ý**: Workflow này không thay thế được giải pháp an toàn mạng chuyên nghiệp, nhưng nó giúp các sếp **cảnh giác hơn** trước các liên kết nguy hiểm. **Luôn tuân thủ các quy tắc an toàn mạng** khi sử dụng công cụ này!

---
:::note[**Lưu Ý Cuối Cùng**]
- **VirusTotal** và **urlscan.io** có giới hạn request miễn phí. Nếu workflow bị chặn, hãy nâng cấp tài khoản.
- **OpenAI** có chi phí cao với GPT-4. Các sếp có thể thử **GPT-3.5-turbo** hoặc **Mistral AI** để tiết kiệm.
- **Telegram Bot** chỉ hoạt động trong chat cá nhân hoặc nhóm có quyền admin.
:::