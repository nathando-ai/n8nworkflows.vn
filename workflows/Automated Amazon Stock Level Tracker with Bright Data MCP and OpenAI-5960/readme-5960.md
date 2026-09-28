---
title: "🚀 **Tự Động Hóa Kiểm Tra & Cảnh Báo Hàng Hết Sản Phẩm Amazon Với Bright Data & OpenAI (Không Cần Code!)**"
description: "Workflow tự động hóa 24/7 kiểm tra mức tồn kho sản phẩm Amazon, cảnh báo hàng hết cho nhà cung cấp qua email, và sử dụng AI để phân tích dữ liệu chính xác. Giúp doanh nghiệp tránh thiếu hàng, tối ưu chuỗi cung ứng và tiết kiệm thời gian kiểm tra thủ công."
slug: "tieu-dong-hoa-amazon-stock-tracker"
tags: [n8n, automation, no-code, ai-summarization, bright-data, openai, ecommerce]
keywords: [tự động hóa amazon stock, kiểm tra tồn kho tự động, cảnh báo hàng hết, bright data mcp, openai chatbot, n8n workflow, tự động hóa bán hàng online]
---

# 🚀 **Tự Động Hóa Kiểm Tra Tồn Kho Amazon & Cảnh Báo Hàng Hết Cho Nhà Cung Cấp**

## **🔍 Nỗi Đau Của Doanh Nghiệp**
Bạn đã bao giờ phải **kiểm tra thủ công** mức tồn kho sản phẩm trên Amazon hàng ngày, chỉ để phát hiện hàng hết khi đã quá muộn? Hoặc phải **gọi điện, gửi tin nhắn** cho nhà cung cấp để yêu cầu restock? Thời gian và công sức tiêu tốn này có thể được **tự động hóa hoàn toàn** với một workflow đơn giản trên **n8n**, kết hợp **Bright Data MCP** (scraping ẩn danh) và **OpenAI** (AI phân tích dữ liệu).

Workflow này sẽ:
✅ **Kiểm tra tự động** mức tồn kho sản phẩm Amazon theo lịch trình (ví dụ: mỗi 6 giờ/lần).
✅ **Dùng AI phân tích** dữ liệu scraped từ Amazon (tránh bị chặn bởi CAPTCHA).
✅ **Gửi email cảnh báo** cho nhà cung cấp khi sản phẩm **hết hàng**.
✅ **Tiết kiệm thời gian** và **giảm thiểu rủi ro thiếu hàng** cho doanh nghiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công hàng ngày.
- **Chính xác cao**: Dùng **Bright Data MCP** (scraping ẩn danh) và **OpenAI** để phân tích dữ liệu chính xác.
- **Cảnh báo kịp thời**: Email tự động đến nhà cung cấp khi hàng hết.
- **Hoạt động liên tục**: Workflow chạy 24/7 theo lịch trình.
- **Dễ mở rộng**: Có thể kiểm tra **nhiều sản phẩm** bằng Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Bright Data MCP** (để scraping Amazon ẩn danh):
   - [Đăng ký Bright Data](https://get.brightdata.com/1tndi4600b25) (Yaron sẽ nhận commission nhỏ từ link này).
✔ **API Key OpenAI** (để sử dụng GPT-4o-mini):
   - [Tạo API Key OpenAI](https://platform.openai.com/account/api-keys).
✔ **Tài khoản Gmail** (để gửi email cảnh báo):
   - Cần **OAuth 2.0** cho Gmail (cấu hình trong n8n).
✔ **URL sản phẩm Amazon** (cần nhập vào node **Define Product URL**).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/5960) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5960) và dán vào **Create Workflow → Import JSON**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow được chia thành **3 phần chính**, các sếp cần chú ý:

#### **🟩 PHẦN 1: Cấu Hình Khởi Động & Lịch Trình**
- **Node: Check Stock Every X Hours (Schedule Trigger)**
  - Chỉnh **interval** (ví dụ: `0 0 */6 * *` để chạy mỗi 6 giờ).
- **Node: Define Product URL**
  - Nhập **URL sản phẩm Amazon** (ví dụ: `https://www.amazon.com/dp/B08XYZ1234`).
  - Có thể thêm **ngưỡng stock** (nếu cần).

#### **🤖 PHẦN 2: Scraping Dữ Liệu Từ Amazon**
- **Node: Scrape Product Data (via Agent)**
  - **Bright Data MCP** sẽ tự động load trang Amazon như một người dùng thực.
  - **OpenAI (Chat)** và **Structured Output Parser** sẽ phân tích dữ liệu scraped.
  - **Kết quả đầu ra** sẽ là JSON như:
    ```json
    {
      "availability": "Out of Stock",
      "title": "Sản phẩm ABC",
      "price": 12.99
    }
    ```

#### **📬 PHẦN 3: Quyết Định & Cảnh Báo**
- **Node: Product In Stock? (If)**
  - Nếu `availability: "In Stock"` → **Do Nothing (NoOp)** (không làm gì).
  - Nếu `availability: "Out of Stock"` → **Email Supplier (Gmail)** (gửi cảnh báo).
- **Node: Email Supplier (Gmail)**
  - Chọn **credentials** là tài khoản Gmail đã cấu hình.
  - **Tiêu đề email**: "Cảnh báo: Sản phẩm [Tên] đã hết hàng".
  - **Nội dung email**: Dùng **OpenAI** tự động tổng hợp thông tin (có thể tùy chỉnh).

---
### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy thử với một sản phẩm mẫu để kiểm tra logic.
- **Bật Active**: Sau khi kiểm tra xong, bật **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kiểm Tra Nhiều Sản Phẩm**:
   - Thay vì nhập URL thủ công, sử dụng **Google Sheets** để lưu danh sách sản phẩm và **loop** qua mỗi hàng.
   - Cấu hình **Google Sheets Node** để đọc dữ liệu và truyền vào **Define Product URL**.

2. **Lưu Log & Báo Cáo**:
   - Thêm **Slack/Telegram Node** để gửi thông báo khi hàng hết.
   - Sử dụng **Google Drive** để lưu lịch sử cảnh báo.

3. **Tối Ưu AI**:
   - Thay đổi **prompt** trong **OpenAI Chat** để AI phân tích dữ liệu chi tiết hơn (ví dụ: kiểm tra stock trên nhiều trang Amazon).

4. **Cảnh Báo Trước Hết Hàng**:
   - Thêm **ngưỡng stock** (ví dụ: dưới 5 sản phẩm) và gửi email cảnh báo sớm hơn.

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho những doanh nghiệp muốn **tự động hóa kiểm tra tồn kho Amazon**, tránh thiếu hàng và **tối ưu chuỗi cung ứng**. Với **Bright Data MCP** (scraping ẩn danh) và **OpenAI** (AI phân tích), workflow hoạt động **chính xác, an toàn và không cần code**.

**Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả kinh doanh!** 🚀

---
### **🔗 Tài Liệu Tham Khảo**
- [Workflow gốc trên n8n](https://n8n.io/workflows/5960)
- [Bright Data MCP](https://get.brightdata.com/1tndi4600b25)
- [OpenAI API](https://platform.openai.com/account/api-keys)
- [Cách cấu hình Gmail OAuth 2.0](https://docs.n8n.io/integrations/builtins/nodes/Gmail/)

---
### **💬 Có Thắc Mắc?**
Nếu cần hỗ trợ, liên hệ với **Yaron Been** qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos) (có nhiều tutorial tự động hóa hữu ích)