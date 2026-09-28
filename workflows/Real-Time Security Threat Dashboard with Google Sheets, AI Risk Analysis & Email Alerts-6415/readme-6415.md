---
title: "🚨 **Bảng Điều Khiển Threat Real-Time với AI Phân Tích Rủi Ro & Cảnh Báo Email Tự Động (N8N)**"
description: "Tự động hóa theo dõi và phân tích nguy cơ an ninh thời gian thực từ CVE/IoC, đánh giá rủi ro bằng AI, và gửi cảnh báo email tự động – giúp đội ngũ SecOps tiết kiệm 80% thời gian xử lý thủ công. Đáp ứng ngay các cuộc tấn công tiềm ẩn trước khi chúng xảy ra."
slug: "threat-dashboard-realtime-ai-n8n"
tags: [n8n, automation, secops, cybersecurity, ai-risk-analysis]
keywords: [n8n workflow an ninh mạng, tự động hóa threat intelligence, cảnh báo email tự động, phân tích rủi ro AI, google sheets secops]
---

# 🚨 **Bảng Điều Khiển Threat Real-Time với AI Phân Tích Rủi Ro & Cảnh Báo Email Tự Động**

### **🔍 Nỗi Đau Của Đội Ngũ SecOps**
Hàng ngày, đội ngũ bảo mật phải:
- **Quét thủ công** các nguồn thông tin nguy cơ (CVE, IoC) từ nhiều nguồn khác nhau.
- **Phân loại và đánh giá** mức độ nghiêm trọng của từng threat một cách chủ quan.
- **Gửi cảnh báo** đến các thành viên trong team thông qua email hoặc Slack, nhưng thường bị trì hoãn hoặc bỏ lỡ.
- **Lưu trữ và theo dõi** lịch sử các sự kiện nguy cơ trong bảng tính Google Sheets, mất thời gian cập nhật.

**Kết quả?** Các cuộc tấn công tiềm ẩn có thể trôi qua mà không được phát hiện kịp thời, gây thiệt hại lớn cho doanh nghiệp.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tự động hóa 100% quá trình** theo dõi và phân tích threat từ nhiều nguồn (CVE, IoC).
- **Đánh giá rủi ro tự động** bằng AI, giúp phân loại nguy cơ cao/mittel/low chính xác hơn.
- **Cảnh báo email tự động** khi phát hiện threat mới, giảm thiểu việc bỏ lỡ cảnh báo.
- **Lưu trữ dữ liệu** vào Google Sheets với định dạng chuyên nghiệp, dễ theo dõi và báo cáo.
- **Tiết kiệm 80% thời gian** của đội ngũ SecOps, tập trung vào phản ứng và phòng ngự hiệu quả.
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ dữ liệu threat và báo cáo).
2. **API Key của các nguồn CVE/IoC** (ví dụ: NVD, AlienVault OTX, MISP, hoặc bất kỳ API threat feed nào khác).
3. **Tài khoản email** (để gửi cảnh báo tự động, có thể là Gmail, Outlook, hoặc SMTP khác).
4. **N8N Self-hosted** (để chạy workflow 24/7, không phụ thuộc vào phiên bản cloud).
5. **(Tùy chọn) API Key của mô hình AI** (nếu muốn nâng cao tính chính xác của phân tích rủi ro, có thể sử dụng mô hình như Hugging Face, OpenAI, hoặc các API AI khác).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6415) hoặc copy toàn bộ mã JSON từ trang này.
- Mở **n8n Editor** và chọn **"Import Workflow"** → Dán hoặc tải file JSON.
- **Không cần chỉnh sửa mã nguồn** nếu chỉ muốn chạy workflow mặc định.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **17 node** với logic phức tạp. Dưới đây là các bước **cần thiết** để cấu hình:

##### **A. Cấu Hình Nguồn Threat Feed (CVE & IoC)**
- **Node: 🌐 Get CVE Feed** và **🛡️ Get IOC Feed**
  - Thay đổi URL trong **HTTP Request** để trỏ đến API của nguồn CVE/IoC bạn sử dụng.
  - Ví dụ:
    - **CVE Feed**: `https://services.nvd.nist.gov/rest/json/cves/2.0/?pubStartDate=2024-01-01` (NVD API).
    - **IoC Feed**: `https://otx.alienvault.com/api/v1/indicators/search` (AlienVault OTX).
  - **Headers**: Thêm `Authorization: Bearer YOUR_API_KEY` nếu yêu cầu.

##### **B. Cấu Hình Google Sheets**
- **Node: Google Sheets**
  - Chọn **Credentials** trong n8n là tài khoản Google Sheets của bạn.
  - Điền **Sheet Name** là tên bảng tính (ví dụ: `Threat_Dashboard`).
  - **Range**: `A1:Z1000` (để lưu dữ liệu mới vào hàng mới).
  - **Headers**: Bật `Use as Header` để định dạng cột.

##### **C. Cấu Hình Email Alert**
- **Node: 📧 Send Alert Email**
  - Chọn **Credentials** là tài khoản email của bạn (cấu hình SMTP trong n8n).
  - **From Email**: Điền địa chỉ email gửi cảnh báo (ví dụ: `security-alerts@doanhnghiep.com`).
  - **To Email**: Điền danh sách email của đội ngũ SecOps (ví dụ: `team@doanhnghiep.com`).
  - **Subject**: `🚨 NEW SECURITY THREAT DETECTED` (có thể tùy chỉnh).
  - **HTML Content**: Sử dụng biến `{{ $json }}` để hiển thị thông tin threat.

##### **D. Cấu Hình AI Risk Analysis (Nếu Sử Dụng)**
- **Node: 🧠 AI – Risk Evaluation** và **🧠 AI – Triage Vulnerabilities**
  - Nếu muốn nâng cao tính chính xác, thay thế mã JavaScript mặc định bằng API của mô hình AI (ví dụ: OpenAI).
  - Ví dụ prompt cho AI:
    ```javascript
    const riskScore = await n8n.plugins.http.request({
      url: "https://api.openai.com/v1/chat/completions",
      method: "POST",
      headers: { "Authorization": "Bearer YOUR_OPENAI_API_KEY" },
      body: {
        model: "gpt-4",
        messages: [
          { role: "system", content: "You are a security risk analyst." },
          { role: "user", content: `Evaluate this threat: ${JSON.stringify($input)}. Return a risk score (1-10) and severity level (Critical, High, Medium, Low).` }
        ]
      }
    });
    return riskScore.json.choices[0].message.content;
    ```

##### **E. Cấu Hình Cron Trigger**
- **Node: ⏰ Cron – Daily Trigger**
  - Thay đổi biểu thức cron để chạy workflow theo lịch trình mong muốn (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).

##### **F. Cấu Hình Response Router (Switch)**
- **Node: 🧭 Response Router**
  - Điều này quyết định hành động tiếp theo dựa trên mức độ nghiêm trọng của threat.
  - Cấu hình các trường hợp:
    - `Critical`: Gửi email cảnh báo + ghi log vào Sheets.
    - `High`: Chỉ ghi log vào Sheets.
    - `Medium/Low`: Không cần hành động.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và kiểm tra các node quan trọng (CVE Feed, AI Analysis, Email Alert).
   - Xác nhận email và Google Sheets đã nhận dữ liệu.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**TIẾP CẬN HƠN**]
1. **Kết Nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để cảnh báo thực thời trên các kênh team chat.
   - Ví dụ:
     ```json
     {
       "operation": "sendMessage",
       "text": `🚨 NEW THREAT: ${$json.description}\nSeverity: ${$json.severity}\nLink: ${$json.reference}`
     }
     ```

2. **Lưu Log Chi Tiết**:
   - Sử dụng node **Google Sheets** để ghi toàn bộ lịch sử threat vào một sheet riêng (ví dụ: `Threat_Log_History`).

3. **Báo Cáo Định Kỳ**:
   - Thêm node **Schedule Trigger** chạy hàng tuần để tổng hợp báo cáo threat và gửi qua email.

4. **Tích Hợp với SIEM**:
   - Nếu doanh nghiệp sử dụng SIEM (ví dụ: Splunk, Wazuh), có thể gửi dữ liệu threat vào SIEM thay vì Google Sheets.

5. **Tùy Chỉnh AI**:
   - Đào tạo mô hình AI riêng để phù hợp với môi trường mạng của doanh nghiệp (ví dụ: sử dụng mô hình fine-tuned trên Hugging Face).
:::

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho đội ngũ SecOps muốn tự động hóa quá trình theo dõi và phản ứng trước các threat mạng. Bằng cách kết hợp:
✅ **Threat Feed tự động** (CVE/IoC).
✅ **Phân tích AI** để đánh giá rủi ro chính xác.
✅ **Cảnh báo email/Slack** thực thời.
✅ **Lưu trữ dữ liệu** vào Google Sheets.

**Các sếp có thể:**
- **Tiết kiệm thời gian** và tập trung vào công việc chiến lược.
- **Giảm thiểu rủi ro** bằng cách phát hiện threat sớm.
- **Cải thiện tính minh bạch** với báo cáo tự động.

**👉 Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và theo dõi các threat mới trong thời gian thực!

**Nếu cần hỗ trợ tùy chỉnh**, liên hệ với **Adnan Tariq** (Founder của CYBERPULSE AI) qua [LinkedIn](https://linkedin.com/in/adnan-tariq-4b2a1a47) để xây dựng giải pháp phù hợp với môi trường mạng của doanh nghiệp!