---
title: "🛡️ **Tự Động Kiểm Tra Danh Tích File Bằng VirusTotal + Cảnh Báo Slack (Miễn Phí 100%)**"
description: "Workflow tự động hóa kiểm tra danh tính file (MD5/SHA1/SHA256) trên VirusTotal và gửi cảnh báo Slack khi phát hiện file độc hại. Giúp các sếp bảo mật hệ thống, tiết kiệm thời gian kiểm tra thủ công và giảm thiểu rủi ro an ninh."
slug: "tieu-dong-kiem-tra-danh-tich-file-virus-total-slack"
tags: [n8n, automation, cybersecurity, virus-total, slack, no-code]
keywords: [tự động hóa kiểm tra file, virus total api, cảnh báo an ninh mạng, hash file, md5 sha256, n8n workflow security]
---

# 🚀 **Tự Động Kiểm Tra Danh Tích File Bằng VirusTotal + Cảnh Báo Slack (Miễn Phí 100%)**

## **🔍 Nỗi Đau Của Các Sếp**
Trong môi trường làm việc hiện nay, việc tải xuống và chia sẻ file từ nguồn không rõ nguồn gốc là một trong những nguy cơ lớn nhất gây ra **tấn công malware, ransomware** hoặc **gián điệp thông tin**. Các sếp thường phải:
- **Kiểm tra thủ công** từng file bằng VirusTotal (tốn thời gian và dễ bỏ qua).
- **Phản ứng chậm** khi phát hiện file độc hại, dẫn đến rủi ro bảo mật.
- **Không có cảnh báo tự động**, khiến các file nguy hiểm tràn lan trong hệ thống.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động kiểm tra danh tính file** (MD5/SHA1/SHA256) trên VirusTotal.
✅ **Gửi cảnh báo Slack ngay lập tức** khi phát hiện file **độc hại, nghi ngờ** hoặc **không rõ nguồn gốc**.
✅ **Trả về kết quả chi tiết** dưới dạng JSON để các sếp có thể **xác minh và xử lý** một cách nhanh chóng.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Không cần kiểm tra từng file thủ công trên VirusTotal.
- **Bảo mật cao**: Phát hiện và cảnh báo **ngay lập tức** khi file độc hại xuất hiện.
- **Tự động hóa hoàn toàn**: Hoạt động liên tục, không phụ thuộc vào nhân viên.
- **Dữ liệu chi tiết**: Nhận **báo cáo đầy đủ** về danh tính file, bao gồm:
  - **Malicious** (Độc hại)
  - **Suspicious** (Nghi ngờ)
  - **Clean** (An toàn)
  - **Unknown** (Không rõ nguồn gốc)
- **Giao tiếp nhanh chóng**: Cảnh báo Slack giúp **các team IT phản ứng kịp thời**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản VirusTotal** (miễn phí hoặc premium):
   - [Đăng ký VirusTotal](https://www.virustotal.com/) (API Key miễn phí có giới hạn).
   - **Mã API Key** sẽ được sử dụng trong n8n để kết nối với API.

2. **Tài khoản Slack** (để nhận cảnh báo):
   - **Slack API Token** (tạo từ [API Settings](https://api.slack.com/apps)).
   - **Channel Slack** để gửi thông báo (ví dụ: `#security-alerts`).

3. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo **bảo mật và ổn định 24/7**).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định và an toàn**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ nhanh, không lag).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow được cung cấp dưới dạng **JSON**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13229](https://n8n.io/workflows/13229) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào **n8n Editor** (tab `Import`).

:::note[**Lưu ý quan trọng**]
- **Không sử dụng phiên bản n8n cloud** (do yêu cầu API Key và bảo mật).
- **Kiểm tra lại URL webhook** (`/hash-check`) sau khi import.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

Workflow gồm **12 node**, các sếp cần **cấu hình chính xác** các phần sau:

#### **🔹 Node 1: "Receive File Hash" (Webhook)**
- **Đường dẫn (Path):** `/hash-check`
- **Phương thức (HTTP Method):** `POST`
- **Lưu ý:**
  - Các sếp cần **bật Webhook** và **không thay đổi đường dẫn** (nếu muốn sử dụng Slack Slash Command).
  - **Test Webhook** bằng cách gửi request từ Postman:
    ```json
    {
      "text": "SHA256:abc123..."
    }
    ```

#### **🔹 Node 2 & 3: "Normalize Hash from Webhook" (Set) + "IF - Valid Hash Format" (If)**
- **Chức năng:** Kiểm tra và **chuyển đổi định dạng hash** (MD5, SHA1, SHA256) thành **một định dạng chuẩn**.
- **Lưu ý:**
  - Nếu hash **không hợp lệ**, workflow sẽ **trả về "Unknown Hash"** và **không tiếp tục kiểm tra**.
  - **Không cần chỉnh sửa** node này (n8n tự động xử lý).

#### **🔹 Node 4: "HTTP - VirusTotal Hash Lookup" (HTTP Request)**
- **Tham số cần thiết:**
  - **API Key:** Điền **VirusTotal API Key** từ tài khoản của các sếp.
  - **URL:** `https://www.virustotal.com/api/v3/files/{hash}/detects`
  - **Headers:**
    ```json
    {
      "x-apikey": "{{ $node["HTTP - VirusTotal Hash Lookup"].credentials["virusTotalApi"].apiKey }}"
    }
    ```
- **Lưu ý:**
  - Nếu **API Key không đúng**, workflow sẽ **báo lỗi** và không kiểm tra được.
  - **Giới hạn miễn phí:** VirusTotal miễn phí cho **4 request/phút**, **500 request/ngày**.

#### **🔹 Node 5: "IF - Hash Exists in VT" (If)**
- **Chức năng:** Kiểm tra **hash có tồn tại trong VirusTotal** hay không.
- **Lưu ý:**
  - Nếu **hash không tồn tại**, workflow sẽ **trả về "Unknown Hash"** (không cần kiểm tra thêm).

#### **🔹 Node 6: "Function - Calculate Verdict" (Code)**
- **Chức năng:** **Tính toán kết quả** dựa trên:
  - **Số lượng engine phát hiện độc hại** (`positives`).
  - **Tỷ lệ phát hiện** (`positives/total`).
- **Lưu ý:**
  - **Không chỉnh sửa mã** trừ khi các sếp muốn **cập nhật ngưỡng cảnh báo**.
  - **Cấu trúc logic:**
    - **Malicious:** > 50% engine phát hiện.
    - **Suspicious:** 20-50% engine phát hiện.
    - **Clean:** < 20% engine phát hiện.
    - **Unknown:** Hash không tồn tại trên VirusTotal.

#### **🔹 Node 7 & 8: "Slack - Malicious Hash Alert" (Slack) + "Send a message" (Slack)**
- **Tham số cần thiết:**
  - **Credentials:** Chọn **`slackApi`** (đã cấu hình trước).
  - **Message Template:**
    ```json
    {
      "text": "🚨 **ALERT: Malicious Hash Detected** 🚨",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Hash:* `{{ $node["Normalize Hash from Webhook"].json["hash"] }}`\n*Verdict:* `Malicious`\n*Detected by:* {{ $node["HTTP - VirusTotal Hash Lookup"].json["data"]["attributes"]["last_analysis_stats"]["malicious"] }} engines"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "View on VirusTotal"
              },
              "url": "https://www.virustotal.com/gui/file/{{ $node["Normalize Hash from Webhook"].json["hash"] }}/analysis"
            }
          ]
        }
      ]
    }
    ```
- **Lưu ý:**
  - **Chọn channel Slack** để gửi cảnh báo (ví dụ: `#security-alerts`).
  - **Test Slack Bot** trước khi kích hoạt workflow.

#### **🔹 Node 9-12: Các Response (RespondToWebhook)**
- **Trả về kết quả JSON** cho người dùng:
  ```json
  {
    "verdict": "Malicious/Suspicious/Clean/Unknown",
    "hash": "SHA256:abc123...",
    "detections": {
      "malicious": 12,
      "suspicious": 3,
      "clean": 85
    }
  }
  ```
- **Lưu ý:**
  - **Không cần chỉnh sửa** trừ khi muốn **thay đổi định dạng trả về**.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một **hash mẫu** (ví dụ: `SHA256:abc123...`).
2. **Bật Active** workflow.
3. **Gửi request** từ:
   - **Postman** (gửi JSON `{ "text": "SHA256:abc123..." }`).
   - **Slack Slash Command** (nếu cấu hình):
     ```
     /hash-check SHA256:abc123...
     ```

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với SIEM (Security Information & Event Management)**
- **Gửi log** từ n8n đến **SIEM như Splunk, ELK, hoặc Graylog** để **theo dõi và phân tích** các cảnh báo lâu dài.
- **Cách làm:**
  - Sử dụng **node `n8n-nodes-base.httpRequest`** để gửi dữ liệu đến API của SIEM.
  - Ví dụ: Gửi JSON cảnh báo đến **Splunk HTTP Event Collector**.

### **2. Tự Động Xóa File Độc Hại**
- **Kết hợp với node `n8n-nodes-base.fileSystem`** để **xóa file** khi phát hiện **Malicious**.
- **Cách làm:**
  - Thêm node **`File System`** sau khi nhận **verdict "Malicious"**.
  - Cấu hình **đường dẫn file** và **thao tác xóa**.

### **3. Cảnh Báo Email (Ngoài Slack)**
- **Sử dụng node `n8n-nodes-base.email`** để gửi **email cảnh báo** cho team IT.
- **Cách làm:**
  - Cấu hình **SMTP** (Gmail, Outlook, hoặc server email doanh nghiệp).
  - Tạo **template email** tự động với kết quả kiểm tra.

### **4. Lưu Log Kiểm Tra**
- **Sử dụng node `n8n-nodes-base.database`** (SQLite, PostgreSQL) hoặc **Google Sheets** để **lưu lịch sử kiểm tra**.
- **Cách làm:**
  - Thêm node **`Set`** sau khi nhận kết quả.
  - Gửi dữ liệu vào **Google Sheets** hoặc **database** để **theo dõi lâu dài**.

### **5. Hỗ Trợ File Upload (Nâng Cao)**
- **Thay vì chỉ nhận hash**, workflow có thể **kiểm tra file trực tiếp** bằng:
  - **Node `n8n-nodes-base.httpRequest`** để upload file.
  - **Tính hash** trong n8n trước khi gửi đến VirusTotal.
- **Cách làm:**
  - Thêm node **`File Upload`** (n8n có sẵn node `n8n-nodes-base.fileSystem`).
  - Sử dụng **`crypto` module** trong **Code Node** để tính hash.

---

## 📌 **Kết Luận**

Workflow **"Kiểm Tra Danh Tích File Bằng VirusTotal + Cảnh Báo Slack"** là **giải pháp tự động hóa an ninh mạng hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** kiểm tra file thủ công.
✔ **Phát hiện sớm** các file độc hại.
✔ **Cảnh báo ngay lập tức** qua Slack.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để đảm bảo bảo mật).
2. **Import workflow** và **cấu hình API Key**.
3. **Test với một hash mẫu** và **bật hoạt động**.
4. **Kết nối Slack** để nhận cảnh báo tự động.

**🚀 Bắt đầu tự động hóa bảo mật ngay bây giờ!** Nếu có bất kỳ câu hỏi, các sếp có thể **comment bên dưới** hoặc liên hệ với **Low-Code Automation Expert** Edson Encinas qua [n8n.io](https://n8n.io/).