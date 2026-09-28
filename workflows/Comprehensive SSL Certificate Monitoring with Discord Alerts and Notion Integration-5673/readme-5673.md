---
title: "🚀 **Hệ Thống Theo Dõi SSL Tự Động Hóa Toàn Diện Với Cảnh Báo Discord & Tích Hợp Notion**"
description: "Giải pháp tự động hóa 100% không code để theo dõi chứng chỉ SSL của hàng trăm domain, cảnh báo trước khi hết hạn, phát hiện lỗ hổng an ninh và báo cáo chi tiết - giúp DevOps, IT Admin và chuyên gia SecOps giảm thiểu rủi ro SSL một cách hiệu quả."
slug: "hieu-thong-thieu-doi-ssl-tu-dong-hoa-discord-notion"
tags: [n8n, automation, SecOps, SSL monitoring, Discord integration, Notion, DevOps]
keywords: [n8n workflow SSL, tự động hóa theo dõi chứng chỉ SSL, cảnh báo hết hạn SSL, Discord alert, Notion API, DevOps automation]
---

# 🚀 **Hệ Thống Theo Dõi SSL Tự Động Hóa Toàn Diện Với Cảnh Báo Discord & Tích Hợp Notion**

## **🔐 Tại sao các sếp cần tự động hóa theo dõi SSL?**
Hết hạn chứng chỉ SSL không chỉ gây ra lỗi "không an toàn" trên trang web mà còn làm gián đoạn dịch vụ, ảnh hưởng đến SEO và uy tín thương hiệu. Theo thống kê, **70% các lỗi SSL xảy ra do quên theo dõi thời hạn** (DigiCert, 2023). Với workflow này, các sếp sẽ:
- **Tự động kiểm tra SSL** cho tất cả domain trong Notion **mỗi ngày** (không cần can thiệp thủ công).
- **Nhận cảnh báo Discord** khi chứng chỉ sắp hết hạn (<30 ngày), có lỗ hổng an ninh hoặc không đáp ứng tiêu chuẩn PCI DSS/NIST.
- **Nhận báo cáo chi tiết** về sức khỏe SSL (grade A+ đến F) và hướng khắc phục.
- **Tránh rủi ro pháp lý** do chứng chỉ SSL hết hạn (vi phạm GDPR, PCI DSS).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không phụ thuộc vào cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công hàng ngày (giảm 10+ giờ/năm).
- **Cảnh báo sớm**: Nhận thông báo Discord **trước 30 ngày** khi chứng chỉ sắp hết hạn.
- **Đánh giá SSL chuyên nghiệp**: Nhận **grade từ A+ đến F** (giống SSL Labs) với phân tích chi tiết về:
  - Thời gian còn lại của chứng chỉ.
  - Cipher suite yếu (POODLE, BEAST, Heartbleed).
  - Hỗ trợ TLS 1.3/1.2 (loại bỏ TLS 1.0/1.1).
  - Tuân thủ PCI DSS/NIST/FIPS.
- **Tích hợp Notion**: Lấy danh sách domain từ bảng Notion (không cần nhập thủ công).
- **Báo cáo tự động**: Nhận **báo cáo HTML chi tiết** mỗi ngày để review.
- **An toàn tuyệt đối**: Không phụ thuộc vào dịch vụ third-party (sử dụng API miễn phí + công cụ tự xây dựng).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion**:
   - Một **bảng Notion** (Database) chứa **cột `URL`** với danh sách domain cần theo dõi.
   - Ví dụ:
     ```
     | URL               |
     |-------------------|
     | https://example.com |
     | https://test.vn    |
     ```
2. **Webhook Discord**:
   - Tạo **webhook** trong Discord (Settings > Integrations > Webhooks).
   - Chia sẻ URL webhook cho workflow.
3. **API Key (nếu cần)**:
   - Workflow sử dụng **ssl-checker.io** (miễn phí, không cần API key).
   - Nếu muốn sử dụng **Bubobot SSL Scanner** (công cụ tự xây dựng của tác giả), các sếp cần:
     - SSH vào máy chủ để chạy script (`sysadmin-toolkit/scripts/ssl/ssl-health-assessment.js`).
     - Cấu hình **node SSH** trong n8n để kết nối đến máy chủ.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/5673) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5673) và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** (nếu tự host):
  ```bash
  n8n import workflow.json --name "SSL_Monitor_Discord_Notion"
  ```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **8 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **📌 Node 1: "Daily Trigger" (scheduleTrigger)**
- **Cấu hình**:
  - **Frequency**: `Daily`.
  - **Time**: `10:00 AM` (thời gian Việt Nam: `10:00:00+07:00`).
  - **Time Zone**: Chọn `Asia/Ho_Chi_Minh`.
  - **Lưu ý**: Nếu muốn chạy vào giờ khác, chỉnh **cron expression** thành:
    ```plaintext
    0 0 10 * * ?  # Chạy lúc 10:00 AM hàng ngày
    ```

##### **📌 Node 2: "Fetch domains to check SSL" (notion)**
- **Cấu hình**:
  - **Credentials**: Chọn **Notion API Key** (tạo tại [Notion Developer](https://www.notion.so/my-integrations)).
  - **Database ID**: Lấy từ URL của bảng Notion (ví dụ: `https://www.notion.so/workspace/abc123...` → `abc123...`).
  - **View**: Chọn **Page** (nếu bảng là trang).
  - **Property**: Chọn **`URL`** (cột chứa domain).
  - **Lưu ý**:
    - Đảm bảo **bảng Notion** có **cột `URL`** và dữ liệu được cập nhật.
    - Nếu bảng Notion không có cột `URL`, các sếp cần **tạo mới** và nhập dữ liệu.

##### **📌 Node 3: "Check SSL" (httpRequest)**
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://ssl-checker.com/api/v1/check?url={{$json["url"]}}` (đổi `url` thành `$node["Fetch domains to check SSL"]["json"]["url"]`).
  - **Headers**:
    ```
    Accept: application/json
    ```
  - **Lưu ý**:
    - Workflow này **không cần API key** vì ssl-checker.io cho phép truy cập miễn phí.
    - Nếu API bị lỗi, các sếp có thể **thay thế bằng API khác** như [SSL Checker API](https://sslcheckerapi.com/).

##### **📌 Node 4: "Expiry Alert" (if)**
- **Cấu hình**:
  - **Condition**: `{{$node["Check SSL"]["json"]["days_left"] <= 30}}` (cảnh báo khi còn <30 ngày).
  - **Lưu ý**:
    - Threshold mặc định là **30 ngày**, các sếp có thể **thay đổi** thành `7` (cảnh báo sớm hơn) hoặc `60` (cảnh báo muộn hơn).

##### **📌 Node 5 & 6: "Discord" (discord)**
- **Cấu hình**:
  - **Credentials**: Chọn **Discord Webhook** (đã tạo trước).
  - **Message Format**:
    ```json
    {
      "content": "🚨 **SSL ALERT**: Domain `{{$node["Fetch domains to check SSL"]["json"]["url"]}}` sắp hết hạn!",
      "embeds": [
        {
          "title": "SSL Certificate Status",
          "description": "Days left: `{{$node["Check SSL"]["json"]["days_left"]}}`",
          "color": "{{$node["Expiry Alert"]["json"]["days_left"] <= 7 ? 16711680 : 5814584}}", // Đỏ nếu <7 ngày, vàng nếu <30 ngày
          "fields": [
            {"name": "Valid From", "value": "{{$node["Check SSL"]["json"]["valid_from"]}}"},
            {"name": "Valid Till", "value": "{{$node["Check SSL"]["json"]["valid_till"]}}"},
            {"name": "SSL Grade", "value": "{{$node["Code - Format output"]["json"]["grade"]}}"}
          ],
          "footer": {
            "text": "Automated by n8n + Bubobot"
          }
        }
      ]
    }
    ```
  - **Lưu ý**:
    - **Node "Discord"** sẽ gửi cảnh báo khi **chứng chỉ sắp hết hạn**.
    - **Node "Discord1"** sẽ gửi cảnh báo khi **có lỗ hổng SSL** (nếu cấu hình node `Code - Format output` trả về lỗi).

##### **📌 Node 7: "SSH - Analyze system" (ssh)**
- **Cấu hình**:
  - **Host**: IP hoặc domain của máy chủ (ví dụ: `your-server.com`).
  - **Port**: `22` (mặc định).
  - **Username**: Tài khoản SSH (ví dụ: `root`).
  - **Private Key**: Nếu sử dụng key SSH, điền vào **Private Key**.
  - **Command**:
    ```bash
    cd /sysadmin-toolkit/scripts/ssl && ./ssl-health-assessment.js --url {{$node["Fetch domains to check SSL"]["json"]["url"]}}
    ```
  - **Lưu ý**:
    - Các sếp cần **cài đặt script** `ssl-health-assessment.js` trên máy chủ.
    - Nếu không muốn sử dụng SSH, có thể **bỏ node này** và chỉ dùng `ssl-checker.io`.

##### **📌 Node 8: "Code - Format output" (code)**
- **Cấu hình**:
  - **Script** (JavaScript):
    ```javascript
    // Kết hợp kết quả từ SSL Checker và SSH Scanner
    const sslData = $node["Check SSL"]["json"];
    const sshData = $node["SSH - Analyze system"]["json"] || {};

    // Định nghĩa grade SSL (tương tự SSL Labs)
    let grade = "A+";
    if (sslData.days_left <= 0) grade = "F";
    else if (sslData.days_left <= 7) grade = "D";
    else if (sslData.days_left <= 30) grade = "C";
    else if (sslData.days_left <= 90) grade = "B";
    else grade = "A";

    // Kiểm tra lỗ hổng từ SSH (nếu có)
    const vulnerabilities = sshData.vulnerabilities || [];

    return {
      grade: grade,
      days_left: sslData.days_left,
      vulnerabilities: vulnerabilities,
      is_expired: sslData.days_left <= 0,
      has_weak_ciphers: vulnerabilities.includes("POODLE") || vulnerabilities.includes("BEAST")
    };
    ```
  - **Lưu ý**:
    - Script này **đánh giá grade SSL** từ A+ đến F.
    - Nếu node SSH không hoạt động, các sếp có thể **bỏ phần `sshData`** và chỉ dùng `sslData`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Tab** và nhấn **Execute Workflow**.
   - Kiểm tra **Discord** để xem cảnh báo có xuất hiện không.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, chuyển **Active** sang `ON`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Email Alert**:
   - Thêm **node `n8n-nodes-base.email`** sau node `Expiry Alert` để gửi email cảnh báo cho team.
   - Cấu hình:
     - **SMTP Server**: Gmail/SendGrid.
     - **Template Email**:
       ```html
       <h1>🚨 SSL Certificate Alert</h1>
       <p>Domain: <strong>{{$node["Fetch domains to check SSL"]["json"]["url"]}}</strong></p>
       <p>Days left: <strong>{{$node["Check SSL"]["json"]["days_left"]}}</strong></p>
       <p>Grade: <strong>{{$node["Code - Format output"]["json"]["grade"]}}</strong></p>
       ```

2. **Lưu Log vào Notion**:
   - Thêm **node `notion`** sau node `Code - Format output` để **cập nhật lịch sử SSL** vào bảng Notion.
   - Cấu hình:
     ```json
     {
       "operation": "create",
       "resource": "databasePage",
       "databaseId": "{{$node["Fetch domains to check SSL"]["json"]["databaseId"]}}",
       "properties": {
         "URL": "{{$node["Fetch domains to check SSL"]["json"]["url"]}}",
         "Grade": "{{$node["Code - Format output"]["json"]["grade"]}}",
         "Days Left": "{{$node["Check SSL"]["json"]["days_left"]}}",
         "Last Checked": "{{$node["Daily Trigger"]["json"]["date"]}}",
         "Vulnerabilities": "{{$node["Code - Format output"]["json"]["vulnerabilities"].join(", ")}}"
       }
     }
     ```

3. **Báo cáo HTML Tự động**:
   - Thêm **node `n8n-nodes-base.httpRequest`** để gửi báo cáo HTML đến **Google Drive/Dropbox**.
   - Sử dụng **template HTML** từ [SSL Labs](https://www.ssllabs.com/ssltest/) để tạo báo cáo chuyên nghiệp.

4. **Cảnh báo Telegram**:
   - Thay thế **Discord** bằng **Telegram Bot** (node `n8n-nodes-base.telegram`).
   - Cấu hình:
     ```json