---
title: "🚀 Tự Động Hoàn Thành Báo Cáo Sản Phẩm Keyboard Amazon Với AI + Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa 100% scrape dữ liệu sản phẩm keyboard từ Amazon, tổng hợp thông tin chi tiết bằng AI, và lưu trữ vào Google Sheets để phân tích thị trường. Giúp các sếp tiết kiệm 10+ giờ/tháng so sánh sản phẩm thủ công."
slug: "tieu-dong-hoan-thanh-bao-cao-keyboard-amazon-ai-google-sheets"
tags: [n8n, automation, market-research, ai-summarization, scrape-data, google-sheets]
keywords: [tự động hóa scrape amazon, n8n workflow market research, scrape sản phẩm amazon, google sheets tự động hóa, ai tổng hợp dữ liệu]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Sản Phẩm Keyboard Amazon Với AI + Google Sheets**

### **Giải pháp cho các sếp:**
Bạn đã bao giờ phải mất **3-5 tiếng** mỗi tuần để:
- Tìm kiếm và so sánh hàng trăm sản phẩm keyboard trên Amazon?
- Lọc ra thông tin quan trọng như **giá, đánh giá, mô tả, và đặc điểm kỹ thuật**?
- Lưu trữ dữ liệu vào Excel để phân tích sau?

**Workflow này tự động hóa toàn bộ quá trình** bằng cách:
✅ **Scrape** dữ liệu sản phẩm từ Amazon (không cần API chính thức)
✅ **Tổng hợp** thông tin bằng AI (ScrapeGraphAI) với **ngôn ngữ tự nhiên**
✅ **Lưu trữ** vào Google Sheets với **cấu trúc chuẩn** cho phân tích
✅ **Chạy tự động** hàng ngày/tuần theo lịch trình

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần thủ công scrape và nhập liệu.
- **Dữ liệu chính xác & toàn diện**: AI tự động trích xuất **tên sản phẩm, liên kết, danh mục, mô tả, giá, đánh giá** từ trang Amazon.
- **Cập nhật liên tục**: Dữ liệu tự động sync hàng ngày/ngày để theo dõi xu hướng thị trường.
- **Sẵn sàng phân tích**: Dữ liệu được lưu vào Google Sheets với **cấu trúc chuẩn**, dễ dàng export và sử dụng với **Google Data Studio** hoặc **Excel**.
- **Không cần code**: Cài đặt và chạy chỉ với **n8n Self-hosted** và một số API key.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (không dùng n8n.cloud vì node ScrapeGraphAI chỉ hỗ trợ self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **API Key ScrapeGraphAI**:
   - Đăng ký tại [ScrapeGraphAI](https://scrapegraph.ai/) và lấy **API Key**.
   - Thêm credential trong n8n: **Settings → Credentials → Add → ScrapeGraphAI API**.

3. **Tài khoản Google OAuth2**:
   - Tạo **Google Cloud Project** và kích hoạt **Google Sheets API**.
   - Thêm credential trong n8n: **Settings → Credentials → Add → Google Sheets OAuth2 API**.

4. **Google Sheets mới**:
   - Tạo một **Google Sheet mới** để lưu dữ liệu (ví dụ: `Báo cáo Keyboard Amazon`).
   - **Lưu ý**: Sheet này sẽ được **append** dữ liệu mỗi lần chạy workflow.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6394) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **🕒 Node 1: Automated Schedule Trigger (Lịch trình tự động)**
- **Cấu hình**:
  - **Frequency**: Chọn **Daily** (hoặc Weekly tùy nhu cầu).
  - **Time Zone**: Chọn **Asia/Ho Chi Minh** (hoặc khu vực phù hợp).
  - **Execution Time**: Giờ thích hợp (ví dụ: **7h sáng** để tránh peak traffic Amazon).
- **Lưu ý**:
  - **Không nên chạy quá thường** (ví dụ: hàng giờ) để tránh bị Amazon chặn IP.
  - **Monitor logs** trong n8n để kiểm tra lỗi.

##### **🤖 Node 2: AI-Powered Amazon Product Scraper (ScrapeGraphAI)**
- **Cấu hình**:
  - **Website URL**: Điền **liên kết Amazon search** cho keyboard (ví dụ: `https://www.amazon.com/s?k=keyboard`).
  - **User Prompt**: Sử dụng **ngôn ngữ tự nhiên** để AI biết trích xuất gì:
    ```
    Extract product titles, URLs, categories, prices, ratings, and descriptions from Amazon keyboard search results.
    ```
  - **API Credentials**: Chọn **scrapegraphAIApi** (credential đã thêm trước đó).
- **Lưu ý**:
  - **ScrapeGraphAI là node community**, nên **self-hosted** là bắt buộc.
  - Nếu dữ liệu không đầy đủ, **cập nhật User Prompt** để AI hiểu rõ hơn.

##### **🧱 Node 3: Data Formatting and Processing (Code)**
- **Nội dung code mặc định** đã chuẩn bị để trích xuất:
  ```javascript
  // Extract products array from ScrapeGraphAI response
  const products = $input.all().map(item => {
    return {
      title: item.data.title || "N/A",
      url: item.data.url || "N/A",
      category: item.data.category || "N/A",
      price: item.data.price || "N/A",
      rating: item.data.rating || "N/A",
      description: item.data.description || "N/A"
    };
  });

  // Return formatted data
  return { json: { products } };
  ```
- **Lưu ý**:
  - Nếu muốn **thêm trường dữ liệu**, mở node **Code** và chỉnh sửa.
  - **Kiểm tra logs** để đảm bảo dữ liệu được trích xuất đúng.

##### **📊 Node 4: Google Sheets Data Storage**
- **Cấu hình**:
  - **Spreadsheet**: Chọn **Google Sheet** đã tạo trước đó.
  - **Sheet Name**: Đặt tên **Sheet1** (hoặc tên khác nếu muốn).
  - **Operation**: Chọn **Append** (để thêm dữ liệu mới mỗi lần chạy).
  - **Column Mapping**: N8n sẽ tự động map **title, url, category, price, rating, description**.
- **Lưu ý**:
  - **Kiểm tra cấu trúc Sheet** để đảm bảo các cột phù hợp.
  - Nếu Sheet đã có dữ liệu, **Append** sẽ thêm vào cuối.

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy **Manual Execution** để kiểm tra dữ liệu đầu tiên.
- **Active Workflow**: Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động theo lịch trình.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIẾP CẬN HƠN]
1. **Lọc sản phẩm theo giá**:
   - Thêm **Code node** sau ScrapeGraphAI để lọc sản phẩm dưới **500k**:
     ```javascript
     const filteredProducts = $input.all().filter(item =>
       item.data.price && parseFloat(item.data.price.replace(/[^\d.]/g, '')) < 500000
     );
     return { json: { products: filteredProducts } };
     ```

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Thêm **Node Email** hoặc **Slack** sau Google Sheets để gửi **tin nhắn thông báo** khi workflow chạy thành công.

3. **Lưu log lỗi**:
   - Sử dụng **Node Code** để log lỗi vào **Google Sheets** hoặc **Google Drive**:
     ```javascript
     if ($input.error) {
       $output.set("error", $input.error);
     }
     ```

4. **Tự động cập nhật khi giá thay đổi**:
   - Sử dụng **Node Code** để so sánh giá cũ - mới và gửi **thông báo** khi có sự thay đổi:
     ```javascript
     const currentPrice = $input.all()[0].data.price;
     const lastPrice = $input.all()[0].json.lastPrice || 0;
     if (currentPrice !== lastPrice) {
       $output.set("priceChanged", true);
       $output.set("message", `Giá đã thay đổi từ ${lastPrice} -> ${currentPrice}`);
     }
     ```

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì **data entry thủ công**. Với **AI + n8n + Google Sheets**, bạn có thể:
✔ **Theo dõi xu hướng thị trường** hàng ngày.
✔ **So sánh sản phẩm** một cách nhanh chóng.
✔ **Lưu trữ dữ liệu** sẵn sàng cho phân tích sâu hơn.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n Self-hosted** trên VPS.
2. **Import workflow** và cấu hình API keys.
3. **Bật Active** và **theo dõi kết quả**!

👉 **Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/). 🚀