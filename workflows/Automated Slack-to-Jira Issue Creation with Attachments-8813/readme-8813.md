---
title: "🚀 Tự Động Hóa Tạo Issue Jira Từ Slack Với File Đính Kèm - Không Cần Code"
description: "Giải pháp tự động hóa hoàn toàn chuyển đổi tin nhắn Slack thành issue Jira có file đính kèm (screenshot, tài liệu), tiết kiệm thời gian lên tới 80% cho team DevOps và Project Management. Workflow này tự động tải file từ Slack, phân tích nội dung, tạo issue Jira và gửi thông báo xác nhận - tất cả chỉ với 1 dòng tin nhắn!"
slug: "tieu-dong-hoa-slack-to-jira-voi-file-dinh-kem"
tags: [n8n, automation, jira, slack, no-code, devops, project-management]
keywords: [tự động hóa slack jira, tạo issue jira tự động, upload file đính kèm jira, n8n workflow jira, tự động hóa devops, chuyển đổi tin nhắn slack thành issue]
---

# 🚀 **Tự Động Hóa Tạo Issue Jira Từ Slack Với File Đính Kèm - Không Cần Code**

### **🔥 Nỗi Đau Của Các Sếp: Tốn Thời Gian Và Lỗi Nhân Sự**
Hàng ngày, team DevOps và Project Manager phải:
- **Chuyển đổi tin nhắn Slack thành issue Jira thủ công** (tốn 30-60 phút/ngày).
- **Quên đính kèm file đính kèm** (screenshot, tài liệu) vào issue, dẫn đến mất thông tin quan trọng.
- **Phải nhắc nhở team** gửi thông tin đầy đủ, gây mất hiệu quả.
- **Không theo dõi được lịch sử** của việc chuyển đổi, dẫn đến trùng lặp hoặc thiếu thông tin.

**Giải pháp?** Workflow này **tự động hóa toàn bộ quy trình** chỉ với **1 dòng tin nhắn Slack**, đồng thời **tải tự động tất cả file đính kèm** vào issue Jira. Kết quả:
✅ **Tiết kiệm 80% thời gian** so với làm thủ công.
✅ **Tránh lỗi nhân sự** với việc tự động phân tích và tạo issue.
✅ **Giữ nguyên tất cả file đính kèm** (screenshot, PDF, image) trong Jira.
✅ **Gửi thông báo xác nhận** ngay trên Slack khi issue được tạo thành công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình chuyển đổi Slack → Jira** chỉ với 1 dòng tin nhắn.
- **Tải tự động tất cả file đính kèm** (screenshot, tài liệu) vào issue Jira.
- **Phân tích tự động nội dung tin nhắn** để extraxt **Tiêu đề, Mô tả, Độ ưu tiên** theo định dạng Jira.
- **Gửi thông báo xác nhận** ngay trên Slack với **link issue Jira** và **file đính kèm**.
- **Không cần code** - chỉ cần cấu hình n8n một lần là hoạt động 24/7.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - **Token API Slack** (có quyền `chat:write`, `files:read`, `files:write`).
   - **Channel Slack** để lắng nghe tin nhắn (ví dụ: `#tickets`).
2. **Tài khoản Jira Cloud**:
   - **API Key Jira** (có quyền `Create Issue`, `Attach File`).
   - **Project Jira** để tạo issue (ví dụ: `DevOps`).
3. **File mẫu** (nếu muốn test):
   - Tin nhắn Slack có định dạng:
     ```
     Title: [Tiêu đề Jira]
     Description: [Mô tả chi tiết]
     Priority: [high/medium/low]
     ```
   - File đính kèm (screenshot, PDF, image) trong tin nhắn.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8813](https://n8n.io/workflows/8813) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8813) và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Tạo workflow mới và **copy/paste** từng node theo thứ tự dưới đây.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **11 node**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

##### **A. Cấu Hình Slack Trigger (Node 1)**
- **Node**: `Slack Trigger` (n8n-nodes-base.slackTrigger)
- **Cấu hình**:
  - **Credentials**: Chọn `slackApi` (đã cấu hình trước).
  - **Channel**: Nhập `#tickets` (hoặc channel muốn lắng nghe).
  - **Event**: Chọn `message` (chỉ lắng nghe tin nhắn mới).
  - **Filter**: Bỏ trống (hoặc thêm regex nếu muốn lọc tin nhắn cụ thể).

##### **B. Cấu Hình Jira Credentials (Node 3 & 5)**
- **Node**: `Upload Attachment to Jira` và `Create Jira Issue` (cả 2 đều dùng `jiraSoftwareCloudApi`).
- **Cấu hình**:
  - **Credentials**: Chọn `jiraSoftwareCloudApi` (đã cấu hình trước).
  - **Project Key**: Nhập `DEVOPS` (hoặc project muốn tạo issue).
  - **Issue Type**: Chọn `Bug` hoặc `Task` (tùy thuộc vào yêu cầu).

##### **C. Cấu Hình Code Nodes (Node 2 & 6)**
- **Node 2: Prepare Files for Processing**
  - **Mục đích**: Chuẩn bị file đính kèm cho việc tải lên.
  - **Code mẫu** (không cần chỉnh sửa, chỉ cần chạy):
    ```javascript
    return {
      files: $input.all().files,
      message: $input.all().message
    };
    ```
- **Node 6: Parse Message into Jira Format**
  - **Mục đích**: Phân tích tin nhắn Slack để extraxt **Tiêu đề, Mô tả, Độ ưu tiên**.
  - **Code mẫu** (cần chỉnh sửa regex nếu định dạng tin nhắn khác):
    ```javascript
    const message = $input.all().message.text;
    const regex = /Title:\s*(.+?)\s*\nDescription:\s*(.+?)\s*\nPriority:\s*(high|medium|low)/is;
    const match = message.match(regex);

    if (match) {
      return {
        title: match[1].trim(),
        description: match[2].trim(),
        priority: match[3].toUpperCase()
      };
    } else {
      return {
        title: "No Title Extracted",
        description: "No Description Extracted",
        priority: "MEDIUM"
      };
    }
    ```

##### **D. Cấu Hình HTTP Request (Node 8 & 9)**
- **Node 8: Get File Info**
  - **Mục đích**: Lấy thông tin file từ Slack (URL private).
  - **Cấu hình**:
    - **Method**: `GET`
    - **URL**: `$node["Prepare Files for Processing"].json["files"][0].url_private` (hoặc dùng `$node["Split Files into Batches"].json["item"].url_private`).
    - **Headers**:
      ```
      Authorization: Bearer {{ $credentials["slackApi"].apiToken }}
      ```
- **Node 9: Download Attachment**
  - **Mục đích**: Tải file từ URL private của Slack.
  - **Cấu hình**:
    - **Method**: `GET`
    - **URL**: `$node["Get File Info"].json["url_private"]`
    - **Headers**:
      ```
      Authorization: Bearer {{ $credentials["slackApi"].apiToken }}
      ```

##### **E. Cấu Hình If Nodes (Node 4 & 7)**
- **Node 4: checking message**
  - **Mục đích**: Kiểm tra xem tin nhắn có định dạng đúng không.
  - **Cấu hình**:
    - **Condition**: `$node["Parse Message into Jira Format"].json.title !== "No Title Extracted"`.
- **Node 7: Check Attachments**
  - **Mục đích**: Kiểm tra xem có file đính kèm không.
  - **Cấu hình**:
    - **Condition**: `$node["Prepare Files for Processing"].json.files.length > 0`.

##### **F. Cấu Hình Slack Reply (Node 5)**
- **Node**: `Reply to Channel On Slack` (n8n-nodes-base.slack)
- **Cấu hình**:
  - **Credentials**: Chọn `slackApi`.
  - **Channel**: `#tickets` (hoặc channel muốn gửi phản hồi).
  - **Message**: Sử dụng **Dynamic Content** để gửi thông báo:
    ```
    Issue đã được tạo thành công!
    - **Tiêu đề**: {{ $node["Parse Message into Jira Format"].json.title }}
    - **Link Jira**: [https://your-jira-domain.atlassian.net/browse/{{ $node["Create Jira Issue"].json.issue.key }}](https://your-jira-domain.atlassian.net/browse/{{ $node["Create Jira Issue"].json.issue.key }})
    - **File đính kèm**: {{ $node["Prepare Files for Processing"].json.files.length }} file
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn mẫu vào Slack với định dạng:
    ```
    Title: Bug: Login failed
    Description: User cannot login after update v2.0
    Priority: high
    ```
  - Kiểm tra **Output** của từng node để đảm bảo không có lỗi.
- **Bật Active**:
  - Chuyển trạng thái workflow từ **Draft** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Tự động tạo issue từ nhiều channel**:
   - Sử dụng **Sticky Note** (Node 10) để lưu danh sách channel cần lắng nghe.
   - Ví dụ: `#bugs`, `#tasks`, `#support`.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.schedule** để chạy workflow hàng ngày và gửi báo cáo tổng hợp issue mới nhất qua Slack/Email.

3. **Lưu log hoạt động**:
   - Sử dụng **n8n-nodes-base.googleSheets** hoặc **n8n-nodes-base.database** để lưu lịch sử issue đã tạo.

4. **Kết hợp với AI**:
   - Sử dụng **n8n-nodes-base.llm** để tự động extraxt thông tin từ tin nhắn Slack nếu định dạng không chuẩn.

5. **Tự động phân loại issue**:
   - Sử dụng **n8n-nodes-base.code** để phân loại issue theo mô hình máy học (ví dụ: Bug, Task, Story).
:::

---

### 📌 **Kết Luận**
Workflows này **giải quyết hoàn toàn vấn đề chuyển đổi tin nhắn Slack thành issue Jira** một cách **tự động, chính xác và không cần code**. Các sếp chỉ cần:
1. **Cấu hình 1 lần** Slack và Jira credentials.
2. **Gửi tin nhắn mẫu** để test.
3. **Bật workflow** và **quên đi** việc chuyển đổi thủ công!

**🚀 Kết quả?** Team DevOps và Project Manager **tiết kiệm thời gian, giảm lỗi và tăng hiệu quả** lên gấp đôi!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Bắt đầu ngay!** Import workflow và **tự động hóa quy trình của bạn** trong vòng 10 phút! 🚀