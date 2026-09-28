---
title: "🚀 **Tự Động Hóa Cảnh Báo Tin Tức Sàn Giao Dịch với RSS, Gemini & Telegram (Không Cần Code!)**"
description: "Workflow tự động hóa theo dõi tin tức liên quan đến cổ phiếu, tóm tắt nội dung bằng AI (Gemini), và gửi cảnh báo tức thời qua Telegram. Giúp các nhà đầu tư không bỏ lỡ tin tức quan trọng, tiết kiệm thời gian và tối ưu hóa quyết định đầu tư."
slug: "tieu-dong-hoa-can-bao-tin-tuc-co-phieu-gemini-telegram"
tags: [n8n, automation, no-code, crypto-trading, ai-summarization, google-sheets, telegram-bot, gemini-ai]
keywords: [n8n workflow tin tức cổ phiếu, tự động hóa cảnh báo stock, Gemini AI tóm tắt tin tức, Telegram alert stock, RSS feed automation]
---

# 🚀 **Tự Động Hóa Cảnh Báo Tin Tức Sàn Giao Dịch với RSS, Gemini & Telegram**

### **Giải pháp cho những nhà đầu tư không muốn bỏ lỡ tin tức quan trọng**
Hàng ngày, thị trường chứng khoán và crypto được cập nhật với hàng trăm tin tức mới: **sự kiện mua lại, IPO, tin tức công ty, biến động giá...**. Nếu theo dõi thủ công, các sếp sẽ phải mất **giờ đồng hồ** mỗi ngày để lọc tin tức, đọc và phân tích. **Workflow này tự động hóa toàn bộ quy trình:**
✅ **Theo dõi tin tức liên tục** từ RSS (Google Alerts) về các từ khóa như *stock acquisition, buyback, NVDA, AAPL...*
✅ **Tóm tắt tin tức bằng AI Gemini** (OpenRouter) để rút gọn nội dung thành **các điểm chính + phân tích ngắn gọn**
✅ **Gửi cảnh báo tức thời qua Telegram** để các sếp **không bỏ lỡ bất kỳ tin tức nào**
✅ **Lưu lịch sử tin tức vào Google Sheets** để theo dõi và phân tích sau này

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải theo dõi tin tức thủ công hàng ngày.
- **Tóm tắt thông minh**: AI Gemini tự động rút gọn tin tức thành **các điểm chính + phân tích ngắn gọn**.
- **Cảnh báo tức thời**: Nhận tin tức quan trọng **trực tiếp qua Telegram** (không phụ thuộc vào email).
- **Lịch sử tin tức**: Tất cả tin tức được **lưu vào Google Sheets** để theo dõi sau này.
- **Tùy chỉnh linh hoạt**: Chỉ cần thay đổi **từ khóa RSS** hoặc **prompt AI**, workflow vẫn hoạt động.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram**:
   - **Bot Token** (tạo từ [@BotFather](https://t.me/BotFather))
   - **Chat ID** của nhóm/đối thoại muốn nhận cảnh báo (có thể lấy bằng [@userinfobot](https://t.me/userinfobot))

✔ **Tài khoản OpenRouter** (dùng cho AI Gemini):
   - [Đăng ký OpenRouter](https://openrouter.ai/) và lấy **API Key**
   - **Model mặc định**: `google/gemini-2.0-flash-exp:free` (miễn phí)

✔ **Tài khoản Jina AI** (dùng để trích xuất nội dung bài viết):
   - [Đăng ký Jina AI](https://www.jina.ai/) và lấy **API Key**

✔ **Tài khoản Google**:
   - **Google Sheets** (sử dụng template đã cung cấp)
   - **Google Alerts** (để lấy RSS feed)

✔ **RSS Feed từ Google Alerts**:
   - Tạo các **Google Alert** với từ khóa như:
     - `NVDA stock acquisition`
     - `AAPL buyback`
     - `IPO 2024`
   - Sao chép **URL RSS** của mỗi alert (ví dụ: `https://www.google.com/alerts/feeds/123456789...`)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/5712](https://n8n.io/workflows/5712) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **n8n Editor** (đảm bảo không có lỗi syntax).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **15 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

##### **🔹 Node Schedule Trigger (Thời gian chạy)**
- **Cấu hình mặc định**: **15 phút/lần** (có thể điều chỉnh).
- **Lưu ý**:
  - Nếu muốn chạy **ngày đêm liên tục**, các sếp nên **self-host n8n** (không dùng phiên bản miễn phí).
  - **Không cần thay đổi** nếu muốn giữ mặc định.

##### **🔹 Node RSS Feed Read (Theo dõi tin tức)**
- **Cấu hình**:
  - **URL RSS**: Sao chép từ **Google Alerts** (ví dụ: `https://www.google.com/alerts/feeds/123456789...`).
  - **Lưu ý**:
    - **Không thể dùng 1 RSS feed duy nhất** cho tất cả tin tức. Các sếp cần **tạo nhiều RSS feed** cho từng từ khóa (ví dụ: 1 cho NVDA, 1 cho AAPL).
    - **Số lượng node RSS**: Workflow hiện có **3 node RSS** (Stock Acquisition, Stock Buyback, NVDA Stock). Các sếp có thể **thêm node mới** nếu cần theo dõi thêm từ khóa.

##### **🔹 Node Merge & Get Real URL (Xử lý URL Google Alerts)**
- **Vấn đề**: Google Alerts trả về **URL redirect** (ví dụ: `https://www.google.com/url?q=https://example.com/news`).
- **Giải pháp**:
  - Node **Merge** kết hợp tất cả tin tức từ các RSS feed.
  - Node **Code (Get Real URL)** trích xuất **URL thực sự** của bài viết.
  - **Lưu ý**:
    - **Không cần chỉnh sửa** nếu đã import workflow chính xác.
    - Nếu gặp lỗi, các sếp có thể **check lại code** trong node **Get Real URL**.

##### **🔹 Node Jina AI (Trích xuất nội dung bài viết)**
- **Cấu hình**:
  - **API Key**: Điền **API Key Jina AI** từ tài khoản của mình.
  - **Lưu ý**:
    - Nếu **API Key hết hạn**, workflow sẽ **bị ngắt** và không trích xuất được nội dung.
    - **Rate limit**: Jina AI có giới hạn free tier (~1000 request/tháng). Nếu quá giới hạn, cần **upgrade tài khoản**.

##### **🔹 Node OpenRouter (Tóm tắt bằng AI Gemini)**
- **Cấu hình**:
  - **API Key**: Điền **API Key OpenRouter**.
  - **Model**: Để mặc định là `google/gemini-2.0-flash-exp:free`.
  - **Prompt**: Workflow đã cấu hình **prompt mặc định** để tóm tắt tin tức. Các sếp có thể **thay đổi** nếu muốn:
    ```json
    "systemMessage": "You are a financial analyst. Summarize the article in 3 bullet points: 1) Main news, 2) Impact on stock price, 3) Recommendation (Buy/Hold/Sell)."
    ```
- **Lưu ý**:
  - **OpenRouter có giới hạn free tier** (~5000 token/tháng). Nếu quá giới hạn, cần **upgrade tài khoản**.
  - **Nếu model không hoạt động**, kiểm tra lại **API Key** và **model name**.

##### **🔹 Node Telegram (Gửi cảnh báo)**
- **Cấu hình**:
  - **Bot Token**: Điền **Token Bot Telegram** (từ @BotFather).
  - **Chat ID**: Điền **Chat ID** của nhóm/đối thoại (lấy từ @userinfobot).
  - **Message Template**: Workflow đã cấu hình **template mặc định** gửi:
    ```
    📢 **New Stock Alert!**
    **Title:** [Tên bài viết]
    **Summary:** [Tóm tắt AI]
    **Recommendation:** [Đánh giá Buy/Hold/Sell]
    **Link:** [URL bài viết]
    ```
  - **Lưu ý**:
    - Nếu **Bot không hoạt động**, kiểm tra lại **Token** và **Chat ID**.
    - **Rate limit Telegram**: Nếu gửi quá nhiều tin tức, Bot có thể bị **block**. Các sếp nên **chỉ gửi tin tức quan trọng**.

##### **🔹 Node Google Sheets (Lưu lịch sử tin tức)**
- **Cấu hình**:
  - **Credentials**: Điền **Google Sheets credentials** (tạo từ n8n).
  - **Sheet Name**: Để mặc định là **"Stock Alerts"** (tương ứng với template đã cung cấp).
  - **Lưu ý**:
    - **Không thể dùng Sheet khác** nếu không thay đổi cấu hình.
    - **Cột cần có**: `Title`, `Summary`, `Recommendation`, `URL`, `Date`.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chạy **manual test** với **1 tin tức mẫu** để kiểm tra:
    - AI có trích xuất nội dung không?
    - AI có tóm tắt đúng không?
    - Telegram có nhận được cảnh báo không?
    - Google Sheets có lưu tin tức không?
- **Bật Active**:
  - Sau khi **test thành công**, các sếp **bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÀY ĐỂ TĂNG HIỆU QUẢ]
- **Thêm nhiều RSS feed hơn**:
  - Các sếp có thể **thêm node RSS mới** để theo dõi thêm từ khóa (ví dụ: `TSLA`, `META`, `AMZN`).
  - **Lưu ý**: Mỗi node RSS cần **URL RSS riêng** từ Google Alerts.

- **Tùy chỉnh prompt AI**:
  - Thay đổi **system message** trong node OpenRouter để:
    - **Đánh giá rủi ro** (ví dụ: "Analyze the risk level: Low/Medium/High").
    - **So sánh với stock hiện tại** (ví dụ: "Compare with current stock price: $X").

- **Gửi cảnh báo qua Slack/Zalo**:
  - Thay thế node Telegram bằng **Slack Webhook** hoặc **Zalo API** để nhận cảnh báo trên nhiều nền tảng.

- **Lưu log vào Database**:
  - Thay vì Google Sheets, các sếp có thể **lưu vào Firebase, Airtable hoặc PostgreSQL** để dễ dàng phân tích dữ liệu.

- **Chỉ cảnh báo tin tức mới**:
  - Sử dụng **node If** để **bỏ qua tin tức đã tồn tại** trong Google Sheets (tránh trùng lặp).

- **Tự động gửi báo cáo hàng tuần**:
  - Thêm **node Schedule Trigger** chạy **1 lần/tuần** và gửi **báo cáo tổng hợp** qua Telegram/Email.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc theo dõi tin tức cổ phiếu thủ công, đồng thời **tự động hóa toàn bộ quy trình** từ **trích xuất → tóm tắt → cảnh báo → lưu trữ**. **Chỉ cần 30 phút setup**, các sếp sẽ **không bỏ lỡ bất kỳ tin tức quan trọng nào** nữa!

🚀 **Hành động ngay**:
1. **Import workflow** từ [n8n.io/workflows/5712](https://n8n.io/workflows/5712).
2. **Điền API Key & Config** theo hướng dẫn trên.
3. **Bật Active** và **nhận cảnh báo tức thời**!

**Nếu gặp vấn đề**, các sếp có thể:
- **Tra cứu community n8n** ([n8n.io/community](https://n8n.io/community)).
- **Đăng câu hỏi** trên [GitHub](https://github.com/n8n-io/n8n/issues).
- **Liên hệ với tôi** để hỗ trợ chi tiết!

---
**Chúc các sếp thành công với tự động hóa đầu tư!** 💰📈