---
title: "🚀 Tự Động Hóa Quá Trình Nhập Nghiệp Viên M365 Toàn Diện Với SharePoint, OneDrive, Teams & AI Claude"
description: "Workflow này tự động hóa toàn bộ quy trình nhập nghiệp viên trong Microsoft 365, từ tạo tài khoản SharePoint, OneDrive, Teams đến gửi email chào mừng cá nhân hóa bằng AI Claude Sonnet 4 - tiết kiệm 80% thời gian thủ công cho bộ phận HR."
slug: "tieu-dong-hoa-qua-trinh-nhap-nghiep-vien-m365"
tags: [n8n, automation, hr, microsoft-365, ai-chatbot, self-hosted]
keywords: [tự động hóa nhập nghiệp viên, Microsoft 365 automation, SharePoint OneDrive Teams, AI Claude Sonnet 4, workflow n8n HR]
---

# 🚀 **Tự Động Hóa Quá Trình Nhập Nghiệp Viên M365 Toàn Diện Với AI Claude**

## **🔥 Nỗi Đau Của Bộ Phận HR**
Hiện nay, khi một nhân viên mới gia nhập công ty, bộ phận HR phải thực hiện **hàng chục bước thủ công** để hoàn tất quy trình nhập nghiệp viên:
- Tạo tài khoản SharePoint và cấu hình quyền truy cập
- Xây dựng không gian OneDrive cá nhân và các thư mục chuyên đề
- Tạo nhóm/channel riêng trong Teams
- Soạn thảo và gửi email chào mừng cá nhân hóa
- Theo dõi và báo cáo tiến độ cho quản lý

**Kết quả?** Thời gian trung bình **từ 30 phút đến 2 giờ/người**, dễ xảy ra lỗi nhân sự và mất tập trung vào công việc chính.

**Giải pháp?** Workflow này **tự động hóa toàn bộ quy trình** bằng n8n + AI Claude Sonnet 4, giúp HR **tiết kiệm 80% thời gian** và giảm thiểu sai sót.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so với thủ công (từ 2 giờ xuống còn 15 phút/người)
✅ **Cá nhân hóa hoàn toàn** email chào mừng bằng AI Claude (phù hợp với từng vị trí, bộ phận)
✅ **Hoạt động 24/7** mà không cần can thiệp của con người
✅ **Báo cáo tự động** tiến độ nhập nghiệp viên qua Teams
✅ **An toàn & ổn định** với hệ thống failsafe chống lỗi toàn diện
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (khuyến nghị VPS để chạy 24/7)
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Tham số API & Credentials**:
   - **Microsoft 365 Developer Account** (đăng ký tại [portal.azure.com](https://portal.azure.com/))
   - **Anthropic API Key** (đăng ký tại [anthropic.com](https://www.anthropic.com/))
   - **Tenant ID**, **Site ID** (SharePoint), **Group ID** (Teams) của công ty
   - **Email mặc định** để gửi welcome email (ví dụ: `hr@congty.com`)

3. **Cấu hình Teams**:
   - Channel mặc định để tạo nhóm mới (ví dụ: `#onboarding`)
   - Bot Teams có quyền gửi tin nhắn tự động

4. **Cấu hình SharePoint**:
   - Library mặc định để lưu thông tin nhập nghiệp viên (ví dụ: `Onboarding`)
   - Quyền truy cập cho bot SharePoint

---
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15628](https://n8n.io/workflows/15628) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor** (trang chủ → "+ New Workflow").
  2. Nhấn **"Import"** → **"From JSON"** và dán toàn bộ mã JSON.
  3. Chọn **"Import"** để hoàn tất.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **19 node** và **4 nhánh song song** (SharePoint, OneDrive, Teams, Email). Dưới đây là **các bước cấu hình quan trọng**:

##### **🔹 Node 1: Microsoft Agent 365 Trigger**
- **Cấu hình**:
  - Chọn **Trigger Type**: `@n8n/n8n-nodes-langchain.microsoftAgent365Trigger`
  - **Mention Keyword**: `@hrbot` (để HR kích hoạt bằng cách nhắn tin `@hrbot new-hire <tên-người>` trong Teams/Outlook)
  - **Payload Format**: Dùng regex để extraxt thông tin nhân viên (ví dụ: `Name: [A-Za-z ]+`, `Position: [A-Za-z ]+`, `Department: [A-Za-z ]+`)

##### **🔹 Node 2 & 3: Parse New Hire + SharePoint (Code Node)**
- **Cấu hình Code Node**:
  ```javascript
  // Dùng regex để extraxt dữ liệu từ payload
  const name = $input.all()[0].json.payload.name;
  const position = $input.all()[0].json.payload.position;
  const department = $input.all()[0].json.payload.department;

  // Trả về JSON chuẩn cho SharePoint
  return {
    json: {
      "EmployeeName": name,
      "Position": position,
      "Department": department,
      "Status": "Pending"
    }
  };
  ```

- **SharePoint Node**:
  - **Operation**: `Create List Item`
  - **Site ID**: ID của SharePoint site (lấy từ URL: `https://tencongty.sharepoint.com/sites/Onboarding/_api/web/lists/getbytitle('Onboarding')`)
  - **List Name**: `Onboarding`
  - **Columns**: Điền theo cấu trúc của bảng SharePoint (ví dụ: `EmployeeName`, `Position`, `Department`)

##### **🔹 Node 4-6: OneDrive (Tạo Thư Mục & Subfolders)**
- **OneDrive: Create Employee Folder**:
  - **Operation**: `createFolder`
  - **Path**: `/Users/${name}` (đổi `${name}` thành biến từ Code Node)
  - **Parent Path**: `/` (thư mục gốc OneDrive)

- **Build SubFolder Paths (Code Node)**:
  ```javascript
  // Tạo 5 thư mục mặc định (ví dụ: Documents, Contracts, Expenses, Projects, Personal)
  const subFolders = [
    `Documents/${name}`,
    `Contracts/${name}`,
    `Expenses/${name}`,
    `Projects/${name}`,
    `Personal/${name}`
  ];

  return { json: { subFolders } };
  ```

- **OneDrive: Create SubFolders**:
  - **Operation**: `createFolder`
  - **Path**: `${subFolder}` (lấy từ Code Node trên)

##### **🔹 Node 7-9: Teams (Tạo Channel & Post Tin Nhắn)**
- **Teams: Create Onboarding Channel**:
  - **Operation**: `createChannel`
  - **Group ID**: ID của nhóm Teams (lấy từ URL: `https://tencongty.microsoftteams.com/groups/...`)
  - **Display Name**: `${name}-Onboarding`
  - **Description**: `Channel dành riêng cho ${name} trong quá trình nhập nghiệp viên`

- **AI: Generate Welcome Email (Agent Node)**:
  - **Model**: `@n8n/n8n-nodes-langchain.agent`
  - **Prompt**:
    ```plaintext
    Tôi là HR Bot của công ty [Tên Công Ty]. Hãy soạn một email chào mừng cá nhân hóa cho nhân viên mới tên {name}, vị trí {position}, bộ phận {department}.
    Email phải bao gồm:
    1. Lời chào đón thân mật
    2. Thông tin cơ bản về công ty (mục tiêu, văn hóa)
    3. Link đến tài liệu nhập nghiệp viên (SharePoint)
    4. Thông tin về Teams channel mới (${name}-Onboarding)
    5. Lời khuyến khích và hỗ trợ
    ```
  - **Model Claude Sonnet 4**: Đảm bảo chọn `claude-sonnet-4-20250514`

- **Outlook: Send Welcome Email**:
  - **Operation**: `sendEmail`
  - **To**: `${email}` (lấy từ payload)
  - **Subject**: `🎉 Chào mừng bạn đến với [Tên Công Ty]!`
  - **Body**: Nội dung từ Agent Node

##### **🔹 Node 10-12: Wait & Merge (Đợi Tất Cả Các Nhánh Hoàn Thành)**
- **Wait: SP & OneDrive**: Đợi SharePoint và OneDrive hoàn tất.
- **Wait: Teams & Email**: Đợi Teams và Email hoàn tất.
- **Wait: All Branches**: Đợi tất cả các nhánh hoàn tất (bao gồm cả lỗi).

##### **🔹 Node 13-15: Build & Post HR Summary Card**
- **Build HR Summary Card (Code Node)**:
  ```javascript
  // Tạo card tổng kết với link và trạng thái
  const summary = {
    title: `📊 Tóm Tắt Nhập Nghiệp Viên: ${name}`,
    sections: [
      {
        activityTitle: "SharePoint",
        activitySubtitle: "✅ Hoàn tất",
        text: `Link: https://tencongty.sharepoint.com/sites/Onboarding/Lists/Onboarding/DispForm.aspx?ID=${sharepointId}`
      },
      {
        activityTitle: "OneDrive",
        activitySubtitle: "✅ Hoàn tất",
        text: `Link: https://tencongty.onedrive.com/...`
      },
      {
        activityTitle: "Teams",
        activitySubtitle: "✅ Hoàn tất",
        text: `Channel: ${name}-Onboarding`
      },
      {
        activityTitle: "Email",
        activitySubtitle: "✅ Gửi thành công",
        text: "Email chào mừng đã được gửi đến ${email}"
      }
    ]
  };

  return { json: summary };
  ```

- **Teams: Post HR Summary Card**:
  - **Operation**: `post`
  - **Channel ID**: ID của channel `#onboarding`
  - **Content**: JSON từ Code Node trên (sử dụng **Adaptive Card** để hiển thị đẹp)

##### **🔹 Node 16-18: Error Handling (Xử Lý Lỗi)**
- **Error Trigger**: Bắt tất cả lỗi từ các nhánh.
- **Build Error Alert Card (Code Node)**:
  ```javascript
  const errorCard = {
    title: `❌ Lỗi Trong Quá Trình Nhập Nghiệp Viên: ${name}`,
    sections: [
      {
        activityTitle: "Lỗi SharePoint",
        activitySubtitle: "❌ ${error.message}",
        text: `ID Lỗi: ${error.id}`
      },
      // Thêm các lỗi khác từ các nhánh
    ]
  };

  return { json: errorCard };
  ```

- **Teams: Post Error Alert**:
  - **Operation**: `post`
  - **Channel ID**: `#hr-alerts` (channel cảnh báo HR)
  - **Content**: JSON từ Code Node lỗi

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CẢI TIẾN TRONG THỰC TIỆN]
1. **Kết hợp với Power Automate**:
   - Sử dụng Power Automate để **cập nhật HRIS** (ví dụ: Workday, BambooHR) khi workflow hoàn tất.

2. **Lưu Log Tự Động**:
   - Thêm node **n8n-nodes-base.http** để gửi log đến **Google Sheets** hoặc **Datadog** để theo dõi.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n-nodes-base.schedule** để gửi báo cáo tổng hợp nhập nghiệp viên hàng tuần qua email.

4. **Cá nhân hóa thêm bằng AI**:
   - Sử dụng **LangChain Agent** để tự động **soạn thảo hợp đồng** hoặc **tạo tài liệu giới thiệu công ty** cho mỗi nhân viên mới.

5. **Tích hợp với Zoom**:
   - Thêm node **Zoom API** để tự động tạo cuộc họp chào mừng cho nhân viên mới.
:::

---

### 📌 **Kết Luận**
Workflow này **tự động hóa hoàn toàn** quy trình nhập nghiệp viên trong Microsoft 365, từ tạo tài khoản đến gửi email chào mừng cá nhân hóa bằng AI Claude Sonnet 4. **Không cần code**, chỉ cần cấu hình và chạy 24/7 trên VPS.

**🚀 Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình các credentials.
3. **Kích hoạt và thử nghiệm** với một nhân viên mẫu.

**Kết quả?** HR của các sếp sẽ **tiết kiệm hàng giờ mỗi tuần**, tập trung vào công việc chiến lược thay vì thủ công!

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/15628)**
**📩 Liên hệ tác giả**: Mychel Garzon - [mychel.garzon@gmail.com](mailto:mychel.garzon@gmail.com)