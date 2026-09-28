---
title: "🔒 **Tự Động Hoàn Tất Quá Trình Thoát Việc (Offboarding) cho Nhân Viên: Khóa Tài Khoản Redmine & GitLab bằng Odoo 18 - N8N**"
description: "Giải pháp tự động hóa 100% không cần code để khóa tài khoản Redmine và GitLab cho nhân viên sau ngày cuối cùng làm việc, giảm thiểu rủi ro an toàn thông tin và tiết kiệm thời gian cho HR/IT. Chỉ cần kết nối Odoo 18, Redmine và GitLab, workflow sẽ hoạt động tự động hàng ngày."
slug: "tieu-dong-hoan-tat-qua-trinh-thoat-viec-odoo-redmine-gitlab"
tags: [n8n, automation, hr, redmine, gitlab, odoo, self-hosted, no-code, api-integration, security]
keywords: [tự động hóa offboarding, khóa tài khoản redmine gitlab, n8n workflow hr, tự động hóa thoát việc, odoo api, redmine api, gitlab api, tự động hóa an toàn thông tin]
---

# 🚀 **Tự Động Hoàn Tất Quá Trình Thoát Việc (Offboarding) cho Nhân Viên: Khóa Tài Khoản Redmine & GitLab bằng Odoo 18**

## **💥 Nỗi Đau Của Các Sếp: Offboarding Chậm Chạp, Rủi Ro An Toàn Thông Tin**
Hàng ngày, các bộ phận HR và IT phải đối mặt với quá trình **thoát việc (offboarding)** phức tạp, tốn thời gian và dễ xảy ra lỗi:
- **HR** phải theo dõi và xác nhận ngày kết thúc hợp đồng của từng nhân viên.
- **IT** phải thủ công tìm kiếm và khóa tài khoản trên **Redmine, GitLab, Jira, Slack, email** để tránh rò rỉ dữ liệu.
- **Rủi ro an toàn thông tin** tăng cao khi tài khoản cũ vẫn hoạt động, đặc biệt là trong môi trường làm việc phân tán.
- **Không tuân thủ chính sách bảo mật**, dẫn đến vi phạm quy định pháp luật về quản lý thông tin nhạy cảm.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** bằng **n8n**, kết nối với **Odoo 18, Redmine và GitLab**, sẽ:
✅ **Khóa tài khoản Redmine & GitLab** ngay sau ngày cuối cùng làm việc.
✅ **Xóa quyền truy cập vào các nhóm dự án** trên Redmine.
✅ **Gửi báo cáo tự động** về quá trình offboarding cho HR/IT.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian IT/HR**: Không cần tìm kiếm và khóa tài khoản thủ công.
- **Giảm thiểu rủi ro an toàn thông tin**: Tài khoản được khóa ngay sau ngày cuối cùng làm việc.
- **Tuân thủ chính sách bảo mật**: Hoạt động tự động, không phụ thuộc vào con người.
- **Báo cáo chi tiết**: Theo dõi được tất cả các tài khoản đã được xử lý.
- **Hoạt động liên tục**: Chỉ cần cài đặt 1 lần, workflow sẽ tự động chạy hàng ngày.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **API Key của Odoo 18** (để truy cập thông tin nhân viên và ngày kết thúc hợp đồng).
2. **API Key Admin của Redmine** (để khóa tài khoản và xóa quyền truy cập).
3. **Personal Access Token Admin của GitLab** (để khóa tài khoản).
4. **Thời gian chạy định kỳ** (ví dụ: 17:00 hàng ngày, trừ ngày cuối tuần).
5. **(Tùy chọn) Webhook Slack/Teams hoặc SMTP** để gửi báo cáo kết quả.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11941](https://n8n.io/workflows/11941) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **"Import"** và chọn file JSON.
  3. Hoặc nhấn **"Create"** → **"Import"** và dán JSON.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **31 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **🔹 Step 1: Schedule Trigger (Định thời gian chạy)**
- **Cấu hình**: Chọn **"Daily"** và thời gian **17:00** (hoặc tùy chỉnh theo nhu cầu).
- **Lưu ý**:
  - **Không chạy vào ngày cuối tuần** (nếu cần, thêm điều kiện trong node `code`).
  - **Test run** trước khi bật **Active**.

##### **🔹 Step 4: Get Employee Resignation in Odoo 18 (Lấy thông tin nhân viên thoát việc)**
- **API Endpoint**: `https://[your-odoo-domain]/api/v8/hr_contract` (hoặc tương tự).
- **Headers**:
  - `Authorization: Bearer [API_KEY_ODOO]`
  - `Content-Type: application/json`
- **Query**:
  ```json
  {
    "filters": [
      ["date_end", "=", "${{ $datetime(2024-01-01) }}"]  // Ngày hiện tại
    ],
    "fields": ["id", "employee_id", "name", "date_end"]
  }
  ```
- **Lưu ý**:
  - Đảm bảo **API Key Odoo** có quyền đọc dữ liệu `hr_contract`.
  - **Test API** trước để xác nhận dữ liệu trả về đúng định dạng.

##### **🔹 Step 9: Get employee information in Odoo 18 (Lấy email làm việc)**
- **API Endpoint**: `https://[your-odoo-domain]/api/v8/hr_employee` (hoặc tương tự).
- **Headers**: Giống như Step 4.
- **Query**:
  ```json
  {
    "filters": [["id", "=", "${{ $node["Step4"].jsonpath("$.id") }}"]],
    "fields": ["email", "name"]
  }
  ```
- **Lưu ý**:
  - **Node `Step10: Handle work_email`** sẽ **trích xuất email** từ dữ liệu Odoo để sử dụng cho Redmine và GitLab.

##### **🔹 Step 11-18: Lock & Remove Redmine Accounts (Khóa và xóa quyền trên Redmine)**
- **API Endpoint Redmine**:
  - **Lấy thông tin người dùng**: `https://[your-redmine-domain]/issues.json?func=show_user&user_id=${{ $node["Step11"].jsonpath("$.id") }}`
  - **Khóa tài khoản**: `PUT https://[your-redmine-domain]/users/${{ $node["Step11"].jsonpath("$.id") }}.json`
    ```json
    {
      "user": {
        "locked": true
      }
    }
    ```
  - **Xóa quyền nhóm**: `DELETE https://[your-redmine-domain]/memberships/${{ $node["Step16"].jsonpath("$.id") }}`
- **Headers**:
  - `X-Redmine-API-Key: [YOUR_REDMINE_API_KEY]`
  - `Content-Type: application/json`
- **Lưu ý**:
  - **Node `Step17: Loop Over memberships_id`** sẽ **lặp qua tất cả nhóm** của người dùng để xóa quyền.
  - **Test API Redmine** trước để đảm bảo không xảy ra lỗi 404 hoặc 403.

##### **🔹 Step 19-28: Block GitLab Accounts (Khóa tài khoản GitLab)**
- **API Endpoint GitLab**:
  - **Lấy thông tin người dùng**: `GET https://gitlab.example.com/api/v4/users?username=${{ $node["Step19"].jsonpath("$.email") }}`
  - **Khóa tài khoản**: `PUT https://gitlab.example.com/api/v4/users/${{ $node["Step19"].jsonpath("$.id") }}`
    ```json
    {
      "active": false
    }
    ```
- **Headers**:
  - `PRIVATE-TOKEN: [YOUR_GITLAB_PERSONAL_ACCESS_TOKEN]`
  - `Content-Type: application/json`
- **Lưu ý**:
  - **Node `Step20-22`** sẽ **kiểm tra** xem người dùng có tồn tại và **không bị khóa/deactivate** trước khi thực hiện khóa.
  - **Test API GitLab** trước để đảm bảo token có quyền admin.

##### **🔹 Node Code (Xử lý lỗi và log)**
- **Node `Step6: Check if there is a valid record`** và **`Step29: Code`** sẽ **lọc bỏ dữ liệu không hợp lệ** và **log lỗi** nếu có.
- **Lưu ý**:
  - **Cập nhật mã JavaScript** trong node `code` nếu cần xử lý trường hợp đặc biệt (ví dụ: email không đúng định dạng).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu (ví dụ: 1 nhân viên thoát việc).
2. **Bật Active** workflow.
3. **Kiểm tra log** trong **n8n Dashboard** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CẬP NHẬT & MỞ RỘNG]
- **Thêm Slack/Teams Notification**:
  - Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để gửi báo cáo kết quả.
  - Ví dụ:
    ```json
    {
      "text": "🚨 Offboarding Report:\n- User: ${{ $node["Step9"].jsonpath("$.name") }}\n- Email: ${{ $node["Step9"].jsonpath("$.email") }}\n- Status: Locked on Redmine & GitLab"
    }
    ```
- **Lưu Log vào Database/Google Sheets**:
  - Sử dụng **node `n8n-nodes-base.googleSheets`** hoặc **`n8n-nodes-base.database`** để ghi lại lịch sử offboarding.
- **Thêm Jira/Confluence**:
  - Nếu công ty sử dụng **Jira**, thêm **node `n8n-nodes-base.jira`** để khóa tài khoản.
- **Báo cáo định kỳ**:
  - Sử dụng **node `n8n-nodes-base.email`** để gửi báo cáo hàng tuần cho HR.
- **Retry Mechanism**:
  - Cập nhật node `code` để **thử lại** nếu API trả về lỗi (ví dụ: 429 Too Many Requests).

---

### 📌 **Kết Luận: Tự Động Hóa Offboarding - Giải Pháp An Toàn & Tiết Kiệm Thời Gian**
Workflow này **giải quyết triệt để** vấn đề **thoát việc thủ công**, giúp:
✔ **IT không phải tìm kiếm và khóa tài khoản** một cách mệt mỏi.
✔ **HR có báo cáo chi tiết** về quá trình offboarding.
✔ **An toàn thông tin được bảo vệ** bằng cách khóa tài khoản ngay sau ngày cuối cùng làm việc.
✔ **Tuân thủ chính sách bảo mật** một cách tự động.

**👉 Hãy áp dụng ngay workflow này trên VPS của mình để tiết kiệm thời gian và giảm thiểu rủi ro!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Bắt đầu tự động hóa offboarding ngay hôm nay!** 🚀