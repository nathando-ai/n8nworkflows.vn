---
title: "🚨 **Tự Động Hóa Cảnh Báo Downtime Thực Tế → Jira + Slack Routing Smart (Không Cần Code!)**"
description: "Workflow này tự động chuyển cảnh báo downtime từ uptime monitoring (Pingdom, UptimeRobot...) sang Jira để theo dõi và tự động gửi cảnh báo đến thành viên Slack đang online, giảm thiểu thời gian phản hồi và tối ưu hóa quản lý on-call. Đảm bảo không một sự cố nào bị bỏ qua!"
slug: "tieu-dung-thuc-te-den-jira-slack-routing-smart"
tags: [n8n, automation, devops, jira, slack, uptime-monitoring, no-code]
keywords: [n8n workflow downtime, tự động hóa cảnh báo downtime, jira alert automation, slack on-call rotation, uptime monitoring alert]
---

# 🚨 **Tự Động Hóa Cảnh Báo Downtime Thực Tế → Jira + Slack Routing Smart**

## **💥 Nỗi Đau Của Các Sếp Khi Quản Lý Downtime Thủ Công**
Hàng ngày, các sếp phải:
- **Chờ đợi** cảnh báo từ uptime monitoring (Pingdom, UptimeRobot, Datadog...) và **chuyển đổi** chúng thành ticket Jira để theo dõi.
- **Tìm kiếm** thành viên Slack đang online để thông báo sự cố, dẫn đến **trễ thời gian phản hồi** và **rủi ro mất khách hàng**.
- **Quản lý thủ công** on-call rotation, khiến việc phân công cảnh báo trở nên **phức tạp và không hiệu quả**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lọc** chỉ cảnh báo **critical** (status = "down") từ uptime tools.
✅ **Tạo ticket Jira** với tất cả chi tiết (service name, downtime duration, error code, impact).
✅ **Tìm và chọn** thành viên Slack **đang online** để gửi cảnh báo **ngay lập tức**.
✅ **Xử lý tình huống khẩn cấp** (nếu không ai online, workflow sẽ gửi đến thành viên đầu tiên).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 50% thời gian** trong việc xử lý cảnh báo downtime.
- **Giảm thiểu rủi ro** do sự cố không được phát hiện kịp thời.
- **Cá nhân hóa cảnh báo** với thông tin chi tiết từ uptime tools.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Tối ưu hóa on-call rotation** với logic chọn người online.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Jira** (đã cấu hình API key hoặc OAuth).
2. **Tài khoản Slack** (đã tạo **channel on-call** và cấp quyền cho bot n8n).
3. **Uptime Monitoring Tool** (Pingdom, UptimeRobot, Datadog,...) **cấu hình webhook** gửi cảnh báo đến n8n.
4. **VPS Self-hosted n8n** (để workflow chạy liên tục).
5. **Credentials cho các node**:
   - **Webhook**: Path và HTTP Method (POST).
   - **Jira**: Project Key, Issue Type, và API Token.
   - **Slack**: Token Bot và ID Channel on-call.
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/12060) (đăng nhập tài khoản n8n).
2. **Nhấp vào "Export"** (icon ba chấm) → Chọn **"Export as JSON"**.
3. **Trên n8n Editor**, nhấp **"Import"** → Dán JSON và nhấn **"Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/12060](https://n8n.io/workflows/12060).
2. **Trên n8n Editor**, nhấp **"Import"** → Dán JSON và nhấn **"Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Receive Uptime Alert (Webhook)**
- **Cấu hình Webhook**:
  - **Path**: `7347e828-de5e-4368-9222-d53d9815789b` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Payload Format**: Chọn **"Raw"**.
  - **Credentials**: Tạo mới từ **Uptime Monitoring Tool** (ví dụ: Pingdom) và **gửi webhook** đến URL này:
    ```
    https://[Tên-Domain-N8N]/webhook/7347e828-de5e-4368-9222-d53d9815789b
    ```
    *(Thay `[Tên-Domain-N8N]` bằng domain của VPS n8n self-hosted).*

#### **🔹 Node 2: Filter for Critical Status (If)**
- **Cấu hình điều kiện**:
  - **Field**: `status` (trong payload từ uptime tool).
  - **Operator**: `is equal to`.
  - **Value**: `"down"` (hoặc `"critical"` nếu uptime tool sử dụng).
  - **Lưu ý**: Nếu uptime tool gửi status khác, **cập nhật giá trị này** để workflow chỉ xử lý cảnh báo **critical**.

#### **🔹 Node 3: Create New Jira Incident (Jira)**
- **Cấu hình Jira**:
  - **Credentials**: Chọn tài khoản Jira đã cấu hình.
  - **Project Key**: Nhập **key dự án** (ví dụ: `DEV`).
  - **Issue Type**: Chọn loại ticket (ví dụ: `Incident`).
  - **Fields to Map**:
    | **Jira Field**       | **Data from Webhook**          |
    |----------------------|--------------------------------|
    | Summary              | `{{$json["service_name"]}} is DOWN` |
    | Description          | `Downtime: {{$json["duration"]}} | Error: {{$json["error_code"]}} | Impact: {{$json["customer_impact"]}}` |
    | Priority             | `High`                         |
    | Labels               | `uptime-alert`                 |
    | Assignee             | *Không cần thiết (sẽ tự động gán sau)* |

#### **🔹 Node 4 & 5: Get On-Call Channel Members + Split/Process Each Member (Slack + SplitInBatches)**
- **Cấu hình Slack**:
  - **Credentials**: Chọn bot Slack đã cấu hình.
  - **Channel ID**: Nhập **ID của channel on-call** (lấy từ `https://[slack-domain].slack.com/apps/[app-id]/configure`).
  - **Lưu ý**:
    - Nếu chưa có channel, tạo một channel mới (ví dụ: `#on-call-devops`).
    - Cấp quyền cho bot n8n vào channel này.

#### **🔹 Node 6: Check Slack User Presence (Slack)**
- **Cấu hình**:
  - **Credentials**: Chọn cùng bot Slack như trên.
  - **User ID**: Sẽ được **auto-populate** từ node `SplitInBatches`.

#### **🔹 Node 7: Select Active On-Call User (Code)**
- **Mã JavaScript mặc định** đã xử lý logic:
  ```javascript
  // Lọc người online (presence = "active")
  const activeUsers = $input.all().filter(user => user.presence === "active");

  // Nếu có người online, chọn ngẫu nhiên
  if (activeUsers.length > 0) {
    const randomIndex = Math.floor(Math.random() * activeUsers.length);
    return activeUsers[randomIndex];
  }
  // Nếu không ai online, chọn người đầu tiên
  else {
    return $input.all()[0];
  }
  ```
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi logic (ví dụ: ưu tiên người nào đó).

#### **🔹 Node 8: Notify Selected User (Slack)**
- **Cấu hình**:
  - **Credentials**: Chọn bot Slack.
  - **Message Format**:
    ```markdown
    *🚨 ALERT: {{$json["service_name"]}} is DOWN*
    *Downtime:* {{$json["duration"]}}
    *Error:* {{$json["error_code"]}}
    *Impact:* {{$json["customer_impact"]}}
    *Jira Ticket:* [{{$json["jira_url"]}}]({{$json["jira_url"]}})
    ```
  - **Lưu ý**: Đảm bảo **Jira URL** được truyền từ node `Create New Jira Incident`.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **webhook test** từ Postman hoặc uptime tool với payload mẫu:
     ```json
     {
       "service_name": "API Payment Gateway",
       "status": "down",
       "duration": "15 minutes",
       "error_code": "503",
       "customer_impact": "High",
       "timestamp": "2024-05-20T10:00:00Z"
     }
     ```
   - Kiểm tra:
     - **Jira** có ticket mới không?
     - **Slack** có cảnh báo được gửi đến người online không?

2. **Bật Active**:
   - Nhấp **"Active"** trên workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Tools Khác**
- **Email Notification**: Thêm node **Email** để gửi cảnh báo đến email quản lý.
- **PagerDuty/Zendesk**: Kết nối với node **PagerDuty** hoặc **Zendesk** để tạo ticket triệt để.
- **Telegram Alerts**: Sử dụng node **Telegram** để cảnh báo thêm trên Telegram.

### **2. Log & Audit**
- **Lưu log downtime**: Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử cảnh báo.
- **Báo cáo định kỳ**: Sử dụng node **Google Calendar** hoặc **Email** để gửi báo cáo tuần/month về downtime.

### **3. Tối Ưu Hóa On-Call Rotation**
- **Sử dụng node `set`** để lưu trạng thái người đã được gọi để tránh gọi lại liên tục.
- **Kết hợp với `stickyNote`** để lưu danh sách người on-call theo tuần.

### **4. Cảnh Báo Multi-Channel**
- **Gửi cảnh báo đến Email + Slack**: Sử dụng node **Email** song song với Slack.
- **Cảnh báo cho CEO**: Thêm điều kiện trong node **If** để chỉ cảnh báo CEO khi downtime > 30 phút.

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc quản lý downtime thủ công, đồng thời **tăng cường tính chuyên nghiệp** với:
✔ **Tự động hóa end-to-end** từ uptime tools → Jira → Slack.
✔ **Smart routing** chỉ gửi cảnh báo đến người online.
✔ **Theo dõi chi tiết** với Jira và log tự động.

**🚀 Hành động ngay!**
1. **Cài n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với dữ liệu thật** và bật Active.

**🎁 Đăng ký VPS cho n8n với giảm giá:**
👉 [TinoHost (Mã: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388) - **Giảm 39%**
👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)

**Chỉ cần 10 phút setup, nhưng tiết kiệm hàng giờ mỗi tuần!** 💪