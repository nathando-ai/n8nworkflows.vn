---
title: "🚀 Tự Động Hóa Tạo Phiếu Báo Giá Thực Tế cho Odoo qua Telegram với AI Google Gemini"
description: "Workflow này tự động hóa quá trình tạo phiếu báo giá Odoo từ tin nhắn Telegram, sử dụng trí tuệ nhân tạo Google Gemini để phân tích yêu cầu khách hàng và tạo phiếu báo giá chính xác trong thời gian thực. Giúp doanh nghiệp tiết kiệm thời gian, giảm sai sót và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoa-tao-phieu-bao-gia-odoo-telegram-gemini"
tags: [n8n, automation, no-code, CRM, AI Chatbot, Odoo, Google Gemini, Telegram Bot]
keywords: [tự động hóa Odoo, tạo phiếu báo giá tự động, AI Google Gemini, Telegram bot CRM, n8n workflow, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Tạo Phiếu Báo Giá Odoo Thực Tế qua Telegram với AI Google Gemini**

### **Giải pháp cho doanh nghiệp bán hàng muốn:**
- **Tiết kiệm 80% thời gian** tạo phiếu báo giá thủ công.
- **Giảm sai sót** trong quá trình nhập liệu và tính toán.
- **Cung cấp trải nghiệm khách hàng cá nhân hóa** với phản hồi nhanh chóng.
- **Hoạt động 24/7** mà không cần can thiệp của nhân viên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Điều này đảm bảo tính bảo mật cao và khả năng mở rộng cho tương lai.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
Workflow này **tự động hóa toàn bộ quy trình từ nhận yêu cầu khách hàng đến tạo phiếu báo giá Odoo**, với sự hỗ trợ của **AI Google Gemini** để phân tích và xử lý thông tin một cách chính xác và nhanh chóng.

:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Khách hàng nhận phiếu báo giá trong **vài giây** thay vì chờ đợi nhiều giờ.
✅ **Tính chính xác cao**: AI phân tích yêu cầu và tính toán giá trị tự động, giảm thiểu lỗi nhập liệu.
✅ **Cá nhân hóa giao tiếp**: Hệ thống trả lời khách hàng bằng cách **hỏi lại chi tiết** nếu cần thiết.
✅ **Hoạt động liên tục**: Workflow hoạt động **24/7** mà không cần can thiệp của nhân viên.
✅ **Tích hợp hoàn hảo với Odoo**: Phiếu báo giá được tạo và lưu trữ ngay trong hệ thống Odoo, đồng bộ hóa dữ liệu.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi triển khai workflow, các sếp cần chuẩn bị các thông tin sau:

### **1. Tài khoản và API Keys**
- **Tài khoản Telegram Bot**:
  - Bot Token (tạo từ [@BotFather](https://t.me/BotFather)).
  - Chat ID của khách hàng (hoặc nhóm chat) để nhận tin nhắn.
- **Tài khoản Odoo**:
  - URL của instance Odoo (ví dụ: `https://odoo.example.com`).
  - Username và Password của người dùng có quyền truy cập vào module **Sale**.
- **Google Cloud API Key**:
  - API Key cho **Google Vertex AI** (để sử dụng Google Gemini).
  - [Hướng dẫn đăng ký API Key](https://cloud.google.com/vertex-ai/docs/general/access-control).
- **N8n Self-hosted**:
  - Workflow này **không hoạt động trên n8n.cloud** do yêu cầu tính bảo mật cao (API keys và dữ liệu Odoo).

### **2. Cấu hình Odoo**
- **Module cần cài đặt**:
  - `sale` (đã có sẵn trong Odoo).
  - `base_import` (nếu cần nhập sản phẩm từ file).
- **Cấu hình quyền**:
  - Người dùng n8n phải có quyền **tạo phiếu báo giá (quotation)** và **tạo đơn hàng bán (sale order)**.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **file JSON**. Các sếp có thể import nó bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/9148](https://n8n.io/workflows/9148) (ấn nút **Export**).
- **Trên n8n Editor**:
  - Nhấn **Import** → Chọn file JSON vừa tải.
  - Hoặc **copy/paste** nội dung JSON vào **Import Workflow** (nút **Import** ở góc trên bên phải).

:::note[Lưu ý]
- **Không sử dụng n8n.cloud** vì yêu cầu API keys và dữ liệu Odoo phải được bảo mật.
- **Không chia sẻ API keys** với bất kỳ ai.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Telegram Trigger**
- **Node**: `Telegram Trigger`
  - **Credentials**: Thêm bot token từ `@BotFather`.
  - **Message Filter**: Đặt `text` để nhận tất cả tin nhắn văn bản.
  - **Chat ID**: Điền chat ID của khách hàng (hoặc nhóm chat) muốn tương tác.

#### **B. Cấu hình Google Gemini AI**
Workflow sử dụng **Google Gemini** để phân tích yêu cầu khách hàng và tạo phiếu báo giá. Các node liên quan:
- **Node**: `Google Gemini Chat Model`, `Google Gemini Chat Model1`, `Google Gemini Chat Model2`, `Google Gemini Chat Model3`, `Google Gemini Chat Model5`
  - **Credentials**: Thêm API Key Google Cloud.
  - **Model**: Chọn `gemini-1.0-pro` (hoặc phiên bản mới nhất).
  - **Prompt**: Các prompt đã được tối ưu sẵn trong workflow, nhưng các sếp có thể **cập nhật lại** nếu cần:
    ```json
    "prompt": "Tôi là trợ lý bán hàng tự động. Hãy phân tích yêu cầu của khách hàng và trả lời bằng cách tạo phiếu báo giá Odoo. Dữ liệu khách hàng và sản phẩm sẽ được cung cấp từ Odoo."
    ```

#### **C. Cấu hình Odoo**
Workflow tương tác với Odoo thông qua các node:
- **Node**: `Product Data`, `Sale Quotation1`, `Sale Order1`, `Search Customer`, `Create Contact`, `Get Product Variant`, `Get Sales Order Details`
  - **Credentials**: Thêm thông tin Odoo (URL, username, password).
  - **Module**: Chọn `sale` và `product`.
  - **Lưu ý**:
    - **Tên Sheet/Table**: Đảm bảo các trường như `name`, `product_id`, `partner_id` khớp với cấu trúc Odoo.
    - **Quản lý sản phẩm**: Nếu sản phẩm có biến thể (variant), workflow sẽ tự động chọn phiên bản phù hợp.

#### **D. Cấu hình AI Agent**
Workflow sử dụng **AI Agent** để quản lý logic tự động:
- **Node**: `AI Agent`, `From AI`, `Quote Creator`
  - **Tool Workflows**: Các node `toolWorkflow` (ví dụ: `Sale Quotation1`, `Create Sales Order SubWorkflow`) sẽ được gọi tự động khi AI cần thực hiện hành động.
  - **Memory Buffer**: Node `Window Buffer Memory1` lưu trữ lịch sử đối thoại để AI hiểu ngữ cảnh.

#### **E. Cấu hình Switch và Logic điều kiện**
Workflow sử dụng **Switch** để kiểm tra điều kiện:
- **Node**: `Switch`, `Switch1`, `Switch2`, `Check Existing Customer`
  - Ví dụ:
    - Nếu khách hàng **không tồn tại**, workflow sẽ tạo **contact mới**.
    - Nếu yêu cầu **không hợp lệ**, AI sẽ hỏi lại khách hàng.

#### **F. Cấu hình Telegram phản hồi**
- **Node**: `Telegram2`, `Telegram3`, `Telegram1`
  - **Credentials**: Sử dụng cùng bot token như ở phần Telegram Trigger.
  - **Message**: Workflow sẽ tự động gửi phản hồi cho khách hàng qua Telegram.

---

### **3. Kích hoạt ⚡️**
Sau khi cấu hình xong, các sếp thực hiện:
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn từ Telegram đến bot (ví dụ: *"Tôi muốn báo giá sản phẩm A và B"*).
   - Kiểm tra phản hồi từ AI và phiếu báo giá được tạo trong Odoo.
2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải của n8n Editor.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tích hợp với Slack/Email**
- **Node**: `Telegram` → Thay thế bằng `Slack` hoặc `Email` để gửi phản hồi.
- **Cách làm**:
  - Thêm **credentials Slack/Email** vào n8n.
  - Sửa lại node `Telegram2`, `Telegram3` thành `Slack` hoặc `Email`.

### **2. Lưu log hoạt động**
- **Node**: `StickyNote` (nếu có trong workflow) hoặc thêm node `Set` để lưu log.
- **Cách làm**:
  - Thêm node `Set` sau `Telegram Trigger` để lưu tin nhắn khách hàng vào một file CSV hoặc database.

### **3. Gửi báo cáo định kỳ**
- **Node**: `Execute Workflow Trigger` → Tạo một workflow riêng để gửi báo cáo phiếu báo giá đã tạo.
- **Cách làm**:
  - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày/giờ.
  - Gửi báo cáo qua **Email** hoặc **Slack**.

### **4. Cập nhật sản phẩm tự động**
- **Node**: `Product Data` → Kết hợp với **Google Sheets** hoặc **API của nhà cung cấp** để cập nhật giá sản phẩm.
- **Cách làm**:
  - Thêm node `Google Sheets` hoặc `HTTP Request` để lấy dữ liệu sản phẩm mới nhất.

### **5. Hỗ trợ nhiều ngôn ngữ**
- **Node**: `Google Gemini Chat Model` → Cập nhật prompt để hỗ trợ tiếng Việt/tiếng Anh.
- **Cách làm**:
  ```json
  "prompt": "Tôi là trợ lý bán hàng tự động. Hãy phân tích yêu cầu của khách hàng và trả lời bằng tiếng Việt. Dữ liệu khách hàng và sản phẩm sẽ được cung cấp từ Odoo."
  ```

---

## 📌 **Kết luận**
Workflow này **cải thiện đáng kể hiệu suất bán hàng** của doanh nghiệp bằng cách tự động hóa quá trình tạo phiếu báo giá Odoo từ Telegram, với sự hỗ trợ của **AI Google Gemini**. Các sếp không chỉ **tiết kiệm thời gian** mà còn **giảm sai sót** và **cải thiện trải nghiệm khách hàng**.

:::success[**Hành động ngay hôm nay!**]
1. **Chuẩn bị** tài khoản Odoo, Telegram Bot và API Key Google Cloud.
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test Run** với dữ liệu mẫu và **bật Active**.
4. **Tích hợp thêm** Slack/Email hoặc báo cáo định kỳ nếu cần.

**Nếu có vấn đề**, các sếp có thể liên hệ với tác giả [Evozard](https://n8n.io/workflows/9148) hoặc cộng đồng n8n trên [Discord](https://n8n.io/discord).

**🚀 Hãy tự động hóa bán hàng của mình ngay bây giờ!** 🚀
---