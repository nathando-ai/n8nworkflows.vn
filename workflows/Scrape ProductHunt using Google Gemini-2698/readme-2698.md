---
title: "🚀 Tự Động Hóa Scrape & Phân Tích Sản Phẩm Trên Product Hunt Với Google Gemini (Không Cần Code)"
description: "Workflow tự động hóa scrape dữ liệu sản phẩm từ Product Hunt, phân tích nội dung bằng Google Gemini AI, và trả về kết quả JSON chuẩn cho marketing, sản phẩm hoặc nghiên cứu thị trường. Tiết kiệm thời gian lên đến 80% so với phương pháp thủ công."
slug: "tieu-dong-hoa-scrape-producthunt-google-gemini"
tags: [n8n, automation, no-code, ai, marketing, google-gemini, product-hunt]
keywords: [scrape product hunt n8n, tự động hóa phân tích sản phẩm, google gemini api n8n, workflow marketing sản phẩm, scrape website không code]
---

# 🚀 **Tự Động Hóa Scrape & Phân Tích Sản phẩm Trên Product Hunt Với Google Gemini**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm thời gian** khi phân tích sản phẩm mới trên Product Hunt (thay vì copy-paste thủ công).
- **Hiểu sâu hơn về xu hướng thị trường** nhờ phân tích tự động bằng AI Google Gemini.
- **Tích hợp dữ liệu vào CRM, Airtable, hoặc Slack** để quyết định marketing nhanh chóng.
- **Không cần viết một dòng code** – chỉ cần cấu hình và chạy 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud. Với VPS, các sếp có thể:
✅ **Tùy chỉnh API keys** (không bị giới hạn bởi phiên bản cloud).
✅ **Chạy liên tục 24/7** (không bị ngắt kết nối).
✅ **Tích hợp nhiều dịch vụ** (Google Gemini, Slack, Airtable...) một cách linh hoạt.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI).
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Scrape và phân tích **100 sản phẩm trong 5 phút** (thay vì 2-3 giờ thủ công).
- **Dữ liệu chính xác**: Trích xuất **tên, mô tả, link, và đánh giá** từ Product Hunt một cách tự động.
- **Phân tích sâu bằng AI**: Google Gemini **tóm tắt, phân loại, và đánh giá** sản phẩm theo yêu cầu của các sếp.
- **Kết quả chuẩn JSON**: Dữ liệu sẵn sàng **tích hợp vào CRM, Airtable, hoặc gửi qua Slack**.
- **Hoạt động liên tục**: Workflow chạy **mỗi khi có yêu cầu mới** (vía webhook) mà không cần can thiệp.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Product Hunt** (để scrape dữ liệu).
✅ **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
✅ **Credentials cho n8n** (để kết nối với Google Gemini và trả về kết quả).
✅ **Webhook URL** (để nhận yêu cầu scrape từ bên ngoài).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không scrape liên tục** (mà chỉ hoạt động khi được gọi qua webhook).
- **Không cần API key Product Hunt** (do workflow scrape thông qua HTTP Request).
- **Google Gemini** sẽ phân tích nội dung và trả về kết quả **bằng JSON**, dễ dàng tích hợp vào hệ thống khác.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**.

#### **Cách import từ file JSON:**
1. Tải file JSON từ [n8n.io/workflows/2698](https://n8n.io/workflows/2698).
2. Trên **n8n Dashboard**, chọn **"Import"** → Chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

#### **Cách copy/paste JSON:**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Click vào **"Import"** → Chọn **"Paste JSON"** → Dán JSON từ workflow gốc.
3. Click **"Import"** để hoàn tất.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: "Receive Product Request" (Webhook)**
- **Chức năng**: Nhận yêu cầu scrape từ bên ngoài (ví dụ: từ Slack, Telegram, hoặc API).
- **Cấu hình**:
  - **HTTP Method**: `POST` (để gửi dữ liệu scrape).
  - **Credentials**: Chọn **"None"** (nếu không cần xác thực).
  - **Path**: Giữ nguyên `/product-request` (hoặc thay đổi theo yêu cầu).

#### **🔹 Node 2: "Fetch Product HTML" (HTTP Request)**
- **Chức năng**: Scrape trang Product Hunt để lấy HTML của sản phẩm.
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://www.producthunt.com/posts/{product_id}` (thay `{product_id}` bằng ID sản phẩm từ yêu cầu webhook).
  - **Headers**:
    ```
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
    ```
  - **Credentials**: Chọn **"None"** (không cần đăng nhập).

#### **🔹 Node 3: "Extract Inline Scripts" (Code)**
- **Chức năng**: Trích xuất **script JavaScript** từ trang HTML để phân tích.
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu các sếp đã import workflow hoàn chỉnh.
  - Nếu cần thay đổi, các sếp có thể mở **Code Editor** và chỉnh sửa logic trích xuất.

#### **🔹 Node 4: "Process Script with LLM" (Chain LLM)**
- **Chức năng**: Chuẩn bị dữ liệu cho Google Gemini phân tích.
- **Cấu hình**:
  - **Model**: Giữ nguyên (do workflow đã cấu hình sẵn).
  - **Input**: Dữ liệu từ Node 3 (script trích xuất).

#### **🔹 Node 5: "Analyze Script with Google Gemini" (lmChatGoogleGemini)**
- **Chức năng**: **Phân tích sâu** sản phẩm bằng Google Gemini AI.
- **Cấu hình QUAN TRỌNG**:
  - **API Key**: Điền **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
  - **Prompt**: Giữ nguyên (hoặc tùy chỉnh theo yêu cầu phân tích):
    ```
    Analyze the following product script from Product Hunt. Extract:
    - Product name
    - Description
    - Key features
    - Target audience
    - Potential improvements
    Return the result in JSON format.
    ```
  - **Model**: Chọn **"gemini-pro"** (hoặc phiên bản mới nhất).

#### **🔹 Node 6: "Format Product Data to JSON" (Output Parser Structured)**
- **Chức năng**: Chuyển kết quả phân tích thành **JSON chuẩn**.
- **Cấu hình**:
  - **Schema**: Giữ nguyên (do workflow đã định nghĩa sẵn).
  - **Output**: Dữ liệu sẽ được trả về dưới dạng JSON dễ tích hợp.

#### **🔹 Node 7: "Send JSON Response to Client" (Respond To Webhook)**
- **Chức năng**: Trả về kết quả JSON cho người gửi yêu cầu.
- **Cấu hình**:
  - **Response Type**: `JSON`.
  - **Headers**: Giữ nguyên (để client nhận được dữ liệu một cách dễ dàng).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một yêu cầu webhook với **product_id** (ví dụ: `123456789`).
   - Kiểm tra kết quả trả về có phải JSON không?
2. **Bật Active workflow**:
   - Click **"Active"** trên dashboard n8n.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Tích hợp với Slack/Telegram để nhận thông báo**
- Sử dụng **node Slack** hoặc **Telegram Bot** để gửi kết quả phân tích ngay khi có sản phẩm mới.
- **Cách làm**:
  1. Thêm **node Slack** sau Node 7.
  2. Cấu hình **webhook URL** của Slack Bot.
  3. Gửi tin nhắn tự động khi có kết quả mới.

### **🔹 Lưu log phân tích vào Google Sheets/Airtable**
- Sử dụng **node Google Sheets** hoặc **Airtable** để lưu lịch sử phân tích.
- **Cách làm**:
  1. Thêm **node Google Sheets** sau Node 6.
  2. Chọn **Sheet** và **Range** để lưu dữ liệu.
  3. Cấu hình **credentials** của Google Sheets.

### **🔹 Tự động scrape định kỳ (dùng Cron Job)**
- Nếu các sếp muốn **scrape tất cả sản phẩm mới trên Product Hunt hàng ngày**, có thể:
  - Sử dụng **node Cron** (n8n có hỗ trợ).
  - Cấu hình **lịch chạy** (ví dụ: 9h sáng hàng ngày).
  - Gửi kết quả vào **Slack** hoặc **Email**.

### **🔹 Tùy chỉnh prompt cho Google Gemini**
- Nếu các sếp muốn **phân tích theo yêu cầu riêng**, hãy chỉnh sửa **prompt** trong Node 5:
  - Ví dụ: **"Phân tích sản phẩm theo góc độ SEO"** hoặc **"Đánh giá tính khả thi kinh doanh"**.

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa scrape và phân tích sản phẩm trên Product Hunt một cách nhanh chóng, chính xác và không cần code**. Với **Google Gemini**, các sếp có thể **hiểu sâu hơn về xu hướng thị trường**, **tích hợp dữ liệu vào hệ thống**, và **quyết định marketing hiệu quả**.

🚀 **Hành động ngay hôm nay**:
1. **Self-host n8n** trên VPS để chạy 24/7.
2. **Import workflow** và cấu hình API Key Google Gemini.
3. **Test run** với một sản phẩm mẫu.
4. **Tích hợp với Slack/Airtable** để sử dụng hiệu quả.

**Cần hỗ trợ tùy chỉnh?** Liên hệ với **Mauricio Perera** (tác giả workflow) qua [LinkedIn](https://www.linkedin.com/in/mauricioperera/) để xây dựng workflow phù hợp với nhu cầu riêng của các sếp!

---
**Chúc các sếp thành công với tự động hóa!** 💪🚀