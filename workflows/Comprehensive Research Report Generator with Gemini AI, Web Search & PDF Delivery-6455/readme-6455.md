---
title: "📚 Tự Động Hoà Báo Cáo Nghiên Cứu Chi Tiết Với Gemini AI, Tìm Kiếm Web & Gửi PDF (N8n)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo báo cáo nghiên cứu chuyên nghiệp với Gemini AI, tìm kiếm thông tin từ web, tổng hợp và gửi PDF tự động - tiết kiệm thời gian lên đến 80% so với làm thủ công."
slug: "tieu-dong-hoa-bao-cao-nghien-cuu-gemini-ai"
tags: [n8n, automation, no-code, ai-gemini, content-creation, google-sheets, pdf-generation]
keywords: [n8n workflow gemini ai, tự động hóa báo cáo nghiên cứu, tạo báo cáo với gemini, gửi pdf tự động, tìm kiếm web với tavily, n8n google sheets]
---

# 🚀 **Tự Động Hoà Báo Cáo Nghiên Cứu Chi Tiết Với Gemini AI, Web Search & PDF Delivery**

## **🔍 Nỗi Đau Của Các Sếp Khi Tạo Báo Cáo Nghiên Cứu**
Làm việc với báo cáo nghiên cứu thường là một quá trình **mệt mỏi, tốn thời gian và dễ sai sót**:
- **Tìm kiếm thông tin**: Phải tra cứu trên nhiều nguồn web, Google Scholar, hoặc tài liệu PDF để thu thập dữ liệu.
- **Tổng hợp nội dung**: Ghép ghép các đoạn văn bản từ nhiều nguồn khác nhau, đảm bảo logic và tránh trùng lặp.
- **Cải tiến nội dung**: Đảm bảo báo cáo có **cấu trúc chuyên nghiệp**, **mở đầu hấp dẫn** và **mục lục rõ ràng**.
- **Gửi kết quả**: Chuyển đổi nội dung thành **PDF** và gửi qua email hoặc Google Sheets cho đồng nghiệp.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình với:**
✅ **Gemini AI** (Google) và **Claude 3.5** (OpenRouter) để viết nội dung chuyên nghiệp.
✅ **Tìm kiếm web thông minh** với Tavily để lấy thông tin mới nhất.
✅ **Tổng hợp tự động** các chương, mở đầu và mục lục.
✅ **Xuất PDF** và gửi qua email hoặc Google Sheets.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **8-10 giờ/lần** xuống còn **10-15 phút** (tùy độ phức tạp).
- **Nội dung chuyên nghiệp**: Báo cáo được viết bởi **AI Gemini & Claude**, đảm bảo **logic, chính xác và sáng tạo**.
- **Tìm kiếm thông tin toàn diện**: Dùng **Tavily** để lấy dữ liệu từ web, Google Scholar và PDF.
- **PDF tự động**: Xuất báo cáo thành **PDF đẹp mắt** và gửi qua email hoặc lưu vào Google Sheets.
- **Cập nhật liên tục**: Dễ dàng **cập nhật lại báo cáo** khi có thông tin mới.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng **Google Sheets** và **Gemini API**).
2. **Tavily API Key** (để tìm kiếm web).
3. **API Template.io** (để tạo PDF).
4. **OpenRouter API Key** (để sử dụng mô hình Claude 3.5).
5. **Google Sheets Template** (được cung cấp trong hướng dẫn).
6. **Tài khoản Gmail** (nếu muốn gửi PDF qua email).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/6455](https://n8n.io/workflows/6455) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/6455](https://n8n.io/workflows/6455).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán vào.
3. Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Cấu Hình Google Sheets**
Workflow sử dụng **Google Sheets** để:
- **Lưu dữ liệu đầu vào** (chủ đề, yêu cầu).
- **Cập nhật nội dung** (mở đầu, chương, mục lục).
- **Xuất PDF cuối cùng**.

**Cách thiết lập:**
1. Tải **Google Sheet Template** từ [đây](https://docs.google.com/spreadsheets/d/16WekkajqKqMAwrERVjQo2XdzhKCU7QcprfasZnyK0CA/edit?usp=sharing).
2. **Copy sheet** và đặt tên phù hợp (ví dụ: `BaoCaoNghienCuu_2024`).
3. **Cập nhật trong workflow**:
   - Trong node **`Get Sources`**, **`Send Sources`**, **`Get All Content`**, **`Send ToC`**, **`Send Intro`**, **`Update row in sheet`**...
   - Điền **Sheet Name** là tên sheet bạn vừa copy (không dấu cách, dùng `_` thay thế).

#### **🔹 Cấu Hình Tavily API (Tìm Kiếm Web)**
Workflow sử dụng **5 node Tavily** để tìm kiếm thông tin từ web.
**Cách thiết lập:**
1. Đăng ký **Tavily API** tại [tavily.com](https://tavily.com/).
2. Nhận **API Key** và thêm **header Authorization** trong **5 node `Tavily`**:
   ```
   Authorization: Bearer <your_tavily_api_key>
   ```
3. **Kiểm tra** trong node **`Tavily`**, **`Tavily1`**, **`Tavily2`**, **`Tavily3`**, **`Tavily4`**.

#### **🔹 Cấu Hình OpenRouter (Claude 3.5)**
Workflow sử dụng **Claude 3.5 (anthropic/claude-3.5-sonnet)** để viết nội dung.
**Cách thiết lập:**
1. Đăng ký **OpenRouter** tại [openrouter.ai](https://openrouter.ai/).
2. Nhận **API Key** và thêm vào **credentials `openRouterApi`** trong n8n.
3. **Kiểm tra** trong tất cả node **`OpenRouter Chat Model`** (có 7 node).

#### **🔹 Cấu Hình Google Gemini API**
Workflow cũng sử dụng **Gemini Pro** (Google) để viết nội dung.
**Cách thiết lập:**
1. Bật **Google Vertex AI** và tạo **API Key** tại [Google Cloud Console](https://console.cloud.google.com/).
2. Thêm **credentials `googlePalmApi`** trong n8n.
3. **Kiểm tra** trong node **`Google Gemini Chat Model`** (có 7 node).

#### **🔹 Cấu Hình API Template.io (Tạo PDF)**
Workflow sử dụng **API Template.io** để chuyển nội dung thành PDF.
**Cách thiết lập:**
1. Đăng ký tại [API Template.io](https://apitemplate.io/).
2. Nhận **API Key** và thêm vào **credentials `apiTemplateIoApi`**.
3. **Kiểm tra node `Download PDF`** và **`Generate PDF`**.

#### **🔹 Cấu Hình Gmail (Nếu Gửi PDF)**
Nếu muốn **gửi PDF qua email**, cấu hình node **`Send Report`**:
1. Thêm **credentials `gmailOAuth2`** trong n8n.
2. Điền **Email nhận** và **Tiêu đề email** trong node.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Điền **chủ đề nghiên cứu** vào Google Sheets (cột `Topic`).
   - Chạy **Test Execution** trong n8n để kiểm tra.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động khi có dữ liệu mới.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Dữ Liệu Đầu Vào**
- **Điền rõ ràng chủ đề** trong Google Sheets để AI viết nội dung chính xác.
- **Cập nhật thường xuyên** các nguồn tham khảo trong sheet để AI lấy dữ liệu mới nhất.

### **2. Kết Hợp Với Slack/Telegram**
- Thêm **node `webhook`** để nhận yêu cầu từ Slack/Telegram và kích hoạt workflow.
- Cấu hình **Slack/Telegram Bot** để gửi thông báo khi báo cáo hoàn thành.

### **3. Lưu Log & Theo Dõi**
- Thêm **node `Set`** để lưu **log hoạt động** vào Google Sheets.
- Dùng **node `Code`** để format lại dữ liệu trước khi xuất PDF.

### **4. Cập Nhật Nội Dung Định Kỳ**
- Sử dụng **n8n Cron Trigger** để tự động cập nhật báo cáo mỗi tháng.
- Kết hợp với **Google Calendar** để gửi báo cáo định kỳ.

### **5. Tạo Báo Cáo Đa Ngôn Ngữ**
- Thêm **node `lmChatGoogleGemini`** với mô hình **Gemini Multilingual** để viết báo cáo bằng nhiều ngôn ngữ.

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp:
✔ **Tiết kiệm thời gian** lên đến **80%** so với làm thủ công.
✔ **Tạo báo cáo chuyên nghiệp** với AI Gemini & Claude.
✔ **Tìm kiếm thông tin toàn diện** từ web và PDF.
✔ **Xuất PDF tự động** và gửi qua email/Google Sheets.

**🚀 Hãy áp dụng ngay để tự động hóa báo cáo nghiên cứu của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 Xem workflow gốc:** [n8n.io/workflows/6455](https://n8n.io/workflows/6455)
**📌 Template Google Sheets:** [Google Sheet Template](https://docs.google.com/spreadsheets/d/16WekkajqKqMAwrERVjQo2XdzhKCU7QcprfasZnyK0CA/edit?usp=sharing)