---
title: "🏠 Tự Động Hoàn Thành Danh Sách Tài Sản Cá Nhân Với Notion + AI Claude (Không Cần Code)"
description: "Workflow tự động hóa tạo danh sách tài sản cá nhân chi tiết từ hình ảnh, văn bản và tự động tổng hợp vào Notion với AI Claude. Giúp các sếp tiết kiệm thời gian lên tới 80% trong việc quản lý tài sản, đồng thời đảm bảo dữ liệu chính xác và được phân loại tự động."
slug: "tieu-dong-hoan-thanh-danh-sach-tai-san-notion-ai-claude"
tags: [n8n, automation, no-code, ai-summarization, notion-integration, anthropic-claude]
keywords: [n8n workflow tài sản cá nhân, tự động hóa danh sách tài sản, Notion + AI Claude, quản lý tài sản không code, danh sách tài sản tự động hóa]
---

# 🚀 **Tự Động Hoàn Thành Danh Sách Tài Sản Cá Nhân Với Notion + AI Claude**

### **Giải pháp cho nỗi đau:**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Quét và ghi chép** danh sách tài sản (đồ điện tử, quần áo, đồ nội thất, tài liệu quan trọng...) bằng tay.
- **Phân loại và cập nhật** thông tin vào Notion, Google Sheets hoặc Excel một cách thủ công.
- **Lo lắng về mất mát** khi không có bản sao kỹ thuật số hoặc dữ liệu không được cập nhật kịp thời.
- **Khó khăn trong việc tìm kiếm** tài sản khi cần (ví dụ: bảo hiểm, bán hàng, di chuyển nhà).

**Workflow này tự động hóa toàn bộ quá trình** bằng cách:
✅ **Nhận dữ liệu** từ hình ảnh, văn bản hoặc nhập thủ công qua Webhook.
✅ **Tự động phân tích và tổng hợp** thông tin tài sản bằng AI Claude (Anthropic).
✅ **Tạo trang Notion chi tiết** với hình ảnh, mô tả, giá trị, và thông tin liên quan.
✅ **Tự động upload hình ảnh** vào Notion, giúp quản lý tài sản trở nên **sạch sẽ, dễ dàng truy cập và bảo mật**.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công.
- **Dữ liệu chính xác và tự động cập nhật**, không bị lỗi nhân thủ.
- **Tạo danh sách tài sản chuyên nghiệp** với hình ảnh, mô tả AI và giá trị tự động phân loại.
- **Dễ dàng tìm kiếm và quản lý** tài sản từ bất kỳ thiết bị nào qua Notion.
- **Bảo mật cao** với Notion và API Claude, không cần lo lắng về rò rỉ dữ liệu.
- **Mở rộng sử dụng** cho quản lý tài sản doanh nghiệp, kho hàng, hoặc even di sản gia đình.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion** (đã cài đặt [n8n Notion Integration](https://n8n.io/integrations/n8n-nodes-base/notion/)).
2. **API Key của Notion**:
   - Mở Notion → **Settings & Members** → **Integrations** → **Create an integration** → Copy **API Key**.
3. **API Key của Anthropic Claude**:
   - Đăng ký tại [Anthropic Developer Portal](https://www.anthropic.com/api) và lấy **API Key**.
4. **Webhook URL** để nhận dữ liệu:
   - Sau khi import workflow, **Webhook URL** sẽ được cung cấp trong node **"When Inventory Posted"**.
5. **Dữ liệu mẫu** (tùy chọn):
   - Các sếp có thể gửi **hình ảnh hoặc văn bản** về Webhook để test (ví dụ: danh sách tài sản trong file PDF, hình ảnh chụp danh sách, hoặc JSON).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/15263](https://n8n.io/workflows/15263) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/15263](https://n8n.io/workflows/15263) (chọn **Export as JSON** → Copy toàn bộ).
2. **Mở n8n Editor** → **Create new workflow** → **Paste JSON** → **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Webhook (Node "When Inventory Posted")**
- **Path**: Đảm bảo giữ nguyên `inventory-notion` (không thay đổi).
- **HTTP Method**: Giữ nguyên `POST`.
- **Credentials**: Chọn `httpHeaderAuth` (nếu đã cấu hình).

#### **B. Cấu hình Notion (Các node liên quan)**
1. **Node "Add Page to Notion"**:
   - **Credentials**: Chọn `notionApi` (đã điền API Key Notion).
   - **Database/Page**: Chọn **Database** hoặc **Page** Notion muốn lưu dữ liệu (ví dụ: "Danh sách tài sản gia đình").
   - **Properties**: Cấu hình các trường như `Name`, `Description`, `Value`, `Image` (tùy chỉnh theo cấu trúc Notion của các sếp).

2. **Node "Initiate Notion Upload Session" và "Upload Images to Notion"**:
   - **Credentials**: Chọn `notionApi`.
   - **URL**: Đảm bảo sử dụng URL API của Notion (n8n sẽ tự động lấy từ credentials).

3. **Node "Add Page to Notion" (lần thứ 2)**:
   - Sau khi AI tổng hợp dữ liệu, node này sẽ **cập nhật trang Notion** với thông tin mới.

#### **C. Cấu hình AI Claude (Node "Claude Sonnet Model")**
- **Model**: Giữ nguyên `claude-sonnet-4-6` (mô hình Claude mới nhất).
- **Credentials**: Chọn `anthropicApi` (đã điền API Key Claude).
- **Prompt (tùy chỉnh)**:
   - Nếu muốn thay đổi cách AI phân tích, các sếp có thể chỉnh sửa **Prompt** trong node **"Home Inventory AI Agent"** (node `agent`).
   - Ví dụ:
     ```json
     "prompt": "Tôi sẽ gửi cho bạn danh sách tài sản dưới dạng JSON hoặc hình ảnh. Hãy phân tích và trả về một cấu trúc dữ liệu Notion chuẩn với các trường sau: Name, Description, Value, Category, ImageUrl. Nếu có hình ảnh, hãy mô tả chi tiết và gán giá trị tự động."
     ```

#### **D. Cấu hình File Handling (Node "Convert Images to Files" và "Split Image Files")**
- **Operation**: Giữ nguyên `toBinary` (chuyển hình ảnh thành file binary).
- **Node "Extract Image Keys" (Code Node)**:
  - Nếu cần chỉnh sửa logic xử lý hình ảnh, các sếp có thể mở node này và sửa code JavaScript (nhưng **không cần thiết** nếu dữ liệu mẫu đúng định dạng).

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi **dữ liệu mẫu** (ví dụ: một hình ảnh chụp danh sách tài sản hoặc JSON) về **Webhook URL**.
   - Kiểm tra **Output** của node **"Parse Structured Output"** để đảm bảo AI Claude phân tích đúng.
2. **Bật Active workflow**:
   - Sau khi test thành công, **nhấp vào "Active"** để workflow chạy liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tự động hóa từ email hoặc Slack**
- **Kết hợp với node `n8n-nodes-base.email`** để nhận danh sách tài sản qua email và chuyển sang Webhook.
- **Kết hợp với node `n8n-nodes-base.slack`** để thông báo khi có tài sản mới được cập nhật.

### **2. Lưu log và báo cáo định kỳ**
- **Thêm node `n8n-nodes-base.ftp` hoặc `n8n-nodes-base.googleDrive`** để lưu log hoạt động của workflow.
- **Tạo báo cáo hàng tháng** bằng cách kết nối với **Google Sheets** hoặc **Notion Dashboard**.

### **3. Phân loại tài sản theo giá trị**
- **Tùy chỉnh Prompt AI** để Claude phân loại tài sản theo giá trị (ví dụ: "Tài sản > 10 triệu", "Tài sản < 1 triệu").
- **Sử dụng node `n8n-nodes-base.filter`** để lọc và tạo trang Notion riêng cho từng loại.

### **4. Xử lý nhiều loại file**
- **Hỗ trợ PDF, Excel, Word**: Sử dụng node `n8n-nodes-base.convertToFile` kết hợp với **OCR (Optical Character Recognition)** để chuyển văn bản từ file thành JSON.
- **Dùng node `n8n-nodes-base.googleDrive`** để tự động tải file từ Google Drive vào workflow.

### **5. Bảo mật dữ liệu**
- **Mật mã hóa API Key**: Sử dụng **n8n Secrets Management** để lưu trữ API Key Claude và Notion an toàn.
- **Chỉ cho phép truy cập Webhook** từ IP cụ thể (cấu hình trong n8n hoặc máy chủ VPS).

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào những việc quan trọng hơn, đồng thời **tạo ra một hệ thống quản lý tài sản chuyên nghiệp, tự động và an toàn**. Bằng cách kết hợp **Notion (để lưu trữ)** và **AI Claude (để phân tích)**, các sếp có thể:
✔ **Quên đi việc ghi chép thủ công**.
✔ **Tìm kiếm tài sản trong giây lát**.
✔ **Bảo vệ tài sản bằng cách có bản sao kỹ thuật số chi tiết**.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa danh sách tài sản của mình!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và phản hồi:**
Nếu các sếp có **ý tưởng cải tiến** hoặc **vấn đề gặp phải**, hãy comment bên dưới hoặc liên hệ với tác giả [Warren Gates](https://n8n.io/workflows/15263) để được hỗ trợ! 🤝