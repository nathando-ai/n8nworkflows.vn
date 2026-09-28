---
title: "🚀 Tự Động Hóa Xác Minh & Nâng Cao Thông Tin Lead với Octave + Slack (Không Cần Code)"
description: "Workflow tự động hóa nhận lead từ webhook, xác minh chất lượng và bổ sung thông tin chi tiết bằng AI Octave, sau đó gửi cảnh báo trực tiếp Slack - giúp đội Sales tiết kiệm 80% thời gian nghiên cứu lead."
slug: "tieu-dong-hoa-xac-minh-nang-cao-lead-octave-slack"
tags: [n8n, automation, ai-summarization, sales-automation, octave, slack-integration]
keywords: [tự động hóa lead qualification, n8n workflow octave, xác minh lead bằng ai, cảnh báo lead slack, tự động hóa sales]
---

# 🚀 **Tự Động Hóa Xác Minh & Nâng Cao Thông Tin Lead với Octave + Slack**

### **🔍 Nỗi Đau Của Đội Sales Hiện Nay**
Các sếp đã từng gặp phải tình huống này chưa?
- Nhận được hàng chục lead mỗi ngày từ website, landing page, hoặc form đăng ký.
- Đội Sales phải tốn thời gian **nghiên cứu từng lead** để xác định:
  - **Đây có phải là lead phù hợp** với ICP (Ideal Customer Profile) của công ty?
  - **Pain points** (vấn đề đau đầu) của họ là gì?
  - **Giá trị cụ thể** công ty có thể mang lại?
  - **Tham chiếu** (references) từ khách hàng tương tự?
- Kết quả? **80% thời gian** của Sales bị "chôn" trong công việc thủ công, còn lead "chết yên" vì không được theo dõi kịp thời.

**Workflow này giải quyết tất cả!**
Sử dụng **AI Octave** để tự động:
✅ **Xác minh chất lượng lead** (qualification) so với ICP của doanh nghiệp.
✅ **Bổ sung thông tin chi tiết** (enrichment) về pain points, value props, và references.
✅ **Gửi cảnh báo Slack** với thông tin đầy đủ, giúp Sales **nhận lead "sẵn sàng bán"** ngay lập tức.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian nghiên cứu lead**: AI xử lý tất cả, Sales chỉ cần gọi điện.
- **Chất lượng lead cao hơn**: Chỉ những lead **phù hợp + có giá trị** mới được chuyển đến Sales.
- **Cảnh báo tức thời**: Thông tin lead được gửi Slack ngay khi nhận được, không bỏ lỡ lead nào.
- **Cá nhân hóa thông tin**: AI cung cấp **pain points cụ thể** và **giá trị công ty mang lại**, giúp Sales chuẩn bị tốt hơn cho cuộc gọi.
- **Hoạt động 24/7**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của nhân viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Octave**:
   - API Key của Octave (được gọi là `octaveApi` trong workflow).
   - **Agent ID** cho việc **qualifyPerson** và **enrichPerson** (xem hướng dẫn [Octave Docs](https://octave.ai/docs)).
   - **Configurate qualification** tại cấp độ Product/Persona/Segment (ví dụ: điểm số tối thiểu để được xem là lead phù hợp).

2. **Tài khoản Slack**:
   - **OAuth 2.0 API Token** (được gọi là `slackOAuth2Api` trong workflow).
   - **Channel Slack** để nhận cảnh báo (ví dụ: `#sales-leads`).

3. **Webhook**:
   - **Đường dẫn webhook** để nhận dữ liệu lead từ hệ thống của doanh nghiệp (ví dụ: từ CRM, landing page, hoặc form đăng ký).
   - **Format dữ liệu lead**: Workflow giả định lead có các trường như `name`, `email`, `company`, `phone`, `website`, `jobTitle`, `description`.

4. **Hệ thống tự động hóa n8n**:
   - **Self-hosted n8n** (khuyến nghị để workflow chạy 24/7).
   - **N8n Community Nodes** (đã bao gồm trong workflow).
   - **Octave Nodes** (cần cài đặt từ [n8n.io](https://n8n.io/nodes/)).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo **2 cách**:
- **Tải file JSON**:
  1. Tải workflow từ [n8n.io/workflows/7615](https://n8n.io/workflows/7615) (chọn "Download JSON").
  2. Trên **n8n Editor**, nhấn **"Import"** và chọn file JSON vừa tải.
- **Copy/Paste JSON**:
  1. Mở file JSON từ link trên.
  2. Trên **n8n Editor**, nhấn **"Import"** → **"Paste JSON"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **5 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node 1: Inbound Lead Webhook**
- **Cấu hình**:
  - **Path**: Thay thế `your-webhook-path-here` bằng đường dẫn webhook của doanh nghiệp (ví dụ: `/api/leads`).
  - **Method**: Đặt thành `POST` (nếu lead được gửi qua API).
  - **Payload Format**: Đảm bảo dữ liệu lead được gửi theo **JSON** với các trường như:
    ```json
    {
      "name": "Tên Lead",
      "email": "email@doanhnghiep.com",
      "company": "Tên Công Ty",
      "phone": "0123456789",
      "website": "https://doanhnghiep.com",
      "jobTitle": "Chức vụ",
      "description": "Mô tả lead (nếu có)"
    }
    ```
  - **Credentials**: Không cần (webhook không yêu cầu API key).

##### **🔹 Node 2: Qualify Lead with Octave**
- **Cấu hình**:
  - **Credentials**: Chọn `octaveApi` (đã cấu hình trước khi import).
  - **Operation**: Đặt thành `qualifyPerson` (không cần thay đổi).
  - **Agent ID**: Thay thế bằng **Agent ID** của Octave (xem [hướng dẫn Octave](https://octave.ai/docs)).
  - **Input Data**: Workflow tự động lấy dữ liệu từ **Node 1 (Webhook)**.
  - **Output**: Octave trả về **điểm số qualification** (score) và **phân loại lead** (good/bad fit).

##### **🔹 Node 3: Filter Qualified Leads**
- **Cấu hình**:
  - **Filter Condition**: Thay đổi **threshold** để loại bỏ lead có điểm số thấp.
    - Ví dụ: Chỉ giữ lead có `score > 5` (thay đổi trong **Filter** node).
    - Cách thiết lập:
      1. Nhấn **"Add Filter"** trong node Filter.
      2. Chọn `score` (trường trả về từ Octave).
      3. Đặt điều kiện: `> 5` (hoặc số điểm phù hợp với ICP của doanh nghiệp).
  - **Lưu ý**: Nếu không cấu hình, tất cả lead sẽ được chuyển sang Node 4.

##### **🔹 Node 4: Enrich Lead with Context**
- **Cấu hình**:
  - **Credentials**: Chọn `octaveApi` (giống Node 2).
  - **Operation**: Đặt thành `enrichPerson` (không cần thay đổi).
  - **Agent ID**: Giữ nguyên **Agent ID** của Octave (cùng với Node 2).
  - **Input Data**: Lấy dữ liệu từ **Node 3 (Filter)**.
  - **Output**: Octave bổ sung thông tin chi tiết như:
    - **Pain points** (vấn đề đau đầu của lead).
    - **Value propositions** (giá trị công ty mang lại).
    - **References** (tham chiếu từ khách hàng tương tự).
    - **Responsibilities** (vai trò của lead trong công ty).

##### **🔹 Node 5: Send Enriched Lead Alert (Slack)**
- **Cấu hình**:
  - **Credentials**: Chọn `slackOAuth2Api` (đã cấu hình trước khi import).
  - **Channel**: Thay thế `#sales-leads` bằng **channel Slack** muốn nhận cảnh báo.
  - **Message Format**: Workflow tự động tạo **message Slack** với thông tin:
    ```markdown
    *🚀 Lead mới được xác minh:*
    **Tên**: {{ $node["Inbound Lead Webhook"].json["name"] }}
    **Email**: {{ $node["Inbound Lead Webhook"].json["email"] }}
    **Điểm số**: {{ $node["Qualify Lead with Octave"].json["score"] }}/10
    **Pain points**: {{ $node["Enrich Lead with Context"].json["painPoints"] }}
    **Giá trị công ty**: {{ $node["Enrich Lead with Context"].json["valuePropositions"] }}
    **Tham chiếu**: {{ $node["Enrich Lead with Context"].json["references"] }}
    **Link CRM**: [Đường dẫn CRM](https://crm-doanhnghiep.com/lead/{{ $node["Inbound Lead Webhook"].json["id"] }})
    ```
  - **Lưu ý**:
    - Nếu muốn **customize format**, các sếp có thể chỉnh sửa **template message** trong node Slack.
    - Thêm **emoji** hoặc **button** để tương tác (ví dụ: "Xác nhận lead", "Bỏ qua").

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **dữ liệu mẫu lead** qua webhook (ví dụ: bằng Postman hoặc cURL).
   - Kiểm tra **Slack** để xem thông báo có xuất hiện không.
   - Kiểm tra **Octave Dashboard** để xác nhận lead đã được **qualify** và **enrich**.

2. **Bật Active**:
   - Sau khi test thành công, chuyển **status** của workflow từ **"Inactive"** sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với CRM**:
   - Sau khi nhận lead từ Slack, **auto-add** vào CRM (ví dụ: HubSpot, Salesforce) bằng **n8n CRM nodes**.
   - Cách làm:
     - Thêm **node HubSpot** hoặc **Salesforce** sau node Slack.
     - Sử dụng **API key** của CRM và **mapping fields** (ví dụ: `email` → `email`, `score` → `lead_score`).

2. **Lưu Log & Analytics**:
   - Thêm **node StickyNote** (đã có trong workflow) để **ghi lại lịch sử lead**.
   - Sử dụng **n8n Database nodes** (PostgreSQL, MongoDB) để lưu dữ liệu lead dài hạn.
   - **Báo cáo định kỳ**: Tạo workflow khác để gửi **tổng hợp lead** hàng tuần qua Email hoặc Slack.

3. **Tự động Gọi Điện**:
   - Kết hợp với **Twilio** hoặc **CallFire** để **auto-call** lead sau khi nhận cảnh báo Slack.
   - Cách làm:
     - Thêm **node Twilio** sau node Slack.
     - Sử dụng **SMS/Call API** để gọi điện tự động với **script chuẩn bị** (ví dụ: "Xin chào, tôi là [Tên], từ [Công Ty]. Tôi có thể hỗ trợ bạn về [Pain Point] không?").

4. **Cảnh Báo Trực Tuyến**:
   - Thay vì Slack, các sếp có thể gửi cảnh báo qua:
     - **Email** (n8n Email node).
     - **Telegram** (n8n Telegram node).
     - **Microsoft Teams** (n8n Teams node).

5. **Tối Ưu Hóa Octave**:
   - **Customize qualification rules** tại Octave để phù hợp với ICP của doanh nghiệp.
   - **Thêm fields enrichment**: Ví dụ, yêu cầu Octave bổ sung **budget**, **timeline**, hoặc **competitors** của lead.
   - **A/B Testing**: Sử dụng **nhiều Agent ID** khác nhau để so sánh chất lượng enrichment.

6. **Tự Động Xóa Lead Trùng Lặp**:
   - Thêm **node Filter** trước Node 2 để loại bỏ lead đã tồn tại trong CRM.
   - Cách làm:
     - Sử dụng **n8n Database node** để check lead đã tồn tại.
     - Nếu tồn tại, **skip** lead đó.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa 100% quá trình qualification & enrichment lead**.
✔ **Tiết kiệm thời gian** cho đội Sales để tập trung vào **gọi điện và đóng giao dịch**.
✔ **Nâng cao chất lượng lead** với thông tin chi tiết từ AI Octave.
✔ **Cảnh báo tức thời** qua Slack, không bỏ lỡ lead nào.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động chính xác.
3. **Bật Active** và **nhận lead "sẵn sàng bán"** mỗi ngày!

---
:::note[💡 CHÚ Ý CUỐI CÙNG]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow chạy **24/7** mà không phụ thuộc vào n8n.io.
- **Octave API** có giới hạn call (check [Octave Pricing](https://octave.ai/pricing)).
- **Slack OAuth Token** cần **quyền cao** (ví dụ: `chat:write`, `files:write`) để gửi thông báo.
- **Cập nhật thường xuyên**: Octave và n8n có thể update API, các sếp nên **check định kỳ** để cập nhật workflow.

**🚀 CÓ THỂ BẮT ĐẦU NGAY!** [Tải workflow từ n8n.io](https://n8n.io/workflows/7615)
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPS