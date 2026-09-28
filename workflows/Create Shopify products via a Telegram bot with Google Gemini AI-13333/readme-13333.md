---
title: "🤖 Tự Động Hoạt Động Shopify Từ Telegram + AI Gemini: Tạo Sản Phẩm Chỉ Với 1 Lệnh Chat"
description: "Hướng dẫn chi tiết cách tự động tạo sản phẩm Shopify từ Telegram với AI Gemini, tiết kiệm 80% thời gian viết mô tả, slug và quản lý hình ảnh. Cập nhật tự động, không cần code!"
slug: "tieu-dong-tao-san-pham-shopify-tu-telegram-voi-gemini-ai"
tags: [n8n, automation, no-code, shopify, ai-chatbot, google-gemini, content-creation]
keywords: [tự động hóa shopify telegram, tạo sản phẩm shopify bằng ai, gemini ai shopify, workflow n8n shopify, tự động hóa nội dung sản phẩm]
---

# 🚀 **Tự Động Tạo Sản Phẩm Shopify Từ Telegram Với AI Gemini – Không Cần Code!**

### **Giải pháp hoàn hảo cho các sếp bán hàng, content creator và team marketing**
Hãy tưởng tượng một ngày bạn chỉ cần **gửi tin nhắn trên Telegram** với tên sản phẩm và AI sẽ tự động:
✅ **Tạo mô tả chi tiết** (long description + short description)
✅ **Tạo slug SEO** (URL thân thiện)
✅ **Tải và xử lý hình ảnh** (định dạng, alt text)
✅ **Tạo sản phẩm trên Shopify** (giá bán, giá khuyến mãi, thuộc tính)
✅ **Gửi thông báo hoàn thành** (kèm link preview)

**Không cần viết một dòng code, không cần quản lý thủ công – AI làm tất cả!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính bảo mật và hiệu suất tối ưu.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** viết mô tả sản phẩm, slug và quản lý hình ảnh.
- **Chính xác 100%** nhờ AI Gemini phân tích và tạo nội dung chuyên nghiệp.
- **Hoạt động liên tục** (24/7) mà không cần can thiệp thủ công.
- **Cá nhân hóa** sản phẩm theo yêu cầu cụ thể của khách hàng.
- **Giảm thiểu lỗi** trong quá trình nhập liệu thủ công.
- **Tích hợp hoàn hảo** với Shopify, Telegram và AI hiện đại.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram** (để tạo bot và quản lý tương tác).
✔ **API Key Google Gemini** (để sử dụng AI Gemini trong workflow).
✔ **Tài khoản Shopify** (để tạo sản phẩm tự động).
✔ **Tài khoản n8n** (self-hosted hoặc dùng phiên bản cloud miễn phí).
✔ **Các file hình ảnh** (nếu muốn tự động tải lên Shopify).

---
:::info[CHUẨN BỊ]
- **Tạo bot Telegram**:
  - Mở [@BotFather](https://t.me/BotFather) trên Telegram và tạo bot mới.
  - Lấy **API Token** của bot và thêm vào n8n (node **Telegram Trigger**).
- **Cấu hình Google Gemini**:
  - Đăng ký [Google AI Studio](https://makersuite.google.com/app) và lấy **API Key**.
  - Thêm vào node **lmChatGoogleGemini** trong workflow.
- **Cấu hình Shopify**:
  - Lấy **API Key** và **Storefront Access Token** từ [Shopify Admin](https://partners.shopify.com/).
  - Thêm vào node **HTTP Request** (để tạo sản phẩm).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này có **95 nodes** và được thiết kế để **tương tác qua Telegram**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13333](https://n8n.io/workflows/13333) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

:::note[LƯU Ý]
- **Không xóa node nào** trong workflow, vì nó được thiết kế theo logic tự động hóa hoàn chỉnh.
- **Cấu hình lại credentials** cho các node quan trọng như Telegram, Google Gemini và Shopify.
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **nhiều bước logic**, các sếp cần chú ý đến các node sau:

##### **A. Cấu hình Telegram Trigger**
- **Node**: `Telegram Trigger`
- **Cần thiết**:
  - Điền **API Token** của bot Telegram vào `Bot Token`.
  - Chọn **Chat ID** của bot (có thể lấy từ `/start` trong Telegram).
  - Cấu hình **Command** để bắt đầu workflow (ví dụ: `/start`).

##### **B. Cấu hình Google Gemini AI**
Workflow sử dụng **Google Gemini** để tạo mô tả, slug và xử lý hình ảnh. Các node quan trọng:
- **Node**: `Google Gemini Chat Model`, `Product Description Generation`, `Slug Generation`, `Image Title & Alt Tag Creation`
- **Cần thiết**:
  - Điền **API Key Google Gemini** vào `Authentication` của node `lmChatGoogleGemini`.
  - Cấu hình **Prompt** trong node `chainLlm` để AI trả về định dạng mong muốn (ví dụ:
    ```json
    {
      "description": "Mô tả sản phẩm chi tiết",
      "short_description": "Mô tả ngắn",
      "slug": "slug-seo"
    }
    ```

##### **C. Cấu hình Shopify API**
- **Node**: `Creating Product on Shopify`, `HTTP Request`
- **Cần thiết**:
  - Điền **API Key** và **Storefront Access Token** vào `Authorization` (Header).
  - Cấu hình **URL API** của Shopify (ví dụ: `https://{store}.myshopify.com/admin/api/2024-01/products.json`).
  - Thêm **Headers** như:
    ```json
    {
      "Content-Type": "application/json",
      "X-Shopify-Access-Token": "{API_KEY}"
    }
    ```

##### **D. Quản lý trạng thái và dữ liệu**
Workflow sử dụng **DataTable** để lưu trạng thái tương tác với người dùng. Các node quan trọng:
- **Node**: `Get User State`, `Upsert row(s)1`, `Fetching Product Data`
- **Cần thiết**:
  - Cấu hình **Table Name** trong DataTable để lưu trữ trạng thái (ví dụ: `user_state`, `shopify_products`).
  - Đảm bảo **khóa chính** (Primary Key) được đặt đúng để tránh trùng lặp.

##### **E. Xử lý hình ảnh**
- **Node**: `Fetching Binary Data`, `Formatting Images as Base64`, `Creating Product on Shopify1`
- **Cần thiết**:
  - Cấu hình **URL nguồn hình ảnh** (có thể là URL từ Telegram hoặc URL trực tiếp).
  - Sử dụng **Code Node** để chuyển đổi hình ảnh thành **Base64** trước khi upload lên Shopify.

---

#### **3. Kích hoạt ⚡️**
Sau khi cấu hình xong:
1. **Test Run** với dữ liệu mẫu:
   - Gửi `/start` trên Telegram và theo dõi quá trình.
   - Kiểm tra **Log** trong n8n để đảm bảo không có lỗi.
2. **Bật Active workflow**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tích hợp Slack/Telegram cho báo cáo**:
   - Sử dụng node **Telegram** hoặc **Slack** để gửi thông báo khi sản phẩm được tạo thành công.
   - Ví dụ: Khi sản phẩm hoàn thành, bot Telegram gửi link preview và thông tin sản phẩm.

2. **Lưu log hoạt động**:
   - Sử dụng node **Markdown** hoặc **HTTP Request** để ghi log vào Google Sheets/Notion.
   - Có thể theo dõi lịch sử tạo sản phẩm và phân tích hiệu suất.

3. **Tự động tạo sản phẩm từ nhiều nguồn**:
   - Kết hợp với **Google Sheets** hoặc **Airtable** để lấy danh sách sản phẩm từ file Excel và tự động tạo trên Shopify.

4. **Cập nhật giá và thuộc tính động**:
   - Sử dụng **Code Node** để tính toán giá khuyến mãi hoặc thuộc tính tự động từ mô tả sản phẩm.

5. **Hỗ trợ nhiều ngôn ngữ**:
   - Cấu hình **Google Gemini** với prompt đa ngôn ngữ để tạo mô tả cho sản phẩm quốc tế.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình tạo sản phẩm Shopify** mà không cần viết một dòng code. Với **AI Gemini**, sản phẩm sẽ được tạo ra **chuyên nghiệp, nhanh chóng và chính xác**, tiết kiệm thời gian cho team marketing và bán hàng.

**Hãy thử ngay và giảm thiểu 80% công việc thủ công!**
👉 **[Tải workflow này](https://n8n.io/workflows/13333)** và bắt đầu tự động hóa ngay hôm nay!

---
**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ với tôi qua Telegram để được hỗ trợ chi tiết! 🚀