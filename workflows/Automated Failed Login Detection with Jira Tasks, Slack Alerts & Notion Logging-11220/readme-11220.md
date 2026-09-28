---
title: "🚨 **Tự Động Hóa Phát Hiện Lỗi Đăng Nhập & Cảnh Báo An Toàn Mạng (Jira + Slack + Notion)**"
description: "Workflow tự động hóa phát hiện và cảnh báo các cuộc tấn công brute-force hoặc lỗi đăng nhập nghi ngờ bằng cách tích hợp Jira, Slack và Notion. Giúp các sếp bảo mật nhanh chóng phản ứng, giảm thiểu rủi ro và tự động hóa lưu trữ log an toàn."
slug: "tieu-dong-hoa-phat-hien-loi-dang-nhap-jira-slack-notion"
tags: [n8n, automation, security, jira, slack, notion, secops, no-code, api-integration]
keywords: [n8n workflow an ninh mạng, tự động hóa phát hiện lỗi đăng nhập, jira alert, slack cảnh báo an toàn, lưu trữ log failed login, tự động hóa secops]
---

# 🚨 **Tự Động Hóa Phát Hiện Lỗi Đăng Nhập & Cảnh Báo An Toàn Mạng (Jira + Slack + Notion)**

## 🔍 **Nỗi Đau Của Các Sếp**
Hàng ngày, hệ thống của các sếp phải chịu đựng hàng loạt **cuộc tấn công brute-force**, **lỗi đăng nhập nghi ngờ** hoặc **thao tác không hợp lệ** từ bên ngoài. Nếu không được phát hiện và xử lý kịp thời, những cuộc tấn công này có thể dẫn đến:
- **Vi phạm dữ liệu nhạy cảm** (thông tin tài khoản, mật khẩu, thông tin cá nhân).
- **Tốn thời gian phản ứng thủ công** (check log, tạo ticket, cảnh báo team).
- **Rủi ro mất mát tài chính** (do hacker chiếm quyền kiểm soát tài khoản).
- **Không có hệ thống lưu trữ log trung tâm** để phân tích sau này.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Phát hiện tức thời** các cuộc tấn công bằng cách phân tích **username + IP + thời gian**.
✅ **Tự động tạo ticket Jira** với chi tiết chi tiết (đơn lẻ hoặc nhóm nhiều lần).
✅ **Gửi cảnh báo Slack** ngay lập tức để team phản ứng nhanh chóng.
✅ **Lưu trữ log failed login** vào **Notion** để phân tích sau này.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian phản ứng**: Cảnh báo tức thời thay vì phải check log thủ công.
- **Giảm thiểu rủi ro**: Phát hiện và chặn tấn công trước khi nó gây hại.
- **Tự động hóa lưu trữ log**: Không cần ghi chép tay vào Excel hoặc Google Sheets.
- **Dễ dàng phân tích sau này**: Dữ liệu được lưu trữ trong **Notion** với định dạng chuyên nghiệp.
- **Tích hợp hoàn hảo**: Hoạt động với **Jira, Slack và Notion** mà không cần viết code.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản và API Key:**
- **Jira Cloud** (để tạo ticket cảnh báo).
- **Slack Workspace** (để gửi cảnh báo đến channel cụ thể).
- **Notion API** (để lưu trữ log failed login).
- **Webhook URL** từ ứng dụng của các sếp (để gửi dữ liệu failed login).

📌 **Thông tin cấu hình:**
- **Dữ liệu đầu vào từ ứng dụng** (username, IP, timestamp, lỗi).
- **Project & Issue Type** trong Jira (ví dụ: "Security Alert").
- **Channel Slack** để nhận cảnh báo.
- **Database Notion** để lưu trữ log (cần tạo trước).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/11220](https://n8n.io/workflows/11220) và upload lên **n8n Editor**.
- **Copy/Paste JSON** vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không sử dụng phiên bản n8n Community** (nên dùng **n8n Enterprise** hoặc **Self-hosted** để ổn định).
- **Không bỏ qua bước test** trước khi kích hoạt workflow.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **15 node**, nhưng các sếp cần chú ý đặc biệt đến các node sau:

##### **🔹 Node "Faield Login Trigger" (Webhook)**
- **Cấu hình:**
  - **Path:** `failed-login`
  - **HTTP Method:** `POST`
  - **URL:** Sẽ được cung cấp sau khi import.
- **Lưu ý:**
  - **Cần kết nối với ứng dụng** của các sếp để gửi dữ liệu failed login.
  - **Test bằng Postman** trước khi kích hoạt:
    ```json
    {
      "username": "testuser",
      "ip": "192.168.1.1",
      "timestamp": "2024-05-20T10:00:00Z",
      "error": "Invalid credentials"
    }
    ```

##### **🔹 Node "Normalize Login Event" (Function)**
- **Chức năng:** Sửa đổi và chuẩn hóa dữ liệu đầu vào.
- **Lưu ý:**
  - **Kiểm tra lại logic** nếu dữ liệu từ ứng dụng khác với định dạng mong đợi.
  - **Cần điền các trường:** `username`, `ip`, `timestamp`, `error`.

##### **🔹 Node "Check Username & IP present" (If)**
- **Điều kiện:**
  - Nếu **username hoặc IP thiếu**, workflow sẽ **tự động gửi cảnh báo Slack** ngay lập tức.
  - Nếu **cả hai đều có**, workflow sẽ kiểm tra xem có **nhiều lần đăng nhập thất bại** không.

##### **🔹 Node "Detect Multiple Attempts" (Function)**
- **Chức năng:** Đếm số lần đăng nhập thất bại của cùng một **username + IP**.
- **Lưu ý:**
  - **Cần cấu hình ngưỡng** (ví dụ: >3 lần là cảnh báo nghiêm trọng).
  - **Dữ liệu đầu ra** sẽ được sử dụng để tạo **Jira ticket chi tiết**.

##### **🔹 Node "Create Ticket - Multiple Attempts" & "Create Ticket - Single Attempt" (Jira)**
- **Cấu hình cần thiết:**
  - **Credentials:** `jiraSoftwareCloudApi` (đã cấu hình trước).
  - **Project:** Chọn project an toàn (ví dụ: "Security Alerts").
  - **Issue Type:** Chọn loại ticket phù hợp (ví dụ: "Security Incident").
  - **Custom Fields (nếu cần):** Thêm trường như `IP Address`, `Number of Attempts`.
- **Lưu ý:**
  - **Test tạo ticket** trước khi kích hoạt workflow.
  - **Cập nhật mô tả ticket** để rõ ràng:
    ```
    **TITLE:** Brute Force Attempt - [Username]
    **DESCRIPTION:**
    - **IP:** [IP Address]
    - **Attempts:** [Number]
    - **Last Attempt:** [Timestamp]
    - **Error:** [Error Message]
    ```

##### **🔹 Node "Slack Alert - Multiple Attempts" & "Slack Alert - Single Attempt" (Slack)**
- **Cấu hình cần thiết:**
  - **Credentials:** `slackApi` (đã cấu hình trước).
  - **Channel:** Chọn channel cảnh báo (ví dụ: `#security-alerts`).
  - **Message Format:** Cần định dạng rõ ràng:
    ```markdown
    *🚨 SECURITY ALERT 🚨*
    **Username:** [Username]
    **IP Address:** [IP]
    **Attempts:** [Number]
    **Last Attempt:** [Timestamp]
    **Action:** [Create Jira Ticket]
    ```
- **Lưu ý:**
  - **Test gửi cảnh báo** trước khi kích hoạt.
  - **Sử dụng emoji và định dạng Markdown** để dễ đọc.

##### **🔹 Node "Login Attempts Data Store in DB" (Notion)**
- **Cấu hình cần thiết:**
  - **Credentials:** `notionApi` (đã cấu hình trước).
  - **Database:** Chọn database Notion đã tạo trước (ví dụ: "Failed Login Logs").
  - **Fields to Map:**
    - `Username` → `Username` (trường trong Notion).
    - `IP` → `IP Address`.
    - `Timestamp` → `Attempt Time`.
    - `Error` → `Error Description`.
- **Lưu ý:**
  - **Tạo database Notion** trước với các trường:
    - `Username` (Text)
    - `IP Address` (Text)
    - `Attempt Time` (Date)
    - `Error Description` (Rich Text)
    - `Status` (Select: "Pending", "Investigated", "Resolved")

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** **Test Run** với dữ liệu mẫu:
  - **Single Attempt:**
    ```json
    {
      "username": "testuser",
      "ip": "192.168.1.1",
      "timestamp": "2024-05-20T10:00:00Z",
      "error": "Invalid credentials"
    }
    ```
  - **Multiple Attempts (3 lần):**
    ```json
    [
      {"username": "testuser", "ip": "192.168.1.1", "timestamp": "2024-05-20T10:00:00Z", "error": "Invalid credentials"},
      {"username": "testuser", "ip": "192.168.1.1", "timestamp": "2024-05-20T10:05:00Z", "error": "Invalid credentials"},
      {"username": "testuser", "ip": "192.168.1.1", "timestamp": "2024-05-20T10:10:00Z", "error": "Invalid credentials"}
    ]
    ```
  - **Missing Fields (username hoặc IP thiếu):**
    ```json
    {
      "ip": "192.168.1.1",
      "timestamp": "2024-05-20T10:00:00Z",
      "error": "Invalid credentials"
    }
    ```
- **Bước 2:** **Kích hoạt workflow** khi tất cả test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cải Tiến Cho Workflow**]
1. **Thêm Log Rotation (Xóa log cũ):**
   - Sử dụng **Notion API** để xóa log cũ hơn **30 ngày** bằng node **Notion Query Database**.
   - **Cách làm:**
     ```javascript
     // Node "Code" (Function)
     const notion = $input.all();
     const now = new Date();
     const thirtyDaysAgo = new Date(now.getTime() - 30 * 24 * 60 * 60 * 1000);

     // Query Notion Database
     const response = await $node["Notion Query Database"].execute({
       database_id: "YOUR_DATABASE_ID",
       filter: {
         property: "Attempt Time",
         date: {
           before: thirtyDaysAgo.toISOString()
         }
       }
     });

     // Delete old records
     for (const page of response.results) {
       await $node["Notion Delete Page"].execute({
         page_id: page.id
       });
     }
     ```

2. **Kết Nối với SIEM (Security Information & Event Management):**
   - Gửi dữ liệu failed login đến **Splunk, ELK Stack hoặc Datadog** để phân tích sâu hơn.
   - **Cách làm:**
     - Thêm node **HTTP Request** để gửi dữ liệu JSON đến SIEM.
     - **Dữ liệu gửi:**
     ```json
     {
       "event": "failed_login",
       "username": $input.all().username,
       "ip": $input.all().ip,
       "timestamp": $input.all().timestamp,
       "severity": $input.all().severity // "low", "medium", "high"
     }
     ```

3. **Tự Động Khóa Tài Khoản (Nếu Cần):**
   - Sử dụng **Jira API** hoặc **Webhook** để gửi yêu cầu khóa tài khoản đến hệ thống quản lý người dùng (ví dụ: **Okta, Azure AD**).
   - **Cách làm:**
     - Thêm node **HTTP Request** để gọi API khóa tài khoản.
     - **Ví dụ API Okta:**
     ```http
     POST https://{yourOktaDomain}/api/v1/users/{userId}/suspend
     Headers: Authorization: SSWS {apiToken}
     ```

4. **Báo Cáo Định Kỳ (Weekly/Monthly):**
   - Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp failed login hàng tuần.
   - **Cách làm:**
     - Thêm **Schedule Node** chạy vào **thứ 7 hàng tuần**.
     - Sử dụng **Notion Query Database** để lấy dữ liệu.
     - Gửi báo cáo qua **Slack** hoặc **Email** (n8n có node **Email**).
     - **Dữ liệu báo cáo:**
     ```
     **Failed Login Report - Week of [Date]**
     - Total Attempts: [Number]
     - Successful Blocked: [Number]
     - Top IPs: [List]
     - Top Users: [List]
     ```

---

### 📌 **Kết Luận**
Workflow này không chỉ **giải quyết vấn đề phát hiện lỗi đăng nhập** mà còn **tự động hóa toàn bộ quy trình phản ứng an toàn**, từ **cảnh báo tức thời** đến **lưu trữ log chuyên nghiệp** và **báo cáo định kỳ**.

**Các sếp hãy:**
✅ **Import workflow ngay** và kết nối với ứng dụng của mình.
✅ **Test với dữ liệu mẫu** trước khi kích hoạt.
✅ **Tận dụng các mẹo nâng cao** để tối ưu hóa hiệu suất.
✅ **Bảo mật hệ thống** của mình bằng cách phát hiện và phản ứng nhanh chóng với các cuộc tấn công!

---
:::success[**Bắt Đầu Ngay Hôm Nay!**]
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/11220)
👉 [Cài đặt n8n Self-hosted trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/) (để ổn định 24/7)