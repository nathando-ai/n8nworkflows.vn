---
title: "🚀 Tự Động Hóa Báo Cáo Ứng Viên Hàng Ngày Theo Chức Vụ Với Gemini AI - Giúp Quản Lý Tuyển Dụng Tiết Kiệm 10+ Giờ/Tuần"
description: "Workflow tự động hóa lấy tất cả email ứng viên mới trong Gmail, trích xuất thông tin chi tiết bằng Gemini AI, phân loại theo chức vụ và quản lý tuyển dụng, gửi báo cáo HTML định kỳ cho các nhà quản lý tuyển dụng. Giúp doanh nghiệp tiết kiệm thời gian, giảm thiểu sai sót và tối ưu quy trình tuyển dụng."
slug: "tieu-dong-hoa-bao-cao-ung-vien-hang-ngay-gemini-ai"
tags: [n8n, automation, ai-summarization, gemini-ai, gmail-automation, hiring-manager]
keywords: [tự động hóa tuyển dụng, gemini ai n8n, báo cáo ứng viên hàng ngày, gửi email tự động gmail, phân loại ứng viên theo chức vụ, tiết kiệm thời gian tuyển dụng]
---

# 🚀 **Tự Động Hóa Báo Cáo Ứng Viên Hàng Ngày Theo Chức Vụ Với Gemini AI**

### **Giải Pháp Cho Nỗi Đau Của Các Quản Lý Tuyển Dụng**
Các sếp tuyển dụng thường phải mất **giờ đồng hồ** mỗi ngày để:
- **Lọc và đọc** hàng chục email ứng viên mới từ Gmail.
- **Trích xuất thông tin** như tên, email, chức vụ, kỹ năng từ email dài dòng.
- **Phân loại ứng viên** theo chức vụ và gán cho quản lý phù hợp.
- **Gửi báo cáo** định kỳ cho đội tuyển, dẫn đến **sai sót** và **trễ nải** trong quyết định tuyển dụng.

**Workflow này tự động hóa toàn bộ quy trình trong 10 phút/ngày**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/tuần** để tập trung vào phỏng vấn và chiến lược tuyển dụng.
✅ **Tránh sai sót** khi trích xuất thông tin bằng trí tuệ nhân tạo Gemini AI.
✅ **Cá nhân hóa báo cáo** theo chức vụ và quản lý tuyển dụng.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình tuyển dụng hàng ngày** (không cần code).
- **Báo cáo HTML đẹp mắt** với thông tin ứng viên được phân loại rõ ràng.
- **Gửi email tự động** đến từng quản lý tuyển dụng với nội dung cá nhân hóa.
- **Tiết kiệm chi phí** so với giải pháp SaaS (không cần trả phí tháng).
- **Dễ dàng mở rộng** cho nhiều chức vụ và quản lý.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail chính** (để lấy email ứng viên và gửi báo cáo).
   - **Credentials**: `gmailOAuth2` (cấu hình trong n8n).
2. **API Key Google Gemini** (để trích xuất thông tin ứng viên).
   - **Credentials**: `googlePalmApi` (cấu hình trong n8n).
3. **Danh sách quản lý tuyển dụng** (gán email cho từng chức vụ).
   - Ví dụ:
     ```json
     {
       "Backend Developer": "manager.backend@example.com",
       "Frontend Developer": "manager.frontend@example.com",
       "Product Manager": "manager.product@example.com"
     }
     ```
4. **Label "applicants"** trong Gmail (để workflow lọc email ứng viên).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7699](https://n8n.io/workflows/7699) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON.
  3. Chọn **Create Workflow** để lưu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Schedule Trigger (Khởi động hàng ngày)**
- **Thời gian**: 6PM IST (hoặc điều chỉnh theo múi giờ của doanh nghiệp).
- **Múi giờ**: Chọn `Asia/Kolkata` (hoặc `Asia/Ho_Chi_Minh` nếu ở Việt Nam).
- **Lưu ý**: Nếu muốn chạy ở múi giờ khác, chỉnh `timezone` trong **Advanced Settings**.

##### **🔹 Node 2 & 3: Fetch & Read Applicant Emails (Lấy email ứng viên)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
- **Operation**: `getAll` (lấy tất cả email mới trong 24h).
- **Label**: Chỉ lấy email có **label "applicants"**.
- **Lưu ý**:
  - Nếu email ứng viên không có label, workflow sẽ bỏ qua.
  - Đảm bảo **gmailOAuth2** có quyền đọc email.

##### **🔹 Node 4: Extract Applicant Details (Trích xuất thông tin bằng Gemini AI)**
- **Credentials**: Chọn `googlePalmApi` (API Key Google Gemini).
- **Prompt mẫu** (cần chỉnh sửa theo yêu cầu):
  ```plaintext
  Extract applicant details from this email in JSON format:
  - Name
  - Email
  - Role
  - Skills
  - Experience
  - Education
  ```
- **Lưu ý**:
  - Nếu API Key không hoạt động, kiểm tra **quota** và **cấp quyền API**.
  - Đảm bảo email ứng viên có đủ thông tin để AI trích xuất.

##### **🔹 Node 5: Assign Manager Emails (Gán quản lý cho ứng viên)**
- **Code Node**: Các sếp cần chỉnh sửa logic gán email quản lý theo chức vụ.
  ```javascript
  // Ví dụ: Mapping chức vụ -> email quản lý
  const roleToManager = {
    "Backend Developer": "manager.backend@example.com",
    "Frontend Developer": "manager.frontend@example.com",
    "Product Manager": "manager.product@example.com"
  };

  // Nếu không tìm thấy chức vụ, gán email mặc định
  const defaultManager = "default.manager@example.com";

  // Gán email quản lý cho ứng viên
  const managerEmail = roleToManager[applicant.role] || defaultManager;
  return { ...applicant, managerEmail };
  ```
- **Lưu ý**:
  - Sửa `roleToManager` phù hợp với doanh nghiệp.
  - Đảm bảo email quản lý tồn tại và có quyền nhận email.

##### **🔹 Node 6: Group & Build HTML Tables (Tạo báo cáo HTML)**
- **Code Node**: Chỉnh sửa logic nhóm ứng viên theo quản lý và chức vụ.
  ```javascript
  // Nhóm ứng viên theo quản lý và chức vụ
  const groupedData = {};
  applicants.forEach(applicant => {
    if (!groupedData[applicant.managerEmail]) {
      groupedData[applicant.managerEmail] = {
        managerEmail: applicant.managerEmail,
        roleGroups: {}
      };
    }
    if (!groupedData[applicant.managerEmail].roleGroups[applicant.role]) {
      groupedData[applicant.managerEmail].roleGroups[applicant.role] = [];
    }
    groupedData[applicant.managerEmail].roleGroups[applicant.role].push(applicant);
  });

  // Chuyển thành HTML
  const htmlTables = Object.entries(groupedData).map(([managerEmail, data]) => {
    return `
      <h2>Báo cáo ứng viên cho ${managerEmail}</h2>
      ${Object.entries(data.roleGroups).map(([role, applicants]) => `
        <h3>${role}</h3>
        <table border="1">
          <tr>
            <th>Tên</th>
            <th>Email</th>
            <th>Kỹ năng</th>
            <th>Trình độ</th>
          </tr>
          ${applicants.map(applicant => `
            <tr>
              <td>${applicant.name}</td>
              <td>${applicant.email}</td>
              <td>${applicant.skills}</td>
              <td>${applicant.experience}</td>
            </tr>
          `).join('')}
        </table>
      `).join('')
    `;
  }).join('');
  return { htmlTables };
  ```
- **Lưu ý**:
  - Chỉnh sửa **cột trong bảng** theo yêu cầu (ví dụ thêm cột "Trình độ").
  - Đảm bảo **HTML có định dạng rõ ràng** để dễ đọc.

##### **🔹 Node 7: Send Digest to Managers (Gửi email báo cáo)**
- **Credentials**: Chọn `gmailOAuth2` (gửi email từ tài khoản chính).
- **Nội dung email**:
  ```html
  <h1>Báo cáo ứng viên mới (${new Date().toLocaleDateString()})</h1>
  ${htmlTables}
  <p>Trân trọng,</p>
  <p>Hệ thống Tự động Hóa Tuyển Dụng</p>
  ```
- **Lưu ý**:
  - Chỉnh sửa **tiêu đề email** và **nội dung** theo yêu cầu.
  - Đảm bảo **gmailOAuth2** có quyền gửi email.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra từng node.
   - Đảm bảo **email mẫu** được trích xuất và gửi đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có ứng viên mới.
   ```javascript
   // Ví dụ: Gửi thông báo Slack
   const slackMessage = `🚀 Ứng viên mới cho ${applicant.role}:\n${applicant.name} (${applicant.email})`;
   return { text: slackMessage };
   ```

2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** để ghi lại lịch sử ứng viên.
   ```javascript
   // Ví dụ: Ghi vào Google Sheets
   const sheetData = {
     "Tên": applicant.name,
     "Email": applicant.email,
     "Chức vụ": applicant.role,
     "Ngày nhận": new Date().toISOString()
   };
   return { data: [sheetData] };
   ```

3. **Gửi báo cáo định kỳ (tuần/Tháng)**:
   - Chỉnh sửa **Schedule Trigger** để chạy hàng tuần/tháng.
   - Ví dụ: `0 0 * * 0` (chạy hàng chủ nhật lúc 00:00).

4. **Tích hợp với CRM (HubSpot/Salesforce)**:
   - Thêm node **HubSpot** hoặc **Salesforce** để tự động thêm ứng viên vào hệ thống.

---

### 📌 **Kết Luận**
Workflow **Daily Applicant Digest by Role with Gemini AI** là giải pháp **tự động hóa hoàn chỉnh** cho quy trình tuyển dụng, giúp các sếp:
✔ **Tiết kiệm thời gian** để tập trung vào công việc chiến lược.
✔ **Tránh sai sót** khi trích xuất thông tin bằng trí tuệ nhân tạo.
✔ **Cá nhân hóa báo cáo** theo chức vụ và quản lý.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**🚀 Hãy áp dụng ngay workflow này và tự động hóa tuyển dụng của doanh nghiệp trong vòng 30 phút!**
Nếu có vấn đề, các sếp có thể **comment dưới bài** hoặc liên hệ với **WeblineIndia** (tác giả của workflow) qua [đây](https://www.weblineindia.com/).

---