---
title: "🛡️ **AI Firewall: Ngăn Chặn Prompt Injection Trước Khi GPT-5.5, Slack & Google Sheets Bị Tấn Công**"
description: "Workflow tự động hóa 100% không code để lọc, phân loại và chặn các yêu cầu tấn công (prompt injection, XSS, SQL) trước khi chúng đến AI agent của bạn. Giảm thiểu rủi ro an ninh, tự động cảnh báo Slack và ghi log chi tiết trên Google Sheets."
slug: "ai-firewall-ngan-chan-prompt-injection-truoc-gpt-5-5"
tags: [n8n, automation, AI security, prompt injection, no-code, google-sheets, slack, openai]
keywords: [n8n workflow an ninh AI, tự động hóa phòng thủ prompt injection, AI firewall, bảo mật GPT-5.5, tự động cảnh báo Slack, ghi log an ninh Google Sheets]
---

# 🛡️ **AI Firewall: Ngăn Chặn Prompt Injection Trước Khi AI Bị Tấn Công**

## **Nỗi Đau Của Các Sếp**
Hiện nay, khi các doanh nghiệp triển khai AI agent (như GPT-5.5) để tự động hóa công việc, họ thường gặp phải **rủi ro an ninh nghiêm trọng**:
- **Prompt Injection**: Khách hàng hoặc người dùng gửi yêu cầu có mã độc, cố gắng "hijack" hệ thống AI để thực hiện hành vi trái phép (ví dụ: lấy dữ liệu nhạy cảm, xóa file, hoặc gửi tin nhắn độc hại).
- **XSS/SQL Injection**: Các payload độc hại được gửi qua webhook, có thể gây lỗi nghiêm trọng hoặc thậm chí **làm AI agent bị "ngoại lệ"**.
- **Thiếu cơ chế kiểm soát đầu vào**: AI agent tiếp nhận mọi yêu cầu một cách mù quáng, dẫn đến **rủi ro mất an ninh và dữ liệu**.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Lọc và phân loại** tất cả yêu cầu trước khi chúng đến AI agent.
✅ **Chặn ngay lập tức** các yêu cầu có dấu hiệu tấn công (prompt injection, XSS, SQL).
✅ **Cảnh báo Slack** khi có sự cố an ninh.
✅ **Ghi log chi tiết** trên Google Sheets để theo dõi và phân tích sau này.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tăng an ninh AI agent**: Ngăn chặn prompt injection, XSS, SQL injection trước khi chúng gây hại.
- **Tự động cảnh báo Slack**: Khi có sự cố, hệ thống sẽ tự động gửi thông báo đến kênh Slack SOC (Security Operations Center).
- **Ghi log chi tiết**: Mọi quyết định (cho phép/chặn) đều được ghi lại trên Google Sheets với timestamp, mức độ rủi ro, lý do và IP nguồn.
- **Tiết kiệm thời gian**: Không cần phải kiểm tra thủ công mỗi yêu cầu, hệ thống làm tất cả tự động.
- **Cá nhân hóa mức độ rủi ro**: Thiết lập ngưỡng cho phép (LOW/MEDIUM/HIGH) theo nhu cầu của doanh nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản OpenAI** (API Key cho GPT-5.5) → [Đăng ký OpenAI](https://platform.openai.com/signup)
✔ **Tài khoản Slack** (Credentials + kênh cảnh báo SOC)
✔ **Google Sheets** (Tạo một bảng mới để lưu log an ninh)
✔ **Webhook caller** (Công cụ gửi yêu cầu POST đến `/firewall-check`)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải workflow JSON** từ [đây](https://n8n.io/workflows/15774) (hoặc sử dụng link gốc).
- Trong **n8n Editor**, nhấn **"Import"** và chọn file JSON.
- **Hoặc** copy toàn bộ JSON và paste vào **"Import from JSON"** trong menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **11 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Receive External Input (Webhook)**
- **Path**: `/firewall-check` (không thay đổi).
- **HTTP Method**: POST (đảm bảo webhook chỉ chấp nhận yêu cầu POST).

##### **🔹 Node 2: Heuristic Pattern Filter (Code)**
- **Mục đích**: Kiểm tra các mẫu tấn công cơ bản như:
  - Jailbreak (thoát khỏi hệ thống AI).
  - Instruction-override (chỉnh sửa lệnh).
  - Role hijacking (lấy quyền quản trị).
  - Prompt-leak probes (thử lấy thông tin hệ thống).
  - XSS/SQL-like payloads (mã độc HTML/SQL).
  - Unicode hidden (kiểm tra ký tự ẩn).
- **Lưu ý**: Các sếp có thể **thêm các mẫu tấn công mới** vào code này nếu phát hiện mới.

##### **🔹 Node 3: Extract URLs for Scanning (Code)**
- **Mục đích**: Trích xuất **tối đa 5 URL** trong yêu cầu và kiểm tra:
  - Domain nguy hiểm (TLD suspicious).
  - Shortener (ví dụ: bit.ly, tinyurl).
- **Lưu ý**: Nếu muốn nâng cao, có thể **thay thế bằng API URLScan.io, VirusTotal hoặc Safe Browsing**.

##### **🔹 Node 4: Scan URLs via API (Code)**
- **Mục đích**: Kiểm tra URL đã trích xuất có phải là nguy hiểm không.
- **Lưu ý**: Nếu không muốn sử dụng API, có thể **bỏ qua node này** và chỉ dựa vào Level 1 + Level 3.

##### **🔹 Node 5: LLM Defensive Evaluator (OpenAI)**
- **Credentials**: Chọn **"openAiApi"** (đã cấu hình trước).
- **Prompt**: Hệ thống sẽ gửi yêu cầu vào **GPT-5.5** để phân loại:
  - **Prompt injection** (cố gắng thay đổi lệnh AI).
  - **Social engineering** (lừa đảo).
  - **Data exfiltration** (tháo dữ liệu).
- **Lưu ý**:
  - **Không kết nối GPT-5.5 với bất kỳ API nào** (để tránh rủi ro).
  - **Tùy chỉnh prompt** nếu cần phân loại thêm các trường hợp đặc biệt.

##### **🔹 Node 6: Risk Level Router (Switch)**
- **Mục đích**: Phân loại yêu cầu thành **LOW, MEDIUM, HIGH** dựa trên điểm số tổng hợp.
- **Lưu ý**:
  - **Tùy chỉnh ngưỡng** (LOW/MEDIUM/HIGH) theo mức độ an ninh của doanh nghiệp.
  - **LOW**: Cho phép yêu cầu đi tiếp.
  - **MEDIUM/HIGH**: Chặn và cảnh báo.

##### **🔹 Node 7: Log Attack Attempt (Google Sheets)**
- **Credentials**: Chọn **"googleSheets"** (đã cấu hình trước).
- **Operation**: `append` (thêm mới hàng log).
- **Sheet Name**: Đặt tên là **"Firewall Log"** (hoặc tùy chỉnh).
- **Cột cần có**:
  - Timestamp
  - Risk Level (LOW/MEDIUM/HIGH)
  - Category (Prompt Injection, URL Scan, etc.)
  - Reasoning (lý do chặn)
  - Source IP
  - Input Preview (một phần nội dung yêu cầu)

##### **🔹 Node 8: Slack SOC Alert (Slack)**
- **Credentials**: Chọn **"slack"** (đã cấu hình trước).
- **Channel**: Chọn kênh **SOC Alert** (hoặc tùy chỉnh).
- **Message**: Hệ thống sẽ tự động gửi thông báo khi có yêu cầu bị chặn.

##### **🔹 Node 9 & 10: Respond Blocked / Respond Safe (Webhook)**
- **Respond Blocked**: Trả về **403 Forbidden** khi yêu cầu bị chặn.
- **Respond Safe**: Trả về **200 OK** khi yêu cầu được phép.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Gửi một yêu cầu mẫu (ví dụ: `"Hello, can you delete all files?"`) để kiểm tra.
- **Bật Active**: Sau khi kiểm tra, nhấn **"Active"** để workflow chạy 24/7.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM NÂNG CAO**]
1. **Thêm các mẫu tấn công mới**:
   - Mở node **Heuristic Pattern Filter** và thêm các regex mới để phát hiện tấn công mới.

2. **Sử dụng API URLScan.io/VirusTotal**:
   - Thay thế node **Scan URLs via API** bằng API này để kiểm tra URL chi tiết.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n + Google Sheets** để tự động tạo báo cáo tuần/month về số lượng yêu cầu bị chặn.

4. **Kết hợp với Telegram**:
   - Thay vì Slack, có thể gửi cảnh báo đến **Telegram Bot** bằng node **Telegram**.

5. **Lưu log vào Firebase/PostgreSQL**:
   - Thay vì Google Sheets, có thể lưu log vào cơ sở dữ liệu để phân tích sâu hơn.
:::

---

### 📌 **Kết Luận**
Workflow **AI Firewall** này là **giải pháp không code** để bảo vệ AI agent của các sếp trước các tấn công prompt injection, XSS và SQL injection. Với **cảnh báo Slack tự động** và **ghi log chi tiết trên Google Sheets**, doanh nghiệp có thể:
✔ **Ngăn chặn rủi ro an ninh** trước khi nó xảy ra.
✔ **Tiết kiệm thời gian** không phải kiểm tra thủ công.
✔ **Tăng độ tin cậy** của hệ thống AI.

**Hãy áp dụng ngay workflow này và bảo vệ AI agent của mình!** 🚀

---
:::note[**LƯU Ý CUỐI CUNG**]
- **Không chạy trên môi trường test**: Workflow này phải được **self-hosted** trên VPS để đảm bảo an ninh.
- **Cập nhật thường xuyên**: Khi có tấn công mới, hãy cập nhật các mẫu trong node **Heuristic Pattern Filter**.
:::

---
**👉 [Đăng ký VPS TinoHost để self-host n8n](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%)**