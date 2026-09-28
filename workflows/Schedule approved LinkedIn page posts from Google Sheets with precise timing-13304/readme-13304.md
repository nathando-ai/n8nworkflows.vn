---
title: "🚀 Tự Động Hoàn Chỉnh & Đăng Bài LinkedIn Từ Google Sheets Với Thời Gian Chỉnh Xác"
description: "Giải pháp tự động hóa 100% không code để các sếp quản lý nội dung LinkedIn Organization Page hiệu quả, với thời gian đăng bài chính xác, quản lý hình ảnh từ Google Drive và theo dõi trạng thái tự động. Giúp tiết kiệm 10+ giờ/tháng và tăng độ chuyên nghiệp cho brand."
slug: "tu-dong-hoan-chinh-dang-bai-linkedin-googlesheets"
tags: [n8n, automation, social-media, linkedin, google-sheets, google-drive, no-code]
keywords: [tự động hóa linkedin, đăng bài linkedin tự động, google sheets linkedin, workflow n8n social media, tự động hóa nội dung mạng xã hội]
---

# 🚀 **Tự Động Hoàn Chỉnh & Đăng Bài LinkedIn Từ Google Sheets Với Thời Gian Chỉnh Xác**

### **Giải pháp cho các sếp quản lý nội dung LinkedIn Organization Page**
Hãy tưởng tượng một ngày không còn phải lo lắng về việc **quên đăng bài**, **đăng sai thời gian**, hoặc **quên cập nhật trạng thái** của bài viết. Workflow này sẽ tự động:
- **Lấy dữ liệu bài viết** từ Google Sheets (đã được phê duyệt).
- **Chọn bài viết** được lên lịch cho ngày hôm nay.
- **Chờ đến thời gian chính xác** (chuyển đổi múi giờ từ Eastern sang múi giờ Việt Nam).
- **Tải hình ảnh** từ Google Drive (nếu có).
- **Đăng bài** lên LinkedIn Organization Page.
- **Cập nhật trạng thái** từ "Đã lên lịch" → "Đã đăng" trong Google Sheets.

**Kết quả?** Các sếp sẽ **tiết kiệm 10+ giờ/tháng**, giảm thiểu lỗi đăng bài, và tăng độ chuyên nghiệp cho brand.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần phải đăng bài thủ công hàng ngày.
✅ **Đăng bài chính xác**: Thời gian đăng bài được tự động điều chỉnh theo múi giờ.
✅ **Quản lý nội dung chuyên nghiệp**: Theo dõi trạng thái bài viết (Đã lên lịch, Đã đăng) trong Google Sheets.
✅ **Tích hợp hình ảnh**: Tự động tải hình ảnh từ Google Drive khi đăng bài Creative Post.
✅ **Hoạt động liên tục**: Workflow chạy tự động 4 lần/ngày (9-12 AM) trong giờ làm việc.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn Organization Page** (đã cấp quyền quản lý).
2. **Tài khoản Google Sheets & Google Drive** (đã kết nối OAuth2).
3. **Bảng Google Sheets** với cấu trúc như sau:
   - **Cột bắt buộc**:
     - `Scheduled On` (ngày lên lịch)
     - `Platform` (phải là "LinkedIn")
     - `Post Type` (Creative Post hoặc Article)
     - `Caption` (nội dung bài viết)
     - `Media URL` (đường dẫn hình ảnh trong Google Drive, nếu có)
     - `Approval Status` (phải là "Good")
     - `Post URL` (sau khi đăng, sẽ tự động cập nhật)
   - **Cột cấu hình**:
     - `.env` (tab riêng): Chứa `LinkedIn Organization ID` và các tham số cấu hình.
4. **API Keys**:
   - `googleSheetsOAuth2Api` (Google Sheets)
   - `linkedInOAuth2Api` (LinkedIn)
   - `googleDriveOAuth2Api` (Google Drive)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/13304](https://n8n.io/workflows/13304) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13304) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **17 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình Credentials (Bắt buộc)**
| Node | Yêu cầu cấu hình |
|------|------------------|
| **Load LinkedIn Organization Credentials** | Điền `LinkedIn Organization ID` trong tab `.env` của Google Sheets. |
| **Fetch Approved LinkedIn Posts** | Chọn `googleSheetsOAuth2Api` và chỉ định **bảng Google Sheets** chứa dữ liệu bài viết. |
| **Download Image from Google Drive** | Chọn `googleDriveOAuth2Api` và nhập **đường dẫn file hình ảnh** từ cột `Media URL`. |
| **Publish Creative Post to LinkedIn / Publish Article Link to LinkedIn** | Chọn `linkedInOAuth2Api` và đảm bảo **quyền API** đã được cấp cho Organization Page. |

##### **B. Cấu hình Timezone (Nếu không dùng Eastern → India)**
- Node **`Wait Until Scheduled Time`** sử dụng múi giờ **Eastern Time (ET)** mặc định.
- **Nếu các sếp ở múi giờ khác**, cần chỉnh sửa **timezone offset** trong node `Wait` bằng cách:
  1. Nhấp chuột phải vào node `Wait Until Scheduled Time` → **Edit**.
  2. Trong **JavaScript code**, thay đổi:
     ```javascript
     const timeZone = "America/New_York"; // Eastern Time
     ```
     thành:
     ```javascript
     const timeZone = "Asia/Ho_Chi_Minh"; // Múi giờ Việt Nam
     ```

##### **C. Cấu hình Organization ID**
- Node **`Publish Creative Post to LinkedIn`** và **`Publish Article Link to LinkedIn`** sử dụng `Organization ID = 56420402` mặc định.
- **Nếu Organization Page khác**, các sếp phải:
  1. Tìm **Organization ID** trong URL LinkedIn:
     ```
     https://www.linkedin.com/company/your-org-id/
     ```
  2. Thay thế `56420402` bằng **Organization ID** mới trong **credentials LinkedIn**.

##### **D. Cấu hình Bảng Google Sheets**
- **Tab `.env`** phải có cấu trúc:
  | Cột | Giá trị |
  |------|---------|
  | `LinkedInOrganizationId` | `56420402` (hoặc Organization ID của các sếp) |
  | `LinkedInAccessToken` | `Bearer [API_TOKEN]` (nếu sử dụng) |

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Thêm **1 bài viết mẫu** vào Google Sheets với:
     - `Scheduled On` = ngày hiện tại.
     - `Approval Status` = "Good".
     - `Post Type` = "Creative Post" (hoặc "Article").
   - Chạy **Manual Trigger** để kiểm tra workflow.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi đăng bài thành công**:
   - Thêm node **`slack`** hoặc **`telegram`** sau node **`Save Post URL & Mark Published`** để thông báo khi bài viết đã đăng.
2. **Lưu log hoạt động**:
   - Thêm node **`stickyNote`** để ghi lại lỗi hoặc trạng thái của workflow.
3. **Tự động tạo bài viết từ AI**:
   - Kết hợp với **node `n8n-nodes-base.llm`** (nếu có) để tự động tạo caption từ mô tả.
4. **Báo cáo định kỳ**:
   - Sử dụng **node `googleSheets`** để tạo báo cáo thống kê bài viết đã đăng trong tháng.
5. **Chuyển đổi múi giờ tự động**:
   - Nếu các sếp có nhiều múi giờ khác nhau, có thể thêm **node `date`** để chuyển đổi thời gian theo yêu cầu.
:::

---

### 📌 **Kết luận**
Workflows này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa hoàn toàn** quá trình đăng bài LinkedIn, **tiết kiệm thời gian** và **tăng độ chuyên nghiệp** cho brand. Với chỉ **vài bước cấu hình**, các sếp có thể **quên đi việc đăng bài thủ công** và tập trung vào nội dung chất lượng hơn.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật Active** để bắt đầu tự động hóa!

🚀 **Hãy để LinkedIn của các sếp hoạt động một cách thông minh và tự động hóa!**