---
title: "🚀 Tự Động Hoá Tìm Kiếm & Gửi Email Tiềm Năng Kinh Doanh Với Claude AI, Apify & Gmail (Không Cần Code)"
description: "Workflow tự động hóa tìm kiếm và gửi email tiềm năng kinh doanh từ dữ liệu web scraping, sử dụng Claude AI để viết nội dung email cá nhân hóa, lưu trữ trên Google Sheets và gửi qua Gmail. Giúp các sếp tiết kiệm thời gian lên tới 80% trong quá trình outreach cold."
slug: "tu-dong-hoa-tim-kiem-va-gui-email-tien-nang-kinh-doanh"
tags: [n8n, automation, lead-generation, ai-outreach, google-sheets, gmail, apify, claude-ai]
keywords: [n8n workflow lead generation, tự động hóa tìm kiếm email doanh nghiệp, Claude AI viết email cá nhân hóa, Apify scraping data, tự động gửi email cold outreach]
---

# 🚀 **Tự Động Hoá Tìm Kiếm & Gửi Email Tiềm Năng Kinh Doanh Với Claude AI, Apify & Gmail**

## **💡 Nỗi Đau Của Các Sếp Trong Quá Trình Outreach Cold**
Bạn đã bao giờ phải:
- **Tốn hàng giờ** để tìm kiếm email, số điện thoại và thông tin liên hệ của khách hàng tiềm năng?
- **Viết hàng chục email** một cách lặp đi lặp lại, thiếu cá nhân hóa?
- **Quên gửi email** hoặc gửi sai thời điểm, mất cơ hội liên hệ?
- **Không theo dõi được** quá trình outreach để tối ưu chiến dịch?

Workflow này **giải quyết tất cả** bằng cách tự động hóa **tất cả quá trình từ tìm kiếm đến gửi email**, với nội dung được viết bởi **Claude AI** (mô hình ngôn ngữ lớn của Anthropic) – giúp email của bạn **trông như được viết tay**, không giống như spam.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 80% thời gian** trong outreach cold (không cần tìm kiếm thủ công).
✅ **Email cá nhân hóa 100%** với nội dung được viết bởi AI (không giống như email template lặp đi lặp lại).
✅ **Lưu trữ dữ liệu leads** trên Google Sheets, dễ dàng theo dõi và phân tích.
✅ **Gửi email tự động** qua Gmail, không lo quên hoặc gửi sai thời điểm.
✅ **Hoạt động 24/7** – không cần can thiệp thủ công.
✅ **Kết hợp với Apify** để scraping dữ liệu từ web, không cần viết code.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Claude AI** (Anthropic API Key) – [Đăng ký miễn phí](https://www.anthropic.com/api).
2. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0) – [Cài đặt OAuth cho Gmail](https://developers.google.com/gmail/api/quickstart/python).
3. **Tài khoản Google Sheets** (đã tạo một bảng mới để lưu leads).
4. **Tài khoản Apify** (để scraping dữ liệu) – [Đăng ký miễn phí](https://www.apify.com/).
5. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7).
6. **Mã Webhook** (sẽ được cung cấp sau khi setup Claude Co-Work).

👉 **🎁 Mã giảm giá VPS cho n8n (Self-hosted):**
- [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã: **VPSN8N** - giảm 39%)
- [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ **50k/tháng**)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/15153](https://n8n.io/workflows/15153) (chọn "Export").
2. **Mở n8n Editor** (trang chủ của workflow).
3. Nhấn **"Import"** và chọn file JSON vừa tải.
4. **Chọn workspace** (nếu có nhiều workspace).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/15153](https://n8n.io/workflows/15153) (chọn "Export" > "Copy JSON").
2. Trong n8n Editor, nhấn **"Import"** > **"Paste JSON"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Webhook (Nhận dữ liệu từ Claude Co-Work)**
- **Không cần chỉnh gì** nếu đã setup Claude Co-Work đúng cách.
- **Path** đã được tự động cấu hình (`1371918c-dcdd-4286-a02e-422a5ec37668`).
- **Lưu ý:** Nếu không nhận được dữ liệu, kiểm tra:
  - **Claude Co-Work** có gửi webhook đúng không?
  - **CORS** của n8n có cho phép domain của Claude Co-Work không?

#### **🔹 Node 2: Split Out (Tách dữ liệu leads thành các record riêng biệt)**
- **Không cần chỉnh** (n8n tự động tách dữ liệu theo cấu trúc JSON từ Claude Co-Work).

#### **🔹 Node 3: Outreach Email Copywriter (Sử dụng Claude AI viết email)**
- **Credentials:** Chọn `"anthropicApi"` (đã setup trước khi import).
- **Prompt mẫu (nếu cần chỉnh sửa):**
  ```json
  "Generate a personalized cold email for a business lead. Use a professional but friendly tone. Include:
  - Subject: [Business Name] – Quick Question About [Industry]
  - Body: [3-4 sentences introducing yourself, mentioning how you found them, and a specific value proposition]
  - Signature: [Your Name], [Your Position], [Company Name]
  - P.S.: [Optional follow-up question or CTA]"
  ```
- **Lưu ý:**
  - Nếu email không phù hợp, chỉnh sửa **prompt** trong node **Code** (Node 5).
  - Đảm bảo **API Key Claude** có đủ credit (mỗi request ~$0.005).

#### **🔹 Node 4: If (Kiểm tra dữ liệu trước khi gửi email)**
- **Không cần chỉnh** (n8n tự động bỏ qua leads không hợp lệ).

#### **🔹 Node 5: Split Email Text (Tách subject & body email)**
- **Mã JavaScript cần chỉnh (nếu cần):**
  ```javascript
  // Nếu dữ liệu từ Claude AI có cấu trúc khác, chỉnh sửa ở đây
  return {
    json: {
      subject: item.json.subject,
      body: item.json.body,
      signature: item.json.signature,
      ps: item.json.ps || ""
    }
  };
  ```
- **Lưu ý:** Nếu Claude AI trả về format khác, hãy **log ra console** để debug.

#### **🔹 Node 6: Send Email to Leads (Gửi qua Gmail)**
- **Credentials:** Chọn `"gmailOAuth2"` (đã setup OAuth 2.0).
- **Lưu ý:**
  - **Không gửi quá 50 email/ngày** (Gmail có giới hạn).
  - **Kiểm tra spam:** Nếu email bị đánh dấu spam, chỉnh sửa **subject** hoặc **nội dung**.
  - **Test trước:** Gửi thử cho 1-2 email trước khi chạy toàn bộ.

#### **🔹 Node 7: Append Leads in Sheet (Lưu dữ liệu vào Google Sheets)**
- **Credentials:** Chọn `"googleSheetsOAuth2Api"`.
- **Sheet Name:** Điền tên sheet (ví dụ: `"Leads"`).
- **Range:** Điền `"Sheet1!A1"` (nếu sheet mới).
- **Lưu ý:**
  - **Kiểm tra quyền truy cập** của Google Sheets OAuth.
  - **Cấu trúc dữ liệu:** Đảm bảo dữ liệu từ Claude Co-Work phù hợp với cột trong sheet.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run (Dữ liệu mẫu):**
   - Nhấn **"Run"** trên node **Webhook** và nhập dữ liệu mẫu từ Claude Co-Work.
   - Kiểm tra:
     - Email có được viết không?
     - Email có được gửi không?
     - Dữ liệu có được lưu vào Google Sheets không?

2. **Bật Active:**
   - Sau khi test thành công, **bật "Active"** trên workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram để báo cáo**
- **Thêm node Slack/Telegram** sau node **Send Email** để thông báo khi email được gửi thành công.
- **Mẫu message:**
  ```
  🚀 Email sent to: {{$node["Send email to Leads"].json["email"]}}
  Subject: {{$node["Send email to Leads"].json["subject"]}}
  ```

### **🔹 Lưu log hoạt động**
- **Thêm node StickyNote** để ghi lại lỗi hoặc thông tin debug.
- **Mẫu log:**
  ```
  [{{$node["Webhook"].date}}] - Lead: {{$node["Webhook"].json["name"]}} - Status: {{$node["Send email to Leads"].status}}
  ```

### **🔹 Gửi báo cáo định kỳ**
- **Sử dụng node Schedule** (n8n Pro) để gửi báo cáo hàng tuần về:
  - Số email đã gửi.
  - Tỷ lệ mở (nếu tích hợp Google Analytics).
  - Leads mới nhất.

### **🔹 Tối ưu Claude AI**
- **Chỉnh sửa prompt** để email phù hợp với ngành nghề:
  - **Dịch vụ SaaS:** Nhấn mạnh tính năng giá trị.
  - **Bán lẻ:** Đề cập đến ưu đãi đặc biệt.
  - **Dịch vụ tư vấn:** Nêu rõ kinh nghiệm của bạn.

### **🔹 Sử dụng Apify để scraping dữ liệu mới**
- **Cài đặt Apify Actor** (ví dụ: [Email Extractor](https://apify.com/alexander-volkov/email-extractor)) để lấy email mới.
- **Kết nối với Webhook** để tự động cập nhật leads.

---

## **📌 Kết Luận: Bắt Đầu Tự Động Hoá Outreach Ngay Hôm Nay!**

Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy** và **quan hệ khách hàng** thay vì làm việc lặp đi lặp lại. Với **Claude AI**, email của bạn sẽ **trông như được viết tay**, không giống như spam – giúp tăng tỷ lệ phản hồi lên **3-5 lần**.

### **🚀 Bước đầu tiên:**
1. **Setup tài khoản** (Claude, Gmail, Google Sheets, Apify).
2. **Import workflow** và **cấu hình credentials**.
3. **Test với 1-2 leads** trước khi chạy toàn bộ.
4. **Bật Active** và **đợi AI làm việc cho bạn!**

**💬 Cần hỗ trợ?** Đăng ký khóa học của **Dr. Firas** để học cách xây dựng workflow tự động hóa chuyên nghiệp:
👉 [Tìm hiểu khóa học](https://automatisation.notion.site/Claude-Cowork-n8n-3423d6550fd98049a8c1eda298bbeb04)

---
**🔥 Chúc các sếp thành công với chiến dịch outreach tự động hóa!** 🚀