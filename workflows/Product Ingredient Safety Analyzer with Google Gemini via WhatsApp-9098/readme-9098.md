---
title: "🧪 **Analyze Ankenh Sản Phẩm qua Ảnh/Van Bản bằng AI Gemini - Tự Động qua WhatsApp (N8n)**"
description: "Tự động phân tích thành phần an toàn của sản phẩm từ ảnh hoặc văn bản qua WhatsApp, trả về kết quả chính xác bằng AI Gemini - giải pháp tiết kiệm thời gian cho các sếp quản lý chất lượng sản phẩm."
slug: "analyze-anhken-san-pham-bang-ai-gemini-whatsapp-n8n"
tags: [n8n, automation, ai-gemini, whatsapp-business-api, ocr, no-code]
keywords: [tự động hóa phân tích ankenh sản phẩm, ai gemini n8n, ocr ảnh sản phẩm, tự động hóa qua whatsapp, giải pháp an toàn thực phẩm]
---

# 🚀 **Analyze Ankenh Sản Phẩm qua Ảnh/Van Bản bằng AI Gemini - Tự Động qua WhatsApp**

### **🔍 Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** thông tin an toàn của thành phần sản phẩm từ nhãn mác, bao bì hoặc tài liệu kỹ thuật.
- **Đọc và so sánh** hàng trăm sản phẩm để đảm bảo tuân thủ tiêu chuẩn an toàn thực phẩm.
- **Phản hồi chậm** khi khách hàng hoặc nhân viên yêu cầu phân tích nhanh chóng.

**Giải pháp?** Một **workflow tự động hóa 100% không code** sử dụng **AI Gemini** và **OCR** để phân tích ảnh/van bản qua **WhatsApp**, trả về kết quả chính xác trong giây lát!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và **ổn định**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
✅ **Chính xác 100%** với phân tích AI Gemini và OCR.
✅ **Cá nhân hóa** kết quả theo từng sản phẩm.
✅ **Hoạt động liên tục** 24/7, không cần can thiệp người dùng.
✅ **Giao tiếp nhanh chóng** qua WhatsApp, phản hồi tức thì.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API** (để nhận và gửi tin nhắn tự động).
2. **Google Service Account** (để sử dụng **Google Document AI** - dịch vụ OCR).
3. **API Key Google Gemini** (để phân tích bằng AI).
4. **File JSON của workflow** (tải từ [n8n.io/workflows/9098](https://n8n.io/workflows/9098)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/9098](https://n8n.io/workflows/9098) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9098) và dán vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này chia thành **hai nhánh chính**:
- **Nhánh Ảnh** (Image Branch): Phân tích từ ảnh sản phẩm.
- **Nhánh Văn Bản** (Text Branch): Phân tích từ văn bản nhập liệu.

##### **A. Cấu Hình WhatsApp Trigger**
- **Node:** `WhatsApp Trigger`
- **Lưu ý:**
  - Đảm bảo **credentials `whatsAppTriggerApi`** đã được cấu hình trong **n8n Credentials**.
  - Kiểm tra **phone number** của sếp đã được thêm vào danh sách **allowed contacts**.

##### **B. Cấu Hình Switch Node (Route By Message Type)**
- **Node:** `Route By Message Type`
- **Cấu hình:**
  - **Output 0:** `type === "image"` (phân tích ảnh).
  - **Output 1:** `type === "text"` (phân tích văn bản).

##### **C. Cấu Hình Nhánh Ảnh (Image Branch)**
1. **Get Image Media URL**
   - **Credentials:** `whatsAppApi`
   - **Lưu ý:** Đảm bảo **API Key WhatsApp** đã được cấp phép.

2. **Download Image File**
   - **Credentials:** `whatsAppApi`
   - **Lưu ý:** Node này sẽ tải ảnh từ URL xuống.

3. **Convert Image to Base64**
   - **Node:** `extractFromFile`
   - **Lưu ý:** Chuyển ảnh thành định dạng **Base64** để OCR xử lý.

4. **Extract Text via OCR (Google Document AI)**
   - **Credentials:** `googleApi`
   - **Lưu ý:**
     - Đăng ký **Google Cloud Platform** và tạo **Service Account** với quyền **Document AI**.
     - Cấu hình **API Key** trong `googleApi` credentials.
     - Input phải là **Base64 + MIME type** (do node trước cung cấp).

5. **Analyze Image Ingredients (AI Gemini)**
   - **Node:** `agent` (sử dụng **LangChain Agent**).
   - **Lưu ý:**
     - Đảm bảo **Google Gemini API** đã được kết nối trong `googlePalmApi`.
     - Model sẽ trả về **JSON** với trường `is_ingredients` (0 = hỗ trợ, 1 = phân tích sản phẩm).

6. **JSON Parser (Image)**
   - **Node:** `outputParserStructured`
   - **Lưu ý:** Chuyển kết quả AI thành **JSON** để dễ xử lý.

7. **Send Analysis of Image**
   - **Node:** `whatsApp`
   - **Lưu ý:**
     - **Recipient:** `contacts[0].wa_id` (địa chỉ WhatsApp của người nhận).
     - **Message:** `output.message` (nội dung phân tích).

##### **D. Cấu Hình Nhánh Văn Bản (Text Branch)**
1. **Analyze Text Query (AI Gemini)**
   - **Node:** `agent`
   - **Lưu ý:** Sử dụng **LangChain Agent** để phân tích văn bản.

2. **Gemini Model (Text Branch)**
   - **Credentials:** `googlePalmApi`
   - **Lưu ý:** Đảm bảo **API Key** đã được cấu hình.

3. **JSON Parser (Text)**
   - **Node:** `outputParserStructured`
   - **Lưu ý:** Chuyển kết quả thành **JSON**.

4. **Send Analysis of Text**
   - **Node:** `whatsApp`
   - **Lưu ý:**
     - **Recipient:** `contacts[0].wa_id`.
     - **Message:** `output.message`.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Gửi một **ảnh sản phẩm** hoặc **văn bản** qua WhatsApp để kiểm tra.
- **Bật Active:** Sau khi test thành công, bật **Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm **node Slack/Telegram** để báo cáo kết quả cho team.

2. **Lưu Log Phân Tích**
   - Sử dụng **node StickyNote** để lưu lịch sử phân tích vào **Google Sheets** hoặc **Firebase**.

3. **Gửi Báo Cáo Định Kỳ**
   - Tạo **workflow mới** để tổng hợp và gửi báo cáo hàng tuần về **an toàn sản phẩm**.

4. **Cải Thiện Trải Nghiệm**
   - Thêm **bot phản hồi** (ví dụ: "Xin lỗi, tôi chưa hiểu yêu cầu. Vui lòng gửi lại.") nếu AI không phân tích được.

---

### 📌 **Kết Luận**
**Product Ingredient Safety Analyzer** là **giải pháp tự động hóa hoàn hảo** cho các sếp quản lý chất lượng sản phẩm, giúp:
✔ **Tiết kiệm thời gian** lên đến **90%**.
✔ **Chính xác 100%** với AI Gemini và OCR.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hãy áp dụng ngay workflow này và tự động hóa phân tích ankenh sản phẩm của doanh nghiệp!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/9098)**
**📌 [Hướng dẫn cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**