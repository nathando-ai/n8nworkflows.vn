---
title: "🤖 **Tự Động Trích Xuất Dữ Liệu Website Sang JSON Cấu Trúc Với ScrapeNinja & AI - Không Cần Code!**"
description: "Workflow này giúp các sếp tự động hóa việc trích xuất dữ liệu từ bất kỳ trang web nào thành JSON cấu trúc, sẵn sàng cho phân tích AI và ứng dụng trong SaaS. Giảm thiểu thời gian phát triển 80% so với phương pháp thủ công!"
slug: "tieu-dung-trich-xuat-du-lieu-website-sang-json"
tags: [n8n, automation, web-scraping, ai, scrapeNinja, no-code, SaaS]
keywords: [n8n workflow scraping, tự động hóa trích xuất dữ liệu website, scrapeNinja API, AI phân tích dữ liệu, JSON structured data, tự động hóa không code]
---

# 🚀 **Tự Động Trích Xuất Dữ Liệu Website Sang JSON Cấu Trúc Với ScrapeNinja & AI**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm hàng giờ** mỗi tuần trích xuất dữ liệu từ website thủ công?
- **Không cần viết code** nhưng vẫn muốn dữ liệu sạch, cấu trúc và AI-ready?
- **Cập nhật dữ liệu tự động** hàng ngày mà không lo bị block bởi CAPTCHA?

Workflow này là **công cụ siêu mạnh** cho các nhà phát triển, founder SaaS và chuyên gia dữ liệu, giúp bạn **trích xuất dữ liệu từ bất kỳ trang web nào** (bao gồm cả trang có JavaScript động) và chuyển thành **JSON cấu trúc**, sẵn sàng để:
✅ **Nạp vào LLM** (Google Gemini, ChatGPT...) để phân tích.
✅ **Lưu vào cơ sở dữ liệu** (Google Sheets, PostgreSQL...).
✅ **Tích hợp vào ứng dụng SaaS** của bạn.
✅ **Tự động hóa báo cáo** hàng ngày/ngày.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **hoạt động 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS ổn định.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho scraping)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với phương pháp thủ công (không cần viết regex hay XPath).
- **Dữ liệu sạch & cấu trúc** (JSON) ngay từ lần đầu, không cần post-process.
- **Không bị block** bởi CAPTCHA hoặc IP ban (ScrapeNinja có hệ thống proxy và user-agent quản lý).
- **Tích hợp AI** (Google Gemini, ChatGPT...) để tự động phân tích hoặc tổng hợp dữ liệu.
- **Hoạt động tự động** (cập nhật hàng ngày/tuần/month) mà không cần can thiệp.
- **Mở rộng dễ dàng** cho nhiều trang web khác nhau với cùng một workflow.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản ScrapeNinja**:
   - [Đăng ký miễn phí](https://scrapeninja.net/) (có phiên bản free với giới hạn request).
   - **API Key** (tìm trong Dashboard của ScrapeNinja).
2. **Tài khoản Google Cloud (nếu sử dụng Google Gemini)**:
   - [Đăng ký API Key](https://aistudio.google.com/app/apikey) (miễn phí 300$ credit đầu tiên).
3. **Tài khoản n8n** (nếu chưa có):
   - [Tạo tài khoản](https://n8n.io/) và cài đặt **n8n Cloud** hoặc **self-host**.

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/2812).
**Bước 2:** Trong **n8n Editor**, chọn **"Import"** và chọn file JSON đã tải.
**Bước 3:** Chọn **"Import"** để workflow xuất hiện trong danh sách.

---
#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **6 node chính**, mỗi node đều cần cấu hình kỹ lưỡng:

##### **Node 1: Generate custom web scraper (manualTrigger)**
- **Chức năng**: Bắt đầu quá trình scraping khi kích hoạt thủ công.
- **Lưu ý**:
  - **Không cần thay đổi gì** nếu chỉ muốn chạy một lần.
  - Nếu muốn **tự động hóa**, các sếp cần kết nối với **n8n Trigger** (ví dụ: Webhook, Cron, hoặc Zapier).

##### **Node 2: ScrapeNinja (trước khi cleanup)**
- **Credentials**: Chọn `"scrapeNinjaApi"` (đã cấu hình API Key ở bước chuẩn bị).
- **Input**:
  - **URL**: Điền địa chỉ trang web cần scraping (ví dụ: `https://example.com`).
  - **Selector**: Nếu muốn trích xuất phần cụ thể, điền **CSS Selector** (ví dụ: `div.product`).
  - **Delay**: Thiết lập thời gian chờ (giúp tránh bị block, mặc định 2-3 giây).

##### **Node 3: Cleanup HTML (CUSTOM.scrapeNinja)**
- **Operation**: Chọn `"cleanup-html"` (đã cấu hình sẵn).
- **Lưu ý**:
  - Node này **xóa bỏ các thẻ HTML không cần thiết** (script, style, comment) để dữ liệu sạch hơn.
  - **Không cần thay đổi** nếu muốn giữ mặc định.

##### **Node 4: Generate JS eval code via LLM (chainLlm)**
- **Credentials**: Chọn `"googlePalmApi"` (API Key Google Gemini).
- **Input**:
  - **Prompt**: Cấu hình sẵn để **tạo mã JavaScript** trích xuất dữ liệu từ HTML đã cleanup.
  - **Model**: Chọn `"gemini-1.5-flash"` (mô hình nhanh và hiệu quả).
  - **Lưu ý**:
    - Nếu muốn **tùy chỉnh prompt**, các sếp có thể thay đổi để AI trả về mã phù hợp với logic scraping cụ thể.

##### **Node 5: Eval generated code to extract data (CUSTOM.scrapeNinja)**
- **Operation**: Chọn `"extract-custom"` (đã cấu hình sẵn).
- **Input**:
  - **HTML Cleaned**: Dữ liệu từ Node 3.
  - **JS Code**: Mã JavaScript từ Node 4.
- **Lưu ý**:
  - Node này **thực thi mã JavaScript** để trích xuất dữ liệu theo logic đã định nghĩa.
  - **Kiểm tra kết quả** trong tab **"Execution"** để đảm bảo dữ liệu đúng format.

##### **Node 6: Google Gemini Chat Model (lmChatGoogleGemini)**
- **Credentials**: Chọn `"googlePalmApi"`.
- **Input**:
  - **Prompt**: Cấu hình để **phân tích hoặc tổng hợp** dữ liệu JSON (ví dụ: *"Tóm tắt thông tin sản phẩm từ dữ liệu này"*).
  - **Model**: Chọn `"gemini-1.5-pro"` (nếu muốn chất lượng cao hơn).
- **Lưu ý**:
  - Node này **không bắt buộc** nhưng rất hữu ích nếu muốn **AI tự động phân tích** dữ liệu trích xuất.

---
#### **3. Kích hoạt ⚡️**
**Bước 1:** Kích hoạt **Node "Generate custom web scraper"** (manualTrigger).
**Bước 2:** Điền **URL** và **Selector** (nếu cần) vào Node **ScrapeNinja**.
**Bước 3:** Chạy workflow và **kiểm tra kết quả** trong tab **"Execution"**:
- Dữ liệu đầu ra sẽ là **JSON cấu trúc**, sẵn sàng để:
  - **Lưu vào Google Sheets** (sử dụng node `n8n-nodes-base.googleSheets`).
  - **Gửi qua Email/Slack** (sử dụng node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack`).
  - **Nạp vào cơ sở dữ liệu** (PostgreSQL, MySQL...).

**Bước 4:** Để **tự động hóa**, các sếp có thể:
- Kết nối với **n8n Trigger Cron** (chạy hàng ngày).
- Sử dụng **Zapier** hoặc **Make (Integromat)** để kích hoạt workflow từ các sự kiện khác.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa báo cáo hàng ngày**:
   - Sử dụng **n8n Trigger Cron** để chạy workflow vào mỗi ngày 8h sáng.
   - **Gửi báo cáo qua Email/Slack** với dữ liệu mới nhất.

2. **Lưu log và theo dõi lỗi**:
   - Sử dụng **node `n8n-nodes-base.telegram`** để nhận thông báo lỗi qua Telegram.
   - Lưu **log execution** vào **Google Drive** hoặc **AWS S3**.

3. **Kết hợp với Google Sheets**:
   - Sau khi trích xuất JSON, sử dụng **node `n8n-nodes-base.googleSheets`** để tự động cập nhật bảng tính.
   - Ví dụ: Dữ liệu từ scraping sẽ tự động thêm vào sheet mới mỗi ngày.

4. **Tùy chỉnh AI Prompt**:
   - Nếu muốn **AI phân tích chi tiết hơn**, thay đổi prompt trong **node `chainLlm`** ví dụ:
     ```plaintext
     "Tôi có một trang web bán sách với dữ liệu sau: {{{$json}}}. Vui lòng:
     1. Lọc ra các sách có giá > 500k.
     2. Tóm tắt 3 sản phẩm có rating cao nhất.
     3. Gợi ý một sản phẩm tương tự cho mỗi sản phẩm trong danh sách."
     ```

5. **Mở rộng cho nhiều trang web**:
   - Sử dụng **node `n8n-nodes-base.foreach`** để chạy workflow cho nhiều URL cùng lúc.
   - Ví dụ: Trích xuất dữ liệu từ 10 trang web khác nhau trong một lần chạy.

---

### 📌 **Kết luận**
Workflow này là **công cụ không thể thiếu** cho các founder SaaS, nhà phát triển và chuyên gia dữ liệu muốn:
✔ **Tự động hóa scraping** mà không cần viết code.
✔ **Nạp dữ liệu vào AI** (Google Gemini, ChatGPT...) để phân tích.
✔ **Cập nhật dữ liệu tự động** hàng ngày mà không lo bị block.

**Hành động ngay hôm nay!**
1. **Đăng ký ScrapeNinja** và **Google Cloud API**.
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Kích hoạt tự động hóa** với **n8n Trigger Cron** hoặc **Zapier**.

**🚀 [Tải workflow ngay từ đây](https://n8n.io/workflows/2812) và bắt đầu tự động hóa dữ liệu của bạn!**

---
**Cần hỗ trợ thêm?**
- **Trang hỗ trợ ScrapeNinja**: [https://scrapeninja.net/docs](https://scrapeninja.net/docs)
- **Community n8n**: [https://community.n8n.io](https://community.n8n.io)