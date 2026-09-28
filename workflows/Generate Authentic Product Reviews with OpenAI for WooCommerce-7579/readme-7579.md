---
title: "🤖 Tự Động Hóa Xây Dựng Đánh Giá Sản Phẩm Tự Nhiên cho WooCommerce với OpenAI (N8N)"
description: "Workflow này tự động tạo đánh giá sản phẩm chân thực, tự nhiên bằng AI và đăng trực tiếp lên cửa hàng WooCommerce của các sếp, tiết kiệm thời gian và nâng cao uy tín thương hiệu. Kết quả: Danh sách sản phẩm được đánh giá tự động, tăng độ tin cậy cho khách hàng."
slug: "tu-dong-hoa-tao-danh-gia-san-pham-woocommerce-openai"
tags: [n8n, automation, woocommerce, ai-content, openai, no-code]
keywords: [n8n workflow woocommerce, tự động hóa đánh giá sản phẩm, tạo nội dung AI cho WooCommerce, tự động hóa bán hàng online, AI viết đánh giá sản phẩm tự nhiên]
---

# 🚀 **Tự Động Hóa Xây Dựng Đánh Giá Sản Phẩm Tự Nhiên cho WooCommerce với OpenAI**

### **Nỗi Đau Của Các Sếp**
Các sếp bán hàng online thường gặp khó khăn khi:
- **Thiếu đánh giá sản phẩm** để tăng độ tin cậy cho khách hàng mới.
- **Tốn thời gian** viết đánh giá thủ công, đặc biệt khi có hàng trăm sản phẩm.
- **Đánh giá không tự nhiên**, gây mất uy tín nếu quá công thức hóa.

Workflow này **giải quyết tất cả** bằng cách tự động tạo **đánh giá sản phẩm chân thực, tự nhiên** bằng AI (OpenAI) và đăng trực tiếp lên WooCommerce. **Không cần code, chỉ cần 10 phút setup!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần viết đánh giá thủ công cho hàng trăm sản phẩm.
✅ **Đánh giá tự nhiên** – AI tạo nội dung giống như khách hàng thực sự đánh giá.
✅ **Tăng uy tín thương hiệu** – Sản phẩm có nhiều đánh giá chân thực, giúp khách hàng tin tưởng hơn.
✅ **Hoạt động tự động** – Chỉ cần kích hoạt workflow 1 lần, nó sẽ chạy liên tục cho tất cả sản phẩm.
✅ **Tối ưu SEO** – Đánh giá sản phẩm giúp cải thiện xếp hạng trên Google.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WooCommerce** với quyền API (để fetch và post dữ liệu).
2. **API Key OpenAI** (để sử dụng GPT-4 hoặc GPT-3.5).
3. **Credentials HTTP Basic Auth** cho WooCommerce (tạo từ Dashboard WooCommerce → API → Add Key).
4. **Tài khoản n8n** (self-hosted hoặc dùng phiên bản cloud miễn phí).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/7579) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7579) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **Node 1: Manual Trigger (Bắt Đầu Workflow)**
- **Tên:** "When clicking ‘Execute workflow’"
- **Lưu ý:** Chỉ cần kích hoạt 1 lần, workflow sẽ tự chạy cho tất cả sản phẩm.

##### **Node 2: Fetch Products from WooCommerce (Lấy Dữ liệu Sản Phẩm)**
- **Type:** `httpRequest`
- **Credentials:** `httpBasicAuth` (đã tạo từ WooCommerce).
- **URL:** `https://[domain].com/wp-json/wc/v3/products` (thay `[domain]` bằng domain của sếp).
- **Query Parameters:**
  ```json
  {
    "per_page": 100,
    "status": "publish"
  }
  ```
- **Lưu ý:** Nếu có nhiều sản phẩm, có thể chia thành nhiều lần fetch với `per_page=100`.

##### **Node 3: Build Product Comment Prompt (Xây Dựng Prompt AI)**
- **Type:** `set`
- **Cấu hình:**
  ```json
  {
    "json": {
      "prompt": "You are a customer who recently bought {{product_name}}. Write a natural and authentic review for this product. Keep it 3-5 sentences long, detailed, and positive. Include specific features and benefits. Avoid generic phrases like 'great product' or 'highly recommended'. Instead, mention things like 'the quality is excellent' or 'the packaging is very sturdy'. Here is the product details:\n\n- Name: {{product_name}}\n- Description: {{product_description}}\n- Price: {{product_price}}\n- Categories: {{product_categories}}\n\nWrite the review in a natural tone as if a real customer wrote it."
    }
  }
  ```
- **Lưu ý:** Thay `{{product_name}}`, `{{product_description}}`, `{{product_price}}`, `{{product_categories}}` bằng dữ liệu từ Node 2.

##### **Node 4: Generate Product Comment (AI) (Tạo Đánh Giá Bằng OpenAI)**
- **Type:** `openAi`
- **Credentials:** `openAiApi` (đã cấu hình API Key OpenAI).
- **Model:** Chọn `gpt-4` (hoặc `gpt-3.5-turbo` nếu tiết kiệm chi phí).
- **Prompt:** Sử dụng dữ liệu từ Node 3.
- **Lưu ý:**
  - Đảm bảo **API Key OpenAI** có đủ credit.
  - Nếu AI trả về kết quả không tốt, có thể điều chỉnh prompt để cụ thể hơn.

##### **Node 5: Extract AI Output (Lọc Kết Quả AI)**
- **Type:** `set`
- **Cấu hình:**
  ```json
  {
    "json": {
      "review": "{{$node["Generate Product Comment (AI)"].json.output.text}}"
    }
  }
  ```
- **Lưu ý:** Đảm bảo kết quả từ OpenAI được trích xuất chính xác.

##### **Node 6: Post Review to Product (Đăng Đánh Giá Lên WooCommerce)**
- **Type:** `httpRequest`
- **Credentials:** `httpBasicAuth` (cùng với Node 2).
- **URL:** `https://[domain].com/wp-json/wc/v3/products/{{product_id}}/comments` (thay `{{product_id}}` bằng ID sản phẩm).
- **Headers:**
  ```json
  {
    "Content-Type": "application/json"
  }
  ```
- **Body (JSON):**
  ```json
  {
    "comment": "{{$node["Extract AI Output"].json.review}}",
    "author": "AI Review Generator",
    "author_email": "noreply@yourdomain.com",
    "status": "approved"
  }
  ```
- **Lưu ý:**
  - Đảm bảo **ID sản phẩm** đúng và **status=approved** để đánh giá hiển thị ngay.
  - Nếu gặp lỗi, kiểm tra **credentials HTTP Basic Auth** và **API Key OpenAI**.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1 sản phẩm mẫu để kiểm tra kết quả.
2. **Bật Active workflow** và chạy để tự động hóa cho tất cả sản phẩm.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram** để thông báo khi workflow hoàn thành:
   - Sử dụng node `slack` hoặc `telegramBot` để gửi tin nhắn khi đánh giá được đăng thành công.

2. **Lưu Log** để theo dõi lỗi:
   - Thêm node `set` để lưu kết quả vào Google Sheets hoặc Notion.

3. **Chạy Định Kỳ** (nếu cần):
   - Sử dụng node `setInterval` để chạy workflow hàng ngày/tuần.

4. **Tùy Chỉnh Prompt** để phù hợp với ngành hàng:
   - Nếu bán **sản phẩm điện tử**, prompt có thể nhấn mạnh về **chất lượng màn hình** hoặc **tính năng AI**.
   - Nếu bán **thời trang**, tập trung vào **thiết kế** và **phong cách**.

5. **Sử Dụng Multiple Models** (nếu có budget):
   - Thay đổi giữa `gpt-4` và `gpt-3.5-turbo` để tối ưu chi phí.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc viết đánh giá sản phẩm thủ công, đồng thời **tăng uy tín thương hiệu** bằng cách tự động tạo nội dung chân thực. **Chỉ cần 10 phút setup**, workflow sẽ hoạt động **24/7**, giúp WooCommerce của các sếp **hấp dẫn khách hàng hơn** và **tăng doanh số**.

**Hãy áp dụng ngay và xem kết quả!** 🚀
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với tác giả [Ali Khosravani](https://n8n.io/workflows/7579) để hỗ trợ.

---
**#TựĐộngHóaWooCommerce #AIContent #N8NWorkflow #TăngDoanhSốOnline**