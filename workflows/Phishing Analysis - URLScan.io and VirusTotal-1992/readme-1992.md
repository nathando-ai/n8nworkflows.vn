---
title: "🛡️ **Phishing Analysis: Tự Động Xác Minh URL Giả Mạo Bằng URLScan.io & VirusTotal (N8n)**
description: "Workflow tự động hóa 100% không code để phân tích URL trong email Outlook, cảnh báo phishing bằng 2 công cụ an ninh hàng đầu. Giúp các sếp tiết kiệm thời gian, giảm rủi ro tấn công, và tự động hóa quy trình SecOps."
slug: "phishing-analysis-urlscan-virustotal-n8n"
tags: [n8n, automation, secops, cybersecurity, no-code, microsoft-outlook, urlscan-io, virustotal]
keywords: [tự động hóa phân tích phishing, n8n workflow secops, urlscan io api, virustotal api, tự động hóa an ninh mạng, cảnh báo email giả mạo]
---

# 🚀 **Phishing Analysis: Tự Động Xác Minh URL Giả Mạo Bằng URLScan.io & VirusTotal**

## **🔍 Nỗi Đau Của Các Sếp: Phishing Làm Giảm Sản Xuất & Tăng Rủi Ro**
Hàng ngày, các sếp phải đối mặt với **nguy cơ phishing** từ email giả mạo, gây ra:
✅ **Thiệt hại tài chính** (do chuyển khoản sai, rò rỉ dữ liệu)
✅ **Gián đoạn hoạt động** (do email chứa malware, ransomware)
✅ **Tốn thời gian** (phải kiểm tra thủ công từng URL trong email)

**Giải pháp?** Một **workflow tự động hóa** phân tích URL trong email bằng **URLScan.io** (analyze website behavior) và **VirusTotal** (check malware), báo cáo kết quả ngay trên **Slack** hoặc **Outlook**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần code, chỉ cần cấu hình API keys.
- **Cảnh báo phishing ngay lập tức**: URL được phân tích và báo cáo trong vòng **1 phút**.
- **Tối ưu hóa an ninh**: Loại bỏ email giả mạo trước khi tác động đến hệ thống.
- **Hoạt động 24/7**: Dùng **Schedule Trigger** để chạy định kỳ (ví dụ: hàng giờ).
- **Báo cáo chi tiết**: Kết quả từ **URLScan.io + VirusTotal** được gộp và gửi qua Slack.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
✔ **Tài khoản Microsoft Outlook** (để lấy email chưa đọc)
✔ **API Key của URLScan.io** ([Đăng ký miễn phí](https://urlscan.io/register))
✔ **API Key của VirusTotal** ([Đăng ký miễn phí](https://www.virustotal.com/gui/join-us))
✔ **Webhook Slack** (để nhận báo cáo)
✔ **n8n Self-hosted** (để chạy 24/7)
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow Official](https://n8n.io/workflows/1992) hoặc copy **JSON** từ tab **"Export"** trong n8n Editor.
- **Dán vào n8n Editor** và nhấn **"Import"**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **16 node**, các sếp cần chú ý cấu hình sau:

#### **🔹 Node "Get all unread messages" (Outlook)**
- **Credentials**: Chọn `"microsoftOutlookOAuth2Api"` (đã cấu hình trước khi import).
- **Operation**: Đảm bảo chọn `"getAll"` để lấy tất cả email chưa đọc.

#### **🔹 Node "Find indicators of compromise" (Code)**
- **Mã Python**: Sử dụng thư viện `ioc-finder` để tìm URL trong email.
- **Lưu ý**: Nếu không có thư viện, các sếp phải **cài đặt thêm** trong **n8n Code Node**:
  ```python
  import ioc_finder
  ```
  (Nếu không có, có thể thay bằng **regex** đơn giản để tìm URL).

#### **🔹 Node "URLScan: Scan URL" & "VirusTotal: Scan URL"**
- **Credentials**:
  - `urlScanIoApi` (API Key URLScan.io)
  - `virusTotalApi` (API Key VirusTotal)
- **Lưu ý**:
  - **URLScan.io** yêu cầu **đợi 1 phút** để hoàn thành scan (do đó có node `Wait 1 Minute`).
  - **VirusTotal** cũng cần thời gian để trả về báo cáo (do đó có node `Wait` sau `Scan URL`).

#### **🔹 Node "Merge Reports"**
- **Kết hợp dữ liệu** từ URLScan.io và VirusTotal để báo cáo đầy đủ.

#### **🔹 Node "sends slack message"**
- **Credentials**: Chọn `"slackApi"` (đã cấu hình webhook Slack).
- **Thông tin báo cáo**:
  - **Tiêu đề email**, **người gửi**, **ngày gửi**.
  - **Kết quả phân tích** (malicious/suspicious/clean).
  - **Link URL** để kiểm tra chi tiết.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với **email mẫu** (ví dụ: email chứa URL phishing).
2. **Bật Active** workflow.
3. **Chạy định kỳ** bằng **Schedule Trigger** (ví dụ: hàng giờ).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CẢNH BÁO PHISHING HIỆU QUẢ]
- **Kết hợp với Microsoft Defender for Office 365**: Nếu đã có, có thể **bỏ node Outlook** và lấy email từ API của Defender.
- **Gửi báo cáo qua Email**: Thay vì Slack, có thể dùng **n8n Email Node** để gửi báo cáo tự động.
- **Lưu log vào Google Sheets/Notion**: Dùng **n8n Google Sheets Node** để ghi lại lịch sử phân tích.
- **Tự động xóa email phishing**: Sau khi phân tích, có thể **xóa email** bằng **Outlook API** nếu kết quả là **malicious**.
:::

---

## 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa phân tích phishing**, tiết kiệm **thời gian và giảm rủi ro** từ email giả mạo. **Chỉ cần cấu hình API keys và chạy**, hệ thống sẽ **liên tục cảnh báo** các URL nguy hiểm!

**🚀 Hãy áp dụng ngay và bảo vệ doanh nghiệp của mình!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/1992)**
**📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/hosting/installation/)**