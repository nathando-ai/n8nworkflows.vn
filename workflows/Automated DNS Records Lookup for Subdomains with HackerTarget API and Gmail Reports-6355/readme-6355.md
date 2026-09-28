---
title: "🚀 **Tự Động Hóa Kiểm Tra DNS Tất Cả Subdomain Bằng API HackerTarget + Báo Cáo Email (N8N)**"
description: "Workflow này tự động quét và thu thập tất cả các DNS records của subdomain liên quan đến một miền cụ thể (ví dụ: example.com), sau đó gửi báo cáo định dạng Markdown qua email. Giúp các sếp IT/SOC giảm thiểu công việc thủ công, phát hiện lỗ hổng DNS, và đáp ứng các tiêu chuẩn an ninh như ISO 27001, NIST CSF, Essential Eight."
slug: "tieu-dong-hoa-kiem-tra-dns-subdomain-hacker-target"
tags: [n8n, automation, security, dns-monitoring, compliance, gmail, api, no-code]
keywords: [n8n workflow dns, tự động hóa kiểm tra subdomain, báo cáo an ninh email, hacker target api, n8n secops, tự động hóa it security]
---

# 🚀 **Tự Động Hóa Kiểm Tra DNS Tất Cả Subdomain Bằng HackerTarget + Báo Cáo Email (N8N)**

### **🔍 Nỗi Đau Của Các Sếp IT/SOC**
Trong môi trường IT hiện nay, việc **quét thủ công DNS records** của hàng nghìn subdomain để phát hiện:
- **DNS misconfigured** (cấu hình sai),
- **DNS stale** (lỗi thời),
- **DNS malicious** (xâm nhập),
- **Thiếu hụt visibility** về cấu trúc DNS,
là một công việc **mệt mỏi, tốn thời gian và dễ bỏ sót**.

Hơn nữa, việc này còn **không đáp ứng được các tiêu chuẩn an ninh** như ISO 27001, NIST CSF, hoặc Essential Eight, khiến các sếp phải lo lắng về **việc tuân thủ pháp lý** và **rủi ro an ninh**.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động quét tất cả subdomain** của miền mục tiêu.
✅ **Lấy toàn bộ DNS records** (A, AAAA, CNAME, TXT, MX, NS, SOA).
✅ **Định dạng báo cáo dưới dạng Markdown** (dễ đọc, chia sẻ).
✅ **Gửi báo cáo qua email** (hoặc Slack/Notion) **mỗi ngày/tuần**.
✅ **Đáp ứng các tiêu chuẩn an ninh** (ISO 27001, NIST, SOC 2, CIS Controls).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần quét thủ công hàng trăm subdomain.
- **Phát hiện lỗ hổng DNS**: Nhận báo cáo chi tiết về DNS misconfigured, stale, hoặc malicious.
- **Tự động hóa an ninh**: Đáp ứng **ISO 27001 (A.12.6.1)**, **NIST CSF (DE.CM-7)**, **Essential Eight**, và **SOC 2**.
- **Báo cáo dễ đọc**: Định dạng **Markdown** cho cả kỹ sư và quản lý.
- **Audit-ready**: Dữ liệu có thể lưu trữ hoặc chuyển cho **SOC/IT Security**.
- **Hoạt động liên tục**: Chạy tự động **mỗi ngày/tuần** bằng Cron.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HackerTarget API** (để lấy danh sách subdomain).
✔ **Tài khoản Gmail** (hoặc thay thế bằng Slack/Notion/Webhook).
✔ **Miền mục tiêu** (ví dụ: `example.com`).
✔ **API Key của HackerTarget** (nếu có).
✔ **Email nhận báo cáo** (cần cấu hình trong node Gmail).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6355](https://n8n.io/workflows/6355).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste JSON** vào **Create Workflow** → **Paste JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **10 node**, các sếp cần chú ý cấu hình các node sau:

##### **🌐 Node "Target Domain" (Set)**
- **Điền miền mục tiêu** (ví dụ: `example.com`).
- **Lưu ý**: Nếu muốn tự động hóa, sau này có thể kết nối với **Cron Node** để chạy định kỳ.

##### **📡 Node "Subdomain Enum" (HTTP Request)**
- **API Endpoint**: `https://api.hackertarget.com/hostsearch/?q={domain}`
  *(Thay `{domain}` bằng biến `{{$node["🌐 Target Domain"].json()["domain"]}}`)*
- **Headers**:
  - `User-Agent`: `n8n-workflow`
  - `Authorization`: `Bearer {API_KEY_HACKERTARGET}` *(nếu có)*
- **Lưu ý**: Nếu không có API Key, có thể sử dụng **miễn phí** của HackerTarget (nhưng có giới hạn).

##### **🧠 Node "Parse Subdomains" (Code)**
- **Mã JavaScript** đã được tối ưu để **lọc và định dạng** danh sách subdomain.
- **Không cần chỉnh sửa** trừ khi muốn thay đổi logic.

##### **🌐 Node "DNS Records" (HTTP Request)**
- **API Endpoint**: `https://api.hackertarget.com/dnslookup/?q={subdomain}`
  *(Thay `{subdomain}` bằng biến `{{$node["📡 Subdomain Enum"].json()["data"]}}`)*
- **Headers**:
  - `User-Agent`: `n8n-workflow`
  - `Authorization`: `Bearer {API_KEY_HACKERTARGET}` *(nếu có)*

##### **📝 Node "Format DNS Markdown" & "Parse DNS Records" (Code)**
- **Định dạng dữ liệu** thành **Markdown** (dễ đọc).
- **Không cần chỉnh sửa** trừ khi muốn thay đổi format.

##### **🔗 Node "Merge DNS + Subdomain" (Merge)**
- **Gộp dữ liệu** từ subdomain và DNS records.
- **Không cần chỉnh sửa**.

##### **🧩 Node "Merge All Markdown" (Code)**
- **Kết hợp tất cả dữ liệu** thành **báo cáo Markdown cuối cùng**.

##### **📧 Node "Gmail" (Gmail)**
- **Cấu hình OAuth2**:
  - **Email**: `abc@gmail.com` *(thay bằng email nhận báo cáo của các sếp)*
  - **Tên người gửi**: `N8N DNS Report Bot`
  - **Tiêu đề email**: `DNS Report for {{$node["🌐 Target Domain"].json()["domain"]}}`
  - **Nội dung**: Dữ liệu Markdown từ node trước.
- **Lưu ý**:
  - Nếu muốn gửi đến **Slack/Notion/Webhook**, thay thế node Gmail bằng **Slack API** hoặc **HTTP Request**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với miền mẫu (`example.com`).
2. **Kiểm tra email** nhận được báo cáo Markdown.
3. **Bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
- **Kết nối với Cron Node** để chạy **mỗi ngày/tuần**.
- **Thay thế Gmail bằng Slack/Notion**:
  - Sử dụng **Slack Webhook** hoặc **Notion API** thay vì Gmail.
- **Lưu log vào Google Sheets/Notion**:
  - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử.
- **Gửi báo cáo đến SIEM**:
  - Sử dụng **HTTP Request** để gửi dữ liệu đến **Splunk/ELK**.
- **Kết hợp với LLM (AI)**:
  - Sử dụng **n8n-nodes-ai** để **tự động phân tích** DNS records có nguy cơ.
:::

---

### 📌 **Kết Luận**
Workflow này **giúp các sếp IT/SOC**:
✔ **Tự động hóa kiểm tra DNS** mà không cần code.
✔ **Phát hiện lỗ hổng an ninh** một cách nhanh chóng.
✔ **Đáp ứng các tiêu chuẩn ISO 27001, NIST, SOC 2**.
✔ **Tiết kiệm thời gian** và **giảm thiểu rủi ro**.

**🚀 Hãy áp dụng ngay và tự động hóa an ninh DNS của doanh nghiệp!**

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/6355)** | **📧 Liên hệ tác giả Adnan Tariq** ([LinkedIn](https://linkedin.com/in/adnan-tariq-4b2a1a47))