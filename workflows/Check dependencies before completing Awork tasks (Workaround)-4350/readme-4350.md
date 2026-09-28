---
title: "🔍 **Tự Động Hóa Kiểm Tra Đ inter phụ thuộc trước khi Hoàn Thành Task trên Awork (Không cần Code!)**"
description: "Workflow n8n giúp tự động kiểm tra và hủy bỏ trạng thái 'Hoàn thành' của task trên Awork nếu có phụ thuộc hoặc subtask chưa hoàn thành, đồng thời thêm ghi chú tự động. Giúp các sếp tiết kiệm thời gian và tránh lỗi thủ công."
slug: "tieu-dong-hoa-kiem-tra-dependency-tren-awork"
tags: [n8n, automation, Awork, IT Ops, no-code, workflow tự động hóa]
keywords: [n8n workflow Awork, tự động hóa phụ thuộc task, kiểm tra subtask trên Awork, tự động hóa quản lý dự án, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Kiểm Tra Đ inter phụ thuộc trước khi Hoàn Thành Task trên Awork**

### **Giải pháp cho các sếp quản lý dự án bị "đau đầu" với phụ thuộc task và subtask**
Làm việc với **Awork** nhưng thường gặp tình huống sau?
- **Task được đánh dấu "Hoàn thành" nhưng phụ thuộc (dependency) vẫn chưa xong** → Làm mất thời gian sửa lại.
- **Subtask chưa hoàn thành nhưng task cha đã được đánh dấu "Done"** → Làm mất tính logic trong quản lý dự án.
- **Phải kiểm tra thủ công hàng loạt task** để đảm bảo logic phụ thuộc đúng → Tốn thời gian và dễ bị bỏ sót.

**Workflow này sẽ tự động giải quyết tất cả!** Nó sẽ:
✅ **Kiểm tra tất cả phụ thuộc (dependency) và subtask** trước khi cho phép đánh dấu task là "Hoàn thành".
✅ **Hủy bỏ trạng thái "Done"** nếu phát hiện phụ thuộc/subtask chưa xong và **thêm ghi chú tự động** để giải thích lý do.
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính bảo mật và hiệu suất cao.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ nhanh, ổn định)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công hàng loạt task.
- **Tránh lỗi logic**: Task chỉ được đánh dấu "Done" khi **tất cả phụ thuộc và subtask** đều hoàn thành.
- **Ghi chú tự động**: Khi workflow hủy bỏ trạng thái "Done", nó sẽ **thêm ghi chú rõ ràng** để người dùng hiểu lý do.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
- **Cá nhân hóa**: Có thể **bật/tắt** các tính năng phụ thuộc, subtask, hoặc ghi chú theo nhu cầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Awork** và **API Key** của Awork (để kết nối với API).
✔ **Thiết lập Webhook** trên Awork để nhận thông báo khi trạng thái task thay đổi.
✔ **Cấu hình Credentials** cho n8n:
   - **Header Auth** (để kết nối với API Awork).
   - **Custom Auth** (nếu cần thiết cho việc thêm ghi chú).

🔹 **Cách tạo API Key Awork**:
   - Truy cập [Client Applications & API Keys](https://support.awork.com/en/articles/5415664-client-applications-and-api-keys) trên Awork.
   - Tạo **một API Key mới** và lưu trữ an toàn.

🔹 **Cách thiết lập Webhook trên Awork**:
   - Truy cập [Webhooks](https://support.awork.com/en/articles/5415462-webhooks) và tạo **một Webhook mới**.
   - Chọn **event**: `Task status changed`.
   - **Bật "Only events from first level properties"** để giảm số lượng gọi Webhook không cần thiết.
   - **Gán URL Webhook** từ n8n (sau khi import workflow).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** của workflow từ [n8n.io/workflows/4350](https://n8n.io/workflows/4350).
- **Mở n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Hoặc copy/paste JSON** từ file vào ô **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **không sử dụng package Awork Community** (do không hỗ trợ tất cả API calls), nên các sếp phải cấu hình **HTTP Request nodes** như sau:

##### **A. Cấu hình Webhook (Node: "Webhook call by Awork")**
- **Key Parameters**:
  - `path`: `57b88b94-6228-4e49-897d-64bf8c7d32db` (không cần thay đổi).
  - `httpMethod`: `POST` (không cần thay đổi).
- **Credentials**:
  - Chọn **Header Auth** đã tạo trước đó (ví dụ: `Awork API Access`).

##### **B. Cấu hình "Workflow config" (Node: "Workflow config")**
Đây là **node quan trọng nhất**, các sếp phải cấu hình các tham số sau:
| **Tham số**               | **Kiểu dữ liệu** | **Mô tả**                                                                 | **Gía trị mặc định (nếu không cần thiết)** |
|---------------------------|------------------|---------------------------------------------------------------------------|---------------------------------------------|
| `finishedStateLabels`     | Array (string)   | Danh sách **label trạng thái "Done"** của task (ví dụ: `["Done", "Completed"]`). | `["Done"]`                                  |
| `useDependencies`         | Boolean          | **Bật/tắt** kiểm tra phụ thuộc (dependency).                             | `true`                                       |
| `useTreeStructure`        | Boolean          | **Bật/tắt** kiểm tra subtask (cấu trúc cây).                             | `true`                                       |
| `addComments`             | Boolean          | **Bật/tắt** thêm ghi chú khi rollback trạng thái.                         | `true`                                       |
| `commentTextDependencies` | String           | **Nội dung ghi chú** khi phụ thuộc chưa hoàn thành.                     | `"Task này chưa hoàn thành vì phụ thuộc [TASK_ID] chưa xong."` |
| `commentTextTreeStructure`| String           | **Nội dung ghi chú** khi subtask chưa hoàn thành.                       | `"Task này chưa hoàn thành vì subtask [SUBTASK_ID] chưa xong."` |

🔹 **Lưu ý**:
- Nếu `addComments = true`, thì **cần điền cả `commentTextDependencies` và `commentTextTreeStructure`**.
- Nếu `useDependencies = false`, workflow sẽ **bỏ qua bước kiểm tra phụ thuộc**.
- Nếu `useTreeStructure = false`, workflow sẽ **bỏ qua bước kiểm tra subtask**.

##### **C. Cấu hình Credentials cho HTTP Request nodes**
Tất cả các **node `httpRequest`** trong workflow cần **credentials Header Auth** (đã tạo ở bước A).
- **Tên credentials**: `Awork API Access` (hoặc tên tùy chỉnh).
- **Header**:
  - `name`: `Authorization`
  - `value`: `Bearer {API_KEY_AWORK}` (thay `{API_KEY_AWORK}` bằng API Key thực tế).

##### **D. Test Run trước khi kích hoạt**
- **Chạy test** với một task mẫu để đảm bảo workflow hoạt động đúng.
- **Kiểm tra log** để xác nhận:
  - Nếu task có phụ thuộc/subtask chưa xong → Trạng thái sẽ được **rollback** và **thêm ghi chú**.
  - Nếu task không có phụ thuộc/subtask → Trạng thái "Done" sẽ được giữ nguyên.

---

#### **3. Kích hoạt ⚡️**
- Sau khi cấu hình xong, **bật Active** cho workflow.
- **Kiểm tra lại Webhook** trên Awork để đảm bảo nó hoạt động.
- **Monitor log** trong n8n để theo dõi hoạt động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram để báo cáo**
   - Thêm **node `slack`** hoặc `telegram` sau khi workflow rollback trạng thái để **báo cáo tự động** cho team.
   - Ví dụ: `"Task [TASK_ID] đã bị rollback vì phụ thuộc [DEPENDENCY_ID] chưa xong!"`

2. **Lưu log hoạt động**
   - Thêm **node `set`** để lưu dữ liệu rollback vào **Google Sheets** hoặc **Notion** để theo dõi lịch sử.

3. **Tự động gửi báo cáo định kỳ**
   - Sử dụng **node `schedule`** để chạy workflow hàng ngày và gửi **báo cáo tổng hợp** về task bị rollback.

4. **Cấu hình email thông báo**
   - Thêm **node `email`** để gửi **email tự động** cho người quản lý khi có task bị rollback.

5. **Tùy chỉnh comment theo nhóm task**
   - Sử dụng **node `code`** để **động học** nội dung comment dựa trên loại phụ thuộc/subtask.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp quản lý dự án trên Awork **tránh lỗi logic**, **tiết kiệm thời gian** và **cải thiện hiệu quả quản lý**. Bằng cách **tự động kiểm tra phụ thuộc và subtask**, nó đảm bảo **task chỉ được đánh dấu "Done" khi thực sự xong**, đồng thời **thêm ghi chú rõ ràng** để team hiểu lý do.

**Hãy áp dụng ngay và làm việc hiệu quả hơn!** 🚀
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với cộng đồng n8n để hỗ trợ.

---
**🔹 Xem thêm:**
- [Tutorial cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/)
- [Hướng dẫn thiết lập Webhook Awork](https://support.awork.com/en/articles/5415462-webhooks)