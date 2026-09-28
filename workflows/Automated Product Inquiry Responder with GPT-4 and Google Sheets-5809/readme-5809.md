---
title: "🤖 **Tự Động Hóa Trả Lời Hỏi Đáp Sản Phẩm Bằng GPT-4 + Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa trả lời các câu hỏi về sản phẩm từ khách hàng bằng trí tuệ nhân tạo GPT-4, kết hợp với cơ sở dữ liệu Google Sheets. Giúp doanh nghiệp tiết kiệm thời gian hỗ trợ, giảm tải cho bộ phận chăm sóc khách hàng và cung cấp phản hồi chính xác 24/7."
slug: "tieu-dong-hoa-tra-loi-hoi-dap-san-pham-gpt4-google-sheets"
tags: [n8n, automation, AI chatbot, support chatbot, google sheets, openai, gpt-4]
keywords: [n8n workflow tự động hóa, trả lời hỏi đáp sản phẩm bằng AI, tự động hóa hỗ trợ khách hàng, gpt-4 n8n, google sheets api, chatbot không code]
---

# 🚀 **Tự Động Hóa Trả Lời Hỏi Đáp Sản phẩm Bằng GPT-4 + Google Sheets**

### **Giải pháp cho doanh nghiệp bị "ngập" câu hỏi về sản phẩm?**
Hàng ngày, bộ phận hỗ trợ khách hàng của các sếp phải mất nhiều thời gian để trả lời các câu hỏi như:
- *"Sản phẩm này có size nào khác không?"*
- *"Giá của model này bao nhiêu?"*
- *"Sản phẩm này có phù hợp với nhu cầu của tôi không?"*

Với **Automated Product Inquiry Responder**, các sếp có thể **tự động hóa 100% quá trình trả lời** bằng trí tuệ nhân tạo GPT-4, kết hợp với cơ sở dữ liệu sản phẩm trên Google Sheets. Khách hàng sẽ nhận được **phản hồi nhanh chóng, chính xác và thân thiện**, trong khi các sếp tiết kiệm **giờ làm việc quý giá** cho những công việc có giá trị hơn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian hỗ trợ khách hàng**: Giảm tải cho bộ phận chăm sóc, tự động trả lời **ngay lập tức** (thời gian phản hồi < 5 giây).
✅ **Trả lời chính xác và cá nhân hóa**: GPT-4 phân tích yêu cầu khách hàng và **lấy dữ liệu từ Google Sheets** để trả lời chi tiết.
✅ **Hoạt động 24/7**: Không cần nhân viên trực ca, hệ thống hoạt động **mọi lúc mọi nơi**.
✅ **Giảm chi phí vận hành**: Không cần tuyển thêm nhân viên hỗ trợ, tiết kiệm ngân sách.
✅ **Cải thiện trải nghiệm khách hàng**: Phản hồi nhanh chóng và **mang tính chuyên nghiệp**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản n8n** (self-hosted hoặc n8n.cloud).
- **API Key OpenAI** (để sử dụng GPT-4 và GPT-3.5-Turbo).
- **Tài khoản Google Cloud** (để kết nối với Google Sheets).
- **Google Sheet chứa danh sách sản phẩm** (cấu trúc bao gồm: **Brand, Model, Size, Price, Description, etc.**).
- **URL Webhook** (để nhận các yêu cầu từ khách hàng).

---
:::info[CHUẨN BỊ]
**Cấu trúc Google Sheet cần có:**
| Brand  | Model       | Size | Price | Description          |
|--------|-------------|------|-------|----------------------|
| Nike   | Air Max 90  | 42   | 1.2M  | Giày thể thao cao cấp |
| Adidas | Ultraboost  | 41   | 1.5M  | Giày chạy bộ siêu nhẹ |

**Lưu ý:** Các cột phải có tên **khớp với logic trong node "Filter Products"** (xem phần hướng dẫn dưới đây).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor.

**Bước 1:** Tải file JSON từ [n8n.io/workflows/5809](https://n8n.io/workflows/5809).
**Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON → Nhấn **"Import"**.

**Hoặc:**
- Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5809) (ấn **Export** trên trang workflow).
- Paste vào **n8n Editor** → Nhấn **"Import"**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **A. Cấu hình Credentials**
Các sếp cần **thiết lập credentials** cho các node quan trọng:

| **Node**               | **Credentials cần thiết**          | **Hướng dẫn cấu hình**                                                                 |
|------------------------|-------------------------------------|----------------------------------------------------------------------------------------|
| **OpenAI Chat Model**  | `openAiApi`                         | - Đăng nhập vào [OpenAI API](https://platform.openai.com/account/api-keys).             |
|                        |                                     | - Tạo **API Key** và copy vào **n8n Credentials** (Settings → Credentials → Add → OpenAI). |
| **Google Sheets**      | `googleSheetsOAuth2Api`            | - Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/).             |
|                        |                                     | - Tạo **OAuth 2.0 Client ID** và kết nối với Google Sheet.                            |
| **Webhook**           | -                                   | - Chọn **HTTP Method: POST** và **Path: /shoe-orders**.                                |

##### **B. Cấu hình Node "Product Database" (Google Sheets)**
- **Sheet Name:** Điền tên **exact** của Google Sheet chứa sản phẩm (không dấu cách).
- **Range:** Điền **tên sheet + phạm vi dữ liệu** (ví dụ: `Sheet1!A1:E100`).
- **Headers:** Chọn **"Yes"** nếu sheet có tiêu đề (Brand, Model, Size, etc.).

##### **C. Cấu hình Node "Filter Products" (Code)**
Node này **lọc sản phẩm** dựa trên yêu cầu của khách hàng. Các sếp cần **chỉnh sửa logic** trong **Custom JavaScript** như sau:

```javascript
// Kiểm tra nếu có dữ liệu từ Google Sheets
if (!$input.all().length) {
    return { json: { error: "No products found in database." } };
}

// Lấy dữ liệu từ Google Sheets
const products = $input.all();

// Lấy thông tin từ yêu cầu khách hàng (đã được Parse Request AI xử lý)
const customerRequest = $input.previous().json;

// Ví dụ: Lọc sản phẩm theo Brand và Size
const filteredProducts = products.filter(product =>
    product.Brand.toLowerCase().includes(customerRequest.brand.toLowerCase()) &&
    product.Size === customerRequest.size
);

return { json: { products: filteredProducts } };
```

**Lưu ý:**
- Các sếp cần **điều chỉnh logic lọc** theo cấu trúc **Google Sheet** của mình.
- Nếu khách hàng không nhập **Brand hoặc Size**, hệ thống sẽ trả lời **"Không tìm thấy sản phẩm phù hợp"**.

##### **D. Cấu hình Node "AI Manager" (ChainLLM)**
Node này **tạo phản hồi tự động** cho khách hàng. Các sếp có thể **cập nhật Prompt** để phù hợp với **ngôn ngữ và tone** của doanh nghiệp.

**Prompt mẫu:**
```plaintext
Bạn là một trợ lý hỗ trợ khách hàng chuyên nghiệp của [Tên Doanh Nghiệp].
Hãy trả lời khách hàng một cách ** thân thiện, chuyên nghiệp và chi tiết** dựa trên thông tin sau:

- **Yêu cầu của khách hàng:** {{customerRequest}}
- **Danh sách sản phẩm phù hợp:** {{products}}

**Yêu cầu:**
1. Nếu có sản phẩm phù hợp, hãy liệt kê chi tiết (Brand, Model, Size, Price, Description).
2. Nếu không có sản phẩm, hãy đề xuất các sản phẩm tương tự hoặc giải thích lý do.
3. Kết thúc bằng câu hỏi: "Nếu có thắc mắc khác, hãy để lại tin nhắn nhé!"

**Tránh:**
- Trả lời quá ngắn gọn.
- Sử dụng từ ngữ không chuyên nghiệp.
```

---

#### **3. Kích hoạt ⚡️**
**Bước 1: Test Run với dữ liệu mẫu**
- Gửi một **yêu cầu mẫu** đến Webhook (ví dụ: `POST /shoe-orders` với body JSON):
  ```json
  {
    "brand": "Nike",
    "size": "42",
    "question": "Giày Air Max 90 size 42 có còn hàng không?"
  }
  ```
- Kiểm tra **Output** của node **"Send Response"** để đảm bảo phản hồi đúng định dạng.

**Bước 2: Bật Active Workflow**
- Nhấn **"Active"** trên workflow → **"Save"**.

---
### ✍️ **Mẹo & gợi ý nâng cao**

#### **1. Kết nối với Slack/Telegram để nhận thông báo**
Các sếp có thể **thêm node Slack/Telegram** để:
- **Nhận thông báo** khi có yêu cầu mới.
- **Gửi phản hồi** cho khách hàng qua kênh chat.

**Cách làm:**
- Thêm **node Slack** (n8n-nodes-base.slack) sau node **"Send Response"**.
- Cấu hình **Webhook URL** từ Slack và **điền vào Credentials**.

#### **2. Lưu log tất cả các yêu cầu**
Để **theo dõi và phân tích** hiệu suất, các sếp có thể:
- Thêm **node Google Sheets** sau **"Send Response"** để **lưu log** (thời gian, yêu cầu, phản hồi).
- Sử dụng **node Email** (n8n-nodes-base.email) để **gửi báo cáo hàng ngày** cho quản lý.

#### **3. Cập nhật cơ sở dữ liệu sản phẩm tự động**
Nếu sản phẩm thường xuyên thay đổi, các sếp có thể:
- **Kết nối với ERP/CRM** (Shopify, WooCommerce) để **cập nhật Google Sheets tự động**.
- Sử dụng **node HTTP Request** để gọi API từ hệ thống quản lý sản phẩm.

#### **4. Sử dụng GPT-4 cho phản hồi phức tạp**
Nếu khách hàng đặt **câu hỏi phức tạp** (ví dụ: *"Sản phẩm này phù hợp với ai?"*), các sếp có thể:
- **Tăng cường Prompt** trong node **"AI Manager"** để GPT-4 **phân tích sâu hơn**.
- Thêm **node Code** để **xử lý logic đặc biệt** (ví dụ: so sánh sản phẩm).

---
### 📌 **Kết luận**
**Automated Product Inquiry Responder** là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa 100% quá trình trả lời hỏi đáp sản phẩm**.
✔ **Giảm tải cho bộ phận hỗ trợ**, tiết kiệm **thời gian và chi phí**.
✔ **Cung cấp trải nghiệm khách hàng chuyên nghiệp**, ngay cả khi doanh nghiệp hoạt động **24/7**.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** (OpenAI + Google Sheets).
3. **Test với dữ liệu mẫu** và **bật Active**.
4. **Kết nối với Slack/Telegram** để quản lý dễ dàng hơn.

**Không cần là dev, không cần code – chỉ cần n8n!** 🚀

---
**Bạn có thắc mắc về workflow này?** Để lại comment bên dưới hoặc liên hệ với tôi qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 💪