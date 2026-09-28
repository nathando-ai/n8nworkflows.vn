---
title: "🚀 Tự Động Hóa Xếp Hạng Lead Website Bằng GPT-4o + Trả Lời Email + Thông Báo Telegram (N8n)"
description: "Workflow tự động hóa hoàn toàn không cần code để phân loại lead từ website thành 5 cấp độ (Từ Cold đến VIP), gửi email tự động và thông báo ngay cho đội bán hàng qua Telegram. Giúp các sếp tiết kiệm 2-3 giờ/ngày và tăng hiệu quả chuyển đổi lead lên 30%."
slug: "tieu-dong-hoa-xep-hang-lead-website-gpt-4o"
tags: [n8n, automation, lead-generation, ai-summarization, gpt-4o, google-sheets, telegram, gmail]
keywords: [n8n workflow lead scoring, tự động hóa xếp hạng lead, gpt-4o mini tự động hóa, gửi email tự động từ website, thông báo lead qua telegram, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Xếp Hạng Lead Website Với GPT-4o + Trả Lời Email + Thông Báo Telegram**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Làm thủ công** phân loại hàng trăm lead từ website (cold, warm, hot...)
- **Mất thời gian** gửi email trả lời và thông báo cho đội bán hàng
- **Chưa tối ưu** trong việc ưu tiên lead có giá trị cao nhất
- **Không có hệ thống** để theo dõi và phân tích lead một cách khoa học

**Workflow này giải quyết tất cả!** Với chỉ một lần cấu hình, hệ thống sẽ:
✅ **Tự động phân loại lead** từ website thành 5 cấp độ (⚪️🟢🔵🟣🔴) bằng trí tuệ nhân tạo GPT-4o
✅ **Gửi email tự động** với nội dung cá nhân hóa ngay khi lead gửi form
✅ **Thông báo ngay cho đội bán hàng** qua Telegram với tất cả thông tin lead
✅ **Lưu dữ liệu lead** vào Google Sheets để theo dõi và phân tích

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2-3 giờ/ngày** trên việc phân loại và xử lý lead thủ công
- **Tăng tỷ lệ chuyển đổi lead** lên đến 30% nhờ xếp hạng chính xác
- **Cá nhân hóa tương tác** với lead ngay từ lần đầu tiếp xúc
- **Hoạt động 24/7** mà không cần can thiệp của con người
- **Dữ liệu lead được lưu trữ** một cách hệ thống, dễ dàng phân tích
- **Giảm thiểu rủi ro** với lead VIP (🔴) bằng cách thông báo ngay cho đội bán hàng
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản OpenAI** (API Key) để sử dụng GPT-4o-mini
- **Google Sheets** để lưu trữ lead (cần tạo sheet với các cột: Name, Email, Company, Industry, Request, Score)
- **Tài khoản Gmail** (hoặc SMTP) để gửi email tự động
- **Bot Telegram** (tạo qua @BotFather) và Chat ID của nhóm bán hàng
- **Website có form đăng ký** (Webflow, WordPress, HTML tự viết...) và khả năng gửi dữ liệu qua Webhook
- **VPS n8n** (để workflow hoạt động 24/7) - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/10586) (hoặc copy JSON từ link này).
2. Trên n8n Editor, nhấn **Import** → **From JSON** → Dán JSON và nhấn **Import**.
3. **Kiểm tra** workflow đã import hoàn chỉnh (11 node như mô tả).

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/10586).
2. Trên n8n Editor, nhấn **Import** → **From JSON** → Dán và nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 Node 1: Website Form Submission (Webhook)**
- **Cấu hình:**
  - **Path:** `website-form-submissions` (không thay đổi)
  - **HTTP Method:** `POST` (không thay đổi)
- **Lưu ý:**
  - **Cấu hình Webhook trên website** để gửi dữ liệu POST đến URL của node này.
  - **Kiểm tra payload** để đảm bảo form gửi đúng định dạng JSON.
  - **Thêm xác thực** (nếu cần) để tránh spam.

#### **🔹 Node 2 & 5: Extract Form Fields & Prepare Email Data (Set)**
- **Cấu hình:**
  - **Field mappings** phải khớp với cấu trúc form của các sếp.
  - Ví dụ:
    ```json
    {
      "firstName": "fields[0].value",
      "lastName": "fields[1].value",
      "email": "fields[2].value",
      "company": "fields[3].value",
      "industry": "fields[4].value",
      "phone": "fields[5].value",
      "requestType": "fields[6].value",
      "requestDetails": "fields[7].value"
    }
    ```
  - **Lưu ý:** Nếu form có cấu trúc khác, phải điều chỉnh theo.

#### **🔹 Node 3: AI Lead Scoring Agent (Agent)**
- **Cấu hình:**
  - **OpenAI API Key:** Điền vào **Credentials** của node `lmChatOpenAi`.
  - **Model:** Đã mặc định là `gpt-4o-mini` (rẻ và hiệu quả).
  - **Prompt:** Workflow đã tối ưu sẵn, **không cần chỉnh sửa** trừ khi cần thay đổi logic xếp hạng.
- **Lưu ý:**
  - **Score sẽ trả về dưới dạng emoji:**
    - ⚪️ Cold Lead
    - 🟢 Warm Lead
    - 🔵 Hot Lead
    - 🟣 Qualified Lead
    - 🔴 VIP Lead
  - **Nếu muốn thay đổi logic xếp hạng**, chỉnh sửa **prompt** trong node `OpenAI Chat Model`.

#### **🔹 Node 4: OpenAI Chat Model (lmChatOpenAi)**
- **Cấu hình:**
  - **Model:** Đã mặc định là `gpt-4o-mini` (không cần thay đổi).
  - **Input:** Dữ liệu từ node `AI Lead Scoring Agent`.
  - **Lưu ý:** Node này **không cần cấu hình thêm**, chỉ cần đảm bảo `OpenAI API Key` đã điền đúng.

#### **🔹 Node 6: Save to Lead Database (Google Sheets)**
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Sheet ID:** Thay thế `YOUR_GOOGLE_SHEET_ID` bằng **Sheet ID** của Google Sheets của các sếp.
    - **Cách lấy Sheet ID:**
      1. Mở Google Sheets → URL sẽ có dạng: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/edit`.
      2. Copy phần `[SHEET_ID]` (vd: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Range:** `Sheet1!A1` (giả sử dữ liệu được ghi từ ô A1).
  - **Headers:** Bật `Use headers` và chọn các cột phù hợp (Name, Email, Company, Score...).
- **Lưu ý:**
  - **Tạo sheet mới** với các cột: `Name`, `Email`, `Company`, `Industry`, `Request`, `Score`.
  - **Kiểm tra quyền truy cập** của OAuth2 để n8n có thể ghi dữ liệu.

#### **🔹 Node 7: Notify Sales Team (Telegram)**
- **Cấu hình:**
  - **Credentials:** Chọn `telegramApi` (đã cấu hình trước).
  - **Chat ID:** Thay thế `YOUR_TELEGRAM_CHAT_ID` bằng **Chat ID** của nhóm Telegram.
    - **Cách lấy Chat ID:**
      1. Gửi tin nhắn cho bot qua Telegram.
      2. Bot trả về Chat ID (vd: `-1001234567890`).
  - **Message:** Workflow đã cấu hình sẵn, **không cần chỉnh sửa** trừ khi muốn thay đổi nội dung thông báo.
- **Lưu ý:**
  - **Tạo bot Telegram** qua @BotFather và thêm bot vào nhóm bán hàng.
  - **Kiểm tra quyền** của bot có thể gửi tin nhắn không.

#### **🔹 Node 8: Send Auto-Reply Email (Gmail)**
- **Cấu hình:**
  - **Credentials:** Chọn `gmailOAuth2Api` (đã cấu hình trước).
  - **To:** `{$.json["email"]}` (địa chỉ email của lead).
  - **Subject:** `Xin chào {$.json["firstName"]}, cảm ơn bạn đã liên hệ!`
  - **Body:** Workflow đã cấu hình sẵn email mẫu, **cần chỉnh sửa** để phù hợp với brand của các sếp.
    - Ví dụ:
      ```html
      <p>Xin chào {$.json["firstName"]},</p>
      <p>Cảm ơn bạn đã liên hệ với {Tên Công Ty} qua website của chúng tôi.</p>
      <p>Chúng tôi đã nhận được yêu cầu của bạn về: <strong>{$.json["requestDetails"]}</strong>.</p>
      <p>Đội ngũ của chúng tôi sẽ liên hệ với bạn trong vòng 24 giờ để hỗ trợ.</p>
      <p>Trân trọng,</p>
      <p>Đội ngũ {Tên Công Ty}</p>
      ```
- **Lưu ý:**
  - **Kích hoạt "Less secure app access"** trong Gmail (nếu cần) hoặc sử dụng OAuth2.
  - **Test email** trước khi kích hoạt workflow để đảm bảo nội dung đúng.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Gửi một form test từ website (hoặc sử dụng **Test Tab** trong n8n Editor).
   - Kiểm tra:
     - Email tự động có được gửi không?
     - Telegram có thông báo không?
     - Google Sheets có ghi dữ liệu không?
     - Score lead có hợp lý không?

2. **Bật Active:**
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Xếp Hạng Lead**
- **Thay đổi logic xếp hạng** bằng cách chỉnh sửa **prompt** trong node `OpenAI Chat Model`:
  ```json
  {
    "task": "Xếp hạng lead dựa trên các tiêu chí sau:",
    "criteria": [
      {"name": "Đã xác nhận ngân sách", "weight": 3},
      {"name": "Đã xác nhận thời gian", "weight": 2},
      {"name": "Liên hệ từ công ty lớn", "weight": 2},
      {"name": "Yêu cầu phức tạp", "weight": 1}
    ],
    "input": {
      "name": "{$.json["firstName"]} {$.json["lastName"]}",
      "company": "{$.json["company"]}",
      "industry": "{$.json["industry"]}",
      "request": "{$.json["requestDetails"]}"
    },
    "output": "Trả về emoji: ⚪️ (Cold), 🟢 (Warm), 🔵 (Hot), 🟣 (Qualified), 🔴 (VIP)"
  }
  ```

### **2. Thêm Slack/Email Báo Cáo Định Kỳ**
- **Sử dụng node `Set` + `Schedule`** để gửi báo cáo hàng ngày/tuần về lead mới và xếp hạng.
- **Ví dụ:**
  - Lọc lead mới trong Google Sheets.
  - Gửi báo cáo qua Slack/Email với thống kê:
    - Số lead mới.
    - Phân bố theo cấp độ (⚪️, 🟢, 🔵, 🟣, 🔴).
    - Lead VIP cần ưu tiên.

### **3. Kết Nối Với CRM (Salesforce, HubSpot, Pipedrive)**
- **Thêm node `Salesforce`/`HubSpot`** sau node `Google Sheets` để tự động đồng bộ lead vào CRM.
- **Cấu hình:**
  - Chọn `Salesforce OAuth2` (hoặc `HubSpot OAuth2`).
  - Map dữ liệu từ Google Sheets sang CRM.

### **4. Thêm SMS cho Lead VIP (🔴)**
- **Sử dụng node `Twilio`** để gửi SMS cho lead có score 🔴.
- **Cấu hình:**
  - Thêm node `Twilio` sau node `Telegram`.
  - Gửi tin nhắn:
    ```text
    Xin chào {$.json["firstName"]}, lead của bạn đã được xếp hạng VIP. Chúng tôi sẽ liên hệ ngay trong giờ!
    ```

### **5. Lưu Log & Theo Dõi Hiệu Quả**
- **Thêm node `StickyNote`** để lưu log mỗi lần xử lý lead.
- **Sử dụng node `Google Sheets`** để ghi lịch sử hoạt động.
- **Tạo dashboard** với Google Data Studio để theo dõi:
  - Tỷ lệ chuyển đổi lead theo cấp độ.
  - Thời gian phản hồi trung bình.
  - Lead VIP đã được xử lý.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa quá trình xếp hạng, trả lời và thông báo lead một cách **chính xác, nhanh chóng và không cần code**. Với chi phí thấp (khoảng **$0.0001/lead** cho GPT-4o-mini) và hiệu quả cao, các sếp sẽ tiết kiệm **2-3 giờ/ngày** và tăng **tỷ lệ chuyển đổi lead lên 30%**.

**Hành động ngay hôm nay:**
1. **Đăng ký VPS n8n** để lưu trữ workflow 24/7: 👉 [TinoHost](https://