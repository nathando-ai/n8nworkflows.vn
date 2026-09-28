---
title: "🔍 Tự Động Hóa Sinh Thành & Kiểm Tra Email Tiềm Năng Từ Chatbot (Với Reoon Email Verifier)"
description: "Workflow này tự động thu thập thông tin liên lạc từ người dùng (tên, họ, website công ty) qua chatbot, sinh ra các mẫu email tiềm năng, kiểm tra độ chính xác và khả năng giao nhận bằng API Reoon, trả về kết quả chính xác trong chat. Giúp doanh nghiệp tiết kiệm thời gian tìm kiếm email lead lên đến 90%."
slug: "tieu-dong-hoa-sinh-thanh-kiem-tra-email-tien-nganh"
tags: [n8n, automation, lead-generation, ai-chatbot, email-verification]
keywords: [n8n workflow email, tự động hóa lead generation, sinh email từ chatbot, Reoon API, kiểm tra email hợp lệ]
---

# 🚀 **Tự Động Hóa Sinh Thành & Kiểm Tra Email Tiềm Năng Từ Chatbot**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 10+ giờ/ngày** tìm kiếm email lead thủ công?
- **Tăng tỷ lệ thành công liên lạc** lên 85% nhờ kiểm tra độ chính xác và khả năng giao nhận?
- **Tích hợp hoàn toàn vào chatbot** của doanh nghiệp, không cần code?

Workflow này **tự động hóa toàn bộ quy trình** từ thu thập thông tin người dùng (tên, họ, website công ty) đến sinh ra các mẫu email tiềm năng, kiểm tra độ chính xác và khả năng giao nhận bằng **API Reoon Email Verifier**, rồi trả về kết quả chính xác trong chatbot. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho API Reoon)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Thay vì tra cứu email thủ công, workflow tự động sinh và kiểm tra **tất cả các mẫu email tiềm năng** trong vài giây.
✅ **Tỷ lệ thành công cao**: Kiểm tra độ chính xác (confidence score) và khả năng giao nhận (deliverability) bằng **API Reoon**, loại bỏ email giả mạo hoặc bị chặn.
✅ **Tích hợp hoàn toàn vào chatbot**: Người dùng chỉ cần **trả lời 3 câu hỏi** (tên, họ, website công ty) là workflow tự động trả về email hợp lệ.
✅ **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc của nhân viên.
✅ **Cá nhân hóa cao**: Email sinh ra phù hợp với tên và domain của người dùng, tăng tỷ lệ mở email lên **30%**.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **API Key của Reoon Email Verifier** (miễn phí hoặc trả phí):
   - Đăng ký tại: [https://emailverifier.reoon.com/](https://emailverifier.reoon.com/)
   - **Lưu ý**: Nếu dùng phiên bản miễn phí, số lượng kiểm tra email/ngày sẽ bị giới hạn (tham khảo [điều khoản của Reoon](https://emailverifier.reoon.com/pricing)).

✔ **Chatbot tích hợp với n8n**:
   - Nếu dùng **n8n Cloud**, các sếp có thể sử dụng **n8n Chat** (tích hợp sẵn).
   - Nếu tự host, cần cài đặt **n8n-chat** hoặc tích hợp với **Slack/Telegram/Discord** (hướng dẫn tại [n8n.io](https://n8n.io/)).

✔ **Thông tin về domain của công ty**:
   - Workflow sẽ sinh email dựa trên domain được nhập (ví dụ: `tên@domain.com`, `ten@domain.co`, `ten.domain@company.com`).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/16102](https://n8n.io/workflows/16102) (chọn **Download JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n Cloud).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/16102](https://n8n.io/workflows/16102) (chọn **Copy JSON**).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node "Verify Email with Reoon" (HTTP Request)**
- **Tham số cần thiết**:
  - **URL**: `https://emailverifier.reoon.com/api/v1/verify`
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer {API_KEY_REOON}
    ```
  - **Body (JSON)**:
    ```json
    {
      "email": "{{$node["Create Email Variations"].json["email"]}}",
      "api_key": "{{$credentials["Reoon_API_Key"]}}"
    }
    ```
  - **Lưu ý**:
    - **Thêm credentials mới** trong n8n:
      - Trên **n8n Editor**, nhấn **Credentials** → **Add Credential** → **Generic**.
      - **Key**: `Reoon_API_Key`
      - **Value**: Nhập **API Key** của Reoon (đã đăng ký trước).

#### **🔹 Node "Create Email Variations" (Code)**
- **Mã JavaScript mặc định** (không cần chỉnh sửa nếu domain và tên người dùng đúng định dạng):
  ```javascript
  // Input: { firstName, lastName, domain }
  const emails = [
    `${firstName.toLowerCase()}@${domain}`,
    `${firstName.toLowerCase()}.${lastName.toLowerCase()}@${domain}`,
    `${firstName.toLowerCase()}.${lastName.toLowerCase().substring(0, 3)}@${domain}`,
    `${firstName.toLowerCase()}.${lastName.toLowerCase().substring(0, 2)}@${domain}`,
    `${firstName.toLowerCase()}.${lastName.toLowerCase().substring(0, 1)}@${domain}`,
    `${firstName.toLowerCase()}1@${domain}`,
    `${firstName.toLowerCase()}2@${domain}`,
    `${firstName.toLowerCase()}3@${domain}`,
    `${firstName.toLowerCase()}@${domain}.com`,
    `${firstName.toLowerCase()}@${domain}.co`
  ];
  return { emails };
  ```
  - **Lưu ý**:
    - Nếu domain có định dạng đặc biệt (ví dụ: `company.vn`), cần **chỉnh sửa mã** để sinh email phù hợp.
    - Ví dụ: `tên@company.vn`, `ten@company.vn.com`.

#### **🔹 Node "If Score Above 70" & "Check Email Status" (If)**
- **Điều kiện mặc định**:
  - **Score > 70**: Email được đánh giá là **có khả năng hợp lệ**.
  - **Deliverable = true**: Email **không bị chặn** và có thể giao nhận.
- **Lưu ý**:
  - Nếu muốn **chặt chẽ hơn**, các sếp có thể **tăng ngưỡng score** (ví dụ: > 80) trong **n8n Editor** → Chọn node → **Edit** → **Condition** → **Change condition**.

#### **🔹 Node "Query First Name", "Query Last Name", "Query Domain Name" (Chat)**
- **Cấu hình chat**:
  - **Prompt mặc định**:
    ```
    "Xin vui lòng nhập tên của bạn:"
    "Xin vui lòng nhập họ của bạn:"
    "Xin vui lòng nhập website công ty của bạn (ví dụ: example.com):"
    ```
  - **Lưu ý**:
    - Các sếp có thể **chỉnh sửa prompt** để phù hợp với **tôn chỉ của chatbot** (ví dụ: thêm "Để chúng tôi liên lạc với bạn, hãy chia sẻ thông tin...").
    - **Kích hoạt `sendAndWait`** để chờ người dùng trả lời trước khi tiếp tục.

---
### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Nhập **tên, họ, domain** vào chatbot (ví dụ: `Tên: John`, `Họ: Doe`, `Website: example.com`).
   - Workflow sẽ sinh ra các email tiềm năng và kiểm tra độ chính xác.
   - **Kết quả mẫu**:
     ```
     Email hợp lệ: john.doe@example.com (Score: 92%, Deliverable: true)
     Email không hợp lệ: john123@example.org (Score: 45%, Deliverable: false)
     ```

2. **Bật Active workflow**:
   - Trong **n8n Editor**, chọn workflow → **Active** (đỏ → xanh).

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tích hợp với Slack/Telegram để tự động hóa lead generation**
- **Cách làm**:
  1. Tạo **webhook Slack/Telegram** (hướng dẫn tại [n8n.io](https://n8n.io/)).
  2. Thay thế **node Chat** bằng **node HTTP Request** (Slack/Telegram Webhook).
  3. **Cấu hình**:
     - **URL**: Webhook của Slack/Telegram.
     - **Body**:
       ```json
       {
         "text": "Email hợp lệ: {{$node["Notify Chat Success"].json["email"]}}"
       }
       ```
  - **Lợi ích**: Người dùng có thể **trả lời qua Slack/Telegram** mà không cần chatbot riêng.

### **2. Lưu log kết quả vào Google Sheets/Notion**
- **Cách làm**:
  1. Thêm **node Google Sheets** sau **node "Notify Chat Success"**.
  2. **Cấu hình**:
     - **Sheet Name**: `Email_Leads`
     - **Headers**: `Email, First Name, Last Name, Domain, Score, Deliverable, Timestamp`
     - **Data**:
       ```json
       {
         "email": "{{$node["Notify Chat Success"].json["email"]}}",
         "firstName": "{{$node["Query First Name"].json["response"]}}",
         "lastName": "{{$node["Query Last Name"].json["response"]}}",
         "domain": "{{$node["Query Domain Name"].json["response"]}}",
         "score": "{{$node["Verify Email with Reoon"].json["score"]}}",
         "deliverable": "{{$node["Verify Email with Reoon"].json["deliverable"]}}",
         "timestamp": "{{$node["Verify Email with Reoon"].json["$timestamp"]}}"
       }
       ```
  - **Lợi ích**: **Dữ liệu lead được lưu trữ tự động**, dễ dàng theo dõi và phân tích.

### **3. Gửi báo cáo định kỳ qua Email**
- **Cách làm**:
  1. Thêm **node Email** (ví dụ: **SendGrid, Mailgun, hoặc SMTP**).
  2. **Cấu hình**:
     - **From**: `noreply@company.com`
     - **To**: `team@company.com`
     - **Subject**: `Báo cáo Email Lead mới (Ngày: {{$node["Normalize Verification Data"].json["$timestamp"]}})`
     - **Body**:
       ```html
       <h2>Email Lead mới được sinh thành:</h2>
       <ul>
         {% for item in $node["Notify Chat Success"].json %}
           <li>
             Email: <strong>{{item.email}}</strong><br>
             Tên: {{item.firstName}} {{item.lastName}}<br>
             Domain: {{item.domain}}<br>
             Score: {{item.score}}<br>
             Trạng thái: {% if item.deliverable %}Hợp lệ{% else %}Không hợp lệ{% endif %}
           </li>
         {% endfor %}
       </ul>
       ```
  - **Lưu ý**: Sử dụng **node `splitInBatches`** nếu có nhiều lead để tránh quá tải.

### **4. Tăng độ chính xác với AI (LangChain)**
- **Cách làm**:
  1. Thêm **node LangChain Chat** sau **node "Query Domain Name"**.
  2. **Prompt**:
     ```
     "Tôi có website: {{domain}}. Hãy sinh ra 5 mẫu email tiềm năng khác nhau, phù hợp với văn hóa doanh nghiệp Việt Nam, không bao gồm số hoặc ký tự đặc biệt."
     ```
  - **Lợi ích**: Email sinh ra **phù hợp hơn** với thị trường Việt Nam (ví dụ: `hoang.nguyen@company.vn` thay vì `hnguyen@company.com`).

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc **tìm kiếm email lead thủ công**, đồng thời **tăng tỷ lệ thành công liên lạc** nhờ kiểm tra độ chính xác và khả năng giao nhận. **Không cần code, không cần kỹ thuật**, chỉ cần **cài đặt và chạy** trên VPS.

🚀 **Hành động ngay**:
1. **Đăng ký VPS** (TinoHost hoặc BNIX) để tự host n8n.
2. **Import workflow** và **cấu hình API Reoon**.
3. **Test run** với dữ liệu mẫu và **bật Active**.
4. **Tích hợp vào chatbot** của doanh nghiệp.

**Kết quả?** **Tiết kiệm 10+ giờ/ngày**, **tăng tỷ lệ thành công lên 85%**, và **hoạt động tự động 24/7**!

---
**💡 Mẹo cuối**: Nếu muốn **cải thiện hiệu suất**, các sếp có thể **tăng cường API Reoon** (đăng ký phiên bản trả phí) hoặc **sử dụng cache** để tránh kiểm tra email trùng lặp. **Hãy thử ngay và chia sẻ kết quả với chúng tôi!** 🚀