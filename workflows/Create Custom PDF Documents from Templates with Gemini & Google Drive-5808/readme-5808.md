---
title: "📄 Tự Động Tạo PDF Tùy Chỉnh Từ Template Google Docs Với Gemini AI & Google Drive (N8N)"
description: "Workflow này chuyển đổi các template hợp đồng, đơn giấy tờ trên Google Docs thành PDF sẵn sàng ký kết chỉ trong vài phút, hoàn toàn tự động hóa mà không cần code. Giúp tiết kiệm thời gian, giảm lỗi và tăng tốc độ phê duyệt."
slug: "tay-dong-tao-pdf-tu-template-google-docs-voi-gemini"
tags: [n8n, automation, google-drive, ai-chatbot, no-code, google-docs, gemini-ai]
keywords: [n8n workflow pdf tự động, tự động hóa tài liệu google docs, gemini ai tạo pdf, template hợp đồng tự động hóa, google drive api n8n]
---

# 🚀 **Tự Động Tạo PDF Tùy Chỉnh Từ Template Google Docs Với Gemini AI & Google Drive**

## **Giới Thiệu**
Bạn có bao giờ phải sao chép template hợp đồng, đơn giấy tờ, hoặc NDA từ Google Docs, điền thông tin thủ công và chuyển đổi thành PDF để gửi cho khách hàng hoặc đồng nghiệp? **Quá trình này tốn thời gian, dễ sai sót và không thể mở rộng khi số lượng template tăng lên.**

Workflow này **giải quyết tất cả những vấn đề đó** bằng cách:
✅ **Tự động hóa hoàn toàn** quá trình tạo PDF từ template Google Docs
✅ **Xóa bỏ sai sót** nhờ kiểm tra bắt buộc các trường cần thiết
✅ **Tăng tốc độ phê duyệt** với PDF sẵn sàng gửi chỉ một cú nhấp chuột
✅ **Hỗ trợ vô hạn template** – thêm template mới vào Google Drive mà không cần chỉnh sửa workflow
✅ **Không cần code** – chạy trên n8n + Google Apps Script, tự host hoặc cloud

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công
- **Giảm 90% lỗi** nhờ kiểm tra tự động các trường bắt buộc
- **Tạo PDF tùy chỉnh** chỉ trong vài phút, không cần kỹ năng kỹ thuật
- **Mở rộng dễ dàng** – thêm template mới mà không cần chỉnh sửa workflow
- **Hoạt động 24/7** – tự động hóa hoàn toàn, không phụ thuộc vào nhân viên
:::

---
## 🎯 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Google Drive & Google Docs**
- **1 folder `Templates/`** (không chứa sub-folder) để lưu tất cả template Google Docs
- **1 folder `Generated/`** để lưu các bản sao PDF sau khi tạo
- **Các template phải tuân theo quy tắc:**
  - **Placeholder:** `{{UPPER_CASE}}` (không dấu, không khoảng trắng)
  - **Khối điều kiện:** `[[BLOCK_NAME:START]]...[[BLOCK_NAME:END]]` (có dòng trống trước `START`)
  - **META_JSON:** Một khối cuối cùng chứa metadata JSON (sẽ được xóa sau khi điền)
  - **Mô tả:** Điền vào phần **Description** của Google Docs (1 dòng)

### **2. API Keys & Credentials**
- **Google Drive OAuth2 API** (Full Access)
- **Google Docs OAuth2 API** (Full Access)
- **Google Gemini API Key** (hoặc OpenAI API Key nếu thay thế)
- **(Tùy chọn)** PostgreSQL credential (nếu sử dụng bộ nhớ chat)

### **3. Google Apps Script**
- **2 file script:**
  - [GetMetaData.gs](https://www.notion.so/Apps-Script-source-code-Notion-Link-22b3f8a1e57f8015a280d90de16c031f?pvs=21)
  - [FillDocument.gs](https://www.notion.so/Apps-Script-source-code-Notion-Link-22b3f8a1e57f8015a280d90de16c031f?pvs=21)
- **Cấp quyền API:**
  - Bật **Google Docs API** và **Google Drive API** trong cài đặt dự án
  - Đặt **Deploy → New Deployment → Web App** với quyền **Anyone** (không phải **Me**)

---
## 🚀 **Cách import & lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
1. Tải file `DocAgent.json` từ [n8n.io/workflows/5808](https://n8n.io/workflows/5808)
2. Trong n8n Editor, chọn **Settings → Import Workflow** và chọn file JSON
3. **Không có lỗi node?** Chỉ cần chọn **credentials** cho mỗi node (Google Drive, Gemini, OAuth2...)

### **2. Các lưu ý BẮT BUỘC phải chỉnh 📌**
#### **A. Cấu hình TemplateList Node**
1. Mở node **Template List** → thay thế `'%3CYOUR_PARENT_ID%3E'` bằng **ID folder `Templates/`** của bạn (lấy từ liên kết Google Drive)
   - Ví dụ: Nếu folder ID là `1AbCdEfGhIjKlMnOpQrStUvWxYz`, thay thế thành `'1AbCdEfGhIjKlMnOpQrStUvWxYz'`
2. **Chạy node** (nhấp chuột phải → **Execute Node**) và sao chép toàn bộ JSON response
3. Dán JSON này vào:
   - **DocAgent** → *System Prompt* (phần trên)
   - **User Choice Match Check** → *System Prompt* (phần trên)

#### **B. Cấu hình Google Apps Script**
1. **Tạo bản sao** 2 file script từ [Notion Link](https://www.notion.so/Apps-Script-source-code-Notion-Link-22b3f8a1e57f8015a280d90de16c031f?pvs=21)
2. **Deploy Web App:**
   - Chọn **Deploy → New Deployment → Web App**
   - **Execute as:** Me
   - **Who has access:** Anyone
   - **Cấp quyền API** cho `https://script.google.com/macros/s/.../exec`
3. **Cập nhật URL trong n8n:**
   - **GetMetaData Node:** `URL = <WEB_APP_URL>?mode=meta&id={{ $json["id"] }}`
   - **FillDocument Node:** `URL = <WEB_APP_URL>`

#### **C. Cấu hình Credentials**
- **Google Drive OAuth2:** Chọn **Drive API (v3) Full Access**
- **Google Docs OAuth2:** Chọn cùng tài khoản
- **Google Gemini API:** Điền API Key
- **(Tùy chọn)** PostgreSQL: Nếu muốn lưu bộ nhớ chat

### **3. Kích hoạt ⚡️**
1. **Bật workflow** (Active)
2. **Test với `/start`** trong chat panel
3. **Chọn template** → điền thông tin → **Confirm**
4. **Kiểm tra PDF** trong folder `Generated/` trên Google Drive

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa template**
- **Sử dụng placeholder chuẩn:** `{{UPPER_CASE}}` (không dấu, không khoảng trắng)
- **Định dạng khối điều kiện:** `[[BLOCK_NAME:START]]...[[BLOCK_NAME:END]]` (có dòng trống trước `START`)
- **Thêm mô tả ngắn** vào phần **Description** của Google Docs

### **2. Kết hợp với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi PDF sẵn sàng
- Ví dụ:
  ```json
  {
    "node": "slack",
    "operation": "sendMessage",
    "text": "PDF đã tạo sẵn: {{ $json["downloadLink"] }}"
  }
  ```

### **3. Lưu log hoạt động**
- Thêm node **Google Sheets** để ghi lại lịch sử tạo PDF
- Cấu hình:
  - **Sheet Name:** `PDF_Logs`
  - **Columns:** `Template Name, User, Date, Status`

### **4. Gửi báo cáo định kỳ**
- Sử dụng **n8n Scheduler** để gửi báo cáo hàng tuần về số lượng PDF tạo
- Ví dụ:
  - **Trigger:** `n8n-nodes-base.schedule`
  - **Action:** `Send Email` với thống kê từ Google Sheets

---
## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc thủ công mệt mỏi** khi tạo PDF từ template, đồng thời **giảm thiểu sai sót và tăng tốc độ phê duyệt**. Với chỉ **vài bước cấu hình**, bạn có thể tự động hóa hoàn toàn quá trình tạo tài liệu tùy chỉnh, mở rộng dễ dàng khi có thêm template mới.

**Bắt đầu ngay hôm nay!**
1. **Chuẩn bị Google Drive** theo hướng dẫn
2. **Import workflow** và cấu hình credentials
3. **Test với `/start`** và tạo PDF đầu tiên

:::success[💡 LƯU Ý CUỐI CÙNG]
- **Nếu gặp lỗi 403 Apps Script**, đảm bảo **Deploy → Web App → Who has access = Anyone**
- **Nếu placeholder không được nhận diện**, kiểm tra **định dạng UPPER_CASE** và **không dấu**
- **Cập nhật TemplateList** mỗi khi thêm template mới
:::

---
### 🔗 **Tài liệu tham khảo**
- [Template mẫu](https://www.notion.so/Simple-sample-template-Template-Link-22b3f8a1e57f8070beacd034ba6f557f?pvs=21)
- [Google Apps Script source](https://www.notion.so/Apps-Script-source-code-Notion-Link-22b3f8a1e57f8015a280d90de16c031f?pvs=21)
- [Tạo VPS cho n8n](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Hãy chia sẻ kết quả của bạn sau khi áp dụng!** 🚀