---
title: "🎨 Tự Động Hoà Hợp Ảnh Quảng Cáo Sản Phẩm Với AI (OpenAI + Gemini) - Không Cần Code!"
description: "Workflow tự động hóa tạo ảnh quảng cáo sản phẩm chuyên nghiệp từ ảnh sản phẩm và ảnh mô hình/người mẫu bằng AI multimodal (OpenAI + Gemini), đồng bộ với Google Drive & Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/ngày so với làm thủ công."
slug: "tieu-dong-hoa-tao-anh-quang-cao-san-pham-ai"
tags: [n8n, automation, content-creation, ai-multimodal, google-workspace, openai, gemini]
keywords: [n8n workflow tự động hóa, tạo ảnh quảng cáo AI, OpenAI Gemini tự động, tự động hóa marketing, Google Drive Google Sheets n8n, AI tạo hình ảnh không code]
---

# 🚀 **Tự Động Tạo Ảnh Quảng Cáo Sản Phẩm Với AI: Từ Ảnh Thô → Ảnh Chuyên Nghiệp Chỉ Với 1 Clic**

### **Nỗi Đau Của Các Sếp Trong Marketing**
Làm thế nào để tạo ra **ảnh quảng cáo chuyên nghiệp** cho sản phẩm của mình mà không phải tốn hàng giờ để:
❌ **Chỉnh sửa ảnh thủ công** trên Photoshop/Canva?
❌ **Tìm kiếm ảnh mô hình/người mẫu phù hợp** trên Unsplash/Pexels?
❌ **Viết mô tả chi tiết** về sản phẩm để AI hiểu đúng?
❌ **Đồng bộ hóa dữ liệu** giữa Google Sheets, Google Drive và các công cụ marketing?

**Workflow này giải quyết tất cả!** Sử dụng **AI multimodal (OpenAI + Gemini)** để tự động **tạo ảnh quảng cáo ấn tượng** từ ảnh sản phẩm và ảnh mô hình, đồng thời **cập nhật tự động** vào Google Drive và Google Sheets.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày**: Không cần chỉnh sửa ảnh thủ công.
- **Ảnh chuyên nghiệp 24/7**: AI tự động tạo ra **ảnh quảng cáo ấn tượng** với phong cách nhất quán.
- **Đồng bộ hóa tự động**: Dữ liệu sản phẩm và ảnh được cập nhật **real-time** vào Google Sheets và Google Drive.
- **Cá nhân hóa cao**: AI phân tích **độ sáng, phong cách, màu sắc** của ảnh mô hình để tạo ra **ảnh quảng cáo phù hợp** với sản phẩm.
- **Hoạt động liên tục**: Workflow chạy **mỗi ngày** theo lịch trình, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Workspace** (Google Drive + Google Sheets) với quyền **quản trị viên** để:
   - Tạo **Google Sheets** chứa danh sách sản phẩm (cột: `Product Name`, `Product Image URL`, `Influencer Image URL`).
   - Tạo **Google Drive folder** để lưu ảnh quảng cáo tự động tạo.
2. **API Key OpenAI** (để phân tích ảnh và tạo mô tả).
3. **API Key OpenRouter** (để sử dụng **Gemini AI** tạo ảnh).
4. **Thời gian định kỳ** (workflow chạy hàng ngày theo lịch trình).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8627](https://n8n.io/workflows/8627) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --name "Automated Product Ad Image Creation"
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **3 phần chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Step 1: Trigger & Chuẩn Bị Dữ Liệu**
- **Schedule Trigger**:
  - Đặt **thời gian chạy hàng ngày** (ví dụ: 8h sáng).
  - **Lưu ý**: Nếu chưa có **Google Sheets** chứa dữ liệu sản phẩm, tạo **mẫu file** như sau:
    | Product Name | Product Image URL | Influencer Image URL | Status |
    |--------------|-------------------|----------------------|--------|
    | Sản phẩm A  | `https://drive.google.com/...` | `https://drive.google.com/...` | Pending |

- **Google Sheets (Get Row)**:
  - Chọn **tab** chứa dữ liệu sản phẩm.
  - **Filter**: Lấy dữ liệu theo **ngày hiện tại** (ví dụ: `=TODAY()`).
  - **Lưu ý**: Cột `Status` phải có giá trị `Pending` để workflow xử lý.

- **Google Drive (Download Product Image & Influencer Image)**:
  - Đảm bảo **credentials `googleDriveOAuth2Api`** đã được cấu hình.
  - **Folder**: Chỉ định **folder cụ thể** trong Google Drive để tải ảnh.

##### **🔹 Step 2: AI Phân Tích & Tạo Ảnh**
- **OpenAI (Analyze Image)**:
  - **API Key**: Điền vào `openAiApi` trong **Credentials**.
  - **Prompt**: AI sẽ phân tích ảnh mô hình để tạo **mô tả chi tiết** (độ sáng, phong cách, màu sắc).
  - **Lưu ý**: Nếu không muốn sử dụng OpenAI, có thể **bỏ qua node này** và sử dụng **Gemini AI** để phân tích.

- **HTTP Request (OpenRouter Gemini)**:
  - **API Key**: Điền vào **OpenRouter** (hoặc sử dụng **Gemini API** của Google).
  - **Prompt mẫu**:
    ```
    Generate a professional ad image combining the product image and influencer image.
    Use the following description from OpenAI analysis: [INSERT_ANALYSIS_HERE].
    Output should be a high-quality image in base64 format.
    ```
  - **Lưu ý**: Nếu không có API Key, **thay thế bằng một node khác** như **MidJourney API** hoặc **DALL·E 3**.

- **Code Node (base64 cleanup)**:
  - **Lưu ý**: Node này **xóa prefix `data:image/...;base64,`** khỏi output của Gemini.
  - **Mã mặc định**:
    ```javascript
    return {
      ...$input.all(),
      base64Image: $input.current().base64Image.replace(/^data:image\/[a-zA-Z]+;base64,/, "")
    };
    ```

##### **🔹 Step 3: Lưu & Cập Nhật**
- **Google Drive (Upload Image)**:
  - **Folder**: Chỉ định **folder lưu ảnh quảng cáo tự động**.
  - **Tên file**: Tự động tạo từ `Product Name + Date` (ví dụ: `Sản phẩm_A_2024-05-20.png`).

- **Google Sheets (Append / Update Row)**:
  - **Cột cập nhật**:
    - `Ad Image URL`: Link Google Drive của ảnh mới tạo.
    - `Status`: Đổi từ `Pending` → `Published`.
  - **Lưu ý**: Nếu muốn **ghi log**, thêm cột `Last Updated` với `=NOW()`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi ảnh quảng cáo tự động vào Slack/Telegram**:
   - Thêm **node `webhook`** để gửi thông báo khi ảnh được tạo.
   - **Mẫu thông báo**:
     ```
     🚀 **New Ad Image Ready!**
     Product: [Product Name]
     Ad Image: [Google Drive Link]
     Status: Published
     ```

2. **Lưu log hoạt động**:
   - Thêm **Google Sheets node** để ghi **lịch sử chạy**, **thời gian xử lý**, và **status lỗi** (nếu có).

3. **Kết hợp với CRM (HubSpot/Zoho)**:
   - Sử dụng **node `HTTP Request`** để cập nhật **mô tả sản phẩm** và **ảnh quảng cáo** vào CRM.

4. **Tối ưu hóa AI với Prompt Engineering**:
   - Thay đổi **prompt** của Gemini để tạo ra **ảnh phù hợp với brand** của doanh nghiệp.
   - Ví dụ:
     ```
     Generate an ad image that matches our brand style (minimalist, vibrant, luxury).
     Use the following color palette: [Insert Hex Codes].
     ```

5. **Chạy workflow theo yêu cầu (không chỉ hàng ngày)**:
   - Thay **Schedule Trigger** bằng **Webhook** để kích hoạt khi có **yêu cầu mới** từ người dùng.
:::

---

### 📌 **Kết Luận: Áp Dụng Ngay & Tiết Kiệm Thời Gian!**
Workflow này **giải phóng các sếp** khỏi công việc **tạo ảnh quảng cáo thủ công**, đồng thời **tăng hiệu quả marketing** với **ảnh chuyên nghiệp, nhất quán và tự động hóa**.

👉 **Bắt đầu ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Google Sheets, Google Drive và API Keys**.
3. **Chạy thử với 1 sản phẩm mẫu**.
4. **Bật Active** và **nhận ảnh quảng cáo tự động mỗi ngày!**

**💡 Mẹo cuối**: Nếu gặp lỗi, kiểm tra **log trong Google Sheets** và **credentials API** (OpenAI/Gemini).

---
**🚀 Cần hỗ trợ kỹ thuật?** Liên hệ với **iTechNotion** (tác giả workflow) qua [website](https://itechnotion.com) hoặc **n8n Community** để tối ưu hóa workflow!