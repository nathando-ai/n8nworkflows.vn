---
title: "🚀 Tự Động Hóa Xác Minh Yêu Cầu Bảo Hiểm qua SMS & AI Voice Agent với Aloware - Giảm 80% Công Việc Tiếp Nối Lead"
description: "Workflow tự động hóa nhận yêu cầu báo giá bảo hiểm từ website/form, xác minh thông tin qua SMS và AI Voice Agent, tự động phân loại và gửi dây chuyền chăm sóc phù hợp. Giúp các sếp tiết kiệm thời gian, tăng tỷ lệ chuyển đổi lead thành khách hàng."
slug: "tieu-dong-hoa-xac-minh-yeu-cau-bao-hiem-sms-ai-voice-agent"
tags: [n8n, automation, lead-generation, ai-chatbot, aloware, no-code]
keywords: [n8n workflow bảo hiểm, tự động hóa lead bảo hiểm, AI Voice Agent, Aloware SMS, tự động hóa tiếp nhận yêu cầu báo giá]
---

# 🚀 **Tự Động Hóa Xác Minh Yêu Cầu Bảo Hiểm qua SMS & AI Voice Agent với Aloware**

### **Giải pháp cho các sếp bảo hiểm:**
Hàng ngày, các sếp phải mất **3-5 giờ** để tiếp nhận, xác minh và phân loại hàng chục yêu cầu báo giá bảo hiểm từ website, form online hoặc đối tác. Quá trình này thường bao gồm:
❌ **Nhập liệu thủ công** vào hệ thống CRM (Aloware).
❌ **Gửi SMS xác nhận** một cách chậm chạp.
❌ **Phân loại lead** dựa trên mức độ ưu tiên (urgent/standard) mà không có tự động hóa.
❌ **Mất thời gian gọi điện** để xác minh thông tin chi tiết (hiện trạng bảo hiểm, ngày hết hạn, số lượng xe/người bảo hiểm...).

**Workflow này tự động hóa toàn bộ quy trình trong 10 giây!** Sau khi nhận được yêu cầu báo giá, hệ thống sẽ:
✅ **Tự động tạo contact** trong Aloware với thông tin chi tiết.
✅ **Gửi SMS xác nhận** ngay lập tức.
✅ **Phân loại lead** theo mức độ ưu tiên (urgent → gọi AI Voice Agent, standard → dây chuyền chăm sóc tự động).
✅ **Tiết kiệm 80% thời gian** cho team tiếp thị và chăm sóc khách hàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và tính liên tục.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** tiếp nhận và phân loại lead: Không cần nhập liệu thủ công vào Aloware.
- **Tăng tỷ lệ chuyển đổi lead** nhờ AI Voice Agent xác minh thông tin chi tiết (hiện trạng bảo hiểm, ngày hết hạn, số lượng xe/người bảo hiểm...).
- **Chăm sóc khách hàng cá nhân hóa**: SMS xác nhận tự động + dây chuyền chăm sóc phù hợp với mức độ ưu tiên.
- **Hoạt động 24/7**: Không cần can thiệp của con người, giảm thiểu lỗi và tăng hiệu suất.
- **Tăng doanh thu**: Nhiều lead được xử lý nhanh chóng hơn, giảm tỷ lệ bỏ cuộc.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Aloware** (CRM dành cho bảo hiểm) với quyền API.
2. **API Token Aloware**: Được tạo trong **Settings > API Tokens** của Aloware.
3. **Số điện thoại Aloware (LINE Phone)**: Được cấu hình trong Aloware để gửi SMS.
4. **Hai dây chuyền (Sequences) trong Aloware**:
   - **AI Voice Agent Sequence**: Dùng để gọi AI xác minh thông tin chi tiết (hiện trạng bảo hiểm, ngày hết hạn, số lượng xe/người bảo hiểm...).
   - **Nurture Sequence**: Dây chuyền chăm sóc tự động cho lead không ưu tiên.
5. **URL Webhook của n8n**: Cần kết nối với form báo giá trên website hoặc đối tác lead vendor.
6. **Các biến môi trường (n8n Variables)**:
   - `ALOWARE_API_TOKEN`: API Token của Aloware.
   - `ALOWARE_LINE_PHONE`: Số điện thoại Aloware để gửi SMS.
   - `ALOWARE_AI_SEQUENCE_ID`: ID của dây chuyền AI Voice Agent.
   - `ALOWARE_NURTURE_SEQUENCE_ID`: ID của dây chuyền Nurture.
   - `AGENCY_NAME`: Tên công ty bảo hiểm.
   - `AGENT_NAME`: Tên nhân viên/đại lý (nếu cần).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15030) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** (trang chủ của n8n) và nhấn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập.
- Workflow sẽ tự động được tạo với 7 node như mô tả dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **7 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **Node 1: "Quote Request Received" (Webhook)**
- **Chức năng**: Nhận yêu cầu báo giá từ website/form hoặc đối tác lead vendor.
- **Cấu hình**:
  - **Path**: `insurance-quote-request` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Credentials**: Chọn **None** (n8n sẽ tự động tạo URL webhook).
- **Lưu ý**:
  - Sau khi import, copy **URL Webhook** từ node này và **kết nối với form báo giá** trên website hoặc hệ thống của đối tác lead vendor.
  - Ví dụ: Nếu form trên website gửi dữ liệu POST đến `https://tên-domain-n8n.com/webhook/insurance-quote-request`, thì các sếp cần đảm bảo form gửi đúng URL này.

##### **Node 2: "Normalize Quote Data" (Set)**
- **Chức năng**: Chuẩn hóa dữ liệu đầu vào (tách biệt các trường dữ liệu như `insurance_type`, `coverage_status`, `urgency`, `ZIP`).
- **Cấu hình**:
  - **Set JSON Path**: Điền vào ô `json` với cấu trúc dữ liệu chuẩn như sau (thay thế giá trị mẫu bằng trường thực tế từ form):
    ```json
    {
      "insurance_type": "$json.insurance_type",
      "coverage_status": "$json.coverage_status",
      "urgency": "$json.urgency",
      "ZIP": "$json.ZIP",
      "custom_fields": {
        "quote_details": "$json.quote_details"
      }
    }
    ```
  - **Lưu ý**:
    - Các trường `insurance_type`, `coverage_status`, `urgency`, `ZIP` phải khớp với dữ liệu form gửi lên.
    - Trường `custom_fields.quote_details` dùng để lưu thông tin chi tiết của yêu cầu báo giá.

##### **Node 3 & 4: "Aloware: Create Contact with Quote Details" & "Aloware: Send Quote Acknowledgment SMS" (HTTP Request)**
- **Chức năng**: Tạo contact mới trong Aloware và gửi SMS xác nhận.
- **Cấu hình chung**:
  - **URL**: `https://api.aloware.com/v1/contacts` (đối với Create Contact) và `https://api.aloware.com/v1/sms` (đối với Send SMS).
  - **Headers**:
    - `Authorization`: `Bearer $ALOWARE_API_TOKEN` (sử dụng biến môi trường).
    - `Content-Type`: `application/json`.
  - **Body (Create Contact)**:
    ```json
    {
      "first_name": "$json.first_name",
      "last_name": "$json.last_name",
      "email": "$json.email",
      "phone": "$json.phone",
      "custom_fields": {
        "insurance_type": "$json.insurance_type",
        "coverage_status": "$json.coverage_status",
        "urgency": "$json.urgency",
        "quote_details": "$json.custom_fields.quote_details"
      }
    }
    ```
  - **Body (Send SMS)**:
    ```json
    {
      "to": "$json.phone",
      "message": "Xin chào $json.first_name! Chúng tôi đã nhận được yêu cầu báo giá bảo hiểm của bạn. Đội ngũ của chúng tôi sẽ liên hệ trong thời gian sớm nhất. Cảm ơn bạn!",
      "from": "$ALOWARE_LINE_PHONE"
    }
    ```
  - **Lưu ý**:
    - Thay thế `$json.first_name`, `$json.last_name`, `$json.email`, `$json.phone` bằng các trường tương ứng từ form.
    - Đảm bảo biến môi trường `ALOWARE_API_TOKEN` và `ALOWARE_LINE_PHONE` đã được thiết lập trong **n8n Variables**.

##### **Node 5: "Is Urgent Quote?" (If)**
- **Chức năng**: Phân loại lead theo mức độ ưu tiên (`urgency`).
- **Cấu hình**:
  - **Condition**: `$json.urgency === "urgent"`.
  - **Lưu ý**:
    - Giá trị `urgent` phải khớp với dữ liệu từ form (ví dụ: `urgent`, `high`, `1`...).
    - Nếu lead **không** ưu tiên, workflow sẽ chuyển sang Node 7 ("Aloware: Enroll in Nurture Sequence").

##### **Node 6: "Aloware: Enroll in AI Voice Agent Sequence" (HTTP Request)**
- **Chức năng**: Gọi AI Voice Agent để xác minh thông tin chi tiết (hiện trạng bảo hiểm, ngày hết hạn, số lượng xe/người bảo hiểm...).
- **Cấu hình**:
  - **URL**: `https://api.aloware.com/v1/sequences/$ALOWARE_AI_SEQUENCE_ID/enroll`.
  - **Headers**: Như Node 3 (Authorization, Content-Type).
  - **Body**:
    ```json
    {
      "contact_id": "$json.id", // ID của contact vừa tạo trong Aloware
      "custom_fields": {
        "preferred_time": "$json.preferred_time" // Nếu form có trường này
      }
    }
    ```
  - **Lưu ý**:
    - Thay thế `$ALOWARE_AI_SEQUENCE_ID` bằng ID của dây chuyền AI Voice Agent trong Aloware.
    - Đảm bảo dây chuyền này đã được cấu hình để gọi AI với các câu hỏi:
      - "Bạn hiện đang có bảo hiểm nào không?"
      - "Ngày hết hạn bảo hiểm là khi nào?"
      - "Bạn có bao nhiêu người/xe cần bảo hiểm?"

##### **Node 7: "Aloware: Enroll in Nurture Sequence" (HTTP Request)**
- **Chức năng**: Gửi lead vào dây chuyền chăm sóc tự động (nếu không ưu tiên).
- **Cấu hình**:
  - **URL**: `https://api.aloware.com/v1/sequences/$ALOWARE_NURTURE_SEQUENCE_ID/enroll`.
  - **Headers**: Như Node 3 (Authorization, Content-Type).
  - **Body**:
    ```json
    {
      "contact_id": "$json.id"
    }
    ```
  - **Lưu ý**:
    - Thay thế `$ALOWARE_NURTURE_SEQUENCE_ID` bằng ID của dây chuyền Nurture trong Aloware.
    - Dây chuyền này nên bao gồm:
      - Email tự động.
      - SMS định kỳ.
      - Gọi điện tự động (nếu cần).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và gửi một yêu cầu báo giá mẫu từ form (hoặc gọi API webhook với dữ liệu mẫu).
   - Kiểm tra:
     - Contact có được tạo trong Aloware không?
     - SMS xác nhận có được gửi không?
     - Lead được phân loại đúng (urgent → AI Voice Agent, standard → Nurture)?
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau Node 5 (`Is Urgent Quote?`) để thông báo lead ưu tiên cho team.
   - Cấu hình:
     ```json
     {
       "text": "🚨 Lead ưu tiên mới! - $json.first_name $json.last_name (Số điện thoại: $json.phone)"
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Set** sau Node 6 và Node 7 để lưu thông tin vào một sheet Google Sheets hoặc database.
   - Ví dụ:
     ```json
     {
       "log": {
         "timestamp": "$now",
         "contact_id": "$json.id",
         "action": "$node.name",
         "status": "success"
       }
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule** (n8n) để chạy workflow hàng ngày/tuần và gửi báo cáo số lượng lead được xử lý, tỷ lệ chuyển đổi, và thông tin chi tiết qua email (n8n-nodes-base.email).

4. **Tối ưu AI Voice Agent**:
   - Cập nhật dây chuyền AI Voice Agent trong Aloware để hỏi thêm thông tin như:
     - "Bạn có ý định thay đổi bảo hiểm hiện tại không?"
     - "Bạn quan tâm đến gói bảo hiểm nào (gói cơ bản, toàn diện, gia đình...)?"

5. **Tích hợp với Google Sheets**:
   - Thêm node **Google Sheets** sau Node 2 để lưu toàn bộ dữ liệu yêu cầu báo giá vào một sheet.
   - Cấu hình:
     - **Sheet Name**: `Insurance_Quotes`.
     - **Range**: `A1` (đầu tiên).
     - **Data**: `$json`.

---

### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn công việc thủ công** trong quá trình tiếp nhận và xác minh yêu cầu báo giá bảo hiểm. Các sếp sẽ:
✔ **Tiết kiệm 80% thời gian** cho team tiếp thị và chăm sóc khách hàng.