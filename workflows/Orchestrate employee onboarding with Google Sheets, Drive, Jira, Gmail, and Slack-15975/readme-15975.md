---
title: "🚀 Tự Động Hóa Quá Trình Nhập Nhân Viên (Onboarding) Toàn Diện Với n8n: Từ Webhook Đến Slack, Gmail & Jira"
description: "Giải pháp tự động hóa 100% không code giúp doanh nghiệp tự động hóa toàn bộ quy trình nhập nhân viên từ nhận yêu cầu đến hoàn tất, kết hợp Google Sheets, Google Drive, Jira, Gmail và Slack. Tiết kiệm thời gian lên đến 80% cho bộ phận HR và IT."
slug: "tieu-dong-hoa-qua-trinh-nhap-nhan-vien-n8n"
tags: [n8n, automation, hr-automation, google-sheets, jira, gmail, slack, no-code, self-hosted]
keywords: [tự động hóa nhập nhân viên, workflow n8n hr, tự động hóa jira google drive, tự động hóa onboarding, n8n google sheets, tự động hóa nhan vien]
---

# 🚀 **Tự Động Hóa Quá Trình Nhập Nhân Viên (Onboarding) Toàn Diện Với n8n**

### **Giải pháp cho nỗi đau của bộ phận HR và IT**
Nhập nhân viên là một trong những quy trình phức tạp và tốn thời gian nhất trong doanh nghiệp. Các sếp thường phải:
- **Nhập liệu thủ công** vào Google Sheets, Jira, và Google Drive.
- **Gửi email** xác nhận và hướng dẫn cho nhân viên mới.
- **Phân công công việc** cho IT và HR qua Slack/Jira.
- **Theo dõi tiến độ** qua nhiều hệ thống khác nhau, dễ bị lỗi hoặc quên bước.

**Kết quả?** Tốn thời gian, dễ sai sót, và không có báo cáo thống kê rõ ràng.

**Workflow này giải quyết tất cả đó!** Với **15 node n8n**, bạn có thể tự động hóa **tất cả quy trình nhập nhân viên** từ khi nhận yêu cầu đến khi hoàn tất, kết hợp **Google Sheets, Google Drive, Jira, Gmail và Slack** một cách mượt mà.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** cho bộ phận HR và IT.
- **Giảm sai sót** nhờ tự động hóa và kiểm tra dữ liệu.
- **Cá nhân hóa thông báo** cho mỗi nhân viên mới (email + Slack).
- **Theo dõi toàn diện** qua Google Sheets và Jira.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Báo cáo tự động** gửi cho HR khi quy trình hoàn tất.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
- **Tài khoản và API Key**:
  - **Google Sheets & Google Drive**: OAuth 2.0 credentials (cài đặt ở [Google Cloud Console](https://console.cloud.google.com/)).
  - **Jira Cloud**: API Token (tạo ở [Jira Settings](https://id.atlassian.com/manage-profile/security/api-tokens)).
  - **Gmail**: OAuth 2.0 credentials (cài đặt ở [Google Cloud Console](https://console.cloud.google.com/)).
  - **Slack**: API Token (tạo ở [Slack API](https://api.slack.com/apps)).
- **Google Sheet mẫu**: Một bảng Google Sheets để lưu lịch sử nhập nhân viên (cấu trúc sẽ được hướng dẫn).
- **Jira Project**: Một dự án Jira để tạo Epic và Task cho quy trình onboarding.
- **Webhook URL**: Một URL để nhận dữ liệu từ hệ thống nội bộ (hoặc sử dụng Webhook của n8n).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/15975) hoặc sử dụng file JSON đã cung cấp.
2. Mở **n8n Editor** (trang chủ của n8n).
3. Nhấp vào **Import** (icon "↑" ở góc trên bên phải).
4. Chọn file JSON và nhấp **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor**.
2. Nhấp vào **Create new workflow** (hoặc mở một workflow trống).
3. Nhấp vào **Import** và chọn **Paste JSON**.
4. Dán toàn bộ JSON từ file và nhấp **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Webhook Trigger**
- **Node**: `New Hire Webhook Trigger`
- **Cấu hình**:
  - **Path**: `employee-onboarding` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (sử dụng Webhook mặc định của n8n).
- **Lưu ý**:
  - Nếu sử dụng Webhook từ hệ thống nội bộ, đảm bảo hệ thống đó gửi **dữ liệu JSON** theo cấu trúc:
    ```json
    {
      "fullName": "Nguyễn Văn A",
      "workEmail": "a@doanhnghiep.com",
      "department": "Marketing",
      "managerEmail": "manager@doanhnghiep.com",
      "phone": "0123456789"
    }
    ```
  - Nếu không chắc, **test với dữ liệu mẫu** trước khi chạy thực tế.

---

#### **B. Cấu hình Google Sheets**
- **Node**: `Log New Hire Record` và `Update Onboarding Tracker Status`
- **Cấu hình chung**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
  - **Sheet Name**: Đặt tên bảng (ví dụ: `Onboarding Tracker`).
  - **Range**: Đặt tên sheet (ví dụ: `Sheet1`).
- **Cấu trúc Google Sheet**:
  | Column Name       | Data Type  |
  |--------------------|------------|
  | `fullName`         | Text       |
  | `workEmail`        | Email      |
  | `department`       | Text       |
  | `managerEmail`     | Email      |
  | `status`           | Text       |
  | `onboardingDate`   | Date       |
  | `driveFolderLink`  | URL        |
  | `jiraEpicLink`     | URL        |

- **Lưu ý**:
  - Node `Log New Hire Record` **thêm dữ liệu mới** (`operation: append`).
  - Node `Update Onboarding Tracker Status` **cập nhật trạng thái** (`operation: update`).

---

#### **C. Cấu hình Google Drive**
- **Node**: `Create Employee Onboarding Folder`, `Grant Employee Folder Access`, `Find Created Onboarding Folder`
- **Cấu hình chung**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder Name**: Sử dụng biến `{{ $node["Normalize Employee Data"].json["fullName"] }}` (ví dụ: `Onboarding - Nguyễn Văn A`).
- **Lưu ý**:
  - **Folder Parent**: Chọn **Google Drive root** hoặc một folder cụ thể (ví dụ: `Onboarding Folders`).
  - **Grant Access**: Điền email nhân viên vào trường `email` (sử dụng biến `{{ $node["Normalize Employee Data"].json["workEmail"] }}`).
  - **Verify Folder Match**: Node này **kiểm tra lại** folder đã tạo có đúng tên không.

---

#### **D. Cấu hình Jira**
- **Node**: `Create IT Access Task`, `Create HR Checklist Task`, `Create Onboarding Epic`
- **Cấu hình chung**:
  - **Credentials**: Chọn `jiraSoftwareCloudApi`.
  - **Project Key**: Đặt tên dự án Jira (ví dụ: `ONB`).
  - **Issue Type**:
    - **Epic**: `Epic` (cho quy trình onboarding).
    - **Task**: `Task` (cho IT và HR).
- **Lưu ý**:
  - **Epic Name**: Sử dụng biến `{{ $node["Normalize Employee Data"].json["fullName"] }} - Onboarding`.
  - **Task Description**:
    - **IT Task**: `Setup IT access for {{ $node["Normalize Employee Data"].json["fullName"] }}`.
    - **HR Task**: `Complete HR onboarding for {{ $node["Normalize Employee Data"].json["fullName"] }}`.
  - **Assign To**: Gán cho thành viên IT/HR cụ thể (ví dụ: `it-team@doanhnghiep.com`).

---

#### **E. Cấu hình Gmail**
- **Node**: `Send Welcome Email to Employee`, `Send HR Completion Summary`
- **Cấu hình chung**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **From Email**: Đặt email gửi (ví dụ: `hr@doanhnghiep.com`).
- **Lưu ý**:
  - **Welcome Email**:
    - **Subject**: `Welcome to {{ $node["Normalize Employee Data"].json["department"] }}!`
    - **Body**: Thêm link Google Drive và hướng dẫn onboarding.
  - **Completion Summary**:
    - **Subject**: `Onboarding Completed: {{ $node["Normalize Employee Data"].json["fullName"] }}`
    - **Body**: Tóm tắt thông tin và link Jira.

---

#### **F. Cấu hình Slack**
- **Node**: `Send Team Onboarding Notification`
- **Cấu hình**:
  - **Credentials**: Chọn `slackApi`.
  - **Channel**: Chọn channel Slack (ví dụ: `#hr-updates`).
  - **Message**: Sử dụng template:
    ```plaintext
    *New Onboarding Started!*
    👋 **{{ $node["Normalize Employee Data"].json["fullName"] }}** ({{ $node["Normalize Employee Data"].json["workEmail"] }})
    📌 **Department**: {{ $node["Normalize Employee Data"].json["department"] }}
    🔗 **Drive Folder**: [{{ $node["Find Created Onboarding Folder"].json["webViewLink"] }}]({{ $node["Find Created Onboarding Folder"].json["webViewLink"] }})
    📋 **Jira Epic**: [{{ $node["Create Onboarding Epic"].json["key"] }}]({{ $node["Create Onboarding Epic"].json["self"] }})
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một yêu cầu test đến Webhook (ví dụ bằng Postman hoặc cURL):
     ```bash
     curl -X POST https://your-n8n-url/webhook/employee-onboarding \
     -H "Content-Type: application/json" \
     -d '{"fullName": "Test User", "workEmail": "test@example.com", "department": "IT", "managerEmail": "manager@example.com"}'
     ```
   - Kiểm tra các node có hoạt động không (màu xanh lá cây).
2. **Bật Active workflow**:
   - Nhấp vào **Active** ở góc trên bên phải của canvas.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tích hợp với hệ thống nội bộ**
- Nếu doanh nghiệp có **API hoặc hệ thống CRM**, thay vì sử dụng Webhook của n8n, bạn có thể **cấu hình Webhook từ hệ thống đó** để gửi dữ liệu trực tiếp vào n8n.

### **2. Lưu log và báo cáo định kỳ**
- Thêm **node `googleSheets`** để tạo **báo cáo hàng tháng** về số lượng nhân viên mới nhập.
- Sử dụng **node `gmail`** để gửi báo cáo tự động vào cuối tháng.

### **3. Kết hợp với LLM (ChatGPT, Bard)**
- Thêm **node `n8n-nodes-base.llm`** để tự động **tạo nội dung email** cho nhân viên mới dựa trên thông tin trong Google Sheets.

### **4. Thông báo lỗi tự động**
- Thêm **node `slack`** để gửi thông báo lỗi nếu dữ liệu không hợp lệ (ví dụ: email không đúng định dạng).

### **5. Tự động xóa folder cũ**
- Thêm **node `googleDrive`** để xóa folder onboarding sau **30 ngày** (sử dụng **node `set`** để tính ngày và **node `googleDrive`** với `operation: delete`).

---

## 📌 **Kết luận**
Workflow này **giải phóng bộ phận HR và IT** khỏi công việc lặp lại, **giảm sai sót**, và **cung cấp tính minh bạch** cho toàn bộ quy trình onboarding. Với **n8n**, bạn không cần viết một dòng code nào cả – chỉ cần **cấu hình và chạy**!

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với dữ liệu mẫu** và **bật chạy**!

**Nếu có vấn đề**, để lại comment bên dưới hoặc liên hệ với **WeblineIndia** (tác giả workflow) qua [n8n.io](https://n8n.io/workflows/15975).

---
**Chúc các sếp thành công với tự động hóa onboarding!** 🚀