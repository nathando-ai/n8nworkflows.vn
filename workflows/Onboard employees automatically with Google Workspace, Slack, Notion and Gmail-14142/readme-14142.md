---
title: "🚀 Tự Động Hóa Quá Trình Nhập Nhân Viên Từ Ngày 0 Đến Ngày 30 Với Google Workspace, Slack, Notion & Gmail (Không Cần Code)"
description: "Giải pháp tự động hóa toàn bộ quy trình onboard mới nhân viên từ tạo tài khoản Google Workspace, gửi thông báo Slack, tạo checklist Notion cho đến báo cáo hoàn thành ngày 30 - tiết kiệm 10+ giờ công cho bộ phận HR mỗi tháng."
slug: "tieu-dong-hoa-qua-trinh-nhap-nhan-vien-google-workspace-slack-notion-gmail"
tags: [n8n, automation, hr, google-workspace, slack, notion, gmail, no-code, workflow-templates]
keywords: [tự động hóa nhật ký nhân sự, onboard nhân viên tự động, n8n workflow hr, tự động hóa google workspace, checklist onboarding, báo cáo hoàn thành ngày 30]
---

# 🚀 **Tự Động Hóa Quá Trình Nhập Nhân Viên Từ Ngày 0 Đến Ngày 30 Với Google Workspace, Slack, Notion & Gmail**

### **Giải pháp hoàn hảo cho bộ phận HR: Tiết kiệm 10+ giờ công mỗi tháng, giảm thiểu lỗi thủ công và cải thiện trải nghiệm onboard cho nhân viên mới**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gặp lỗi, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, không lag)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công/tháng** cho bộ phận HR: Không cần nhập liệu thủ công, tạo tài khoản Google, gửi email, hoặc theo dõi checklist.
- **Trải nghiệm onboard chuyên nghiệp**: Nhân viên mới nhận được tài khoản Google ngay lập tức, checklist rõ ràng trên Notion, và thông báo tự động từ Slack/Gmail.
- **Theo dõi hiệu quả**: Hệ thống tự động cảnh báo nếu nhân viên không hoàn thành ≥3 nhiệm vụ trong tuần đầu tiên.
- **Báo cáo tự động ngày 30**: Slack tự động gửi thông báo hoàn thành cho manager và nhân viên.
- **Giảm thiểu lỗi**: Không cần nhớ mật khẩu, không quên gửi email, hoặc mất checklist.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Workspace Admin SDK** (OAuth2 với scope `admin.directory.user.create`).
   - **Slack Bot Token** (scope `chat:write`).
   - **Notion Integration Token** (có quyền truy cập vào database).
   - **Gmail OAuth2 Credential** (để gửi email tự động).

2. **Thông tin cấu hình cụ thể**:
   - **ID Channel Slack** cho `#general` và `#managers` (thay thế `C00GENERAL000` và `C00MANAGERS000`).
   - **ID Database Notion** (thay thế `YOUR_ONBOARDING_DB_ID`).
   - **Mô hình webhook** để nhận dữ liệu từ HR system (cấu trúc JSON như ví dụ dưới đây).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/14142](https://n8n.io/workflows/14142) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/14142](https://n8n.io/workflows/14142).
2. Trên n8n Editor, nhấn **Import** → **Paste JSON** và dán vào.
3. Nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **12 node** với logic phức tạp. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **🔹 Node 1: New Employee Webhook (n8n-nodes-base.webhook)**
- **Path**: `onboarding` (không thay đổi).
- **HTTP Method**: `POST`.
- **Lưu ý**:
  - Cần tạo **webhook URL** từ n8n và cung cấp cho HR system để gửi dữ liệu mới nhân viên.
  - **Payload mẫu** (JSON POST):
    ```json
    {
      "employee_name": "Jane Smith",
      "employee_email": "jane@company.com",
      "manager_email": "mgr@company.com",
      "department": "Engineering",
      "start_date": "2025-04-01",
      "employee_id": "EMP-0042"
    }
    ```

#### **🔹 Node 2: Build Payload (n8n-nodes-base.code)**
- **Logic**: Kiểm tra và chuẩn hóa dữ liệu đầu vào.
- **Lưu ý**: Không cần chỉnh sửa, chỉ cần đảm bảo payload từ webhook đúng định dạng.

#### **🔹 Node 3: Provision Google Account (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **URL**: `https://admin.googleapis.com/admin/directory/v1/users`
  - **Method**: `POST`.
  - **Headers**:
    - `Authorization`: `Bearer {Google_OAuth2_Token}` (đặt từ credential Google Workspace).
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "primaryEmail": "{{$node["Build Payload"].json["employee_email"]}}",
      "name": {
        "givenName": "{{$node["Build Payload"].json["employee_name"].split(' ')[0]}}",
        "familyName": "{{$node["Build Payload"].json["employee_name"].split(' ')[1]}}"
      },
      "password": "Temp@123!",  // Mật khẩu tạm thời (cần thay đổi sau)
      "orgUnitPath": "/Engineering"  // Thay đổi theo cấu trúc org của công ty
    }
    ```
- **Lưu ý**:
  - Thay thế `Engineering` bằng **org unit** phù hợp.
  - Sau khi tạo tài khoản, **nhân viên mới** sẽ nhận email từ Google với mật khẩu tạm thời.

#### **🔹 Node 4: Post Welcome Slack (n8n-nodes-base.slack)**
- **Cấu hình**:
  - **Slack Credential**: Chọn credential Slack đã cấu hình trước.
  - **Channel**: Thay thế `C00GENERAL000` bằng **ID channel #general** của công ty.
  - **Message Template**:
    ```markdown
    🎉 **Welcome to the team, {{ $node["Build Payload"].json["employee_name"] }}!** 🎉
    Your Google Workspace account has been created! 👉 [Sign in here](https://mail.google.com)
    Temporary password: **Temp@123!** (Please change it after login)
    ```
- **Lưu ý**:
  - Thay thế `Temp@123!` bằng mật khẩu tạm thời phù hợp.

#### **🔹 Node 5: Create Notion Onboarding Page (n8n-nodes-base.notion)**
- **Cấu hình**:
  - **Notion Credential**: Chọn credential Notion đã cấu hình.
  - **Database ID**: Thay thế `YOUR_ONBOARDING_DB_ID` bằng **ID database Notion** của bạn.
  - **Page Content**:
    ```json
    {
      "properties": {
        "Title": {
          "title": [
            {
              "text": {
                "content": "{{ $node["Build Payload"].json["employee_name"] }} Onboarding"
              }
            }
          ]
        },
        "Employee Email": {
          "email": "{{ $node["Build Payload"].json["employee_email"] }}"
        },
        "Status": {
          "select": {
            "name": "In Progress"
          }
        },
        "Tasks": {
          "relation": [
            {
              "id": "6d8b1a2c-3d4e-5f6g-7h8i-9j0k1l2m3n4o"
            },
            {
              "id": "6d8b1a2c-3d4e-5f6g-7h8i-9j0k1l2m3n5p"
            },
            {
              "id": "6d8b1a2c-3d4e-5f6g-7h8i-9j0k1l2m3n6q"
            },
            {
              "id": "6d8b1a2c-3d4e-5f6g-7h8i-9j0k1l2m3r"
            },
            {
              "id": "6d8b1a2c-3d4e-5f6g-7h8i-9j0k1l2m3s"
            }
          ]
        }
      }
    }
    ```
  - **Lưu ý**:
    - Thay thế `6d8b1a2c-3d4e-5f6g-7h8i-9j0k1l2m3n4o` bằng **ID của 5 task** trong database Notion của bạn.
    - Cần tạo **5 task checklist** trước trong Notion với status mặc định là `Pending`.

#### **🔹 Node 6: Send Welcome Email (n8n-nodes-base.gmail)**
- **Cấu hình**:
  - **Gmail Credential**: Chọn credential Gmail đã cấu hình.
  - **To**: `{{ $node["Build Payload"].json["employee_email"] }}`.
  - **Subject**: `Welcome to [Company Name]! Your Onboarding Checklist`.
  - **Body Template**:
    ```html
    <p>Chào {{ $node["Build Payload"].json["employee_name"] }},</p>
    <p>Chúng tôi rất vui mừng bạn đã gia nhập đội ngũ!</p>
    <p>Tài khoản Google Workspace của bạn đã được tạo thành công:</p>
    <ul>
      <li><strong>Email:</strong> {{ $node["Build Payload"].json["employee_email"] }}</li>
      <li><strong>Mật khẩu tạm thời:</strong> Temp@123!</li>
      <li><strong>Đổi mật khẩu:</strong> <a href="https://myaccount.google.com">Đăng nhập và đổi mật khẩu</a></li>
    </ul>
    <p>Bạn có thể theo dõi checklist onboard của mình tại: <a href="https://www.notion.so/your-onboarding-db">Notion Onboarding</a></p>
    <p>Chúc bạn có một ngày đầu tiên tuyệt vời!</p>
    <p>Trân trọng,<br>Đội ngũ HR</p>
    ```
- **Lưu ý**:
  - Thay thế `Temp@123!` và `your-onboarding-db` bằng thông tin thực tế.

#### **🔹 Node 7 & 8: Wait 7 Days & Check Completed Tasks**
- **Node Wait 7 Days**: Không cần chỉnh sửa, chỉ cần đảm bảo workflow hoạt động.
- **Node Check Completed Tasks**:
  - **Query Notion** để lấy danh sách task với `Status = Done`.
  - **Lưu ý**: Cần đảm bảo **database Notion** có cột `Status` với giá trị `Done`.

#### **🔹 Node 9: 3+ Tasks Complete? (n8n-nodes-base.if)**
- **Logic**:
  - Nếu ≥3 task hoàn thành → **tiếp tục đến Node 10 (Wait Until Day 30)**.
  - Nếu <3 task hoàn thành → **tiếp tục đến Node 11 (Alert Manager)**.

#### **🔹 Node 10: Wait Until Day 30**
- **Thời gian chờ**: 23 ngày (tổng cộng 30 ngày từ ngày onboard).

#### **🔹 Node 11 & 12: Day 30 Completion Message / Alert Manager**
- **Node 11 (Day 30 Completion Message)**:
  - Gửi thông báo Slack cho `#general` và `#managers` khi nhân viên hoàn thành ≥3 task.
  - **Template**:
    ```markdown
    🎉 **Congratulations, {{ $node["Build Payload"].json["employee_name"] }}!** 🎉
    You have completed all onboarding tasks! 🚀
    ```
- **Node 12 (Alert Manager — Incomplete Tasks)**:
  - Gửi cảnh báo Slack cho `#managers` khi nhân viên chưa hoàn thành ≥3 task.
  - **Template**:
    ```markdown
    ⚠️ **Alert: Incomplete Onboarding Tasks** ⚠️
    Employee: {{ $node["Build Payload"].json["employee_name"] }}
    Email: {{ $node["Build Payload"].json["employee_email"] }}
    Manager: {{ $node["Build Payload"].json["manager_email"] }}
    Only {{ $node["Check Completed Tasks"].json.length }} tasks completed.
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi **payload mẫu** từ webhook để kiểm tra workflow.
   - Kiểm tra:
     - Tài khoản Google có được tạo không?
     - Slack có nhận được thông báo không?
     - Notion có tạo checklist không?
     - Email có được gửi không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động đổi mật khẩu Google**:
   - Thêm **node HTTP Request** sau khi tạo tài khoản Google để gọi API đổi mật khẩu tự động (sử dụng `admin.directory.users.updatePassword`).

2. **Gửi báo cáo định kỳ**:
   - Thêm **node Slack/Email** để gửi báo cáo tổng hợp về tiến độ onboard của tất cả nhân viên mới mỗi tháng.

3. **Kết hợp với Microsoft Teams**:
   - Thay thế node Slack bằng **Microsoft Teams** để gửi thông báo vào nhóm Teams của công ty.

4. **Lưu log hoạt động**:
   - Thêm **node StickyNote** (n8n-nodes-base.stickyNote) để ghi lại lịch sử hoạt động của workflow.

5. **