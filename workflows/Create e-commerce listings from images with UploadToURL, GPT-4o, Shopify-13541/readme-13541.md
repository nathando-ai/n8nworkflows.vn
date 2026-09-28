---
title: "🚀 Tự Động Hóa Tạo Danh Sách Hàng Hóa E-Commerce Từ Ảnh: Từ UploadToURL → GPT-4o → Shopify/WooCommerce (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn chuyển đổi ảnh sản phẩm thành danh sách bán hàng trên Shopify/WooCommerce chỉ với 1 cú nhấp chuột. Giải phóng thời gian của các sếp khỏi công việc nhập liệu thủ công, tối ưu hóa SEO và tăng tốc độ ra mắt sản phẩm lên 100x."
slug: "tieu-dong-hoa-tao-danh-sach-hang-hoa-e-commerce-tu-anh"
tags: [n8n, automation, e-commerce, ai-multimodal, shopify, woocommerce, gpt-4o, uploadtourl]
keywords: [n8n workflow e-commerce, tự động hóa sản phẩm Shopify, tạo danh sách hàng hóa tự động, GPT-4o Vision cho e-commerce, UploadToURL API, tự động hóa bán hàng online]
---

# 🚀 **Tự Động Hóa Tạo Danh Sách Hàng Hóa E-Commerce Từ Ảnh: Giải Pháp "Upload → AI → Bán" Cho Các Sếp**

### **Nỗi Đau Của Các Sếp Trong E-Commerce**
Các sếp đang mất **từ 2-5 giờ/ngày** để:
- **Upload** ảnh sản phẩm lên hosting và chờ CDN xử lý.
- **Nhập liệu thủ công** tiêu đề, mô tả, thuộc tính (SKU, giá, danh mục) vào Shopify/WooCommerce.
- **Chỉnh sửa SEO** bằng tay, dẫn đến nội dung không đồng nhất và mất thời gian tối ưu.
- **Quên kiểm tra** tính nhất quán giữa ảnh và mô tả, gây mất uy tín cho khách hàng.

**Kết quả?** Sản phẩm ra mắt chậm, chi phí nhân sự cao, và trải nghiệm khách hàng không đồng nhất.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** nhập liệu thủ công (từ 5 giờ/tháng xuống còn 1 giờ).
✅ **Tạo danh sách sản phẩm hoàn chỉnh** chỉ với **1 ảnh + metadata** (SKU, giá, danh mục).
✅ **Nội dung SEO tự động** được GPT-4o Vision phân tích từ ảnh, bao gồm:
   - Tiêu đề hấp dẫn.
   - Mô tả chi tiết với 5 điểm nổi bật.
   - Tags và danh mục phù hợp.
   - URL slug tự động từ AI.
✅ **Hoạt động 24/7** trên VPS, không cần can thiệp của con người.
✅ **Hoàn toàn cá nhân hóa** cho từng sản phẩm, không giống nhau như nhập liệu thủ công.
✅ **Kết nối đa nền tảng**: Shopify **và** WooCommerce trong cùng một workflow.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                          | **Lưu Ý**                                  |
|----------------------|--------------------------------------------------|---------------------------------------------|
| **n8n Self-Hosted**  | VPS với Node.js (cài đặt n8n Community Edition)  | 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm **VPSN8N**) |
| **UploadToURL**      | API Key (tạo từ [uploadtourl.com](https://uploadtourl.com/)) | Node **n8n-nodes-uploadtourl** phải được cài đặt |
| **OpenAI (GPT-4o)**  | API Key (tạo từ [platform.openai.com](https://platform.openai.com/)) | Chọn mô hình **gpt-4o** cho Vision AI        |
| **Shopify**          | API Key + Password (tạo từ [Shopify Admin](https://shopify.com/)) | Cần quyền **Store Owner**                 |
| **WooCommerce**      | Username + Password (tạo từ [WooCommerce REST API](https://woocommerce.com/document/woocommerce-rest-api/)) | Cần quyền **Admin** |
| **Slack (Tùy Chọn)** | Token OAuth 2.0 (tạo từ [api.slack.com](https://api.slack.com/)) | Để thông báo tự động cho team          |

#### **2. Tham Số Cần Điền**
- **DEFAULT_PLATFORM**: Đặt giá trị là `shopify` hoặc `woocommerce` (hoặc cả hai).
- **Variable trong Workflow**:
  - `publishImmediately`: `true` (nếu muốn sản phẩm xuất bản ngay) hoặc `false` (draft).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/13541) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.

**Bước 2:** Nhấn **Import Workflow** và chọn file JSON đã tải.

```json
// Dữ liệu JSON của workflow (sử dụng để import)
{
  "nodes": [
    {
      "parameters": {
        "path": "product-catalog-upload",
        "httpMethod": "POST"
      },
      "name": "Webhook - Receive Product",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1
    },
    // ... (các node khác sẽ được mô tả chi tiết dưới đây)
  ],
  "connections": {
    // ... (các kết nối giữa nodes)
  }
}
```

**Lưu ý:** Nếu copy/paste JSON, **không bỏ qua dấu phẩy** giữa các node!

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Credentials**
| **Node**                     | **Tham Số Cần Điền**                          | **Lưu Ý**                                  |
|------------------------------|-----------------------------------------------|---------------------------------------------|
| **UploadToURL**              | Credential: `uploadToUrlApi`                   | Điền API Key từ [UploadToURL](https://uploadtourl.com/) |
| **OpenAI (GPT-4o)**          | Credential: `openAiApi`                        | Chọn mô hình **gpt-4o** và điền API Key    |
| **Shopify**                  | Credential: `shopifyApi`                      | Điền API Key + Password từ Shopify Admin    |
| **WooCommerce**              | Credential: `httpBasicAuth`                    | Điền Username + Password từ WooCommerce    |
| **Slack (Tùy Chọn)**         | Credential: `slackOAuth2Api`                  | Điền Token OAuth 2.0 từ Slack              |

##### **B. Cấu Hình Node Quan Trọng**
1. **Webhook - Receive Product**:
   - Đảm bảo **path** là `product-catalog-upload` và **HTTP Method** là `POST`.
   - **Expected Data Format**:
     ```json
     {
       "filename": "string",  // Tên file ảnh (ví dụ: "sneakers-red.jpg")
       "fileUrl": "string",   // URL ảnh (nếu upload từ URL)
       "file": "base64",      // Binary file (nếu upload trực tiếp)
       "sku": "string",       // SKU sản phẩm (sẽ được sanitize)
       "price": 99.99,        // Giá sản phẩm
       "platform": "shopify"  // hoặc "woocommerce"
     }
     ```

2. **GPT-4o Vision - Analyse Product**:
   - **Prompt Template** (được sử dụng trong node Code trước đó):
     ```plaintext
     Analyze the product image at {imageUrl} and generate:
     1. A compelling product title (max 60 chars).
     2. A detailed SEO description (3-4 sentences).
     3. 5 key features as bullet points.
     4. Suggested product category.
     5. Relevant tags (array of 3-5 words).
     6. A short marketing blurb (100 words).
     Return JSON with keys: title, description, features, category, tags, blurb.
     ```

3. **Route by Platform (Switch Node)**:
   - **Case 1**: `{{ $node["Validate & Enrich Payload"].json["platform"] }} == "shopify"`
   - **Case 2**: `{{ $node["Validate & Enrich Payload"].json["platform"] }} == "woocommerce"`

4. **Shopify - Create Product**:
   - **Resource**: `product`
   - **Body Template** (sử dụng trong node Code trước đó):
     ```json
     {
       "title": "{{ $node["Parse & Merge AI Product Data"].json["title"] }}",
       "body_html": "{{ $node["Parse & Merge AI Product Data"].json["description"] }}",
       "images": [
         {
           "src": "{{ $node["Extract Image URL"].json["url"] }}"
         }
       ],
       "status": "{{ $node["Validate & Enrich Payload"].json["publishImmediately"] ? "active" : "draft" }}",
       "variants": [
         {
           "option1": "{{ $node["Validate & Enrich Payload"].json["sku"] }}",
           "price": "{{ $node["Validate & Enrich Payload"].json["price"] }}",
           "inventory_quantity": 1
         }
       ],
       "tags": "{{ $node["Parse & Merge AI Product Data"].json["tags"].join(',') }}"
     }
     ```

5. **WooCommerce - Create Product**:
   - **HTTP Method**: `POST`
   - **URL**: `https://{your-woocommerce-site}/wp-json/wc/v3/products`
   - **Headers**:
     ```
     Content-Type: application/json
     Authorization: Basic {base64(username:password)}
     ```
   - **Body Template**:
     ```json
     {
       "name": "{{ $node["Parse & Merge AI Product Data"].json["title"] }}",
       "description": "{{ $node["Parse & Merge AI Product Data"].json["description"] }}",
       "short_description": "{{ $node["Parse & Merge AI Product Data"].json["blurb"] }}",
       "regular_price": "{{ $node["Validate & Enrich Payload"].json["price"] }}",
       "sku": "{{ $node["Validate & Enrich Payload"].json["sku"] }}",
       "images": [
         {
           "src": "{{ $node["Extract Image URL"].json["url"] }}"
         }
       ],
       "tags": "{{ $node["Parse & Merge AI Product Data"].json["tags"].join(',') }}"
     }
     ```

---

#### **3. Kích Hoạt Workflow ⚡️**
**Bước 1:** Nhấn **Test Run** với dữ liệu mẫu:
```json
{
  "filename": "sneakers-premium.jpg",
  "file": "base64_image_data...",  // hoặc
  "fileUrl": "https://example.com/sneakers.jpg",
  "sku": "SNK-2024-PREMIUM",
  "price": 199.99,
  "platform": "shopify"
}
```

**Bước 2:** Kiểm tra:
- Ảnh được upload thành công lên UploadToURL.
- GPT-4o phân tích ảnh và tạo nội dung.
- Sản phẩm được tạo trên Shopify/WooCommerce.
- (Nếu cấu hình Slack) Thông báo tự động được gửi.

**Bước 3:** Nhấn **Active** để workflow chạy liên tục.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Mobile App**:
   - Sử dụng **Webhook Response** để gửi dữ liệu sản phẩm về app di động của các sếp (ví dụ: SKU, URL sản phẩm, trạng thái).
   - **Cách làm**: Trong node **Build Product Response**, thêm trường `appData` chứa thông tin cần thiết.

2. **Lưu Log Tự Động**:
   - Thêm node **n8n-nodes-base.googleSheets** để ghi lại lịch sử tạo sản phẩm.
   - **Cấu hình**:
     - Sheet Name: `Product_Catalog_Log`
     - Columns: `ProductID`, `Title`, `Platform`, `CreatedAt`, `Status`

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n-nodes-base.email** để gửi báo cáo hàng tuần về số lượng sản phẩm tạo thành công.
   - **Template Email**:
     ```
     Chào các sếp,

     Tính đến ngày {{ $node["Current Date"].json["date"] }}, workflow đã tự động tạo {{ $node["Count Products"].json["total"] }} sản phẩm trên {{ $node["Count Products"].json["platforms"] }}.

     Chi tiết:
     - Shopify: {{ $node["Count Products"].json["shopify"] }} sản phẩm
     - WooCommerce: {{ $node["Count Products"].json["woocommerce"] }} sản phẩm

     Trân trọng,
     Team Automation
     ```

4. **Cải Thiện Hình Ảnh Trước Khi Upload**:
   - Thêm node **n8n-nodes-base.image** để resize ảnh trước khi upload (ví dụ: từ 2000x2000 xuống 800x800).
   - **Cài đặt**:
     - Width: `800`
     - Height: `800`
     - Quality: `85`

5. **Xử Lý Lỗi Hiệu Quả**:
   - Thêm node **n8n-nodes-base.set** để lưu trạng thái lỗi vào biến `errorDetails`.
   - Sau đó, gửi thông báo lỗi đến Slack với chi tiết:
     ```
     ❌ Lỗi khi tạo sản phẩm {{ $node["Validate & Enrich Payload"].json["sku"] }}:
     - Lỗi: {{ $node["Error"].json["message"] }}
     - Ảnh: {{ $node["Extract Image URL"].json["url"] }}
     ```

---
### **📌 Kết Luận: Hãy Tự Động Hóa Ngay Hôm Nay!**
Workflow này **giải phóng các sếp khỏi công việc nhập liệu thủ công**, đồng thời **tối ưu hóa SEO và tăng tốc độ ra mắt sản phẩm**. Với chi phí thấp (chỉ cần 1 VPS và các API miễn phí/low-cost), các sếp sẽ:
✔ **Tiết kiệm hàng giờ/ngày** cho công việc sáng tạo.
✔ **Giảm thiểu sai sót** do nhập liệu bằng tay.
✔ **Cung cấp trải nghiệm khách hàng đồng nhất** trên tất cả kênh bán hàng.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (👉 [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã **VPSN8N**).
2. **Import workflow** và cấu hình credentials.
3. **Test run** với 1-2 sản phẩm mẫu.
4. **Active workflow** và bắt đầu tự động hóa!

**N