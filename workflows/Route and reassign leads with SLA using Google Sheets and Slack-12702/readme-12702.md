---
title: "🚀 Tự Động Hóa Phân Phối & Tái Phân Phối Lead Theo SLA (Google Sheets + Slack) - Không Cần Code"
description: "Workflow tự động phân phối lead mới cho đội ngũ bán hàng theo vòng tròn (Round Robin), theo dõi SLA 1 giờ, tái phân phối tự động và cảnh báo Slack. Giúp tăng tốc độ phản hồi, giảm bỏ lead bị bỏ quên và tối ưu hóa công việc bán hàng."
slug: "tieu-dong-hoa-phan-phoi-tai-phan-phoi-lead-theo-sla"
tags: [n8n, automation, lead nurturing, google-sheets, slack, no-code, sales-automation]
keywords: [n8n workflow lead routing, tự động hóa phân phối lead, SLA automation, Slack notification, Google Sheets CRM]
---

# 🚀 **Tự Động Hóa Phân Phối & Tái Phân Phối Lead Theo SLA (Google Sheets + Slack)**

### **Giải pháp tự động hóa 100% không code cho đội ngũ bán hàng**
Bạn đã từng gặp phải tình trạng lead mới bị "ngủ quên" trong hệ thống? Hoặc phải mất thời gian thủ công phân phối lead cho từng thành viên trong đội ngũ bán hàng? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **Route and Reassign Leads with SLA**, các sếp có thể:
✅ **Phân phối lead mới tự động** theo vòng tròn (Round Robin) cho từng thành viên trong đội ngũ.
✅ **Theo dõi SLA 1 giờ** và **tái phân phối tự động** nếu lead chưa được xử lý.
✅ **Cảnh báo Slack** với nút tương tác để cập nhật trạng thái lead một cách nhanh chóng.
✅ **Cảnh báo Escalation** khi lead bị bỏ quên quá nhiều lần (tránh lead bị mất).

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phân phối lead thủ công, giảm thiểu công việc lặp lại.
- **Tăng tốc độ phản hồi**: Lead được xử lý trong vòng 1 giờ, tránh tình trạng "ngủ quên".
- **Công bằng phân phối**: Round Robin đảm bảo mỗi thành viên đều có cơ hội xử lý lead.
- **Cảnh báo tự động**: Slack thông báo và yêu cầu xác nhận, giúp theo dõi dễ dàng.
- **Escalation tự động**: Khi lead bị bỏ quên quá nhiều lần, hệ thống cảnh báo quản lý.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ danh sách lead và thành viên bán hàng).
2. **Tài khoản Slack** (để gửi thông báo và nút tương tác).
3. **API Key OAuth 2.0** của Google Sheets (để kết nối với Sheets).
4. **Credentials Slack API** (để gửi thông báo và tương tác).
5. **Danh sách thành viên bán hàng** (trong Google Sheets, cột `sales_list`).
6. **Danh sách lead** (trong Google Sheets, cột `leads`).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/12702](https://n8n.io/workflows/12702) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12702) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **3 phần chính**:
- **Phân phối lead mới** (Round Robin).
- **Theo dõi SLA và tái phân phối tự động**.
- **Cảnh báo Slack và Escalation**.

##### **A. Cấu hình Google Sheets**
1. **Tạo 2 Sheet trong Google Sheets**:
   - **Sheet 1**: Danh sách thành viên bán hàng (`sales_list`).
     - Cột `name` (tên thành viên).
     - Cột `email` (email liên lạc).
     - Cột `assigned_leads` (số lead đã được phân phối).
   - **Sheet 2**: Danh sách lead (`leads`).
     - Cột `lead_id` (ID lead).
     - Cột `name` (tên lead).
     - Cột `stage` (trạng thái: NEW, CONTACTED, ESCALATED).
     - Cột `assigned_to` (thành viên được phân phối).
     - Cột `last_contacted` (thời gian cuối cùng được liên lạc).
     - Cột `routing_state` (biến để theo dõi vòng phân phối).

2. **Chỉnh node `3) Get Sales List` và `8) Upsert Lead`**:
   - Điền **ID Sheet** và **Range** (ví dụ: `sales_list!A1:D100`).
   - Đảm bảo cột `assigned_leads` được tính toán tự động.

3. **Chỉnh node `5) Get routing_state`**:
   - Range phải trùng với cột `routing_state` trong `leads`.

##### **B. Cấu hình Slack**
1. **Tạo Credentials Slack API**:
   - Vào **Credentials** trong n8n → Thêm **Slack API**.
   - Chọn **Slack Workspace** và cấp quyền cho n8n.

2. **Chỉnh node `9) Slack Notify (New Lead) & Button`**:
   - Chọn **Channel** (ví dụ: `#sales-leads`).
   - Cấu hình **Message Template** để hiển thị thông tin lead mới:
     ```json
     {
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*New Lead:* <${$jsonPath("$.name")}|${$jsonPath("$.name")}>"
           }
         },
         {
           "type": "actions",
           "elements": [
             {
               "type": "button",
               "text": {
                 "type": "plain_text",
                 "text": "Mark as CONTACTED"
               },
               "url": "https://your-n8n-instance/webhook/demo-stage-update?lead_id=${$jsonPath("$.lead_id")}"
             }
           ]
         }
       ]
     }
     ```

3. **Chỉnh node `🚨 SLACK ESCALATION`**:
   - Chọn **Channel** (ví dụ: `#sales-escalation`).
   - Cấu hình **Message Template** để thông báo Escalation:
     ```json
     {
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*ESCALATION:* Lead <${$jsonPath("$.name")}|${$jsonPath("$.name")}> đã bị bỏ quên quá nhiều lần!"
           }
         }
       ]
     }
     ```

##### **C. Cấu hình SLA Trigger**
1. **Chỉnh node `SLA Trigger (every 1 hour)`**:
   - Đặt **Schedule** là `0 * * * *` (chạy mỗi giờ).
   - Đảm bảo **Active** được bật.

2. **Chỉnh node `SLA) Get Leads (stage=NEW)`**:
   - Range phải trùng với cột `leads` trong Google Sheets.
   - Thêm **Filter Query** để lấy chỉ lead ở trạng thái `NEW`:
     ```json
     {
       "stage": "NEW"
     }
     ```

##### **D. Cấu hình Webhook (STAGE Update)**
1. **Chỉnh node `STAGE) Webhook (/demo-stage-update)`**:
   - Đảm bảo **Path** là `/demo-stage-update`.
   - **HTTP Method** là `POST`.
   - **Active** phải được bật.

2. **Chỉnh node `STAGE) Update lead stage to CONTACTED`**:
   - Range phải trùng với cột `leads`.
   - **Operation** là `update`.
   - **Key Parameters**:
     ```json
     {
       "stage": "CONTACTED",
       "last_contacted": "$$NOW"
     }
     ```

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **Run Workflow** để kiểm tra.
   - Điền dữ liệu mẫu vào **Form Trigger** và kiểm tra kết quả.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** cho tất cả workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với CRM khác**:
   - Thay thế Google Sheets bằng **Salesforce, HubSpot, hoặc PostgreSQL** bằng cách sử dụng **HTTP Request** hoặc **n8n nodes** tương ứng.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **Schedule Trigger** để gửi báo cáo số lead đã được xử lý, lead đang chờ, và lead bị Escalation qua **Email** hoặc **Slack**.

3. **Thêm tính năng chatbot**:
   - Kết nối với **Google Dialogflow** hoặc **Rasa** để tự động trả lời lead mới trước khi chuyển cho bán hàng.

4. **Lưu log hoạt động**:
   - Sử dụng **n8n-nodes-base.stickyNote** để ghi lại lịch sử phân phối và tái phân phối lead.

5. **Tùy chỉnh SLA**:
   - Thay đổi **Schedule Trigger** từ `1 giờ` sang `2 giờ` hoặc `3 giờ` tùy nhu cầu.
:::

---
### 📌 **Kết luận**
Workflow **Route and Reassign Leads with SLA** là giải pháp **tự động hóa hoàn chỉnh** cho việc phân phối và tái phân phối lead, giúp đội ngũ bán hàng **tăng tốc độ phản hồi**, **giảm lead bị bỏ quên** và **tối ưu hóa công việc**.

👉 **Hãy import ngay và thử nghiệm!** Nếu có vấn đề, các sếp có thể liên hệ với tác giả [Muh Resky Adiansyah](https://n8n.io/workflows/12702) để hỗ trợ.

---
:::note[CHÚ Ý]
- **Không cần code**: Workflow này hoàn toàn không cần viết mã, chỉ cần cấu hình các node.
- **Self-hosted**: Để workflow chạy 24/7 ổn định, các sếp nên cài **n8n trên VPS** (không phụ thuộc vào phiên bản miễn phí).
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với việc tự động hóa bán hàng!** 🚀