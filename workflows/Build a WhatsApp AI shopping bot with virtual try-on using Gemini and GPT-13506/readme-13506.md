---
title: "🤖 **Tự Động Hóa Bot Mua Sắm AI Trên WhatsApp Với Hiệu Ứng Thử Trang (VTO) - Sử Dụng Gemini & GPT**"
description: "Tạo bot AI mua sắm thông minh trên WhatsApp với tính năng thử trang ảo (Virtual Try-On) bằng Gemini và GPT-4o, tự động hóa tìm kiếm sản phẩm, đặt hàng và xử lý hình ảnh. Giúp doanh nghiệp tiết kiệm 80% thời gian hỗ trợ khách hàng và tăng tỷ lệ chuyển đổi lên 30%."
slug: "tay-dong-hoa-bot-mua-sam-ai-whatsapp-virtual-try-on"
tags: [n8n, automation, ai-chatbot, whatsapp-bot, virtual-try-on, gemini-api, gpt-4o, self-hosted]
keywords: [n8n workflow whatsapp bot, tự động hóa mua sắm ai, virtual try on với gemini, bot whatsapp sử dụng gpt-4o, tự động hóa bán hàng trên whatsapp, gemini api n8n]
---

# 🚀 **Bot Mua Sắm AI Trên WhatsApp Với Hiệu Ứng Thử Trang (VTO) - Giải Pháp Tự Động Hóa 100% Không Code**

Hiện nay, việc hỗ trợ khách hàng qua WhatsApp vẫn còn phụ thuộc nhiều vào nhân viên, dẫn đến **chậm trễ, sai sót và trải nghiệm khách hàng không đồng nhất**. Các sếp đang phải mất **từ 3-5 tiếng/ngày** để xử lý các yêu cầu tìm kiếm sản phẩm, đặt hàng và hỗ trợ thử trang ảo (VTO) – một quá trình tốn kém thời gian và dễ gây mất hứng thú cho khách.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình mua sắm AI** trên WhatsApp, từ tìm kiếm sản phẩm đến đặt hàng và thử trang ảo.
✅ **Sử dụng Gemini và GPT-4o** để phân loại ý định khách hàng, tìm kiếm sản phẩm thông minh và tạo hiệu ứng thử trang ảo (VTO) từ hình ảnh thực tế.
✅ **Cải thiện trải nghiệm khách hàng** với tính năng tương tác thông minh (nhấn nút đặt hàng hoặc thử trang) và phản hồi tức thời.
✅ **Giảm chi phí vận hành** bằng cách loại bỏ việc hỗ trợ thủ công, tiết kiệm **tới 80% thời gian** và tăng **tỷ lệ chuyển đổi lên 30%**.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**

:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình mua sắm AI** trên WhatsApp, không cần code.
- **Tăng tỷ lệ chuyển đổi lên 30%** nhờ tính năng thử trang ảo (VTO) và đặt hàng một nút.
- **Giảm thời gian hỗ trợ khách hàng từ 5 tiếng/ngày xuống còn 30 phút**, tiết kiệm chi phí nhân sự.
- **Trải nghiệm khách hàng đồng nhất** với phản hồi tức thời và tính năng tương tác thông minh.
- **Hỗ trợ đa ngôn ngữ và cá nhân hóa** thông qua AI (GPT-4o và Gemini).
- **Lưu trữ dữ liệu bán hàng** tự động vào Google Sheets và MongoDB, dễ dàng phân tích.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**

:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:

### **1. WhatsApp Business API**
- **Tài khoản WhatsApp Business** (đăng ký tại [Meta for Developers](https://developers.facebook.com/)).
- **API Credentials** (cấp từ WhatsApp Business API).

### **2. OpenAI API**
- **Tài khoản OpenAI** ([openai.com](https://openai.com/)).
- **API Key** cho:
  - **GPT-5-nano** (để phân loại ý định khách hàng).
  - **GPT-4o** (để xử lý đặt hàng).
  - **OpenAI Embeddings** (để tìm kiếm sản phẩm thông minh).

### **3. Google Gemini API**
- **Tài khoản Google Cloud** ([cloud.google.com](https://cloud.google.com/)).
- **API Key** cho **Gemini API** (để tạo hiệu ứng thử trang ảo).

### **4. MongoDB Atlas**
- **Tài khoản MongoDB Atlas** ([mongodb.com](https://www.mongodb.com/)).
- **Database** với collection `product` và **vector index** tên `ShoppingBot`.
- **API Key** cho MongoDB Atlas.

### **5. Redis**
- **Tài khoản Redis** (có thể sử dụng Redis Cloud hoặc tự host).
- **Credentials** (URL, port, password).

### **6. Google Drive & Google Sheets**
- **Tài khoản Google Workspace** ([google.com/workspace](https://workspace.google.com/)).
- **Service Account** cho Google Drive và Google Sheets.
- **File Google Sheets** để lưu log đơn hàng.

### **7. Dữ liệu sản phẩm**
- **Catalog sản phẩm** đã được **embedding** và lưu vào MongoDB (cần chuẩn bị trước khi chạy workflow).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/13506](https://n8n.io/workflows/13506).
2. Vào **n8n Editor** (self-hosted hoặc n8n.cloud).
3. Nhấn **Import** và chọn file JSON.
4. Hoặc copy toàn bộ JSON và nhấn **Paste JSON**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Các node quan trọng cần cấu hình kỹ lưỡng:

| **Node**                     | **Tham Số Cần Điền**                          | **Lưu Ý**                                                                 |
|------------------------------|-----------------------------------------------|---------------------------------------------------------------------------|
| **WhatsApp Trigger**         | `Phone Number ID`, `API Key`                  | Lấy từ WhatsApp Business API.                                             |
| **OpenAI (GPT-5-nano, GPT-4o)** | `API Key`                                    | Điền API Key từ OpenAI.                                                   |
| **Google Gemini**            | `API Key` (credentials: `googlePalmApi`)     | Điền API Key từ Google Cloud.                                             |
| **MongoDB Atlas**            | `Connection URL`, `Database Name`, `API Key`  | Chắc chắn collection `product` có **vector index** tên `ShoppingBot`.      |
| **Redis**                    | `Host`, `Port`, `Password`                   | Sử dụng Redis Cloud hoặc tự host.                                         |
| **Google Drive**             | `Service Account JSON`                       | Cấp từ Google Cloud Console.                                             |
| **Google Sheets**            | `Spreadsheet ID`, `Service Account JSON`     | Chọn sheet để lưu log đơn hàng.                                         |

#### **B. Cấu Hình Node Quan Trọng**
1. **`WhatsAppTrigger`**:
   - Điền `Phone Number ID` và `API Key` từ WhatsApp Business API.
   - Chọn `Webhook URL` từ n8n (cần mở port 3000 nếu self-hosted).

2. **`MongoDB Atlas`**:
   - Kiểm tra collection `product` có **vector index** tên `ShoppingBot` không.
   - Cấu hình `operation: "insert"` và `operation: "find"` với query phù hợp.

3. **`GoogleGemini` (Virtual Try-On)**:
   - Điền `API Key` vào `credentials: googlePalmApi`.
   - Kiểm tra `operation: "analyze"` và `resource: "image"` để xử lý hình ảnh.

4. **`Redis`**:
   - Cấu hình `TTL` cho các key như `user_session_<waId>` (1 giờ) và `vto_context_<waId>` (10 phút).

5. **`GoogleDrive`**:
   - Chọn `operation: "download"` và điền `fileId` của sản phẩm từ MongoDB.

6. **`GoogleSheetsTool`**:
   - Chọn sheet và cấu hình `operation: "append"` để ghi log đơn hàng.

#### **C. Node Code (Cần Chỉnh Sửa)**
Các node **`code`** trong workflow cần **sửa lại logic** để phù hợp với dữ liệu của các sếp:
- **`Build Redis cache key from search query`**: Chỉnh query để phù hợp với cách lưu trữ sản phẩm.
- **`Parse button and user data`**: Đảm bảo trích xuất `waId`, `productId` và `intent` chính xác.
- **`Build product card message body`**: Cập nhật nội dung nút "Đặt Hàng" và "Thử Trang" theo ngôn ngữ của doanh nghiệp.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn WhatsApp với các intent khác nhau (tìm kiếm sản phẩm, đặt hàng, thử trang).
   - Kiểm tra phản hồi của bot và log trong Google Sheets.
2. **Bật Active workflow**:
   - Đảm bảo tất cả node đều **Active** và không có lỗi.
   - Kiểm tra **Redis** và **MongoDB** để đảm bảo dữ liệu được lưu trữ đúng.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để báo cáo lỗi hoặc cập nhật trạng thái đơn hàng.

2. **Lưu Log Chi Tiết**:
   - Sử dụng **Google Sheets** hoặc **MongoDB** để lưu toàn bộ lịch sử tương tác của khách hàng.

3. **Báo Cáo Định Kỳ**:
   - Tạo workflow riêng để **tổng hợp báo cáo doanh số** hàng ngày/tuần và gửi qua email.

4. **Cải Thiện Hiệu Ứng Thử Trang**:
   - Sử dụng **Gemini Pro** thay vì Gemini Flash nếu chất lượng hình ảnh không đáp ứng.

5. **Hỗ Trợ Nhiều Ngôn Ngữ**:
   - Cấu hình **OpenAI API** với ngôn ngữ khác nhau (Việt Nam, Anh, Trung Quốc...) để hỗ trợ khách hàng quốc tế.

6. **Tích Hợp CRM**:
   - Kết nối với **HubSpot** hoặc **Zoho CRM** để đồng bộ dữ liệu khách hàng và đơn hàng.

7. **Optimize Performance**:
   - Sử dụng **Redis Cluster** nếu lưu trữ nhiều session.
   - Cập nhật **vector index** trong MongoDB để tăng tốc độ tìm kiếm.
---

## 📌 **Kết Luận**

Workflow này không chỉ **tự động hóa toàn bộ quy trình mua sắm AI trên WhatsApp**, mà còn **cải thiện trải nghiệm khách hàng** với tính năng thử trang ảo (VTO) và đặt hàng một nút. Với **tỷ lệ chuyển đổi tăng 30%** và **tiết kiệm 80% thời gian hỗ trợ**, đây là giải pháp **không thể bỏ qua** cho bất kỳ doanh nghiệp bán lẻ nào muốn **tăng doanh thu và tối ưu hóa quy trình bán hàng**.

**Hành động ngay hôm nay:**
1. **Chuẩn bị các credentials** theo danh sách trên.
2. **Import workflow** và cấu hình kỹ lưỡng.
3. **Test run** với dữ liệu mẫu và **bật Active**.
4. **Mở rộng** với các tính năng nâng cao như Slack, CRM hoặc báo cáo tự động.

---
:::success[🎁 **Ưu Đãi Đặc Biệt Cho Các Sếp**]
Để workflow chạy ổn định 24/7, các sếp nên **self-host n8n** trên VPS chất lượng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI).

**Nếu cần hỗ trợ cấu hình, liên hệ BytezTech qua [website](https://byteztech.vn) để được tư vấn miễn phí!** 🚀
:::

---
**Chúc các sếp thành công với bot AI mua sắm thông minh trên WhatsApp!** 🛒🤖