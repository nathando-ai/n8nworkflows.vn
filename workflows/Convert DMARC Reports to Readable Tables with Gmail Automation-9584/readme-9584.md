---
title: "📧 Tự Động Chuyển DMARC Reports Sang Bảng Dữ Liệu Đọc Được Với Gmail (Không Cần Code)"
description: "Workflow tự động hóa lấy DMARC reports từ Gmail, giải nén, chuyển đổi XML thành JSON và tạo bảng dữ liệu dễ đọc, gửi qua email hàng ngày. Giúp các sếp theo dõi bảo mật email hiệu quả mà không cần kỹ thuật."
slug: "tieu-dong-chuyen-dmarc-reports-sang-bang-du-lieu"
tags: [n8n, automation, email, dmarc, gmail, xml-to-json, no-code]
keywords: [tự động hóa dmarc reports, chuyển xml sang json, n8n workflow gmail, bảo mật email, tự động hóa bảo mật domain]
---

# 🚀 **Tự Động Chuyển DMARC Reports Sang Bảng Dữ Liệu Đọc Được Với Gmail**

### **Nỗi Đau Của Các Sếp**
Làm việc với **DMARC reports** từ Gmail hoặc Yahoo thường là một **đau đầu lớn**:
- File được gửi dưới dạng **XML nén (zip/gz)**, khó đọc và phân tích.
- Cần **tìm kiếm thủ công** thông tin quan trọng như lỗi SPF/DKIM, tỷ lệ thất bại...
- **Không có cách tự động hóa** để theo dõi định kỳ, dẫn đến **quá tải công việc** và **rủi ro bảo mật**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy DMARC reports** từ Gmail/Yahoo.
✅ **Giải nén** file XML (zip/gz).
✅ **Chuyển đổi XML → JSON** để dễ phân tích.
✅ **Tạo bảng dữ liệu** dưới dạng HTML.
✅ **Gửi báo cáo hàng ngày** qua email, giúp các sếp **theo dõi bảo mật domain một cách chuyên nghiệp**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở file XML phức tạp hàng ngày.
- **Dữ liệu rõ ràng**: Bảng HTML dễ đọc, phân tích nhanh lỗi SPF/DKIM.
- **Hoạt động tự động**: Báo cáo được gửi hàng ngày **không cần can thiệp**.
- **Bảo mật tăng cao**: Theo dõi định kỳ giúp phát hiện **vi phạm bảo mật sớm**.
- **Dễ mở rộng**: Có thể kết nối với **Airtable/Google Sheets** để lưu trữ lâu dài.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Gmail** (đã kích hoạt DMARC reports).
2. **API Key OAuth2 cho Gmail** (cài đặt trong n8n):
   - Tạo **OAuth2 Credential** trong n8n với quyền:
     - `gmail.readonly` (đọc email)
     - `gmail.send` (gửi email báo cáo)
   - **Cài đặt OAuth2 trong Gmail**:
     - Truy cập [Google Cloud Console](https://console.cloud.google.com/).
     - Tạo **Project mới** → **APIs & Services** → **Credentials** → **OAuth Client ID**.
     - Chọn **Desktop App** → Tải **client_secret.json** → Cấu hình trong n8n.
3. **Thư mục lưu tạm** (n8n sẽ tự động giải nén và xử lý file).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9584](https://n8n.io/workflows/9584).
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor** → Nhấn **Import** → Chọn file JSON.
  - **Hoặc copy/paste** JSON từ file vào **Import Workflow** (tab bên trái).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node `cron` (ScheduleTrigger)**
- **Cấu hình lịch chạy**:
  - Thiết lập **thời gian chạy hàng ngày** (ví dụ: `0 9 * * *` = 9h sáng hàng ngày).
  - **Lưu ý**: Nếu muốn chạy **ngay lập tức**, chọn `* * * * *` (mỗi phút).

##### **🔹 Node `dmarc` (Gmail)**
- **Chọn credential**:
  - Chọn **gmailOAuth2** (đã cấu hình trước).
- **Operation**: Để mặc định là `getAll` (lấy tất cả email DMARC).
- **Lọc email**:
  - Thêm **filter** để chỉ lấy email từ **DMARC Monitor** (ví dụ: `from:"dmarc-monitor@yourdomain.com"`).

##### **🔹 Node `unzip` (Compression)**
- **Chọn file cần giải nén**:
  - Node này tự động lấy **file đính kèm** từ email DMARC.
  - **Không cần cấu hình thêm** (n8n tự động xử lý).

##### **🔹 Node `xml` (ExtractFromFile)**
- **Chọn file XML sau khi giải nén**:
  - Node này **trích xuất nội dung XML** từ file đã giải nén.
- **Operation**: Để mặc định là `xml`.

##### **🔹 Node `xml2json` (XML)**
- **Chuyển XML → JSON**:
  - Node này **tự động chuyển đổi** dữ liệu XML thành JSON.
  - **Không cần cấu hình thêm**.

##### **🔹 Node `set` (Set)**
- **Tạo biến cho email**:
  - Thêm **biến `emailBody`** chứa nội dung HTML của bảng dữ liệu.
  - **Mẫu HTML đơn giản** (n8n tự động tạo từ JSON):
    ```html
    <table border="1">
      <tr><th>Email</th><th>SPF</th><th>DKIM</th><th>DMARC</th></tr>
      {% for item in $json %}
      <tr>
        <td>{{item.email}}</td>
        <td>{{item.spf}}</td>
        <td>{{item.dkim}}</td>
        <td>{{item.dmarc}}</td>
      </tr>
      {% endfor %}
    </table>
    ```

##### **🔹 Node `send` (Gmail)**
- **Chọn credential**: `gmailOAuth2` (cùng credential lấy DMARC).
- **Cấu hình email**:
  - **To**: Địa chỉ email của các sếp (ví dụ: `sếp@doanhnghiep.com`).
  - **Subject**: `DMARC Report - {{ $datetime.now("YYYY-MM-DD") }}`.
  - **Body**: Sử dụng biến `emailBody` từ node `set`.
  - **Attachments**: **Không cần** (n8n đã giải nén và chuyển đổi).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **manual run** để kiểm tra workflow.
   - Kiểm tra **email nhận được** có đúng định dạng HTML không.
2. **Bật Active**:
   - Sau khi test thành công, **bật node `cron`** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Airtable/Google Sheets**:
   - Thêm **node Airtable** hoặc **Google Sheets** sau node `set` để **lưu trữ lâu dài**.
   - Cấu hình **API Key Airtable** hoặc **Google Sheets API**.

2. **Gửi báo cáo qua Slack/Telegram**:
   - Thêm **node Slack Webhook** hoặc **Telegram Bot** sau node `send` để **cảnh báo lỗi DMARC** ngay khi phát sinh.

3. **Tự động phân tích lỗi**:
   - Sử dụng **node LLM (n8n-nodes-base.llm)** để **phân tích tự động** lỗi SPF/DKIM và gửi **cảnh báo chi tiết**.

4. **Lưu log vào Google Drive**:
   - Thêm **node Google Drive** để **lưu file XML gốc** và **bảng dữ liệu** vào một folder riêng.

5. **Tùy chỉnh email theo domain**:
   - Sử dụng **node `set`** để **lọc và gửi báo cáo riêng biệt** cho từng domain (ví dụ: `domain1.com`, `domain2.com`).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **phân tích DMARC thủ công**, đồng thời **tăng cường bảo mật domain** bằng cách theo dõi định kỳ. **Chỉ cần cài đặt 1 lần**, workflow sẽ **chạy tự động hàng ngày**, gửi báo cáo dễ đọc qua email.

**🚀 Hành động ngay!**
- **Cài đặt n8n trên VPS** để workflow chạy 24/7.
- **Cấu hình OAuth2 Gmail** và **import workflow**.
- **Bật chạy** và **theo dõi bảo mật email** một cách chuyên nghiệp!

---
:::note[CHÚ Ý CUỐI CUNG]
- Nếu gặp **lỗi OAuth2**, kiểm tra lại **client_secret.json** và **quyền API**.
- Để **mở rộng**, các sếp có thể **thêm node khác** như **Zapier, Make (Integromat), hoặc Webhooks** để kết nối với hệ thống khác.
- **N8n Self-hosted** là lựa chọn **an toàn và hiệu quả** nhất cho doanh nghiệp.
:::