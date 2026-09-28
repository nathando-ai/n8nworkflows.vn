---
title: "🧹 Tự Động Xóa Tài Khoản Khách Thăm Cũ (B2B Guest) Trên Microsoft Entra ID – Giảm Thiểu Rủi Ro & Tiết Kiệm Thời Gian"
description: "Workflow tự động hóa 100% không code để quét, thông báo và xóa tài khoản khách tham gia (B2B guest) không hoạt động trên Microsoft Entra ID, Teams và SharePoint. Giúp doanh nghiệp duy trì an toàn, giảm chi phí và tự động hóa quản trị Identity Governance."
slug: "tieu-dong-xoa-tai-khoan-khach-tham-cuu-entra-id"
tags: [n8n, automation, Microsoft Entra ID, Microsoft Graph, Teams, SharePoint, no-code, identity-governance, Microsoft 365]
keywords: [tự động hóa xóa tài khoản khách tham gia, Microsoft Entra ID cleanup, tự động hóa quản trị Identity, xóa tài khoản B2B guest không hoạt động, n8n workflow Microsoft Graph]
---

# 🚀 **Tự Động Xóa Tài Khoản Khách Thăm Cũ (B2B Guest) Trên Microsoft Entra ID – Giải Pháp An Toàn & Tiết Kiệm Chi Phí**

### **Nỗi Đau Của Doanh Nghiệp**
Hàng tuần, doanh nghiệp phải mất **giờ đồng hồ** để thủ công kiểm tra danh sách khách tham gia (B2B guest) trên Microsoft Entra ID, xác định tài khoản nào **không hoạt động trong 30 ngày trở lên**, và quyết định xóa chúng. Những tài khoản này không chỉ **tốn chi phí lưu trữ** mà còn **tăng rủi ro an toàn** (ví dụ: tài khoản bị hack, dữ liệu nhạy cảm rò rỉ). Ngoài ra, việc **thông báo cho người quản lý (sponsor)** trước khi xóa cũng là một công việc phức tạp, đòi hỏi sự đồng bộ giữa nhiều hệ thống như **Microsoft Graph, Teams và SharePoint**.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động quét** tất cả tài khoản B2B guest không hoạt động.
✅ **Gửi thông báo tự động** đến người quản lý (sponsor) trên Teams.
✅ **Chờ 72 giờ** để cho phép người quản lý khôi phục nếu cần.
✅ **Xóa tài khoản tự động** nếu không có phản hồi.
✅ **Ghi log thành công/thất bại** lên SharePoint để theo dõi.
✅ **Báo cáo tổng kết** sau mỗi lần chạy (thông qua Teams).

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tuần** cho bộ phận IT/DevOps.
- **Giảm rủi ro an toàn** bằng cách loại bỏ tài khoản không hoạt động.
- **Tự động hóa Identity Governance** mà không cần viết code.
- **Duy trì sạch sẽ danh sách người dùng**, giảm chi phí lưu trữ.
- **Cá nhân hóa thông báo** cho từng sponsor qua Teams.
- **Kiểm soát toàn bộ quy trình** từ quét đến xóa, ghi log.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Microsoft Graph API Key** với quyền:
   - `User.Read.All` (đọc thông tin người dùng)
   - `User.ReadWrite.All` (xóa tài khoản)
   - `User.ReadBasic.All` (lấy thông tin quản lý/sponsor)
   - `SignInLogs.Read.All` (kiểm tra hoạt động đăng nhập)
2. **Thông tin SharePoint**:
   - **ID Site** và **ID List** để ghi log xóa tài khoản.
   - **Permissions** để viết dữ liệu vào SharePoint.
3. **Thông tin Teams**:
   - **Team ID** và **Channel ID** để gửi thông báo, cảnh báo và báo cáo.
4. **Thông tin cấu hình**:
   - **Ngưỡng "stale"** (ví dụ: tài khoản không hoạt động trong 30 ngày).
   - **Thời gian chờ** (72 giờ) trước khi xóa.
5. **VPS n8n** (Self-hosted) để workflow chạy 24/7.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/16118](https://n8n.io/workflows/16118) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và chọn **Import**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **24 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

#### **A. Cấu Hình Node "Set Config Parameters" (Cấu Hình Tham Số)**
- **Tham số cần điền**:
  - `staleDays`: Số ngày không hoạt động để xác định tài khoản "stale" (ví dụ: `30`).
  - `waitHours`: Thời gian chờ trước khi xóa (ví dụ: `72`).
  - **Microsoft Graph Credentials**:
    - `tenantId`, `clientId`, `clientSecret`.
  - **SharePoint Credentials**:
    - `siteId`, `listId`, `sharepointUrl`.
  - **Teams Credentials**:
    - `teamId`, `channelId`, `webhookUrl` (hoặc `auth` nếu dùng OAuth).

#### **B. Node "Initialize Pagination Loop" (Khởi Động Lặp Lại Trang)**
- **Lưu ý**: Node này sử dụng **JavaScript** để quản lý pagination khi lấy dữ liệu từ Microsoft Graph.
- **Không cần chỉnh sửa** nếu đã cấu hình `httpRequest` sau đó đúng.

#### **C. Node "Filter Stale Guest Accounts" (Lọc Tài Khoản Cũ)**
- **Logic**: Node này sử dụng **JavaScript** để kiểm tra tài khoản có hoạt động trong `staleDays` ngày không.
- **Không cần chỉnh sửa** nếu đã cấu hình `staleDays` trong node `Set Config Parameters`.

#### **D. Node "Fetch Guest Manager" (Lấy Thông Tin Quản Lý)**
- **Yêu cầu**: Node này gọi API Microsoft Graph để lấy thông tin **sponsor/manager** của tài khoản.
- **Lưu ý**:
  - Đảm bảo **Microsoft Graph API Key** có quyền `User.ReadBasic.All`.
  - Nếu API trả về lỗi, kiểm tra **credentials** và **scope**.

#### **E. Node "Delete Stale Guest Account" (Xóa Tài Khoản)**
- **Yêu cầu**: Node này gọi API `POST /users/{userId}/delete` để xóa tài khoản.
- **Lưu ý**:
  - **Permissions**: API cần quyền `User.ReadWrite.All`.
  - **Xử lý lỗi**: Nếu xóa thất bại, node sẽ chuyển sang node `Alert Deletion Error` (gửi cảnh báo Teams).

#### **F. Node "Log Deletion in SharePoint" (Ghi Log Xóa)**
- **Yêu cầu**: Node này viết dữ liệu vào **SharePoint List** với các trường:
  - `GuestEmail`, `GuestName`, `SponsorEmail`, `DeletionTime`, `Status`.
- **Lưu ý**:
  - Đảm bảo **SharePoint credentials** có quyền viết dữ liệu.
  - Kiểm tra **ID List** và **trường** trong SharePoint.

#### **G. Node "Post Process Summary in Teams" (Báo Cáo Tổng Kết)**
- **Yêu cầu**: Node này gửi **tóm tắt** sau khi xử lý xong:
  - Số tài khoản stale được phát hiện.
  - Số tài khoản đã xóa thành công.
  - Số tài khoản bị lỗi.
- **Lưu ý**:
  - Đảm bảo **Teams webhook URL** hoặc **credentials OAuth** đúng.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **manual execution** và kiểm tra từng node.
   - Đặc biệt kiểm tra:
     - Node `Filter Stale Guest Accounts` (có lọc đúng tài khoản không?).
     - Node `Delete Stale Guest Account` (xóa thành công không?).
     - Node `Log Deletion in SharePoint` (ghi log đúng không?).
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Workflow Status** sang **Active**.
   - Đảm bảo **schedule trigger** (`Weekly Trigger at 8am Monday`) được kích hoạt.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỢNG MỞ RỘNG]
1. **Kết hợp với Power Automate**:
   - Sử dụng **Power Automate** để tự động tạo **báo cáo Excel** từ dữ liệu SharePoint.
2. **Gửi Email Cảnh Báo**:
   - Thêm node **Email** để gửi cảnh báo đến **DevOps Team** khi có lỗi xóa.
3. **Lưu Log vào OneDrive/SharePoint**:
   - Thay vì SharePoint, có thể lưu log vào **OneDrive** hoặc **Azure Blob Storage**.
4. **Tự động Khôi Phục Tài Khoản**:
   - Thêm logic để **khôi phục tài khoản** nếu sponsor phản hồi trong thời gian chờ.
5. **Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Schedule Node** để gửi **báo cáo tuần/month** qua Email hoặc Teams.
6. **Kết Nối với Jira/ServiceNow**:
   - Khi xóa tài khoản thất bại, tự động tạo **ticket** trong Jira/ServiceNow để IT xử lý.
:::

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho doanh nghiệp muốn **tự động hóa Identity Governance** trên Microsoft Entra ID mà không cần viết code. Bằng cách **quét, thông báo, chờ và xóa** tài khoản B2B guest không hoạt động, các sếp sẽ:
✔ **Giảm rủi ro an toàn**.
✔ **Tiết kiệm thời gian** cho bộ phận IT.
✔ **Duy trì danh sách người dùng sạch sẽ**.
✔ **Cá nhân hóa quy trình** với thông báo Teams và log SharePoint.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** theo hướng dẫn.
3. **Bật schedule** và để workflow làm việc tự động hàng tuần.

**Nếu có vấn đề**, hãy liên hệ với **AutomiQ** (tác giả workflow) qua [info@automiq.fi](mailto:info@automiq.fi) hoặc tham gia **community n8n** để hỗ trợ kỹ thuật.

---
**🚀 Chúc các sếp thành công với quy trình tự động hóa Identity Governance!**