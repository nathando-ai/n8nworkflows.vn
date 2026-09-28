---
title: "🧹 **Tự Động Xóa Channel Trống Slack: Audit & Report Inactive Channels Hàng Tuần (Không Cần Code!)**"
description: "Workflow tự động hóa kiểm tra và báo cáo các channel Slack không hoạt động trong 30 ngày, giúp quản trị viên workspace dọn dẹp, tối ưu hóa không gian làm việc và duy trì hiệu quả giao tiếp. Giúp tiết kiệm thời gian lên đến 10 giờ/tháng và giảm rác thải thông tin trong Slack."
slug: "tieu-dong-xoa-channel-trong-slack"
tags: [n8n, automation, slack, no-code, self-hosted, ai-summarization]
keywords: [tự động hóa slack, audit channel slack, report inactive channels, n8n workflow slack, dọn dẹp workspace slack, tự động hóa không cần code]
---

# 🚀 **Tự Động Xóa Channel Trống Slack: Audit & Report Inactive Channels Hàng Tuần**

---
### **Nỗi Đau Của Các Sếp**
Slack là công cụ không thể thiếu trong việc giao tiếp nội bộ, nhưng sau thời gian dài sử dụng, workspace thường bị "lấn át" bởi các channel trống, không hoạt động, hoặc không còn cần thiết. Các quản trị viên phải:
- **Tìm kiếm thủ công** các channel không hoạt động (tốn thời gian).
- **Quên nhớ** kiểm tra định kỳ, dẫn đến workspace bị lộn xộn.
- **Không có báo cáo tự động**, khiến việc quyết định xóa/archiving trở nên khó khăn.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Kiểm tra tất cả channel công khai** hàng tuần.
✅ **Phân loại channel không hoạt động** trong 30 ngày.
✅ **Tạo báo cáo chi tiết** với thông tin về channel (tên, thành viên, mục đích).
✅ **Gửi báo cáo tự động** đến Slack channel quản trị, giúp các sếp **xóa hoặc archiving** channel một cách nhanh chóng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công, workflow chạy tự động hàng tuần.
- **Duy trì workspace sạch sẽ**: Xóa bỏ channel trống, giảm rác thải thông tin.
- **Quản lý hiệu quả**: Báo cáo chi tiết giúp quyết định xóa/archiving một cách khoa học.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động liên tục 24/7.
- **Cá nhân hóa**: Báo cáo bao gồm thông tin chi tiết (tên channel, thành viên, mục đích).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Slack Workspace** và quyền quản trị (Admin).
2. **Slack App** với các **OAuth scopes** sau:
   - `channels:read` → Đọc danh sách channel.
   - `channels:history` → Lấy lịch sử tin nhắn.
   - `chat:write` → Gửi báo cáo về Slack.
   - *(Không bắt buộc)* `users:read` → Lấy thông tin thành viên (nếu muốn báo cáo chi tiết).
3. **Bot Token Slack** (truy cập [Slack API](https://api.slack.com/apps) để tạo).
4. **n8n Self-hosted** (khuyến nghị để đảm bảo tính riêng tư).
5. **Slack channel quản trị** để nhận báo cáo (ví dụ: `#workspace-admin`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7728](https://n8n.io/workflows/7728).
- **Mở n8n Editor** → Nhấn `Import` → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào `Import Workflow` trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Weekly Schedule Trigger (Khởi động hàng tuần)**
- **Cấu hình**:
  - Chọn **thời gian chạy** (ví dụ: **Mỗi thứ Hai lúc 9h sáng**).
  - Đảm bảo **Active** để workflow chạy tự động.

##### **🔹 Node 2: Get Many Channels (Lấy tất cả channel công khai)**
- **Credentials**: Chọn `slackOAuth2Api` (đã cấu hình trước khi import).
- **Lưu ý**:
  - Đảm bảo **OAuth scopes** đã được cấp quyền (`channels:read`).
  - Nếu gặp lỗi, kiểm tra lại **Bot Token** trong Slack App.

##### **🔹 Node 3: Get the History of a Channel (Lấy lịch sử tin nhắn)**
- **Credentials**: Chọn `slackOAuth2Api` (giống Node 2).
- **Lưu ý**:
  - **Không cần cấu hình thêm**, workflow sẽ tự động lấy lịch sử cho từng channel.
  - Đảm bảo **`channels:history`** được cấp quyền.

##### **🔹 Node 4: Filter Channel with Last Discussion 30 Days Ago (Lọc channel không hoạt động)**
- **Cấu hình**:
  - **Thời gian lọc**: Đặt thành **30 ngày** (có thể thay đổi thành 60/90 ngày nếu cần).
  - **Lưu ý**: Node này sẽ **bỏ qua** channel có tin nhắn trong thời gian này.

##### **🔹 Node 5: Collect Expired Channel Information (Thông tin channel trống)**
- **Lưu ý**:
  - Node này **tự động** trích xuất:
    - Tên channel, ID, số thành viên, ngày tạo, mục đích.
  - **Không cần chỉnh sửa**, nhưng có thể mở **Sticky Note** để xem mã nguồn (nếu cần tùy chỉnh).

##### **🔹 Node 6: Consume Slack Report (Tạo báo cáo Markdown)**
- **Lưu ý**:
  - Node này **sắp xếp dữ liệu** thành format báo cáo dễ đọc.
  - **Không cần chỉnh sửa**, nhưng có thể mở **Code Editor** để xem mã và tùy chỉnh:
    ```javascript
    // Ví dụ: Thay đổi format báo cáo (nếu cần)
    return {
      json: {
        "inactive_channels": data.items.map(item => ({
          name: item.name,
          id: item.id,
          members: item.members.length,
          created_at: item.created_at,
          purpose: item.purpose || "Không rõ mục đích"
        }))
      }
    };
    ```

##### **🔹 Node 7: Send Channel Inactivity Report (Gửi báo cáo về Slack)**
- **Credentials**: Chọn `slackApi` (khác với `slackOAuth2Api`).
- **Cấu hình**:
  - **Channel**: Chọn **Slack channel quản trị** (ví dụ: `#workspace-admin`).
  - **Lưu ý**:
    - Đảm bảo **`chat:write`** được cấp quyền.
    - Báo cáo sẽ được gửi dưới dạng **Markdown** (dễ đọc và chia sẻ).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** để kiểm tra với dữ liệu mẫu.
  - Kiểm tra **Slack channel** đã chọn để xem báo cáo có xuất hiện không.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tự động archiving channel**:
   - Thêm **node Slack API** để **xóa/archiving** channel không hoạt động (ví dụ: channel có <3 thành viên và không hoạt động 60 ngày).
   - **Cách làm**:
     ```javascript
     // Thêm vào Node Code sau "Collect Expired Channel Information"
     return {
       json: {
         "channels_to_archive": data.items
           .filter(item => item.members.length < 3)
           .map(item => ({
             id: item.id,
             action: "archive"
           }))
       }
     };
     ```
   - Sau đó, thêm **node Slack API** với `operation: archive` để thực hiện.

2. **Gửi báo cáo qua Email**:
   - Thêm **node Email** (ví dụ: Gmail, SendGrid) để gửi báo cáo định kỳ cho quản trị viên.
   - **Cách làm**:
     - Thêm **node `n8n-nodes-base.email`** sau Node 6.
     - Cấu hình **người nhận** và **tiêu đề email**.

3. **Lưu log vào Google Sheets/Notion**:
   - Thêm **node Google Sheets** hoặc **Notion** để lưu lịch sử channel đã được kiểm tra.
   - **Cách làm**:
     - Thêm **node `n8n-nodes-base.googleSheets`** và cấu hình sheet tương ứng.

4. **Cảnh báo qua Telegram/Email**:
   - Thêm **node Telegram Bot** hoặc **Email** để cảnh báo khi có channel mới không hoạt động.
   - **Cách làm**:
     - Thêm **node `n8n-nodes-base.telegram`** và cấu hình bot Telegram.

5. **Tùy chỉnh thời gian lọc**:
   - Thay đổi **30 ngày** thành **60/90 ngày** trong Node 4 để phù hợp với chính sách của công ty.
:::

---

### 📌 **Kết Luận**
Workflow **Automated Slack Channel Inactivity Audit** là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa việc dọn dẹp Slack** mà không cần can thiệp thủ công.
✔ **Tiết kiệm thời gian** lên đến **10 giờ/tháng** (so với kiểm tra thủ công).
✔ **Duy trì workspace sạch sẽ**, tăng hiệu quả giao tiếp trong đội nhóm.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Slack App** và **credentials**.
3. **Bật Active** và **chờ báo cáo hàng tuần** tự động xuất hiện!

---
**💡 Bạn có thể tùy chỉnh workflow này để phù hợp với nhu cầu cụ thể của công ty!** Nếu cần hỗ trợ thêm, hãy để lại bình luận hoặc liên hệ với **Trung Tran** (tác giả workflow) qua [LinkedIn](https://www.linkedin.com/in/trungtranempower/) hoặc [n8n Community](https://community.n8n.io/). 🚀