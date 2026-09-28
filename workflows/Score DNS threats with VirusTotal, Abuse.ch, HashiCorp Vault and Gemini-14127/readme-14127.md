---
title: "🛡️ **Tự Động Hóa Đánh Giá Threat DNS với VirusTotal, Abuse.ch, HashiCorp Vault & AI Gemini (N8n Workflow)**
description: "Workflow tự động hóa đánh giá nguy cơ DNS threat từ các nguồn uy tín (VirusTotal, Abuse.ch) kết hợp AI Gemini phân tích và lưu trữ kết quả vào MySQL/MongoDB. Giúp các sếp bảo mật tự động phát hiện và phản ứng với các mối đe dọa mạng 24/7."
slug: "tieu-dong-hoa-danh-gia-threat-dns-voi-virustotal-abusech-gemini"
tags: [n8n, automation, cybersecurity, threat-intelligence, ai-summarization, hashi-vault, mysql, mongodb]
keywords: [n8n workflow threat detection, tự động hóa bảo mật mạng, VirusTotal API, Abuse.ch API, AI Gemini phân tích threat, HashiCorp Vault, tự động hóa SecOps]
---

# 🚀 **Tự Động Hóa Đánh Giá Threat DNS với VirusTotal, Abuse.ch, AI Gemini & HashiCorp Vault**

Hiện nay, các doanh nghiệp thường phải mất nhiều thời gian để **quét và phân tích thủ công** các địa chỉ IP/DNS có thể bị tấn công từ các nguồn như VirusTotal, Abuse.ch hay URLhaus. Các sếp bảo mật phải **so sánh, tổng hợp và phản ứng** với hàng ngàn kết quả mỗi ngày, dẫn đến **sai sót, trễ thời gian phản ứng và chi phí nhân lực cao**.

Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
✅ **Quét và đánh giá** nguy cơ từ VirusTotal, Abuse.ch và URLhaus.
✅ **Sử dụng AI Gemini** để tổng hợp và phân tích kết quả một cách thông minh.
✅ **Lưu trữ dữ liệu** vào MySQL (để theo dõi lịch sử) và MongoDB (để phân tích sâu).
✅ **Gửi báo cáo tự động** qua email khi phát hiện threat nghiêm trọng.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần quét thủ công hàng ngàn IP/DNS mỗi ngày.
- **Phát hiện threat nhanh chóng**: AI Gemini tổng hợp kết quả từ nhiều nguồn và đánh giá mức độ nguy hiểm.
- **Lưu trữ thông minh**: Dữ liệu được chia sẻ giữa MySQL (dữ liệu cấu trúc) và MongoDB (dữ liệu không cấu trúc).
- **Báo cáo tự động**: Email cảnh báo khi phát hiện threat nghiêm trọng.
- **Bảo mật tối ưu**: Tất cả API keys và mật khẩu được quản lý bằng **HashiCorp Vault**.
- **Hoạt động liên tục**: Workflow chạy theo lịch trình (schedule) mà không cần người dùng bật/tắt.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Dịch vụ & API Keys**
| Dịch vụ/API | Mô tả | Yêu cầu |
|-------------|--------|----------|
| **VirusTotal API** | Quét và đánh giá nguy cơ từ IP/DNS | [Đăng ký API key](https://www.virustotal.com/gui/signup) |
| **Abuse.ch API** | Kiểm tra threat từ URLhaus & ThreatFox | [Đăng ký API key](https://abuse.ch/) |
| **Google Gemini API** | AI phân tích tổng hợp kết quả | [Cài đặt n8n-node-langchain](https://docs.n8n.io/integrations/n8n-nodes-base/n8n-nodes-base.lmChatGoogleGemini/) |
| **HashiCorp Vault** | Quản lý mật khẩu & API keys an toàn | [Cài đặt Vault](https://www.vaultproject.io/) |
| **MySQL Database** | Lưu trữ dữ liệu cấu trúc (lịch sử scan) | [Cài đặt MySQL](https://dev.mysql.com/doc/) |
| **MongoDB Database** | Lưu trữ dữ liệu không cấu trúc (threat detail) | [Cài đặt MongoDB](https://www.mongodb.com/) |
| **SMTP (Email)** | Gửi báo cáo cảnh báo | Thông tin SMTP của nhà cung cấp email (Gmail, Outlook...) |

### **2. Cấu hình HashiCorp Vault (BẮT BUỘC)**
Tất cả **API keys, mật khẩu và credentials** phải được lưu trong Vault để tránh rò rỉ:
- **Vault API Token** (để n8n truy cập Vault)
- **VirusTotal API Key**
- **Abuse.ch API Key**
- **MySQL Password**
- **MongoDB Password**
- **SMTP Password** (nếu gửi email)

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/14127](https://n8n.io/workflows/14127) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên máy chủ self-hosted của bạn.
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/14127](https://n8n.io/workflows/14127).
2. Trong **n8n Editor**, chọn **Import** → **Paste JSON** → **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Schedule Trigger**
- **Node: "Schedule Trigger"**
  - Đặt **cron expression** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - **Lưu ý**: Nếu muốn chạy thường xuyên, hãy chọn **Active** và kiểm tra log để tránh quá tải.

#### **🔹 Cấu hình MySQL & MongoDB**
- **Node: "Select rows from a table" (MySQL)**
  - Điền **host, port, database name** và **credentials** từ Vault.
  - **Query SQL**: `SELECT * FROM dns_records WHERE scanned = 0 LIMIT 100;` (lấy 100 bản ghi chưa scan).
- **Node: "Insert doc VirusTotal/ThreatFox/URLhaus" (MongoDB)**
  - Điền **connection string** từ Vault (dạng: `mongodb://username:password@host:port/database`).
  - **Collection name**: Đặt tên phù hợp (ví dụ: `virus_total_results`).

#### **🔹 Cấu hình VirusTotal & Abuse.ch**
- **Node: "VirusTotal IP Scan"**
  - **API Key**: Lấy từ Vault (node **"Virus total API TOKEN"**).
  - **Request Body**: Điền `ip_address` từ dữ liệu MySQL.
- **Node: "Abuse.CH_ThreatFox request"**
  - **API Key**: Lấy từ Vault (node **"Abuse API TOKEN"**).
  - **Headers**: Đảm bảo có `Authorization: Bearer <API_KEY>`.
- **Node: "Abuse.CH_URLHaus"**
  - **URL**: `https://urlhaus.abuse.ch/api/abuseUrlhausSearch/`
  - **Query Parameters**: `search=<ip_address>&max=100`

#### **🔹 Cấu hình AI Gemini**
- **Node: "Google Gemini Chat Model"**
  - **API Key**: Lấy từ Vault (node **"Gemini AI Studio"**).
  - **Prompt**: Sử dụng template đã định sẵn trong workflow để AI phân tích kết quả từ VirusTotal, Abuse.ch.
  - **Lưu ý**: Nếu không có API key, cài đặt [n8n-node-langchain](https://docs.n8n.io/integrations/n8n-nodes-base/n8n-nodes-base.lmChatGoogleGemini/) và kích hoạt Gemini API.

#### **🔹 Cấu hình Email Alert**
- **Node: "Send an Email"**
  - **SMTP Credentials**: Lấy từ Vault (node **"Get Email Pass"**).
  - **Subject**: `🚨 Threat Detected: <IP_ADDRESS> (Score: <SCORE>)`
  - **Body**: Nội dung cảnh báo tự động từ AI (có thể tùy chỉnh trong node **"Parse AI Agent output"**).

#### **🔹 Cấu hình HashiCorp Vault**
- **Node: "Virus total API TOKEN", "Abuse API TOKEN", "MySQL Pass", "Mongo DB Pass", "Get Email Pass"**
  - **Vault Path**: Đặt tên phù hợp (ví dụ: `secrets/n8n/virustotal_api_key`).
  - **Kiểm tra**: Sau khi cấu hình, chạy **Test Run** để đảm bảo Vault trả về credentials đúng.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và nhập **IP/DNS mẫu** vào MySQL.
   - Kiểm tra kết quả từ **VirusTotal, Abuse.ch, AI Gemini và email alert**.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.
   - **Monitor log** trong n8n để đảm bảo workflow chạy ổn định.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Kết hợp với Slack/Telegram**
- Thêm **node Slack/Telegram Webhook** để cảnh báo ngay khi phát hiện threat.
- **Cách làm**:
  ```json
  {
    "name": "Send to Slack",
    "type": "slackWebhook",
    "credentials": ["slackWebhook"],
    "options": {
      "text": "🚨 Threat detected: {{$node["Parse AI Agent output"].json["ip_address"]}} (Score: {{$node["Parse AI Agent output"].json["threat_score"]}})"
    }
  }
  ```

### **🔹 Lưu log vào Elasticsearch**
- Thêm **node Elasticsearch** để lưu tất cả log threat cho phân tích sâu.
- **Cài đặt**: [n8n-node-elasticsearch](https://docs.n8n.io/integrations/n8n-nodes-base/n8n-nodes-base.elasticsearch/)

### **🔹 Tự động cập nhật blacklist**
- Sử dụng **node HTTP Request** để gọi API của **Abuse.ch** và tự động cập nhật blacklist vào MySQL.
- **Ví dụ**:
  ```json
  {
    "name": "Update Blacklist",
    "type": "httpRequest",
    "method": "GET",
    "url": "https://urlhaus.abuse.ch/downloads/feeds/json/abuseurlhaus_feed_all.json",
    "credentials": ["httpHeaderAuth"]
  }
  ```

### **🔹 Báo cáo định kỳ cho CEO**
- Thêm **node Email** gửi **báo cáo tổng hợp** hàng tuần/tháng.
- **Cách làm**:
  - Sử dụng **node Code** để tổng hợp dữ liệu từ MySQL.
  - Gửi qua email với **biểu đồ** (có thể kết hợp với **Google Sheets**).

---
## 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp bảo mật khỏi công việc quét và phân tích thủ công. Bằng cách kết hợp **VirusTotal, Abuse.ch, AI Gemini và HashiCorp Vault**, nó **tự động phát hiện, phân tích và phản ứng** với các threat DNS một cách thông minh và an toàn.

👉 **Hành động ngay**:
1. **Cài đặt n8n trên VPS** (self-hosted) để workflow chạy 24/7.
2. **Cấu hình HashiCorp Vault** để quản lý credentials an toàn.
3. **Import workflow** và **test với dữ liệu mẫu**.
4. **Bật Active** và **monitor log** để đảm bảo hoạt động ổn định.

**🎁 Đăng ký VPS TinoHost với mã giảm giá VPSN8N (giảm 39%)** để tự động hóa bảo mật của doanh nghiệp:
👉 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)

---
**Chúc các sếp thành công với việc tự động hóa bảo mật mạng!** 🚀🔒