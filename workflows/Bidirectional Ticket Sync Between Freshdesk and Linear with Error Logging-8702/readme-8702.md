---
title: "🔄 **Tự Động Hóa Đồng Bộ Ticket Giúp Freshdesk & Linear Hợp Lực 100% – Không Cần Code!** 🚀"
description: "Workflow này tự động đồng bộ hóa hai chiều giữa Freshdesk (hệ thống hỗ trợ khách hàng) và Linear (quản lý công việc), giảm thiểu sai sót, tiết kiệm thời gian và đảm bảo dữ liệu luôn nhất quán. Phù hợp cho các startup, team hỗ trợ khách hàng và doanh nghiệp cần quản lý ticket hiệu quả."
slug: "tieu-dong-bo-ticket-freshdesk-linear"
tags: [n8n, automation, no-code, Freshdesk, Linear, ticket-sync, error-logging, API-integration]
keywords: [tự động hóa Freshdesk Linear, đồng bộ ticket hai chiều, n8n workflow, quản lý hỗ trợ khách hàng, giảm thời gian làm việc, audit log]
---

# 🔄 **Tự Động Hóa Đồng Bộ Ticket Giúp Freshdesk & Linear Hợp Lực – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Quản Lý Ticket Thủ Công**
Các sếp đã từng gặp phải tình huống này chưa?
- **Sai sót dữ liệu**: Khi chuyển đổi ticket từ Freshdesk sang Linear (hoặc ngược lại), thông tin như **trạng thái, ưu tiên, mô tả** dễ bị mất hoặc sai lệch.
- **Tốn thời gian**: Phải copy-paste thông tin giữa hai hệ thống, làm chậm quá trình phản hồi khách hàng.
- **Không theo dõi được lỗi**: Khi có lỗi trong quá trình đồng bộ, khó khăn để debug và khắc phục.
- **Không đồng bộ hai chiều**: Nếu chỉ đồng bộ một chiều (ví dụ, Freshdesk → Linear), khi Linear được cập nhật, Freshdesk sẽ không biết và dẫn đến **dữ liệu không nhất quán**.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Đồng bộ hai chiều** giữa Freshdesk và Linear (khi ticket được tạo hoặc cập nhật ở Freshdesk, nó tự động đồng bộ sang Linear và ngược lại).
✅ **Chuyển đổi tự động** các trường dữ liệu (ví dụ: **trạng thái "Open" → "todo"**, **ưu tiên "Urgent" → "1"**).
✅ **Ghi log lỗi chi tiết** để các sếp dễ dàng theo dõi và khắc phục vấn đề.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy 24/7.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải copy-paste ticket giữa hai hệ thống nữa.
- **Dữ liệu chính xác**: Trạng thái, ưu tiên và mô tả được đồng bộ tự động, giảm thiểu sai sót.
- **Hỗ trợ khách hàng nhanh chóng**: Khi ticket được cập nhật ở Linear, Freshdesk sẽ tự động phản ánh, giúp team phản hồi kịp thời.
- **Theo dõi lỗi dễ dàng**: Tất cả lỗi đồng bộ được ghi log chi tiết, giúp các sếp debug nhanh chóng.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Freshdesk** và **Linear**:
   - API Key của Freshdesk (tạo từ **Admin → API Keys**).
   - API Token của Linear (tạo từ **Settings → API Tokens**).
2. **Webhook URL** của Freshdesk và Linear:
   - Cấu hình **Webhook URL** trong Freshdesk để gửi dữ liệu khi ticket được tạo hoặc cập nhật.
   - Cấu hình **Webhook URL** trong Linear để nhận thông báo khi issue được cập nhật.
3. **Credentials trong n8n**:
   - Tạo **credentials** cho Freshdesk và Linear trong n8n (để lưu trữ API Key/Token an toàn).
4. **Dịch vụ n8n**:
   - **Self-hosted n8n** (khuyến nghị) để workflow chạy ổn định 24/7.
   - **N8n Cloud** (nếu không muốn tự host).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/8702).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **14 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **🗺️ Node "Map Freshdesk Fields to Linear" (Function)**
- **Chức năng**: Chuyển đổi trường dữ liệu từ Freshdesk sang Linear (ví dụ: trạng thái, ưu tiên).
- **Cấu hình**:
  - Đảm bảo **mapping trường** chính xác (ví dụ: `status` ở Freshdesk → `state` ở Linear).
  - Cấu hình **ưu tiên**:
    - Freshdesk: `Low` → Linear: `4`, `Medium` → `3`, `High` → `2`, `Urgent` → `1`.
  - Cấu hình **trạng thái**:
    - Freshdesk: `Open` → Linear: `todo`, `Pending` → `in_progress`, `Resolved` → `done`, `Closed` → `canceled`.

##### **🎯 Node "Create Linear Issue" (HTTP Request)**
- **Chức năng**: Gửi yêu cầu API để tạo issue mới ở Linear.
- **Cấu hình**:
  - **URL**: `https://api.linear.app/graphql`.
  - **Headers**:
    - `Authorization`: `Bearer <API_TOKEN_LINEAR>` (điền từ credentials).
    - `Content-Type`: `application/json`.
  - **Body (GraphQL Mutation)**:
    ```json
    {
      "query": "mutation CreateIssue($input: CreateIssueInput!) { createIssue(input: $input) { issue { id } } }",
      "variables": {
        "input": {
          "title": "{{ $node["🗺️ Map Freshdesk Fields to Linear"].json["title"] }}",
          "description": "{{ $node["🗺️ Map Freshdesk Fields to Linear"].json["description"] }}",
          "state": "{{ $node["🗺️ Map Freshdesk Fields to Linear"].json["state"] }}",
          "priority": "{{ $node["🗺️ Map Freshdesk Fields to Linear"].json["priority"] }}"
        }
      }
    }
    ```

##### **✅ Node "Check Linear Creation Success" (If)**
- **Chức năng**: Kiểm tra nếu tạo issue ở Linear thành công.
- **Cấu hình**:
  - **Condition**: Kiểm tra `data.createIssue.issue.id` có tồn tại không.
  - Nếu thành công → tiếp tục node **"🔗 Link Freshdesk with Linear ID"**.
  - Nếu thất bại → chuyển sang node **"❌ Log Linear Creation Error"**.

##### **🔗 Node "Link Freshdesk with Linear ID" (HTTP Request)**
- **Chức năng**: Cập nhật ticket ở Freshdesk với ID của issue ở Linear (để đồng bộ hai chiều).
- **Cấu hình**:
  - **URL**: `https://<subdomain>.freshdesk.com/api/v2/tickets/<ticket_id>`.
  - **Headers**:
    - `Authorization`: `Basic <API_KEY_FRESHDESK>` (điền từ credentials).
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "ticket": {
        "custom_fields": [
          {
            "id": "<ID_CUSTOM_FIELD_LINEAR_ID>",
            "value": "{{ $node["✅ Check Linear Creation Success"].json["linearIssueId"] }}"
          }
        ]
      }
    }
    ```

##### **📄 Node "Map Linear to Freshdesk Fields" (Function)**
- **Chức năng**: Chuyển đổi trường dữ liệu từ Linear sang Freshdesk (ngược lại với node đầu tiên).
- **Cấu hình**:
  - Đảm bảo **mapping trường** chính xác (ví dụ: `state` ở Linear → `status` ở Freshdesk).
  - Cấu hình **ưu tiên**:
    - Linear: `1` → Freshdesk: `Urgent`, `2` → `High`, `3` → `Medium`, `4` → `Low`.
  - Cấu hình **trạng thái**:
    - Linear: `todo` → Freshdesk: `Open`, `in_progress` → `Pending`, `done` → `Resolved`, `canceled` → `Closed`.

##### **🎣 Webhook Triggers**
- **New Ticket Webhook** (`POST /create-ticket`):
  - Cấu hình trong Freshdesk để gửi dữ liệu khi ticket mới được tạo.
- **Update Ticket Webhook** (`POST /update-ticket`):
  - Cấu hình trong Freshdesk để gửi dữ liệu khi ticket được cập nhật.
- **Linear Issue Updated Webhook** (`POST /linear-issue-updated`):
  - Cấu hình trong Linear để gửi thông báo khi issue được cập nhật.

##### **📌 Node Logging (✅/❌)**
- **Log Linear Creation Success/Error**:
  - Ghi log thành công/thất bại vào **Google Sheets** hoặc **Slack** (các sếp có thể cấu hình).
- **Log Freshdesk Update Success/Error**:
  - Ghi log cập nhật ticket ở Freshdesk thành công/thất bại.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Tạo một ticket mẫu ở Freshdesk và kiểm tra xem nó có được đồng bộ sang Linear không.
   - Cập nhật ticket ở Linear và kiểm tra xem nó có được đồng bộ về Freshdesk không.
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, các sếp có thể **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram**:
   - Cấu hình node **Slack** hoặc **Telegram Bot** để gửi thông báo khi ticket được đồng bộ thành công/thất bại.
   - Ví dụ:
     ```json
     {
       "text": "Ticket {{ $node["🎯 Create Linear Issue"].json["ticketId"] }} đã được đồng bộ sang Linear thành công!"
     }
     ```
2. **Lưu log vào Google Sheets**:
   - Sử dụng node **Google Sheets** để ghi log tất cả hoạt động đồng bộ vào một bảng Excel.
   - Có thể cấu hình để tự động tạo báo cáo hàng ngày.
3. **Kết hợp với AI (LLM)**:
   - Sử dụng node **OpenAI** để tự động phân loại ticket hoặc tạo mô tả chi tiết khi ticket mới được tạo.
   - Ví dụ:
     ```json
     {
       "prompt": "Tóm tắt vấn đề từ mô tả ticket sau: {{ $node["New Ticket Webhook"].json["description"] }}",
       "model": "gpt-3.5-turbo"
     }
     ```
4. **Báo cáo định kỳ**:
   - Sử dụng node **Google Calendar** hoặc **Email** để gửi báo cáo tổng hợp về số lượng ticket đồng bộ mỗi ngày.
5. **Xử lý lỗi tự động**:
   - Cấu hình node **Retry** để tự động thử lại nếu API thất bại (ví dụ, sau 5 giây).
---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa đồng bộ ticket giữa Freshdesk và Linear **không cần viết code**. Bằng cách cấu hình một lần, workflow sẽ chạy **24/7**, giảm thiểu sai sót, tiết kiệm thời gian và đảm bảo dữ liệu luôn nhất quán.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** và webhook.
3. **Test run** và **bật workflow** để bắt đầu tự động hóa!

Nếu các sếp gặp khó khăn trong quá trình cấu hình, hãy liên hệ với **iTechNotion** (tác giả của workflow) qua [đây](https://itechnotion.com/) để được hỗ trợ!

---
**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!**