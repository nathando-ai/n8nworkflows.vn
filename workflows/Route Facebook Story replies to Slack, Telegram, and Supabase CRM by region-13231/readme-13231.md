---
title: "🚀 Tự Động Hóa Trả Lời Story Facebook Sang Slack, Telegram & CRM Supabase Theo Khu Vực - Giảm Thời Gian Phản Hồi 90%"
description: "Workflow này tự động nhận trả lời Story Facebook, phân loại và chuyển đến Slack/Telegram theo khu vực (Á/Âu) và lưu vào CRM Supabase, giúp đội ngũ hỗ trợ phản hồi nhanh chóng 24/7 mà không cần code."
slug: "tu-dong-hoa-tra-loi-story-facebook-sang-slack-telegram-supabase"
tags: [n8n, automation, no-code, facebook-marketing, slack-integration, telegram-bot, supabase-crm, ticket-management]
keywords: [n8n workflow facebook story, tự động hóa trả lời story facebook, CRM Supabase, Slack Telegram integration, phân loại hỗ trợ theo khu vực, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Trả Lời Story Facebook Sang Slack, Telegram & CRM Supabase Theo Khu Vực**

### **Giải Phóng Tay Đội Ngũ Hỗ Trợ: Từ "Chờ Đợi" Sang "Phản Hồi Ngay"**
Hiện nay, khi khách hàng gửi trả lời Story Facebook, đội ngũ hỗ trợ thường phải **quét qua hàng chục tin nhắn**, phân loại theo khu vực (Á/Âu) và chuyển tiếp thủ công sang Slack/Telegram. Kết quả? **Thời gian phản hồi kéo dài, khách hàng mất niềm tin, và công việc trở nên rắc rối**. Workflow này **tự động hóa toàn bộ quy trình** – từ nhận tin nhắn đến phân loại, chuyển tiếp và lưu vào CRM – giúp các sếp **giảm thời gian phản hồi xuống còn 1-2 phút**, đồng thời **tối ưu hóa công việc cho đội ngũ**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Phản hồi ngay lập tức**: Trả lời Story Facebook trong vòng **1-2 phút** thay vì mất giờ quét tin nhắn.
✅ **Phân loại tự động theo khu vực**: Á/Âu được chuyển đến đội ngũ hỗ trợ phù hợp, **không sai khu vực**.
✅ **Lưu trữ toàn bộ lịch sử**: Tất cả tin nhắn được ghi vào **CRM Supabase**, dễ theo dõi và báo cáo.
✅ **Thông báo đa kênh**: **Slack + Telegram** đồng thời, giúp đội ngũ **không bỏ lỡ tin nhắn nào**.
✅ **Tối ưu hóa công việc**: **Không cần code**, chỉ cần cấu hình vài bước là hoạt động.
✅ **Hoạt động 24/7**: Workflow chạy tự động, **không cần người quản lý**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
📌 **Tài khoản & API Keys**:
- **Facebook Developer Account** (để lấy **Webhook URL** và **Page Access Token**).
- **Slack Workspace** (để lấy **Slack API Token** và **Channel ID**).
- **Telegram Bot Token** (để lấy **Chat ID** của nhóm/đội ngũ).
- **Supabase Account** (để tạo **Database** và **Table** lưu tin nhắn).

📌 **Cấu trúc Database Supabase**:
- Table: `facebook_story_replies` (cần các cột: `id`, `sender_id`, `message`, `story_id`, `status`, `assigned_team`, `timezone`).
- Table: `support_teams` (để lưu thông tin đội ngũ Á/Âu).

📌 **Thời gian hỗ trợ**:
- Cần xác định **giờ mở cửa** của đội ngũ Á/Âu (ví dụ: Á: 9h-18h UTC+7, Âu: 9h-18h UTC+1).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13231](https://n8n.io/workflows/13231) hoặc copy toàn bộ JSON từ link trên.
- Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Kích hoạt chế độ "Active"** sau khi import xong.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **11 node**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Facebook Story Reply Webhook**
- **Cấu hình Webhook**:
  - **Path**: `facebook-story-reply` (không đổi).
  - **HTTP Method**: `POST`.
  - **URL Webhook**: Lấy từ **Facebook Developer Dashboard** (cần tạo **Webhook Subscription** cho Page của bạn).
  - **Verify Token**: Đặt một **token ngẫu nhiên** (ví dụ: `my_secret_token`) và **cấu hình trên Facebook Developer** để xác thực.

##### **B. Time-Zone Router (Node Function)**
- **Mục đích**: Phân loại tin nhắn theo **giờ UTC** để chuyển đến đội ngũ Á/Âu.
- **Cấu hình**:
  - Mở node **Time-Zone Router** → **Edit Code**.
  - Sửa logic để phù hợp với **giờ mở cửa** của đội ngũ (ví dụ:
    ```javascript
    if (new Date().getHours() >= 9 && new Date().getHours() < 18) {
      // Á: UTC+7
      if (new Date().getUTCHours() >= 2 && new Date().getUTCHours() < 15) {
        return { path: "telegram-notify-human" }; // Á
      }
    } else if (new Date().getHours() >= 9 && new Date().getHours() < 18) {
      // Âu: UTC+1
      if (new Date().getUTCHours() >= 8 && new Date().getUTCHours() < 23) {
        return { path: "slack-notify-human" }; // Âu
      }
    }
    return { path: "unassigned-path" }; // Nếu ngoài giờ
    ```
  - **Lưu ý**: Cần **chuyển đổi UTC** để phù hợp với múi giờ của đội ngũ.

##### **C. Supabase Credentials**
- **Cấu hình Supabase**:
  - Đăng nhập vào **Supabase Dashboard** → **Project Settings** → **API**.
  - Sao chép **Anon Key** hoặc **Service Role Key** và điền vào **n8n Credentials** (tên: `supabaseApi`).
  - **Table Name**: Đặt là `facebook_story_replies` (phù hợp với cấu trúc trước đó).

##### **D. Slack & Telegram Notifications**
- **Slack**:
  - Tạo **App Slack** → Lấy **Bot Token** và **Channel ID**.
  - Điền vào **n8n Credentials** (tên: `slackApi`).
  - **Message Format**: Sửa nội dung thông báo (ví dụ:
    ```
    *New Facebook Story Reply!*
    **Sender**: {{ $node["Normalize Story Reply Payload"].json["sender_id"] }}
    **Message**: {{ $node["Normalize Story Reply Payload"].json["message"] }}
    **Status**: {{ $node["Assignment Successful?"].json["status"] }}
    ```
  - **Lưu ý**: Cần **định dạng JSON** để hiển thị thông tin rõ ràng.

- **Telegram**:
  - Tạo **Bot Telegram** (trên [@BotFather](https://t.me/BotFather)) → Lấy **API Token**.
  - Điền vào **n8n Credentials** (tên: `telegramApi`).
  - **Chat ID**: Lấy từ **@RawDataBot** (gửi tin nhắn "start" và copy ID).
  - **Message Format**: Tương tự Slack, nhưng **không hỗ trợ markdown** (sử dụng văn bản thô).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **tin nhắn mẫu** từ Facebook Story (sử dụng **Postman** hoặc **công cụ mock API**).
  - Kiểm tra:
    - Tin nhắn có được **lưu vào Supabase** không?
    - **Slack/Telegram** có nhận được thông báo không?
    - **Phân loại khu vực** có chính xác không?
- **Bật Active**:
  - Sau khi test thành công, **bật chế độ Active** trong n8n.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Tất Cả Sự Kiện**:
   - Thêm **node `stickyNote`** để ghi lại **lịch sử hoạt động** (ví dụ: "Tin nhắn #123 đã được chuyển đến đội ngũ Á").
   - **Cách làm**:
     ```javascript
     // Trong node Function "Time-Zone Router", thêm:
     $node.set("log", {
       message: "Tin nhắn đã được phân loại và chuyển đến " + (assignedTeam === "Asia" ? "Á" : "Âu"),
       timestamp: new Date().toISOString()
     });
     ```

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `set` + `schedule`** để gửi **báo cáo hàng ngày** về số lượng tin nhắn chưa xử lý.
   - **Cách làm**:
     - Tạo **workflow mới** với **node `schedule`** (chạy hàng ngày 9h sáng).
     - Query **Supabase** để lấy tin nhắn `status = "unassigned"`.
     - Gửi **Slack/Telegram** báo cáo.

3. **Kết Hợp Với CRM Khác**:
   - Nếu sử dụng **Zoho/HubSpot**, thay thế **Supabase** bằng **Zoho API** hoặc **HubSpot API**.
   - **Cách làm**:
     - Thay node `supabase` bằng `zoho` hoặc `hubspot`.
     - Cấu hình **credentials** tương ứng.

4. **Tự Động Trả Lời Khách Hàng**:
   - Thêm **node `if`** để **trả lời tự động** tin nhắn nhất định (ví dụ: "Cảm ơn bạn đã liên hệ!").
   - **Cách làm**:
     ```javascript
     if ($node.input.data.message.includes("cảm ơn")) {
       return { path: "facebook-reply" };
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng đội ngũ hỗ trợ** khỏi công việc lặp lại, **tăng tốc độ phản hồi** và **tối ưu hóa quản lý tin nhắn**. Với **n8n**, các sếp **không cần code** mà vẫn có thể tự động hóa quy trình phức tạp như phân loại theo khu vực, chuyển tiếp đa kênh và lưu trữ dữ liệu.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với tin nhắn mẫu** trước khi chuyển sang hoạt động thực tế.
3. **Bật Active** và **theo dõi kết quả**!

🚀 **Kết quả?** **Phản hồi nhanh hơn 90%, đội ngũ tập trung vào chất lượng hơn, và khách hàng hài lòng hơn!**

---
**Cần hỗ trợ thêm?** Đăng ký **hỗ trợ kỹ thuật n8n** tại [n8n Community](https://community.n8n.io/) hoặc liên hệ **TinoHost** để tư vấn cài đặt VPS ổn định!