---
title: "🚀 Tự Động Hoá Nghiên Cứu Quảng Cáo Thương Hiệu & Tạo Hình AI với Apify, GPT-4o & Facebook Ad Library"
description: "Workflow tự động hóa phân tích quảng cáo đối thủ trên Facebook, tạo biến thể hình ảnh AI và tổ chức dữ liệu trên Google Drive/Sheets - tiết kiệm 10+ giờ công/tháng cho các sếp marketing."
slug: "tieu-dong-hoa-nghien-cuu-quang-cao-thuong-hieu-va-tao-hinh-ai"
tags: [n8n, automation, content-creation, multimodal-ai, facebook-ad-library, google-drive, openai, apify]
keywords: [n8n workflow tự động hóa, phân tích quảng cáo đối thủ, tạo hình AI từ quảng cáo, tổ chức dữ liệu marketing, tự động hóa content creation]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Quảng Cáo Thương Hiệu & Tạo Hình AI với AI Multimodal**

Bạn đã bao giờ phải tốn **5-10 giờ** mỗi tuần để thủ công:
- **Scrap** quảng cáo của đối thủ trên Facebook Ad Library?
- **Phân tích** hình ảnh, nội dung và chiến lược của họ?
- **Tạo biến thể** hình ảnh mới để tối ưu hóa chiến dịch?
- **Tổ chức** dữ liệu vào Google Drive/Sheets một cách rối loạn?

Workflow này **giải quyết tất cả** với **1 lần click** - tự động hóa **từ việc scrap đến tạo hình AI**, đồng thời **tổ chức dữ liệu theo cấu trúc chuyên nghiệp** trên Google Drive và Google Sheets. **Không cần code**, chỉ cần **cấu hình 10 phút** là có thể **tiết kiệm 100+ giờ/năm** cho đội ngũ marketing!

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Từ 5-10 giờ/tháng xuống **0 giờ** với việc tự động hóa scrap và phân tích.
✅ **Dữ liệu chính xác**: Nhận **20+ quảng cáo đối thủ** cùng metadata (performance, audience, layout) trong **1 lần chạy**.
✅ **Tạo biến thể AI**: **3 hình ảnh mới** cho mỗi quảng cáo đối thủ, với **ngôn ngữ và phong cách khác nhau** (ví dụ: từ "bright blue" → "minimalist pastel").
✅ **Tổ chức chuyên nghiệp**: Dữ liệu được **sắp xếp theo folder logic** trên Google Drive và **ghi log chi tiết** trên Google Sheets.
✅ **Hoạt động 24/7**: Chỉ cần **bật workflow** là nó tự động chạy mỗi khi có dữ liệu mới.
✅ **Cá nhân hóa**: Thay đổi **từ khóa tìm kiếm** hoặc **ngôn ngữ prompt** để phù hợp với chiến dịch của bạn.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản & API Key**
- **Tài khoản Google** (để sử dụng **Google Drive & Google Sheets**).
- **API Key Apify** (để scrap Facebook Ad Library):
  👉 [Đăng ký miễn phí tại Apify](https://apify.com/) → Tạo **API Token** trong **Settings → API Tokens**.
- **Tài khoản OpenAI** (để sử dụng **GPT-4o & DALL·E 3**):
  👉 [Đăng ký tại OpenAI](https://platform.openai.com/) → Tạo **API Key** trong **Settings → API Keys**.
- **Folder Google Drive** (để lưu trữ quảng cáo và hình ảnh AI).

### **2. Tham số cấu hình**
- **Từ khóa tìm kiếm** (ví dụ: "shoes", "digital marketing", "fashion").
- **Thời gian scrape** (ví dụ: 30 ngày trở lại đây).
- **Mã folder Google Drive** (để lưu trữ kết quả).

### **3. Cấu hình Google Sheets**
- **Tạo 1 bảng Google Sheets mới** với **cột**: `Ad ID`, `Ad URL`, `Ad Image URL`, `Ad Text`, `Performance Metrics`, `Generated Images`, `Prompt Variations`.
- **Chia sẻ bảng với n8n** (quyền **Editor**).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6172](https://n8n.io/workflows/6172) (chọn **Export JSON**).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/6172](https://n8n.io/workflows/6172) (chọn **Export JSON** → Copy toàn bộ).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
3. **Chọn "Import"** để workflow xuất hiện.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **4 bước chính**. Dưới đây là **các node quan trọng cần cấu hình**:

#### **📌 Bước 1: Scrap Facebook Ad Library (Node: "Run Ad Library Scraper")**
- **Thay thế `<your-apify-api-key-here>`** trong **HTTP Request** bằng **API Key Apify** của bạn.
- **Cấu hình body JSON** để scrape quảng cáo:
  ```json
  {
    "searchTerm": "shoes",  // Thay đổi thành từ khóa của bạn
    "startDate": "2024-01-01",  // Thời gian bắt đầu scrape
    "endDate": "2024-06-01",  // Thời gian kết thúc
    "limit": 50  // Số lượng quảng cáo scrape (điều chỉnh theo nhu cầu)
  }
  ```
- **Kiểm tra kết quả** sau khi chạy: Nếu không có dữ liệu, kiểm tra lại **API Key** và **từ khóa**.

#### **📌 Bước 2: Lọc & Giới hạn dữ liệu (Node: "Filter" & "Limit")**
- **Node "Filter"** loại bỏ quảng cáo **không có hình ảnh** (chỉ video).
- **Node "Limit"** điều chỉnh **số lượng quảng cáo scrape** (mặc định là 20). **Điều chỉnh số này** nếu muốn scrape nhiều hơn.

#### **📌 Bước 3: Tạo cấu trúc Google Drive (Node: "Google Drive" - Create Folder)**
- **Node "Create Asset Parent Folder"** sẽ tạo **1 folder chính** (ví dụ: `Ad_Archive_20240601`).
- **Node "Create Child Source Folder"** và **"Create Child Spun Folder"** sẽ tạo **2 folder con**:
  - **Source Folder**: Lưu quảng cáo gốc.
  - **Spun Folder**: Lưu hình ảnh AI biến thể.
- **Điền tham số**:
  - **Folder ID**: Lấy từ **Google Drive URL** (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Folder Name**: Thay đổi thành **mã ngày tháng** (ví dụ: `Ad_Archive_20240601`).

#### **📌 Bước 4: Phân tích hình ảnh & tạo biến thể (Node: "OpenAI" & "Spin Prompts")**
- **Node "OpenAI (analyze)"** sử dụng **GPT-4o Vision** để **miêu tả hình ảnh** (ví dụ: "Hình ảnh có nền màu xanh sáng, chữ viết tay").
- **Node "Spin Prompts"** tạo **3 biến thể prompt** cho mỗi hình ảnh (ví dụ:
  1. "Tạo hình ảnh quảng cáo giày với nền xanh sáng, chữ viết tay."
  2. "Tạo hình ảnh giày với phong cách minimalist, màu pastel."
  3. "Tạo hình ảnh giày với hiệu ứng 3D, nền tối.").
- **Cấu hình OpenAI API Key**:
  - Trong **Node "OpenAI"**, điền **API Key** vào **Credentials**.
  - **Model**: Chọn **gpt-4o** (hoặc **gpt-4-turbo** nếu không có).
  - **Temperature**: Đặt **0.7** để đảm bảo kết quả đa dạng.

#### **📌 Bước 5: Tạo hình ảnh AI & lưu trữ (Node: "Generate Image Using GPT Image 1")**
- **Node "Generate Image Using GPT Image 1"** sử dụng **DALL·E 3** để tạo hình ảnh từ **prompt biến thể**.
- **Cấu hình**:
  - **Model**: Chọn **dall-e-3**.
  - **Size**: Chọn **1024x1024** (phù hợp với quảng cáo).
  - **API Key**: Điền **API Key OpenAI** tương tự như trên.
- **Node "Convert to File"** chuyển **hình ảnh từ binary** thành **file downloadable**.

#### **📌 Bước 6: Ghi log vào Google Sheets (Node: "Google Sheets")**
- **Node "Google Sheets (append)"** ghi **tất cả dữ liệu** (quảng cáo gốc + hình ảnh AI) vào **bảng Google Sheets**.
- **Cấu hình**:
  - **Spreadsheet ID**: Lấy từ **URL Google Sheets** (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Đặt là **"Ad_Archive"** (hoặc tên khác).
  - **Range**: Đặt là **"A1"** (nếu bảng mới) hoặc **"A2"** (nếu đã có dữ liệu).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Nhấn **Execute Workflow** và chọn **Test Run**.
   - Kiểm tra **Google Drive** và **Google Sheets** để xác nhận dữ liệu được lưu trữ đúng.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **đổi trạng thái workflow** từ **Inactive** sang **Active**.
   - **Lưu workflow** để nó tự động chạy khi có **manual trigger**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CÁCH LÀM NÂNG CAO**]
### **1. Tự động chạy hàng tuần**
- Sử dụng **n8n Cron Trigger** để **chạy workflow tự động** mỗi tuần (ví dụ: **Thứ 2 hàng tuần lúc 8h sáng**).
- **Cách cấu hình**:
  - Thêm **Node "Cron Trigger"** vào đầu workflow.
  - Đặt **Schedule** là `0 8 * * 1` (lúc 8h sáng, thứ 2).

### **2. Gửi báo cáo tự động qua Email/Slack**
- Thêm **Node "Email"** (n8n-nodes-base.email) hoặc **Node "Slack"** để **gửi báo cáo** khi workflow chạy xong.
- **Ví dụ**:
  - **Node "Email"**: Gửi **tóm tắt kết quả** (số lượng quảng cáo scrape, hình ảnh AI tạo).
  - **Node "Slack"**: Gửi **thông báo** vào channel dự án.

### **3. Lưu log chi tiết vào Google Drive**
- Thêm **Node "Google Drive (append file)"** để **lưu file log** (ví dụ: `Ad_Archive_20240601_log.txt`) với **tất cả dữ liệu scrape**.

### **4. Tối ưu hóa prompt cho kết quả tốt hơn**
- **Thử nghiệm các biến thể prompt** để cải thiện hình ảnh AI:
  - **Prompt 1**: "Tạo hình ảnh quảng cáo sản phẩm với phong cách hiện đại, màu sắc sống động."
  - **Prompt 2**: "Tạo hình ảnh quảng cáo với hiệu ứng 3D, nền tối, chữ viết tay."
  - **Prompt 3**: "Tạo hình ảnh quảng cáo với phong cách minimalist, màu pastel, ảnh chân thực."

### **5. Sử dụng Google Sheets để theo dõi performance**
- Thêm **cột "Performance Metrics"** vào Google Sheets để **so sánh hiệu quả** của quảng cáo gốc vs. biến thể AI.
- **Ví dụ**:
  - **Cột "CTR (Click-Through Rate)"**: So sánh giữa quảng cáo gốc và biến thể.
  - **Cột "Conversion Rate"**: Theo dõi hiệu quả chuyển đổi.

---
## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi việc thủ công scrap và tạo hình ảnh**, đồng thời **tổ chức dữ liệu một cách chuyên nghiệp**. **Chỉ với 10 phút cấu hình**, các sếp có thể:
✅ **Tiết kiệm 10+ giờ/tháng** cho việc phân tích đối thủ.
✅ **Tạo ra hàng chục biến thể hình ảnh AI** để tối ưu hóa chiến dịch.
✅ **Theo dõi tất cả dữ liệu** trên **Google Drive & Sheets** một cách logic.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình API Key & tham số**.
3. **Chạy test** và **bật Active**.
4. **Tự động hóa toàn bộ quy trình** với **1 lần click**.

**Nếu có vấn đề**, các sếp có thể **đăng câu hỏi** trong [community n8n](https://community.n8n.io/) hoặc liên hệ tác giả **Nick Saraev** qua [tài khoản Twitter](https://twitter.com/nick_saraev). **Chúc các sếp thành công!** 🚀

---
:::note[**LƯU Ý CUỐI CÙNG**]
- **N8n Self-hosted** là **lựa chọn tối ưu** để workflow **chạy 24/7** mà không bị giới hạn.
- **Đăng ký VPS** với **TinoHost** (🎁 **Mã giảm giá: VPSN8N**) hoặc **BNIX** để **cài đặt n8n** một cách dễ dàng.
- **Nếu workflow quá tải**, tăng **limit rate** trong **Node "Wait"** để tránh bị **block API**.
:::

---
**👉 [Tải workflow nguyên bản tại đây](https://n8n.io/workflows/6172)** 👈