---
title: "🚀 Tự Động Hóa Sourcing LinkedIn Trên Slack → Google Sheets (Không Trùng Lặp) Với easybits & AI"
description: "Workflow tự động hóa chuyển đổi hồ sơ LinkedIn từ Slack sang Google Sheets với kiểm tra trùng lặp tự động, thông báo kết quả ngay trên Slack. Giúp các sếp HR tiết kiệm 80% thời gian xử lý ứng viên mới."
slug: "tu-dong-hoa-sourcing-linkedin-slack-google-sheets"
tags: [n8n, automation, hr, ai-summarization, google-sheets, slack, easybits]
keywords: [tự động hóa sourcing linkedin, n8n workflow hr, deduplicate candidate, slack automation, google sheets api, easybits extractor]
---

# 🚀 **Tự Động Hóa Sourcing LinkedIn Trên Slack → Google Sheets (Không Trùng Lặp) Với easybits & AI**

### **Giải pháp cho các sếp HR:**
Hàng ngày, các nhà tuyển dụng phải:
- **Tìm kiếm** hồ sơ ứng viên trên LinkedIn (thời gian mất từ 30-60 phút/người).
- **Chuyển đổi** thông tin từ ảnh chụp hoặc PDF LinkedIn sang dạng dữ liệu có cấu trúc (Excel/Google Sheets).
- **Kiểm tra trùng lặp** thủ công với cơ sở dữ liệu hiện có (rất dễ bỏ sót).
- **Gửi thông báo** kết quả cho team (Slack/Email) và cập nhật hồ sơ.

**Workflow này tự động hóa toàn bộ quy trình trong 3 bước:**
1. **Nhận hồ sơ** từ Slack (ảnh chụp hoặc PDF LinkedIn).
2. **Trích xuất dữ liệu** từ ảnh/PDF thành 10 trường thông tin chuẩn (tên, công ty hiện tại, kỹ năng, kinh nghiệm...).
3. **Kiểm tra trùng lặp** với cơ sở dữ liệu ứng viên hiện có và **cập nhật tự động** vào Google Sheets.
4. **Thông báo kết quả** ngay trên Slack với nút liên kết đến hồ sơ (mặc dù đã trùng lặp hay chưa).

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công (không cần copy-paste, không cần kiểm tra trùng lặp).
- **Dữ liệu chính xác 100%** nhờ trích xuất tự động từ easybits (không sai sót như khi nhập thủ công).
- **Không trùng lặp** với cơ sở dữ liệu hiện có (kiểm tra trên `tên + công ty hiện tại`).
- **Hoạt động 24/7** (không cần can thiệp của con người).
- **Cá nhân hóa thông báo** trên Slack với nút liên kết trực tiếp đến Google Sheets.
- **Dữ liệu thống nhất** (hồ sơ LinkedIn và CV được lưu cùng một bảng Google Sheets).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - **Slack App** với các scope sau:
     - `files:read` (đọc file được chia sẻ)
     - `channels:history` (lịch sử tin nhắn trong channel)
     - `chat:write` (gửi tin nhắn)
   - **Bot Slack** được thêm vào channel giám sát (channel này sẽ nhận file LinkedIn).
   - **Event Subscription** được cấu hình để nhận sự kiện `file_shared` từ n8n (cần paste URL trigger của n8n vào Slack App).

2. **Tài khoản Google Sheets**:
   - **File Google Sheets** đã tồn tại với cấu trúc cột phù hợp (các cột phải khớp với output của node `Normalize: Candidate Fields`).
   - **Thông tin OAuth2** để kết nối với n8n (tạo từ [Google Cloud Console](https://console.cloud.google.com/)).

3. **Tài khoản easybits**:
   - Cài đặt **node easybits Extractor** (n8n Cloud: đã có sẵn; tự host: `@easybits/n8n-nodes-extractor`).
   - **API Key** của easybits (đăng ký tại [easybits.com](https://easybits.com/)).

4. **Cấu hình n8n**:
   - **Self-hosted n8n** (khuyến nghị để workflow hoạt động 24/7).
   - **VPS 2GB RAM** (để chạy workflow ổn định).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/16100](https://n8n.io/workflows/16100) (chọn **Export JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create a new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/16100](https://n8n.io/workflows/16100) (chọn **Export JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán mã vào.
3. Chọn **Create a new workflow** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **11 node**, nhưng có **3 node quan trọng nhất** cần cấu hình cẩn thận:

#### **A. Node `Slack Trigger: File Shared`**
- **Cấu hình**:
  - **Credentials**: Chọn `slackApi` (tài khoản Slack đã cấu hình trước).
  - **Channel ID**: Nhập ID của channel Slack bạn muốn giám sát (lấy từ URL channel: `https://slack.com/archives/C1234567890` → `C1234567890`).
  - **Event**: Chọn `file_shared` (sự kiện file được chia sẻ vào channel).
  - **Active**: Bật `Active` để workflow bắt đầu hoạt động.

#### **B. Node `easybits Extract: LinkedIn Profile`**
- **Cấu hình**:
  - **Credentials**: Chọn `easybitsExtractorApi` (API Key của easybits).
  - **Input**: Chọn `data` (dữ liệu từ node `Download File: From Slack`).
  - **Lưu ý**:
    - Node này **trích xuất 10 trường dữ liệu** từ ảnh/PDF LinkedIn (tên, công ty, kỹ năng, kinh nghiệm...).
    - Nếu file là **ảnh chụp**, một số thông tin (như kinh nghiệm chi tiết) có thể bị cắt (do giới hạn hiển thị của LinkedIn).
    - Nếu file là **PDF**, thông tin sẽ đầy đủ hơn.

#### **C. Node `Normalize: Candidate Fields` (Code Node)**
- **Mã code cần chỉnh sửa** (nếu cần):
  ```javascript
  // Chuyển đổi dữ liệu thành mảng và xử lý trường "null"
  const data = $input.all();
  const normalizedData = data.map(item => {
    const normalizedItem = {
      name: item.data.name || "",
      current_company: item.data.current_company || "",
      top_skills: Array.isArray(item.data.top_skills) ? item.data.top_skills.join(", ") : item.data.top_skills || "",
      experience: Array.isArray(item.data.experience) ? item.data.experience.join("; ") : item.data.experience || "",
      source: "LinkedIn (sourced)",
      added_at: new Date().toISOString(),
      // Thêm các trường khác theo cấu trúc của Google Sheets
    };
    return normalizedItem;
  });
  return { json: normalizedData };
  ```
- **Lưu ý**:
  - Các **cột trong Google Sheets** phải khớp với keys trong `normalizedData` (ví dụ: `name`, `current_company`, `top_skills`...).
  - Nếu Google Sheets có cột khác, cần thêm vào mã code trên.

#### **D. Node `Read: Candidate Sheet`**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: Nhập ID của file Google Sheets (lấy từ URL: `https://docs.google.com/spreadsheets/d/1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P7Q8R9S0T12/` → `1A2B3C4D5E6F7G8H9I0J1K2L3M4N5O6P7Q8R9S0T12`).
  - **Sheet Name**: Nhập tên sheet (tab) chứa dữ liệu ứng viên.
  - **Always Output Data**: **BẮT BUỘC bật** (để workflow hoạt động ngay cả khi sheet trống).
  - **Range**: Nhập `A1:Z` (hoặc phạm vi phù hợp với dữ liệu).

#### **E. Node `Append Row: Candidate Sheet`**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: Nhập cùng ID như node `Read: Candidate Sheet`.
  - **Sheet Name**: Nhập cùng tên sheet.
  - **AutoMap Input Data**: Bật để tự động khớp keys với cột trong Google Sheets.
  - **Lưu ý**: Nếu `AutoMap Input Data` không hoạt động, cần **cấu hình thủ công** các cột trong **keyParameters**.

#### **F. Node `Post Confirmation: Slack (via API)` và `Post Duplicate Warning: Slack (via API)`**
- **Cấu hình chung**:
  - **Credentials**: Chọn `slackApi`.
  - **Method**: `POST`.
  - **URL**: `https://slack.com/api/chat.postMessage`.
  - **Headers**:
    - `Content-Type: application/json`
    - `Authorization: Bearer <SLACK_BOT_TOKEN>` (lấy từ Slack App).
  - **Body (JSON)**:
    ```json
    {
      "channel": "{{ $node["Slack: Get File Info"].json["shares.public"]["channel_id"][0] }}",
      "thread_ts": "{{ $node["Slack: Get File Info"].json["shares.public"]["channel_id"][0]["ts"] }}",
      "text": "Candidate confirmed: {{ $input.currentNode().json[0].name }}",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Candidate:* {{ $input.currentNode().json[0].name }}\n*Role:* {{ $input.currentNode().json[0].current_company }}"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "View in Sheet"
              },
              "url": "https://docs.google.com/spreadsheets/d/{{ $node["Append Row: Candidate Sheet"].json["spreadsheetId"] }}/edit#gid=0"
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý**:
    - Thay thế `{{ $input.currentNode().json[0].name }}` và `{{ $input.currentNode().json[0].current_company }}` bằng các trường dữ liệu thực tế.
    - Để **tránh lỗi Block Kit**, các node này **POST trực tiếp API Slack** thay vì dùng node Slack (do node Slack có bug hiển thị không đầy đủ).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với một file mẫu:
   - Upload một file LinkedIn (ảnh hoặc PDF) vào channel Slack đã cấu hình.
   - Kiểm tra workflow có chạy không và dữ liệu có được trích xuất/kiểm tra trùng lặp đúng không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow để nó hoạt động liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết hợp với Telegram/Email**
- Thay vì chỉ thông báo trên Slack, có thể **gửi thông báo đồng thời đến Telegram** hoặc **Email** bằng node `httpRequest` (API Telegram/Email).
- **Cách làm**:
  - Thêm node `httpRequest` sau `Post Confirmation` và `Post Duplicate Warning`.
  - Gửi request đến API Telegram (chatbot) hoặc API Email (như SendGrid).

### **2. Lưu log hoạt động**
- Thêm node `stickyNote` để **lưu log** mỗi khi workflow chạy (giúp theo dõi lỗi và hoạt động).
- **Cách làm**:
  - Thêm node `stickyNote` vào workflow.
  - Cấu hình để lưu dữ liệu như:
    ```json
    {
      "key": "linkedin_sourcing_log",
      "value": {
        "timestamp": new Date().toISOString(),
        "candidate_name": "{{ $input.currentNode().json[0].name }}",
        "status": "{{ $input.currentNode().json[0].is_duplicate ? "Duplicate" : "New" }}"
      }
    }
    ```

### **3. Gửi báo cáo định kỳ**
- Sử dụng **n8n Scheduler** để chạy workflow **hàng ngày** để kiểm tra và báo cáo số lượng ứng viên mới/trùng lặp.
- **Cách làm**:
  - Tạo một **workflow mới** với node `n8n-nodes-base.schedule`.
  - Kết nối với workflow này để lấy báo cáo từ Google Sheets.

### **4. Cải thiện trích xuất dữ liệu**
- Nếu **ảnh chụp LinkedIn** bị cắt thông tin, có thể:
  - Yêu cầu recruiter **chụp PDF** thay vì ảnh (PDF có thông tin đầy đủ hơn).
  - Sử dụng **OCR nâng cao** (như node `ocr` của n8n) để trích xuất từ ảnh.

### **5. Tích hợp với CRM (Salesforce/Zoho)**
- Nếu sử dụng **CRM**, có thể **tự động đồng bộ** dữ liệu ứng viên từ Google Sheets sang CRM.
- **Cách làm**:
  - Thêm node `httpRequest` để gọi API CRM (Salesforce/Zoho).
  - Cấu hình để tạo/ cập nhật lead trong CRM khi ứng viên mới được thêm vào Google Sheets.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc thủ công, **giảm thiểu lỗi trùng lặp**, và **tự động hóa toàn bộ quy trình sourcing LinkedIn**. Với **cấu hình đơn giản** và **hoạt động 24/7**, nó là công cụ không thể thiếu cho bất kỳ team HR nào muốn **tăng hiệu suất và chất lượng tuyển dụng**.

### **Bắt đầu ngay!**
1. **Cài đặt n8