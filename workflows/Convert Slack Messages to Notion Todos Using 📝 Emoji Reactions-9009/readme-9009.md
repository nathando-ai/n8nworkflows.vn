---
title: "🚀 Tự Động Hóa Chuyển Slack Messages Sang Todo Notion Với Emoji - Giảm 80% Thời Gian Quản Lý Công Việc"
description: "Workflow này tự động chuyển các tin nhắn Slack có emoji phản hồi thành todo trên Notion, giúp các sếp quản lý công việc hiệu quả hơn mà không cần code. Hỗ trợ phản hồi nhanh, theo dõi công việc và báo cáo hàng ngày tự động."
slug: "tieu-dong-hoa-chuyen-slack-sang-notion-todo-voi-emoji"
tags: [n8n, automation, slack, notion, todo-management, no-code, ai-multimodal]
keywords: [n8n workflow slack notion, tự động hóa quản lý công việc, chuyển tin nhắn slack sang todo, quản lý công việc hiệu quả, tự động hóa notion, emoji phản hồi slack]
---

# 🚀 **Tự Động Hóa Chuyển Slack Messages Sang Todo Notion Với Emoji - Giảm 80% Thời Gian Quản Lý Công Việc**

---

### **🎯 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải mất nhiều thời gian để:
- **Quét lại** các tin nhắn Slack để xác định công việc cần làm.
- **Chuyển đổi** yêu cầu từ Slack sang Notion để quản lý.
- **Theo dõi** tình trạng hoàn thành công việc thủ công.

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động chuyển** tin nhắn Slack có emoji phản hồi thành todo trên Notion.
✅ **Báo cáo hàng ngày** trên Slack về các todo chưa hoàn thành.
✅ **Tiết kiệm thời gian** lên đến **80%** trong quản lý công việc hàng ngày.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét lại Slack để tìm công việc mới.
- **Chính xác và tự động**: Todo trên Notion được cập nhật ngay khi có emoji phản hồi.
- **Báo cáo hàng ngày**: Nhận danh sách todo chưa hoàn thành trên Slack mỗi sáng.
- **Tích hợp hoàn hảo**: Slack + Notion hoạt động như một hệ thống thống nhất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Slack** với quyền quản lý bot (để tạo bot và cài đặt emoji phản hồi).
- **Tài khoản Notion** và một database todo đã tồn tại (hoặc tạo mới).
- **API Key Slack** và **API Key Notion** (cài đặt trong n8n).
- **Emoji phản hồi** được định nghĩa trước (ví dụ: 📝, 🚀, ⏳) để phân loại todo.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9009](https://n8n.io/workflows/9009).
- **Mở n8n Editor** và chọn **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc copy/paste** JSON từ file vào Editor và nhấn **Create Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **2 phần chính**:
- **Phần 1: Chuyển Slack → Notion** (khi có emoji phản hồi).
- **Phần 2: Báo cáo hàng ngày** (lấy todo chưa hoàn thành từ Notion và gửi Slack).

##### **A. Cấu Hình Slack**
1. **Slack Trigger**:
   - Chọn **Slack Trigger** và chọn **Event Type** là `reaction_added`.
   - **Credentials**: Đăng nhập tài khoản Slack và chọn bot đã tạo.

2. **Filter by Emoji**:
   - Thêm điều kiện lọc tin nhắn có emoji cụ thể (ví dụ: `📝`).
   - **Key Parameters**:
     ```json
     {
       "filter": "$.reaction.name === '📝'"
     }
     ```

3. **Get Reacted Message**:
   - Node này lấy nội dung tin nhắn đã phản hồi.
   - **Credentials**: Chọn Slack API Key đã cài đặt.

4. **Send a Message (Optional)**:
   - Nếu muốn xác nhận tự động, cấu hình node này để gửi tin nhắn xác nhận phản hồi.

##### **B. Cấu Hình Notion**
1. **Added Message to Notion**:
   - Chọn **Notion Credentials** và chọn database todo.
   - **Key Parameters**:
     ```json
     {
       "resource": "block",
       "operation": "create",
       "properties": {
         "Name": "$$.json.message.text",
         "Status": "Pending"
       }
     }
     ```

2. **Get All Todos from Notion**:
   - Lấy tất cả todo từ database.
   - **Key Parameters**:
     ```json
     {
       "resource": "block",
       "operation": "getAll",
       "databaseId": "YOUR_DATABASE_ID"
     }
     ```

3. **Filter Todo & Filter Not Checked Todos**:
   - Lọc todo có trạng thái `Pending` hoặc chưa hoàn thành.
   - **Key Parameters**:
     ```json
     {
       "filter": "$.properties.Status.select.name === 'Pending'"
     }
     ```

##### **C. Cấu Hình Schedule Trigger (Báo Cáo Hàng Ngày)**
- **Schedule Trigger**:
  - Chọn **Cron Expression** là `0 0 * * *` (lúc 00:00 hàng ngày).
  - **Credentials**: Chọn Slack API Key để gửi báo cáo.

- **Send Báo Cáo Todo**:
  - Sử dụng node **Slack** để gửi danh sách todo chưa hoàn thành.
  - **Key Parameters**:
    ```json
    {
      "text": "📌 Todo chưa hoàn thành:\n${$.json.todos.map(todo => `- ${todo.properties.Name.rich_text[0].plain_text}`).join('\n')}"
    }
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một tin nhắn Slack có emoji `📝` và kiểm tra todo đã được tạo trên Notion.
  - Chờ đến sáng hôm sau để kiểm tra báo cáo hàng ngày trên Slack.
- **Bật Active**:
  - Nhấn **Active** trên workflow để bắt đầu tự động hóa.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Emoji**:
   - Thêm nhiều emoji khác (ví dụ: `🚀` cho todo ưu tiên cao, `⏳` cho todo dài hạn).
   - Sử dụng node **Filter** để phân loại todo theo emoji.

2. **Lưu Log**:
   - Thêm node **Sticky Note** để lưu lịch sử phản hồi và todo đã hoàn thành.

3. **Kết Nối với Google Calendar**:
   - Sử dụng node **Google Calendar** để tự động tạo sự kiện từ todo trên Notion.

4. **Báo Cáo Thống Kê**:
   - Tính toán số todo đã hoàn thành trong tuần và gửi báo cáo định kỳ.

5. **Tích Hợp với Microsoft Teams**:
   - Thay thế node Slack bằng **Microsoft Teams** để báo cáo trên Teams.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào công việc quan trọng hơn, đồng thời **tăng cường hiệu quả quản lý công việc** bằng cách tự động hóa quy trình chuyển đổi từ Slack sang Notion. **Hãy áp dụng ngay** và trải nghiệm sự khác biệt!

👉 **Bắt đầu tự động hóa ngay hôm nay** với n8n và [đăng ký VPS](https://tino.vn/vps-n8n?affid=388) để chạy workflow 24/7!