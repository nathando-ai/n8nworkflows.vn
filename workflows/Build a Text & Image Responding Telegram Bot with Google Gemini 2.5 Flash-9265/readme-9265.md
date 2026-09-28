---
title: "🤖 Tự Động Hóa Bot Telegram Thông Minh: Trả Lời Văn Bản & Phân Tích Hình Ảnh Với Google Gemini 2.5 Flash"
description: "Workflow này giúp các sếp xây dựng một bot Telegram thông minh 100% tự động hóa, trả lời văn bản bằng trí tuệ nhân tạo và phân tích hình ảnh với Google Gemini 2.5 Flash, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tay-dong-hoa-bot-telegram-thong-minh-google-gemini"
tags: [n8n, automation, no-code, ai-multimodal, google-gemini, telegram-bot]
keywords: [tự động hóa bot telegram, google gemini 2.5 flash, phân tích hình ảnh bằng ai, trả lời tin nhắn tự động, n8n workflow ai]
---

# 🚀 **Bot Telegram Thông Minh: Trả Lời Văn Bản & Phân Tích Hình Ảnh Với Google Gemini 2.5 Flash**

Hiện nay, việc tương tác với khách hàng qua Telegram đang trở thành một phần không thể thiếu trong chiến lược marketing và hỗ trợ khách hàng của các doanh nghiệp. Tuy nhiên, phải mất nhiều thời gian để trả lời từng tin nhắn, phân tích hình ảnh hoặc tìm kiếm thông tin liên quan. **Workflow này sẽ tự động hóa toàn bộ quy trình đó chỉ với một bot Telegram thông minh!**

Với công nghệ **Google Gemini 2.5 Flash** và **n8n**, các sếp có thể xây dựng một bot không chỉ trả lời văn bản một cách tự nhiên mà còn phân tích hình ảnh, nhớ lại lịch sử hội thoại và trả lời một cách cá nhân hóa. **Không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Bot tự động trả lời tin nhắn văn bản và phân tích hình ảnh ngay lập tức.
- **Trải nghiệm khách hàng nâng cao**: Trả lời một cách tự nhiên, nhớ lại lịch sử hội thoại và phân tích hình ảnh chi tiết.
- **Hỗ trợ đa dạng**: Xử lý cả văn bản và hình ảnh trong một bot duy nhất.
- **Hoạt động liên tục**: Bot hoạt động 24/7 mà không cần can thiệp của con người.
- **Cá nhân hóa**: Bot nhớ lại 20 tin nhắn trước đó để trả lời một cách logic và liên quan.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **Token API**.
   - Thêm **credentials** cho Telegram trong n8n (n8n Dashboard → Credentials → Add → Telegram).

2. **Google Gemini API Key**:
   - Đăng ký tài khoản trên [Google AI Studio](https://ai.google.dev/) và tạo **API Key**.
   - Thêm **credentials** cho Google Gemini trong n8n (n8n Dashboard → Credentials → Add → Google Gemini API).

3. **n8n Workflow**:
   - Cài đặt các **nodes** cần thiết: `n8n-nodes-base.telegram`, `@n8n/n8n-nodes-langchain.googleGemini`, `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`, `@n8n/n8n-nodes-langchain.memoryBufferWindow`.
   - Nếu chưa có, cài đặt từ [n8n Community](https://flows.n8n.io/) hoặc [n8n Marketplace](https://marketplace.n8n.io/).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/9265](https://n8n.io/workflows/9265) hoặc sao chép JSON từ trang này.
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô **Import Workflow**.
3. Nhấn **Import** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

##### **🔹 Telegram Trigger (n8n-nodes-base.telegramTrigger)**
- **Không cần cấu hình thêm**, node này sẽ tự động nhận tin nhắn từ bot Telegram khi được kích hoạt.

##### **🔹 Get a file (n8n-nodes-base.telegram)**
- **Credentials**: Chọn **telegramApi** (đã thêm trước đó).
- **Resource**: Đảm bảo chọn **file** để tải hình ảnh từ tin nhắn.

##### **🔹 Send a text message (n8n-nodes-base.telegram)**
- **Credentials**: Chọn **telegramApi**.
- **Chat ID**: Sử dụng **chatId** từ tin nhắn đầu vào (node này sẽ tự động lấy từ tin nhắn).
- **Text**: Nội dung trả lời từ AI (sẽ được tự động điền từ node **Google Gemini Chat Model**).

##### **🔹 Google Gemini Chat Model (lmChatGoogleGemini)**
- **Credentials**: Chọn **googlePalmApi**.
- **Model**: Chọn **gemini-2.5-flash** (hoặc phiên bản mới nhất).
- **Temperature**: Đặt giá trị từ **0.1 đến 0.7** để đảm bảo trả lời logic và không quá ngẫu nhiên.
- **Max Output Tokens**: Đặt giá trị **500-1000** để đảm bảo trả lời đầy đủ.

##### **🔹 Analyze image (googleGemini)**
- **Credentials**: Chọn **googlePalmApi**.
- **Operation**: Đặt **analyze**.
- **Resource**: Đặt **image**.
- **Image File**: Lấy từ node **Get a file** (tải hình ảnh từ Telegram).

##### **🔹 Route Types (n8n-nodes-base.switch)**
- **Switch Type**: Chọn **JSONPath**.
- **Path**: `$.type` (để phân loại tin nhắn là **text** hoặc **document**).
- **Case 1**: Nếu tin nhắn là **text**, route đến **Map text prompt**.
- **Case 2**: Nếu tin nhắn là **document** (hình ảnh), route đến **Map image prompt**.

##### **🔹 Knowledge Base Agent (agent)**
- **Model**: Chọn **Google Gemini**.
- **Memory**: Chọn **Simple Memory** (đã cấu hình trước).
- **Prompt Template**: Sử dụng mặc định hoặc tùy chỉnh để phù hợp với mục đích sử dụng.
- **Tools**: Đảm bảo **Google Gemini Vision** và **Google Gemini Chat** được kích hoạt.

##### **🔹 Simple Memory (memoryBufferWindow)**
- **Window Size**: Đặt **20** (để bot nhớ lại 20 tin nhắn trước đó).
- **Memory Key**: Đặt **message_history** (hoặc tên phù hợp).

##### **🔹 Map image prompt & Map text prompt (set)**
- **Node này** sẽ chuẩn bị dữ liệu đầu vào cho AI:
  - **Map text prompt**: Chuyển đổi tin nhắn văn bản thành format phù hợp.
  - **Map image prompt**: Chuyển đổi hình ảnh và mô tả từ **Analyze image** thành format phù hợp.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và gửi một tin nhắn văn bản hoặc hình ảnh đến bot Telegram.
   - Kiểm tra bot trả lời như thế nào và điều chỉnh nếu cần.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng node **n8n-nodes-base.slack** để gửi thông báo quan trọng về Slack khi bot nhận được tin nhắn từ Telegram.

2. **Lưu log hoạt động**:
   - Thêm node **n8n-nodes-base.googleSheets** hoặc **n8n-nodes-base.database** để lưu lịch sử hội thoại vào Google Sheets hoặc cơ sở dữ liệu.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **n8n-nodes-base.cron** để gửi báo cáo tổng hợp hoạt động của bot qua email hoặc Telegram hàng ngày/tuần.

4. **Tùy chỉnh prompt**:
   - Để bot trả lời phù hợp với ngành nghề của doanh nghiệp, các sếp có thể chỉnh sửa **prompt template** trong node **Knowledge Base Agent**.

5. **Phân tích hình ảnh nâng cao**:
   - Sử dụng **Google Vision API** để phân tích chi tiết hơn về hình ảnh (nhận diện vật thể, văn bản trong ảnh, màu sắc...).
:::

---

### 📌 **Kết luận**
Workflow này giúp các sếp xây dựng một **bot Telegram thông minh**, tự động trả lời tin nhắn văn bản và phân tích hình ảnh với **Google Gemini 2.5 Flash**, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. **Không cần viết code, chỉ cần import và cấu hình một chút!**

**Hãy áp dụng ngay để tự động hóa tương tác với khách hàng và tăng cường hiệu quả kinh doanh!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/9265) | [Tạo bot Telegram](https://t.me/BotFather)**