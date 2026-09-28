---
title: "🔍 **Tự Động Hóa Báo Cáo Kiểm Tra Blockchain Ethereum & Solana + Xuất PDF Sang Google Drive & Notion**"
description: "Workflow tự động hóa hoàn chỉnh để theo dõi giao dịch Ethereum/Solana, phân tích rủi ro, tạo báo cáo PDF chuyên nghiệp và đồng bộ hóa lên Google Drive & Notion. Giúp các sếp tiết kiệm thời gian kiểm tra thủ công, giảm thiểu lỗi và tăng cường minh bạch trong quản lý blockchain."
slug: "tieu-dong-hoa-bao-cao-kiem-tra-blockchain-ethereum-solana"
tags: [n8n, blockchain, automation, no-code, ai-summarization, google-drive, notion, pdf-export]
keywords: [n8n workflow blockchain, tự động hóa báo cáo kiểm tra, Ethereum Solana audit, xuất PDF Google Drive, Notion integration, API Alchemy Solana]
---

# 🚀 **Tự Động Hóa Báo Cáo Kiểm Tra Blockchain Ethereum & Solana: Từ Theo Dõi Giao Dịch Đến Báo Cáo PDF**

### **Nỗi Đau Của Các Sếp Trong Quản Lý Blockchain**
Hiện nay, việc kiểm tra giao dịch trên **Ethereum** và **Solana** thường đòi hỏi các sếp phải:
- **Theo dõi thủ công** hàng ngàn giao dịch mỗi ngày trên các blockchain khác nhau.
- **Phân tích rủi ro** và tuân thủ (compliance) một cách mệt mỏi, dễ bị lỗi.
- **Tạo báo cáo** bằng Excel/Word, mất thời gian và khó cập nhật.
- **Đồng bộ hóa dữ liệu** giữa các hệ thống (Google Drive, Notion, email) một cách tẻ nhạt.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Theo dõi giao dịch** Ethereum & Solana từ API chính thức.
✅ **Phân tích rủi ro** (0-100) và kiểm tra tuân thủ (compliance).
✅ **Tạo báo cáo PDF** chuyên nghiệp với AI logic.
✅ **Xuất file PDF** lên **Google Drive** và **Notion**.
✅ **Gửi thông báo** tự động cho đội ngũ tài chính và audit.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/ngày** so với cách làm thủ công.
- **Chính xác 100%** với AI phân tích rủi ro và tuân thủ.
- **Báo cáo PDF tự động** với định dạng chuyên nghiệp.
- **Dữ liệu đồng bộ** giữa Google Drive, Notion và email.
- **Minh bạch cao** với lịch sử giao dịch blockchain-native.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                          | **Liên Kết Đăng Ký**                          |
|---------------------------|--------------------------------------------------|-----------------------------------------------|
| **Alchemy (Ethereum)**    | API Key (trong `httpHeaderAuth`)                 | [https://www.alchemy.com/](https://www.alchemy.com/) |
| **Solana Mainnet**        | Không cần API Key (sử dụng `api.mainnet-beta.solana.com`) | [https://solana.com/](https://solana.com/) |
| **APITemplate.io**       | Template ID (cho PDF Generator)                  | [https://www.apitemplate.io/](https://www.apitemplate.io/) |
| **Google Drive**          | OAuth 2.0 Credentials (`googleDriveOAuth2Api`)   | [https://developers.google.com/drive/api/v3/quickstart/python](https://developers.google.com/drive/api/v3/quickstart/python) |
| **Notion**                | API Key (`notionApi`)                           | [https://www.notion.so/api](https://www.notion.so/api) |
| **Email (SMTP)**          | SMTP Credentials (`smtp`)                        | [https://www.emailonacid.com/blog/test-emails/smtp-test/](https://www.emailonacid.com/blog/test-emails/smtp-test/) |

### **2. Hệ Thống N8n**
:::info[**Gợi Ý Hạ Tầng Cho N8n**]
Để workflow hoạt động **24/7** ổn định, các sếp nên cài **n8n Self-hosted** trên VPS.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/8547](https://n8n.io/workflows/8547) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name** (ví dụ: **"Blockchain Audit Reports"**).
4. Nhấn **Import**.

#### **Phương Pháp 2: Copy/Paste JSON**
1. Trên trang workflow gốc, nhấn **Export JSON**.
2. Copy toàn bộ mã JSON.
3. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
4. Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

#### **🔹 Blockchain Event Webhook**
- **Điểm vào hệ thống**: Các dịch vụ bên ngoài (ví dụ: dApp, smart contract) sẽ gọi API này khi có giao dịch mới.
- **Cấu hình**:
  - **Path**: `blockchain-transaction` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (sử dụng mặc định).

#### **🔹 Ethereum Transaction Monitor**
- **Sử dụng API Alchemy** để lấy logs giao dịch.
- **Cấu hình**:
  - **URL**: `https://eth-mainnet.g.alchemy.com/v2/YOUR_API_KEY`
  - **Headers**:
    - `Authorization`: `Bearer YOUR_API_KEY` (điền từ `httpHeaderAuth`).
    - `Content-Type`: `application/json`.
  - **Request Body**:
    ```json
    {
      "query": "eth_getLogs({fromBlock: 0, toBlock: 'latest', topics: [0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef]}",
      "params": []
    }
    ```

#### **🔹 Solana Transaction Monitor**
- **Sử dụng API chính thức của Solana**.
- **Cấu hình**:
  - **URL**: `https://api.mainnet-beta.solana.com`
  - **Headers**:
    - `Content-Type`: `application/json`.
  - **Request Body**:
    ```json
    {
      "jsonrpc": "2.0",
      "id": 1,
      "method": "getRecentPerEpochs",
      "params": []
    }
    ```

#### **🔹 Transaction Data Processor (Node Code)**
- **Logic AI phân tích rủi ro (0-100) và tuân thủ**.
- **Cấu hình**:
  - Mở **Code Editor** và chỉnh sửa logic theo nhu cầu (ví dụ: điểm rủi ro cao cho giao dịch không tuân thủ EIP-1559).
  - **Dữ liệu đầu vào**: JSON từ `Ethereum Transaction Monitor` và `Solana Transaction Monitor`.
  - **Dữ liệu đầu ra**: Thêm trường `riskScore` và `complianceStatus`.

#### **🔹 Audit Report PDF Generator**
- **Sử dụng APITemplate.io** để tạo PDF từ template.
- **Cấu hình**:
  - **URL**: `https://api.apitemplate.io/v1/templates/YOUR_TEMPLATE_ID/generate`
  - **Headers**:
    - `Authorization`: `Bearer YOUR_API_KEY` (điền từ `httpHeaderAuth`).
  - **Request Body**:
    ```json
    {
      "data": {
        "hash": "{{$json.hash}}",
        "blockchain": "{{$json.blockchain}}",
        "riskScore": "{{$json.riskScore}}",
        "date": "{{$json.date}}",
        "link": "{{$json.link}}",
        "compliance": "{{$json.complianceStatus}}"
      }
    }
    ```

#### **🔹 Upload to Google Drive**
- **Tên file**: `Blockchain_Audit_Report_{hash}_{date}.pdf`.
- **Cấu hình**:
  - **Folder ID**: Chọn folder trong Google Drive (cần tạo trước).
  - **File Name**: `{{$json.hash}}_{{$json.date}}.pdf` (định dạng: `0x123...abc_2024-05-20.pdf`).

#### **🔹 Create Notion Audit Entry**
- **Cấu trúc dữ liệu Notion**:
  - **Hash**: `{{$json.hash}}`
  - **Blockchain**: `{{$json.blockchain}}`
  - **Risk Score**: `{{$json.riskScore}}`
  - **Date**: `{{$json.date}}`
  - **Link**: `{{$json.link}}`
  - **Compliance**: `{{$json.complianceStatus}}`
- **Cấu hình**:
  - **Database Name**: Chọn database Notion đã tạo (ví dụ: **"Blockchain Audit"**).
  - **Properties**:
    - `Hash` (Text)
    - `Blockchain` (Select: Ethereum/Solana)
    - `Risk Score` (Number)
    - `Date` (Date)
    - `Link` (URL)
    - `Compliance` (Status: Tuân thủ/Không tuân thủ)

#### **🔹 Finance Team Notification (Email)**
- **Cấu hình email**:
  - **To**: `compliance@company.com` (đội ngũ tuân thủ).
  - **CC**: `audit-logs@company.com` (lịch sử kiểm tra).
  - **Subject**: `📄 Báo Cáo Kiểm Tra Blockchain - {{$json.blockchain}} (Hash: {{$json.hash}})`.
  - **Body**:
    ```html
    <h2>Báo Cáo Kiểm Tra Blockchain</h2>
    <p><strong>Hash:</strong> {{$json.hash}}</p>
    <p><strong>Blockchain:</strong> {{$json.blockchain}}</p>
    <p><strong>Risk Score:</strong> {{$json.riskScore}}/100</p>
    <p><strong>Tuân Thủ:</strong> {{$json.complianceStatus}}</p>
    <p><strong>Link Giao Dịch:</strong> <a href="{{$json.link}}">{{$json.link}}</a></p>
    <p>Tải PDF đầy đủ: <a href="https://drive.google.com/...">Tải File</a></p>
    ```

#### **🔹 Smart Contract Audit Trail**
- **Verify contract ABI** trên Etherscan (Ethereum) hoặc Solscan (Solana).
- **Cấu hình**:
  - **URL Etherscan**: `https://api.etherscan.io/api?module=contract&action=getabi&address=0x123...abc&apikey=YOUR_KEY`.
  - **URL Solscan**: `https://api.solscan.io/address/{address}/abi`.

#### **🔹 Webhook Response**
- **Trả lời xác nhận** cho dịch vụ gọi webhook.
- **Cấu hình**:
  - **Response Body**:
    ```json
    {
      "status": "success",
      "message": "Báo cáo đã được tạo và gửi thành công!",
      "data": {
        "hash": "{{$json.hash}}",
        "driveUrl": "{{$json.driveUrl}}",
        "notionUrl": "{{$json.notionUrl}}"
      }
    }
    ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **giao dịch mẫu** đến `Blockchain Event Webhook`.
   - Kiểm tra **Transaction Data Processor** có phân tích rủi ro đúng không.
   - Xem **PDF Generator** có tạo file PDF không.
   - Đánh giá **Google Drive** và **Notion** có đồng bộ dữ liệu không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - Kiểm tra **Finance Team Notification** có gửi email không.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối Slack/Telegram**
- Thêm **node `slackSend`** hoặc **`telegramSend`** để thông báo tức thời khi có giao dịch mới.
- **Cấu hình**:
  - **Webhook URL**: Từ Slack/Telegram.
  - **Message**:
    ```json
    {
      "text": "🚨 Giao Dịch Mới: {{$json.blockchain}} (Hash: {{$json.hash}})\nRisk: {{$json.riskScore}}%",
      "attachments": [
        {
          "title": "Chi Tiết",
          "title_link": "{{$json.link}}",
          "text": "Tuân Thủ: {{$json.complianceStatus}}"
        }
      ]
    }
    ```

### **2. Lưu Log Tất Cả Giao Dịch**
- Thêm **node `googleSheets`** để ghi tất cả giao dịch vào bảng Google Sheets.
- **Cấu hình**:
  - **Sheet Name**: `Blockchain_Transactions`.
  - **Headers**:
    - `Hash`, `Blockchain`, `Risk Score`, `Date`, `Compliance`, `Link`.

### **3. Gửi Báo Cáo Định Kỳ (Tuần/Tháng)**
- Sử dụng **node `setInterval`** để chạy workflow định kỳ.
- **Cấu hình**:
  - **Interval**: `7 days` (tuần) hoặc `30 days` (tháng).
  - **Action**: Gửi email tổng hợp tất cả giao dịch trong khoảng thời gian đó.

### **4. Tích Hợp với Trello/Jira**
- Thêm **node `trelloCreateCard`** hoặc **`jiraCreateIssue`** để tạo ticket khi phát hiện giao dịch rủi ro cao.
- **Cấu hình**:
  - **Board/List**: `Blockchain Audit`.
  - **Card Title**: `Rủi Ro Cao: {{$json.hash}} (Risk: {{$json.riskScore}}%)`.
  - **Description**:
    ```markdown
    - **Blockchain**: {{$json.blockchain}}
    - **Tuân Thủ**: {{$json.complianceStatus