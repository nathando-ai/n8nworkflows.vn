---
title: "🚀 Tự Động Hóa Xác Minh & Tích Hợp Lead Tiềm Năng từ Jotform sang HubSpot với Google Gemini (AI + CRM)"
description: "Giải pháp tự động hóa 100% không code giúp các sếp **xác minh email, tra cứu thông tin doanh nghiệp, tổng hợp AI và đồng bộ lead chất lượng cao** vào HubSpot, tiết kiệm 80% thời gian nghiên cứu thủ công. Kết quả: CRM được cập nhật liên tục với dữ liệu chính xác, giảm 90% lead giả, và tăng 30% tỷ lệ chuyển đổi."
slug: "tieu-dong-hoa-xac-minh-lead-jotform-hubspot-google-gemini"
tags: [n8n, automation, lead-generation, ai-chatbot, hubspot, google-gemini, jotform, crm]
keywords: [tự động hóa n8n, xác minh lead, google gemini n8n, jotform hubspot, ai lead scoring, tra cứu thông tin doanh nghiệp, giảm lead giả, CRM tự động]
---

# 🚀 **Tự Động Hóa Xác Minh & Tích Hợp Lead Tiềm Năng với AI Google Gemini (Jotform → HubSpot)**

### **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp đang mất **giờ đồng hồ hàng ngày** để:
- **Lọc lead giả**: Email không tồn tại, domain tạm thời (Gmail, Yahoo, @gmail.com.vn...) khiến công việc nghiên cứu trở nên vô nghĩa.
- **Tra cứu thủ công**: Phải mở website của lead, copy-paste thông tin vào Google, hoặc sử dụng các tool trả phí để tìm hiểu **ngành nghề, quốc gia, mô tả công ty**—quá chậm và không hiệu quả.
- **Nhập liệu vào HubSpot**: Dữ liệu không được đồng bộ kịp thời, dẫn đến **trùng lặp, thiếu thông tin**, và sales team phải làm việc với dữ liệu cũ.
- **Không có AI hỗ trợ**: Không có ai tổng hợp thông tin một cách **cá nhân hóa và nhanh chóng** để sales có thể **tư vấn chính xác** ngay từ lần gọi đầu tiên.

**Giải pháp này giải quyết tất cả!** Với **AI Google Gemini + n8n**, các sếp sẽ có một **công cụ tự động hóa hoàn chỉnh** để:
✅ **Xác minh email** (loại bỏ lead giả trong giây lát).
✅ **Tra cứu tự động** thông tin doanh nghiệp từ website (ngành nghề, quốc gia, mô tả).
✅ **Tổng hợp AI** một bản tóm tắt **cá nhân hóa** về lead để sales có thể **tư vấn hiệu quả**.
✅ **Đồng bộ tự động** vào HubSpot với **dữ liệu đầy đủ và chính xác**.
✅ **Gửi thông báo ngay** cho sales team với tất cả thông tin cần thiết.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng. N8n chạy ổn định nhất khi có **RAM 4GB+** và **CPU 2 nhân trở lên**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|------------------------------------------------------------------------------|
| **Tiết kiệm 80% thời gian** | Không cần tra cứu thủ công, xác minh email, hoặc nhập liệu vào HubSpot.    |
| **Giảm 90% lead giả**     | Email được xác minh trước khi đồng bộ vào CRM.                            |
| **Dữ liệu CRM đầy đủ**    | HubSpot được cập nhật với **ngành nghề, quốc gia, mô tả công ty** từ AI. |
| **Tóm tắt AI cá nhân hóa** | Sales nhận được **bản tóm tắt ngắn gọn** về lead để tư vấn hiệu quả.       |
| **Hoạt động liên tục**    | Workflow chạy **24/7** mà không cần can thiệp thủ công.                    |
| **Tăng tỷ lệ chuyển đổi** | Lead được **lọc và tổng hợp** trước khi sales tiếp cận, giảm thời gian nghiên cứu. |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị **dưới đây**:

#### **1. Tài Khoản & API Keys Cần Thiết**
| **Dịch Vụ**       | **Thông Tin Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|-------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Jotform**       | - API Key (tạo tại [Jotform Developer](https://developer.jotform.com/))               | Cần **chọn form** có các trường: **First Name, Last Name, Email, Phone, Website, Note**. |
| **Verifalia**     | - API Key (đăng ký tại [Verifalia](https://verifalia.com/))                          | Dùng để **xác minh email** trước khi đồng bộ.                           |
| **Google Gemini** | - API Key (tạo tại [Google Cloud AI](https://aistudio.google.com/))                   | Cần **bật API Gemini** và cấp quyền cho n8n.                           |
| **HubSpot**       | - OAuth2 Credential (tạo tại [HubSpot Developer](https://developers.hubspot.com/))     | Chọn **permission**: `contacts:crm.objects.contacts.readwrite`.          |
| **Gmail**         | - OAuth2 Credential (tạo tại [Google Cloud Console](https://console.cloud.google.com/)) | Chọn **scope**: `https://www.googleapis.com/auth/gmail.send`.              |

#### **2. Form Jotform Cần Thiết**
- **Trường bắt buộc**:
  - `First Name` (Họ)
  - `Last Name` (Tên)
  - `Email` (Email)
  - `Phone` (Số điện thoại)
  - `Website` (Link website của lead)
  - `Note` (Ghi chú tùy chọn, nếu có)

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [n8n.io/workflows/9732](https://n8n.io/workflows/9732) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.

**Bước 2:** Vào **n8n Dashboard** → **Create Workflow** → **Import from JSON**.

**Bước 3:** Chọn file JSON và nhấn **Import**.

---
#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **8 node** chính. Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: JotForm Trigger (n8n-nodes-base.jotFormTrigger)**
- **Cấu hình**:
  - **API Key**: Điền API Key từ Jotform.
  - **Form ID**: Chọn ID của form Jotform bạn đã tạo.
  - **Trigger**: Chọn **Form Submission** (khi lead gửi form).
  - **Webhook URL**: Điền URL của n8n (cần **bật CORS** nếu form ở domain khác).

##### **🔹 Node 2: Lead Verification (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.verifalia.com/v1/verify`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_VERIFALIA_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "email": "$json['email']",
      "format": "json"
    }
    ```
  - **Lưu ý**:
    - Nếu email **không hợp lệ**, workflow sẽ **dừng lại** (không đồng bộ vào HubSpot).
    - Nếu email **hợp lệ**, dữ liệu sẽ chuyển sang node tiếp theo.

##### **🔹 Node 3: Information Extractor (n8n-nodes-langchain.informationExtractor)**
- **Cấu hình**:
  - **Model**: Chọn **Google Gemini** (hoặc PaLM).
  - **Prompt**:
    ```plaintext
    Extract the following information from the website URL provided:
    - Company Name
    - Industry
    - Country
    - Website Summary (a brief description of the business)
    Format the output as JSON:
    {
      "company_name": "Example Corp",
      "industry": "Technology",
      "country": "Vietnam",
      "website_summary": "A leading SaaS company in Vietnam..."
    }
    ```
  - **Input**: Điền `$json['website']` (trường Website từ Jotform).

##### **🔹 Node 4: Google Gemini Chat Model (n8n-nodes-langchain.lmChatGoogleGemini)**
- **Cấu hình**:
  - **API Key**: Điền API Key Google Gemini.
  - **Prompt**:
    ```plaintext
    You are an AI sales assistant. Analyze the lead data below and provide a concise summary (max 3 sentences) for the sales team to use during their first call.
    Lead Data:
    - Name: $json['firstName'] $json['lastName']
    - Email: $json['email']
    - Phone: $json['phone']
    - Website: $json['website']
    - Company: $json['company_name'] (if available)
    - Industry: $json['industry'] (if available)
    - Country: $json['country'] (if available)
    - Website Summary: $json['website_summary'] (if available)
    ```
  - **Output**: Dữ liệu này sẽ được gửi vào **Gmail Notification** và **HubSpot**.

##### **🔹 Node 5: Create or Update a Contact (n8n-nodes-base.hubspot)**
- **Cấu hình**:
  - **Credentials**: Chọn OAuth2 HubSpot của bạn.
  - **Object Type**: `contacts`
  - **Properties**:
    | **Field**          | **Value**                          |
    |--------------------|------------------------------------|
    | `firstname`        | `$json['firstName']`               |
    | `lastname`         | `$json['lastName']`               |
    | `email`            | `$json['email']`                  |
    | `phone`            | `$json['phone']`                  |
    | `website`          | `$json['website']`                |
    | `company`          | `$json['company_name']` (nếu có)  |
    | `industry`         | `$json['industry']` (nếu có)      |
    | `country`          | `$json['country']` (nếu có)       |
    | `custom_properties`| `$json['website_summary']` (nếu có) |

##### **🔹 Node 6: Send a Message (n8n-nodes-base.gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn OAuth2 Gmail của bạn.
  - **To**: Email của bạn hoặc team sales (ví dụ: `sales@company.com`).
  - **Subject**: `📩 New Lead Verified & Enriched - $json['firstName'] $json['lastName']`
  - **Body (HTML)**:
    ```html
    <h2>Lead Verification Summary</h2>
    <p><strong>Name:</strong> $json['firstName'] $json['lastName']</p>
    <p><strong>Email:</strong> $json['email']</p>
    <p><strong>Phone:</strong> $json['phone']</p>
    <p><strong>Website:</strong> <a href="$json['website']">$json['website']</a></p>

    <h3>AI Analysis:</h3>
    <p>$json['ai_summary']</p>

    <h3>Company Details:</h3>
    <p><strong>Company:</strong> $json['company_name']</p>
    <p><strong>Industry:</strong> $json['industry']</p>
    <p><strong>Country:</strong> $json['country']</p>
    <p><strong>Summary:</strong> $json['website_summary']</p>
    ```
  - **Lưu ý**: `$json['ai_summary']` là kết quả từ **Google Gemini Chat Model**.

---

#### **3. Kích Hoạt ⚡️ Workflow**
**Bước 1: Test Run**
- Nhấn **Run Workflow** và chọn **một lead mẫu** từ Jotform để kiểm tra.
- Kiểm tra:
  - Email có được xác minh không?
  - AI có tra cứu được thông tin website không?
  - HubSpot có được cập nhật không?
  - Email thông báo có được gửi không?

**Bước 2: Bật Active**
- Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi lead gửi form.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Kết Nối với Slack/Telegram**
- Thêm **node Slack/Telegram Webhook** sau **Gmail Notification** để thông báo ngay khi lead mới được xác minh.
- **Cách làm**:
  - Tạo **Slack App** hoặc **Telegram Bot** và lấy **Webhook URL**.
  - Thêm node **HTTP Request** với method `POST` và URL của Slack/Telegram.
  - Body:
    ```json
    {
      "text": "🚀 New Lead Verified!\nName: $json['firstName'] $json['lastName']\nEmail: $json['email']\nAI Summary: $json['ai_summary']"
    }
    ```

#### **2. Lưu Log Tất Cả Lead**
- Thêm **node StickyNote** (n8n-nodes-base.stickyNote) để lưu **tất cả dữ liệu lead** vào một file JSON.
- **Cách làm**:
  - Thêm node **StickyNote** sau **HubSpot Update**.
  - Cấu hình:
    - **Key**: `leads_log`
    - **Value**: `$json` (tất cả dữ liệu lead).
  - Sau đó, **export log** định kỳ để phân tích.

#### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **node Schedule** (n8n-nodes-base.schedule) để gửi **báo cáo hàng tuần** về số lượng lead được xác minh và tỷ lệ chuyển đổi.
- **Cách làm**:
  - Thêm node **Schedule** với thời gian **09:00 hàng thứ 2**.
  - Sau đó, thêm node **HTTP Request** để gọi API của n8n và lấy dữ liệu từ **StickyNote**.
  - Cuối cùng, gửi **email