---
title: "🚀 Tự Động Hóa Dự Báo & Gửi Email Cảnh Báo Hết Hàng Shopify Với GPT-4o (Không Cần Code)"
description: "Workflow tự động hóa hàng ngày dự đoán nguy cơ hết hàng cho sản phẩm Shopify, tính toán tốc độ bán hàng, và gửi email tự động đến nhà cung cấp khi cần tái hàng. Giúp các sếp tiết kiệm thời gian quản lý kho và tránh tình trạng thiếu hàng."
slug: "tự-dộng-hoa-dự-báo-hết-hàng-shopify-gpt-4o"
tags: [n8n, automation, shopify, ai, gpt-4o, ecommerce, crm, no-code, google-sheets, gmail]
keywords: [tự động hóa shopify, dự báo hết hàng, gpt-4o n8n, quản lý kho tự động, email tự động nhà cung cấp, workflow shopify ai]
---

# 🚀 **Tự Động Hóa Dự Báo Hết Hàng Shopify Với GPT-4o & Gửi Email Nhà Cung Cấp**

### **Giải pháp hoàn hảo cho các sếp e-commerce**
Hết hàng là một trong những **nỗi đau lớn nhất** của các cửa hàng Shopify: mất doanh thu, mất khách hàng, và phải chạy đua với thời gian để tái hàng. Thay vì phải kiểm tra thủ công hàng ngày, **chỉ với một workflow tự động hóa**, các sếp có thể:
- **Dự đoán chính xác** ngày hết hàng cho từng sản phẩm dựa trên tốc độ bán hàng thực tế.
- **Tính toán tự động** lượng hàng cần tái mua với buffer an toàn.
- **Gửi email tự động** đến nhà cung cấp khi cần tái hàng, **không cần can thiệp thủ công**.
- **Lưu lịch sử quyết định** trong Google Sheets để theo dõi và phân tích.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần kiểm tra hàng ngày, workflow chạy tự động hàng ngày.
✅ **Dự đoán chính xác**: Sử dụng **GPT-4o** để phân tích nguy cơ hết hàng và lượng hàng cần tái mua.
✅ **Tái hàng kịp thời**: Email tự động gửi đến nhà cung cấp khi cần, **không bỏ lỡ thời điểm tái hàng**.
✅ **Lưu trữ dữ liệu**: Tất cả quyết định tái hàng được **ghi lại trong Google Sheets** để theo dõi.
✅ **Giảm rủi ro thiếu hàng**: Hệ thống cảnh báo trước khi hàng cạn kiệt.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Shopify Store**:
  - Tài khoản Admin với quyền **Custom App**.
  - **API Access Token** (cấp quyền `read_products` và `read_orders`).
- **OpenAI API Key**:
  - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key** cho model **GPT-4o**.
- **Gmail**:
  - Tài khoản Gmail để gửi email tự động (cần **OAuth2**).
  - Danh sách email của nhà cung cấp (điền vào node `Send Reorder Email`).
- **Google Sheets**:
  - Một **Google Sheet** để lưu lịch sử tái hàng (cần **Sheet ID**).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/14143](https://n8n.io/workflows/14143) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Workspace** muốn import và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/14143](https://n8n.io/workflows/14143) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → **Paste JSON** và dán nội dung.
3. Chọn **Workspace** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **10 node** chính, các sếp cần **cấu hình kỹ lưỡng** các node sau:

#### **🔹 Node 1: Daily Inventory Check (ScheduleTrigger)**
- **Thời gian chạy**: Mặc định là **06:00 UTC** (các sếp có thể điều chỉnh theo giờ Việt Nam).
- **Cách chỉnh**:
  - Nhấn **Edit** trên node này.
  - Thay đổi `cron` thành `0 0 6 * * ?` (chạy lúc 6h sáng UTC).
  - **Lưu ý**: Nếu muốn chạy vào giờ Việt Nam (UTC+7), sử dụng `0 0 13 * * ?` (6h sáng UTC = 13h trưa UTC+7).

#### **🔹 Node 2 & 3: Fetch All Products & Fetch Recent Orders (Shopify)**
- **Cấu hình Shopify Credential**:
  - Tạo **new credential** trong n8n với loại **Shopify**.
  - Điền **API Access Token** (lấy từ **Admin → Apps and sales channels → Develop apps**).
  - Chọn **scopes**: `read_products`, `read_orders`.
- **Lưu ý**:
  - Node `Fetch All Products` lấy tất cả sản phẩm và biến thể (variants).
  - Node `Fetch Recent Orders` lấy đơn hàng trong **7 ngày gần nhất**.

#### **🔹 Node 4: Compute Sales Velocity (Code)**
- **Mã JavaScript mặc định**:
  ```javascript
  // Join products and orders, compute velocity (units/day) and days until stockout
  const products = $input.all();
  const orders = $inputItem().json;

  const productsMap = products.reduce((acc, product) => {
    acc[product.id] = product;
    return acc;
  }, {});

  const orderItems = orders.map(order => order.line_items).flat();
  const salesData = orderItems.reduce((acc, item) => {
    const productId = item.variant.id;
    if (productsMap[productId]) {
      const product = productsMap[productId];
      const variantId = item.variant.id;
      const variant = product.variants.find(v => v.id === variantId);

      if (!acc[variantId]) {
        acc[variantId] = {
          inventory_quantity: variant.inventory_quantity,
          units_sold: 0,
          variants: variant
        };
      }
      acc[variantId].units_sold += item.quantity;
    }
    return acc;
  }, {});

  const result = Object.entries(salesData).map(([variantId, data]) => ({
    ...data.variants,
    units_sold: data.units_sold,
    sales_velocity: data.units_sold / 7, // units/day
    days_until_stockout: Math.ceil(data.inventory_quantity / (data.units_sold / 7))
  }));

  return { json: result };
  ```
- **Không cần chỉnh** nếu muốn sử dụng mặc định.

#### **🔹 Node 5: Predict Stockout Risk (Agent) & Node 6: OpenAI — Predict (lmChatOpenAi)**
- **Cấu hình OpenAI Credential**:
  - Tạo **new credential** trong n8n với loại **OpenAI**.
  - Điền **API Key** từ OpenAI.
- **Prompt mặc định** (cần chỉnh để phù hợp):
  ```plaintext
  You are an inventory expert. Analyze the following product data and predict stockout risk:

  - Product ID: {{product.id}}
  - Product Name: {{product.title}}
  - Inventory Quantity: {{product.inventory_quantity}}
  - Units Sold (last 7 days): {{units_sold}}
  - Sales Velocity (units/day): {{sales_velocity}}
  - Days Until Stockout: {{days_until_stockout}}

  Provide a structured response with:
  1. Stockout Risk Level (High/Medium/Low)
  2. Recommended Reorder Quantity (with 20% safety buffer)
  3. Notes (if any)
  ```
- **Lưu ý**:
  - Model mặc định là **GPT-4o** (tốn kém, các sếp có thể thay bằng **GPT-3.5-turbo** để tiết kiệm chi phí).
  - Node **Agent** sẽ gọi API OpenAI và xử lý kết quả.

#### **🔹 Node 7: Stockout Risk Schema (outputParserStructured)**
- **Không cần chỉnh** (n8n tự động phân tích kết quả từ OpenAI).

#### **🔹 Node 8: Should Reorder? (If)**
- **Cấu hình điều kiện**:
  - Mặc định là `should_reorder = true` (nếu AI khuyến nghị tái hàng).
  - Các sếp có thể **thay đổi ngưỡng** (ví dụ: chỉ tái hàng khi `days_until_stockout < 5`).

#### **🔹 Node 9: Send Reorder Email (Gmail)**
- **Cấu hình Gmail Credential**:
  - Tạo **new credential** trong n8n với loại **Gmail OAuth2**.
  - Đăng nhập tài khoản Gmail và cấp quyền.
- **Email mẫu**:
  ```plaintext
  Subject: [ACTION REQUIRED] Reorder Request for {{product.title}} (ID: {{product.id}})

  Dear Supplier,

  This is an automated reorder request for the following product:

  - Product: {{product.title}}
  - Variant: {{product.title}} ({{product.options}})
  - Current Stock: {{product.inventory_quantity}}
  - Units Sold (last 7 days): {{units_sold}}
  - Sales Velocity: {{sales_velocity}} units/day
  - Days Until Stockout: {{days_until_stockout}}

  **Recommended Reorder Quantity:** {{recommended_quantity}} units
  **Stockout Risk Level:** {{stockout_risk_level}}

  Please confirm receipt and delivery time. We appreciate your prompt attention to this matter.

  Best regards,
  [Your Business Name]
  ```
- **Lưu ý**:
  - Thay thế `supplier@example.com` bằng email thực tế của nhà cung cấp.
  - Các sếp có thể **chỉnh sửa email mẫu** trong node này.

#### **🔹 Node 10: Log to Google Sheets (googleSheets)**
- **Cấu hình Google Sheets Credential**:
  - Tạo **new credential** trong n8n với loại **Google Sheets**.
  - Đăng nhập tài khoản Google và cấp quyền.
- **Sheet ID**:
  - Tạo một **Google Sheet mới** và chia sẻ với n8n.
  - Điền **Sheet ID** (tìm trong URL: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/edit`).
- **Cấu trúc dữ liệu**:
  - Các sếp có thể **thay đổi tên cột** trong node này để phù hợp với Sheet.

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử)**:
   - Nhấn **Run Workflow** và chọn **Test Run**.
   - Chọn **Run with sample data** (n8n sẽ tự tạo dữ liệu mẫu).
   - Kiểm tra **log** để đảm bảo workflow chạy đúng.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** trên node **Daily Inventory Check**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp Slack/Telegram để cảnh báo**
- Thêm **node Slack/Telegram Webhook** sau node `Should Reorder?` để gửi thông báo khi có yêu cầu tái hàng.
- **Cách làm**:
  - Tạo **webhook** trên Slack/Telegram.
  - Thêm node **Webhook** và cấu hình URL webhook.
  - Chỉnh node **If** để gửi thông báo khi `should_reorder = true`.

### **2. Lưu log chi tiết vào Google Drive**
- Thay vì chỉ ghi vào Google Sheets, các sếp có thể **ghi log vào Google Drive** với định dạng Excel/PNG.
- **Cách làm**:
  - Thêm node **Google Drive** sau node `Log to Google Sheets`.
  - Chọn **operation: createFile** và cấu hình file mẫu.

### **3. Tự động gửi báo cáo hàng tuần**
- Thêm **node ScheduleTrigger** chạy **tối thứ 7** để tổng hợp báo cáo.
- **Cách làm**:
  - Tạo một workflow mới với node **ScheduleTrigger** (chạy lúc 22:00 UTC).
  - Thêm node **Google Sheets** để ghi báo cáo tổng hợp.
  - Thêm node **Gmail** để gửi báo cáo đến email của các sếp.

### **4. Kết hợp với Zapier/Make (Integromat) để mở rộng**
- Nếu cần **tích hợp thêm dịch vụ** (ví dụ: gửi email qua Mailchimp, cập nhật CRM), các sếp có thể sử dụng **Zapier** hoặc **Make** để kết nối với n8n.

---

## 📌 **Kết luận**
Workflow này **giải quyết hoàn toàn vấn đề hết hàng** cho các cửa hàng Shopify bằng cách:
✔ **Dự đoán chính xác** ngày hết hàng.
✔ **Tái hàng tự động** khi cần.
✔ **Gửi email nhà cung cấp** mà không cần can thiệp thủ công.
✔ **Lưu lịch sử** để theo dõi và phân tích.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình các credential.
2. **Test Run** để đảm bảo hoạt động.
3. **Bật Active** và để workflow chạy tự động hàng ngày!

**Nếu có vấn đề**, các sếp có thể:
- **Tra cứu log** trong n8n Editor.
- **Chỉnh sửa prompt** của GPT-4o để phù hợp với sản phẩm của mình.
- **Mở rộng** bằng cách tích hợp thêm Slack, Telegram hoặc báo cáo tự động.

**Chúc các sếp thành công với việc tự động hóa kho hàng!** 🚀