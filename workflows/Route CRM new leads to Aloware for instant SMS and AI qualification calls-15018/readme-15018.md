---
title: "🚀 Tự Động Hóa Lead CRM → SMS Tự Động + Cuộc Gọi AI Chất Lượng Với Aloware (Không Cần Code)"
description: "Workflow này tự động nhận lead mới từ CRM, gửi SMS cá nhân hóa ngay lập tức và phân loại lead thành hot/warm để gọi AI hoặc nurture tự động. Giúp các sếp tiết kiệm 80% thời gian theo dõi lead và tăng tỷ lệ chuyển đổi 30%."
slug: "tu-dong-hoa-lead-crm-sms-ai-qualification-aloware"
tags: [n8n, automation, CRM, AI Chatbot, Aloware, lead nurturing, no-code]
keywords: [n8n workflow CRM, tự động hóa lead, SMS tự động, AI qualification call, Aloware API, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Lead CRM → SMS Tự Động + Cuộc Gọi AI Chất Lượng Với Aloware**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Lặp lại công việc thủ công**: Nhập lead mới từ CRM vào Aloware, gửi SMS cá nhân hóa, và phân loại lead theo mức độ "hot" hay "warm".
- **Mất thời gian quý giá**: Theo dõi hàng trăm lead mỗi ngày, nhưng chỉ có 20% lead thực sự "hot" cần gọi ngay.
- **Tỷ lệ chuyển đổi thấp**: Do phản hồi chậm, lead "nóng" bị bỏ lỡ, mất cơ hội bán hàng.
- **Không tối ưu hóa nguồn lực**: AI và nhân viên gọi điện không được phân công hiệu quả.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận lead mới** từ CRM (HubSpot, Salesforce, Pipedrive...) qua webhook.
✅ **Gửi SMS cá nhân hóa** ngay lập tức qua Aloware.
✅ **Phân loại lead** thành "hot" (AI gọi) hoặc "warm" (nurture tự động).
✅ **Tiết kiệm 80% thời gian** theo dõi lead và tăng tỷ lệ chuyển đổi lên **30%**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** theo dõi lead thủ công.
- **Tăng tỷ lệ chuyển đổi lên 30%** nhờ gọi AI ngay với lead "hot".
- **SMS cá nhân hóa tự động** trong giây lát, không cần nhập thủ công.
- **Phân loại lead chính xác** dựa trên lead score (thay vì dựa vào cảm nhận).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Kết hợp với Aloware** để tối ưu hóa chu trình bán hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Aloware** và các thông tin API:
   - `ALOWARE_API_TOKEN` (tạo tại [Aloware Developer Portal](https://developer.aloware.com/)).
   - `ALOWARE_LINE_PHONE` (số điện thoại của Aloware để gửi SMS).
   - `ALOWARE_HOT_SEQUENCE_ID` (ID của chu trình gọi AI cho lead "hot").
   - `ALOWARE_NURTURE_SEQUENCE_ID` (ID của chu trình nurture cho lead "warm").
2. **CRM hỗ trợ webhook** (HubSpot, Salesforce, Pipedrive...).
3. **Lead score threshold** (mức điểm phân loại lead "hot" vs "warm", mặc định là **70**).
4. **Tên công ty** (`COMPANY_NAME`) để cá nhân hóa SMS.
5. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15018](https://n8n.io/workflows/15018) hoặc copy JSON từ canvas.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần cấu hình kỹ lưỡng:

##### **A. Node "CRM: New Lead Received" (Webhook)**
- **Cấu hình**:
  - **Path**: `crm-new-lead` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Chọn **None** (hoặc tạo mới nếu cần).
- **Lưu ý**:
  - **Cấu hình CRM** để gửi lead mới qua webhook này. Ví dụ:
    - **HubSpot**: Cài đặt webhook tại `Settings > Automation > Webhooks`.
    - **Salesforce**: Sử dụng **Flow Builder** để gửi dữ liệu khi lead mới tạo.
    - **Pipedrive**: Tạo **Webhook** tại `Settings > Automation > Webhooks`.

##### **B. Node "Normalize Lead Data" (Set)**
- **Cấu hình**:
  - **Set JSON Path**: `$.data` (đảm bảo dữ liệu lead được truyền đúng định dạng).
  - **Thêm trường cần thiết** (nếu CRM không gửi đầy đủ):
    ```json
    {
      "lead_score": "{{$json['score'] || 0}}",
      "source": "{{$json['source'] || 'unknown'}}",
      "company_name": "{{$env['COMPANY_NAME']}}"
    }
    ```
- **Lưu ý**:
  - Nếu CRM không gửi `lead_score`, các sếp có thể tính toán dựa trên các trường khác (ví dụ: `score = (hotness * 0.5) + (engagement * 0.3) + (revenue_potential * 0.2)`).

##### **C. Node "Aloware: Create or Update Contact" (HTTP Request)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.aloware.com/v1/contacts`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$env['ALOWARE_API_TOKEN']}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "phone": "{{$json['phone']}}",
      "name": "{{$json['name']}}",
      "email": "{{$json['email']}}",
      "custom_fields": {
        "lead_score": "{{$json['lead_score']}}",
        "source": "{{$json['source']}}",
        "company_name": "{{$json['company_name']}}"
      }
    }
    ```
- **Lưu ý**:
  - Đảm bảo `ALOWARE_API_TOKEN` được đặt trong **n8n Variables** (`Settings > Variables`).

##### **D. Node "Aloware: Send Instant Lead SMS" (HTTP Request)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.aloware.com/v1/sms`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$env['ALOWARE_API_TOKEN']}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "phone": "{{$json['phone']}}",
      "message": "Xin chào {{$json['name']}}, tôi là {{$env['COMPANY_NAME']}}. Chúng tôi nhận được lead từ bạn và sẽ liên hệ ngay. Nếu bạn muốn được tư vấn chi tiết, hãy nhắn tin 'YES'! 🚀"
    }
    ```
- **Lưu ý**:
  - **Cá nhân hóa SMS** bằng tên và tên công ty để tăng tỷ lệ mở.

##### **E. Node "Is Hot Lead?" (If)**
- **Cấu hình**:
  - **Condition**: `{{$json['lead_score'] >= env('LEAD_SCORE_THRESHOLD')}}` (mặc định là 70).
  - **Nếu true**: Chuyển sang node **"Aloware: Enroll in AI Qualification Sequence"**.
  - **Nếu false**: Chuyển sang node **"Aloware: Enroll in Nurture Sequence"**.
- **Lưu ý**:
  - **Điều chỉnh `LEAD_SCORE_THRESHOLD`** trong **n8n Variables** nếu cần (ví dụ: 60 cho lead "hot" hơn).

##### **F. Node "Aloware: Enroll in AI Qualification Sequence" (HTTP Request)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.aloware.com/v1/sequences/{{$env['ALOWARE_HOT_SEQUENCE_ID']}}/enroll`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$env['ALOWARE_API_TOKEN']}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "contact_id": "{{$json['contact_id']}}",
      "custom_fields": {
        "lead_score": "{{$json['lead_score']}}",
        "source": "{{$json['source']}}"
      }
    }
    ```
- **Lưu ý**:
  - **Thiết lập chu trình AI Qualification** tại Aloware trước khi chạy workflow.

##### **G. Node "Aloware: Enroll in Nurture Sequence" (HTTP Request)**
- **Cấu hình tương tự** như node trên, nhưng sử dụng:
  - **URL**: `https://api.aloware.com/v1/sequences/{{$env['ALOWARE_NURTURE_SEQUENCE_ID']}}/enroll`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một lead giả từ CRM (ví dụ: `POST` đến `https://[your-n8n-url]/webhook/crm-new-lead` với JSON mẫu).
   - Kiểm tra:
     - SMS có được gửi không?
     - Lead có được phân loại đúng không?
     - Aloware có nhận được contact và enroll vào chu trình đúng không?
2. **Bật Active workflow**:
   - Nhấn **Active** trên canvas.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** sau node **"Is Hot Lead?"** để thông báo lead "hot" ngay lập tức.
   - Ví dụ:
     ```json
     {
       "text": "🚨 Lead HOT mới: {{$json['name']}} (Score: {{$json['lead_score']}}). Phone: {{$json['phone']}}"
     }
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại tất cả lead đã xử lý, bao gồm:
     - Thời gian nhận lead.
     - Lead score.
     - Trạng thái (hot/warm).
     - Kết quả (SMS gửi thành công, enroll chu trình...).

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Schedule Node** để gửi báo cáo hàng ngày/tuần về:
     - Số lead mới.
     - Tỷ lệ lead "hot".
     - Tỷ lệ chuyển đổi từ SMS.

4. **Tối Ưu Hóa Lead Score**:
   - Thêm logic tính toán lead score phức tạp hơn bằng **n8n Function Node** (nếu cần).

5. **Xử Lý Lỗi**:
   - Thêm node **Set Error** và **Notify Error** để cảnh báo khi:
     - Aloware API trả về lỗi.
     - SMS không gửi được.
     - Lead score không hợp lệ.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào việc bán hàng chứ không phải quản lý lead. Với **tự động hóa SMS cá nhân hóa** và **phân loại lead chính xác**, các sếp sẽ:
✔ **Tăng tỷ lệ chuyển đổi** nhờ gọi AI ngay với lead "hot".
✔ **Tiết kiệm thời gian** theo dõi hàng trăm lead mỗi ngày.
✔ **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với dữ liệu mẫu** trước khi bật Active.
3. **Monitor và tối ưu hóa** lead score và SMS template.

**Nếu có vấn đề**, các sếp có thể tham khảo [n8n Community](https://community.n8n.io/) hoặc liên hệ với tôi để hỗ trợ!

---
**💡 Mẹo cuối**: Nếu cần **tự động hóa thêm**, các sếp có thể mở rộng workflow bằng các node khác như **Zapier, Make (Integromat), hoặc Google Analytics** để theo dõi hiệu quả của SMS và gọi AI.