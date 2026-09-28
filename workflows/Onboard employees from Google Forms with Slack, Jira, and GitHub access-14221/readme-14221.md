---
title: "🚀 Tự Động Hóa Onboarding Nhân Viên Từ Google Form Sang Slack, Jira & GitHub - Giảm Thời Gian 90% Cho HR"
description: "Workflow tự động hóa hoàn toàn không cần code giúp HR tự động thêm nhân viên mới vào Slack, cấp quyền Jira và GitHub, đồng thời theo dõi tiến độ onboarding từ Google Form. Giúp tiết kiệm thời gian, giảm sai sót và cải thiện trải nghiệm nhân viên."
slug: "tieu-dong-hoa-onboarding-nhan-vien-tu-google-form"
tags: [n8n, automation, hr, google-forms, slack, jira, github, no-code]
keywords: [tự động hóa onboarding nhân viên, n8n workflow hr, google form tự động hóa, cấp quyền jira github tự động, giảm thời gian onboarding]
---

# 🚀 **Tự Động Hóa Onboarding Nhân Viên Từ Google Form Sang Slack, Jira & GitHub**

### **Giải pháp hoàn toàn không cần code cho HR**
Tự động hóa toàn bộ quy trình onboarding nhân viên mới từ khi nhận thông tin từ Google Form đến cấp quyền Slack, Jira và GitHub. **Không cần viết một dòng code nào**, chỉ cần cấu hình và chạy 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình onboarding, giảm thời gian thủ công từ **30 phút/lần** xuống **5 giây/lần**.
- **Chính xác 100%**: Không còn sai sót trong việc cấp quyền Slack, Jira hoặc GitHub.
- **Cá nhân hóa quyền hạn**: Nhân viên mới được tự động thêm vào Slack channel phù hợp và cấp quyền Jira/GitHub theo bộ phận.
- **Theo dõi tiến độ**: Tự động cập nhật trạng thái onboarding trên Google Sheet.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản Google Forms + Google Sheet**:
  - Google Sheet chứa form phản hồi (cần cấu hình **Google Sheets Trigger**).
  - Cột `email`, `department`, `role` (cần được định nghĩa trong form).
- **Tài khoản Slack**:
  - Workspace Slack đã cấu hình với các channel bộ phận (ví dụ: `#marketing`, `#software`).
  - **Admin Slack** để thông báo khi nhân viên đã được onboarding.
- **Tài khoản Jira Cloud**:
  - Project keys và component IDs cho các bộ phận (ví dụ: `PROJ-1` cho Marketing).
  - URL của site Jira.
- **Tài khoản GitHub**:
  - Tổ chức GitHub và repository phù hợp với bộ phận **Software**.
- **API Keys**:
  - **Google Sheets OAuth2** (để đọc và cập nhật sheet).
  - **Slack API Token** (để gửi thông báo và quản lý channel).
  - **Jira API Token** (để tạo task và mời người dùng).
  - **GitHub Personal Access Token** (để cấp quyền repository).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14221](https://n8n.io/workflows/14221) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON hoặc tải file JSON.
- Workflow sẽ tự động tạo ra **10 nodes** như mô tả dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Google Sheets Trigger**
- **Node**: `New Google Form Response`
  - **Google Sheets OAuth2Api**: Chọn credential đã cấu hình trước.
  - **Sheet ID**: Điền ID của Google Sheet chứa form phản hồi (tìm trong URL sheet: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/edit`).
  - **Trigger**: Chọn `New row` để kích hoạt khi có phản hồi mới.

##### **B. Cấu hình Slack**
- **Node**: `Add user to department Slack channel`
  - **Slack API**: Chọn credential Slack đã cấu hình.
  - **Channel IDs**: Trong node **Code** (`Map department and team configuration`), các sếp cần cập nhật **mapping giữa department và channel Slack**:
    ```javascript
    const departmentToChannel = {
      "Marketing": "#marketing",
      "Software": "#software",
      "Sales": "#sales",
      "HR": "#hr"
    };
    ```
    - Thay thế các tên channel phù hợp với workspace Slack của công ty.

- **Node**: `Notify admin if already processed`
  - **Slack API**: Chọn credential Slack.
  - **User ID Admin**: Điền ID của admin Slack (tìm trong `/users` trên Slack API).

##### **C. Cấu hình Jira**
- **Node**: `Create onboarding task in Jira`
  - **Jira Software Cloud API**: Chọn credential Jira.
  - **Project Key**: Trong node **Code**, cập nhật `projectKey` theo cấu trúc:
    ```javascript
    const projectKeys = {
      "Software": "PROJ-SOFTWARE",
      "Marketing": "PROJ-MARKETING"
    };
    ```
    - Thay thế `PROJ-SOFTWARE` và `PROJ-MARKETING` bằng project keys thực tế.

- **Node**: `Invite user to Jira`
  - **URL Jira**: Điền URL của site Jira (ví dụ: `https://yourcompany.atlassian.net`).
  - **Headers**: Thêm `Authorization: Bearer {JIRA_API_TOKEN}`.

##### **D. Cấu hình GitHub (nếu nhân viên thuộc bộ phận Software)**
- **Node**: `Add user to GitHub repository`
  - **URL GitHub**: Cập nhật trong node **HTTP Request**:
    ```
    https://api.github.com/user/repos/{ORG_NAME}/{REPO_NAME}/collaborators/{EMAIL}
    ```
    - Thay `{ORG_NAME}` và `{REPO_NAME}` bằng tổ chức và repository phù hợp.
  - **Headers**: Thêm `Authorization: token {GITHUB_TOKEN}`.

##### **E. Cập nhật Google Sheet**
- **Node**: `Update Google Sheet status to completed`
  - **Google Sheets OAuth2Api**: Chọn credential đã cấu hình.
  - **Range**: Điền `Sheet1!A2` (hoặc tương ứng với ô chứa trạng thái onboarding).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** với dữ liệu mẫu từ Google Form.
   - Kiểm tra:
     - Slack: Nhân viên được thêm vào channel phù hợp.
     - Jira: Task onboarding được tạo và người dùng được mời.
     - GitHub: (nếu thuộc Software) quyền được cấp.
     - Google Sheet: Trạng thái được cập nhật thành `completed`.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm thông báo tự động**:
   - Kết hợp với **Slack** để gửi tin nhắn xác nhận onboarding thành công cho nhân viên mới (sử dụng node **Slack** với template cá nhân hóa).

2. **Lưu log hoạt động**:
   - Thêm node **StickyNote** để ghi lại lịch sử onboarding (ví dụ: `Onboarded: {email} on {date}`).

3. **Báo cáo định kỳ**:
   - Sử dụng **Google Sheets** + **Google Apps Script** để tự động gửi báo cáo số lượng nhân viên onboarding thành công hàng tháng qua email.

4. **Tích hợp với Microsoft Teams**:
   - Thay thế node Slack bằng **Microsoft Teams** để thông báo trên Teams.

5. **Cập nhật quyền động**:
   - Nếu nhân viên chuyển bộ phận, thêm logic trong node **Code** để xóa khỏi channel cũ và thêm vào channel mới.

---

### 📌 **Kết luận**
Workflow này **giải phóng HR khỏi công việc thủ công mệt mỏi**, giúp tự động hóa toàn bộ quy trình onboarding từ khi nhận thông tin từ Google Form đến cấp quyền Slack, Jira và GitHub. **Chỉ cần cấu hình 1 lần**, workflow sẽ hoạt động tự động cho tất cả nhân viên mới.

**Hành động ngay**:
1. Import workflow vào n8n của mình.
2. Cập nhật các credential và cấu hình theo hướng dẫn.
3. Bật **Active** và bắt đầu tự động hóa onboarding!

---
**💡 Cần hỗ trợ thêm?**
- Trả lời câu hỏi trong [n8n Community](https://community.n8n.io/).
- Liên hệ với tác giả Natnail Getachew qua [GitHub](https://github.com/natnail) để chia sẻ ý tưởng cải tiến.