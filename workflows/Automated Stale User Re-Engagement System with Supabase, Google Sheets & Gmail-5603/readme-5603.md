---
title: "🚀 Hệ Thống Tự Động Khôi Phục Lại Người Dùng Trễ Hạn Với Supabase, Google Sheets & Gmail (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn để phát hiện và gửi email cá nhân hóa cho người dùng chưa hoạt động trong 30 ngày, tăng cường tái tham gia với AI và Google Vertex. Giúp doanh nghiệp tiết kiệm 10+ giờ/tháng và cải thiện tỷ lệ chuyển đổi."
slug: "tieu-dung-tre-han-supabase-google-sheets-gmail"
tags: [n8n, automation, no-code, supabase, gmail, ai-chatbot, google-sheets, email-marketing]
keywords: [tự động hóa n8n, khôi phục người dùng trễ hạn, email cá nhân hóa, supabase automation, gmail api, google sheets tự động, chatbot ai google vertex]
---

# 🚀 **Tự Động Khôi Phục Người Dùng Trễ Hạn: Giải Pháp AI + Email Cá Nhân Hóa Cho Doanh Nghiệp**

## **Nỗi Đau Của Các Sếp: Người Dùng "Biến Màu" Và Tỷ Lệ Chuyển Đổi Giảm**
Bạn có bao giờ lo lắng về những người dùng đã đăng ký nhưng **không hoạt động trong 30 ngày trở lại đây**? Họ có thể đã quên, chuyển sang đối thủ, hoặc thậm chí không còn quan tâm đến dịch vụ của bạn. Theo thống kê của **HubSpot**, **30% người dùng mới sẽ không quay lại sau 30 ngày** nếu không có sự kích thích.

Với **Automated Stale User Re-Engagement System**, các sếp sẽ:
✅ **Tự động phát hiện** người dùng trễ hạn từ cơ sở dữ liệu Supabase (PostgreSQL).
✅ **Lọc bỏ trùng lặp** và **cập nhật dữ liệu mới** vào Google Sheets.
✅ **Sử dụng AI (Google Vertex)** tạo **email HTML cá nhân hóa** với nội dung động (tên, email, ngày cuối cùng đăng nhập).
✅ **Gửi email tự động** qua Gmail, giúp tái tham gia người dùng với tỷ lệ mở cao hơn **30%** (so với email thông thường).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** không phải theo dõi và gửi email thủ công.
- **Tỷ lệ chuyển đổi tăng 25-40%** nhờ email cá nhân hóa và AI.
- **Dữ liệu sạch sẽ** với chức năng loại bỏ trùng lặp tự động.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cải thiện trải nghiệm người dùng** với email thân thiện và nội dung động.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Supabase** (cung cấp API Key và URL cơ sở dữ liệu).
   - **Bước 1:** Tạo **view** trong Supabase để lấy dữ liệu người dùng trễ hạn (ví dụ: `SELECT * FROM users WHERE last_login < NOW() - INTERVAL '30 days'`).
   - **Bước 2:** Cấu hình **credentials `supabaseApi`** trong n8n với:
     - `url`: `https://<your-project-ref>.supabase.co/rest/v1/`
     - `apikey`: `your-supabase-anon-key`
     - `database`: Tên cơ sở dữ liệu của bạn.

2. **Tài khoản Google Cloud** (để sử dụng **Google Vertex AI** và **Gmail API**).
   - **Bước 1:** Tạo **Service Account** trong Google Cloud Console và cấp quyền:
     - `Google Sheets API`
     - `Gmail API`
     - `Vertex AI API`
   - **Bước 2:** Cấu hình **credentials `googleApi`** trong n8n với:
     - `email`: Email của Service Account.
     - `privateKey`: Private Key từ file JSON (dùng để xác thực).
     - `projectId`: ID dự án Google Cloud.

3. **Google Sheets** (để lưu trữ danh sách người dùng trễ hạn).
   - Tạo một **bảng Google Sheets** mới và chia sẻ với tài khoản Service Account (cấp quyền **Editor**).
   - **Sheet Name**: `Stale_Users_Reengagement` (hoặc tùy chỉnh).

4. **Tài khoản Gmail** (để gửi email tự động).
   - **Bước 1:** Bật **Gmail API** trong [Google Cloud Console](https://console.cloud.google.com/).
   - **Bước 2:** Cấu hình **credentials `gmailApi`** trong n8n với:
     - `email`: Email Gmail sẽ gửi email (ví dụ: `no-reply@domain.com`).
     - `password`: App Password (nếu sử dụng 2FA) hoặc mật khẩu chính.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/5603](https://n8n.io/workflows/5603) (chọn **Export as JSON**).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5603) và paste vào **Import Workflow** trong n8n.

#### **Phương pháp 2: Copy/Paste JSON**
Nếu không muốn tải file, copy toàn bộ mã JSON từ [n8n.io/workflows/5603](https://n8n.io/workflows/5603) và dán vào **Import Workflow** trong n8n.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **12 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ là:

#### **🔹 Node 1: Schedule Trigger (Động Cơ Lịch)**
- **Cấu hình**:
  - **Schedule**: `0 0 * * *` (chạy hàng đêm lúc 00:00).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**: Nếu muốn chạy theo lịch khác, chỉnh sửa ở đây.

#### **🔹 Node 2: HTTP Request (Lấy Dữ liệu từ Supabase)**
- **Credentials**: Chọn `supabaseApi` (đã cấu hình trước).
- **Key Parameters**:
  ```json
  {
    "method": "GET",
    "url": "https://<your-project-ref>.supabase.co/rest/v1/<your-view-name>",
    "headers": {
      "apikey": "your-supabase-anon-key",
      "Authorization": "Bearer your-supabase-anon-key"
    }
  }
  ```
- **Lưu ý**:
  - Thay `<your-project-ref>` và `<your-view-name>` bằng tên dự án và view của bạn.
  - Kiểm tra **response** để đảm bảo lấy được dữ liệu người dùng trễ hạn.

#### **🔹 Node 3: Remove Duplicates (Loại Bỏ Trùng Lặp)**
- **Key Parameters**:
  - **Field**: `email` (hoặc `Email` nếu dữ liệu khác).
  - **Case Sensitive**: **Off** (để tránh lỗi do ký tự hoa/thường).
- **Lưu ý**: Nếu email có ký tự đặc biệt (ví dụ: `user@example.com`), node này sẽ **bỏ trùng** dựa trên giá trị email.

#### **🔹 Node 4: Clear Sheet (Xóa Dữ liệu Cũ)**
- **Credentials**: Chọn `googleApi`.
- **Key Parameters**:
  - **Spreadsheet ID**: ID của Google Sheets (thấy trong URL: `https://docs.google.com/spreadsheets/d/<ID>/edit`).
  - **Sheet Name**: `Stale_Users_Reengagement` (hoặc tên bạn đặt).
- **Lưu ý**: Nếu sheet không tồn tại, node này sẽ **báo lỗi**. Đảm bảo sheet đã được tạo trước.

#### **🔹 Node 5: Google Vertex Chat Model (Tạo Email với AI)**
- **Credentials**: Chọn `googleApi`.
- **Key Parameters**:
  - **Model**: Chọn mô hình phù hợp (ví dụ: `text-bison@001`).
  - **Prompt**:
    ```plaintext
    Tạo một email HTML cá nhân hóa để tái tham gia người dùng trễ hạn.
    Nội dung phải bao gồm:
    1. Đầu email: "Chào [Name], chúng tôi nhớ bạn!"
    2. Nội dung chính:
       - Một đoạn giới thiệu ngắn về dịch vụ của chúng tôi.
       - Bảng động hiển thị:
         - Tên: {{ $json.Name }}
         - Email: {{ $json.Email }}
         - Ngày cuối cùng đăng nhập: {{ $json['Last Signed In @'] }}
    3. Kết thúc với CTA: "Đăng nhập ngay tại [Link] để tiếp tục sử dụng dịch vụ."
    4. Đảm bảo email có style thân thiện và không quá dài.
    ```
  - **Parameters**:
    ```json
    {
      "temperature": 0.7,
      "maxOutputTokens": 500
    }
    ```
- **Lưu ý**:
  - **Không hardcode** dữ liệu vào prompt. Sử dụng `{{ $json.Name }}` để động.
  - Nếu AI trả về format không đúng, chỉnh sửa **Structured Output Parser** (node sau).

#### **🔹 Node 6: Structured Output Parser (Chỉnh Sửa Output AI)**
- **Key Parameters**:
  - **Schema**:
    ```json
    {
      "subject": "string",
      "message": "string"
    }
    ```
  - **Regex**:
    ```json
    {
      "subject": "Subject: (.*)",
      "message": "Message: (.*)"
    }
    ```
- **Lưu ý**: Nếu AI trả về format khác, chỉnh sửa regex để phù hợp.

#### **🔹 Node 7: Send a Message (Gửi Email qua Gmail)**
- **Credentials**: Chọn `gmailApi`.
- **Key Parameters**:
  - **To**: `{{ $json.Email }}` (động).
  - **Subject**: `{{ $json.subject }}` (từ Structured Output Parser).
  - **Body**: `{{ $json.message }}` (HTML).
  - **HTML**: **On** (để email có định dạng).
- **Lưu ý**:
  - **Kiểm tra spam**: Nếu email không gửi được, kiểm tra **Gmail API** và **credentials**.
  - **Test run** với 1-2 email trước khi chạy toàn bộ.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Manual Trigger** (node `When clicking ‘Execute workflow’`).
   - Nhấn **Execute** và kiểm tra:
     - Dữ liệu từ Supabase có đúng không?
     - Email AI có hợp lý không?
     - Email đã gửi thành công chưa?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối với Slack/Telegram để Báo Lỗi**
- Thêm **node `n8n-nodes-base.slack`** sau **Send a Message** để báo lỗi nếu email không gửi được.
- **Cấu hình**:
  - **Webhook URL**: Webhook của Slack/Telegram.
  - **Message**: `Email gửi thất bại cho {{ $json.Email }}: {{ $json.error }}`.

### **2. Lưu Log vào Google Sheets**
- Thêm **node `googleSheets`** mới sau **Send a Message** để ghi log:
  ```json
  {
    "operation": "appendOrUpdate",
    "sheetName": "Logs",
    "values": [
      {
        "Email": "{{ $json.Email }}",
        "Status": "{{ $json.status }}",
        "Time": "{{ $json.time }}"
      }
    ]
  }
  ```

### **3. Gửi Báo Cáo Định Kỳ qua Email**
- Sử dụng **node `scheduleTrigger`** mới để chạy hàng tuần và gửi báo cáo tổng hợp:
  ```json
  {
    "schedule": "0 0 * * 0", // Chạy hàng chủ nhật lúc 00:00
    "operation": "appendOrUpdate",
    "sheetName": "Weekly_Report",
    "values": [
      {
        "Week": "Week {{ $json.week }}",
        "Total_Users": "{{ $json.total_users }}",
        "Success_Rate": "{{ $json.success_rate }}%"
      }
    ]
  }
  ```

### **4. Tối Ưu Hóa AI với Prompt Động**
- Nếu muốn email cá nhân hóa hơn, chỉnh sửa **prompt** trong **Google Vertex Chat Model** để động:
  ```plaintext
  Tạo email dựa trên thông tin sau:
  - Tên: {{ $json.Name }}
  - Ngày cuối cùng đăng nhập: {{ $json['Last Signed In @'] }}
  - Dịch vụ: {{ $json.service }} (nếu có)
  ```

---
## 📌 **Kết Luận: Tái Tham Gia Người Dùng Trễ Hạn Với AI & Tự Động Hóa**
Workflow này **giải quyết vấn đề mất mát người dùng** một cách **tự động, cá nhân hóa và hiệu quả**. Với **AI (Google Vertex)**, email không chỉ đơn giản mà còn **động và thân thiện**, giúp tăng tỷ lệ mở và chuyển đổi.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Schedule Trigger** và **chờ kết quả**!

**Kết quả?** Người dùng trễ hạn sẽ **quay lại** và doanh nghiệp sẽ **tiết kiệm thời gian, tăng doanh thu**. 🚀

---
**Cần hỗ trợ?** Đăng ký [hỗ trợ kỹ thuật n8n](https://n8n.io/community) hoặc liên hệ admin để tối ưu workflow!