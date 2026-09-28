---
title: "🚀 Chuyển Đổi Tin Nhắn Âm Telegram Sang Email Chuyên Nghiệp Tự Động Với Whisper, GPT-4 & Gmail"
description: "Workflow tự động hóa hoàn toàn không code giúp chuyển đổi tin nhắn âm thanh từ Telegram thành email chuyên nghiệp với nội dung tự động viết bởi AI (Whisper + GPT-4), tiết kiệm thời gian lên tới 90% cho các sếp và nhân viên liên lạc thường xuyên qua Telegram."
slug: "chuyen-doi-tin-nhan-am-telegram-sang-email-chuyen-nghiep"
tags: [n8n, automation, no-code, ai-multimodal, telegram, gmail, openai, whisper, gpt-4]
keywords: [n8n workflow telegram email, tự động hóa email từ âm thanh, chuyển đổi tin nhắn âm thanh sang văn bản, gpt-4 viết email tự động, whisper openai, tự động hóa liên lạc doanh nghiệp]
---

# 🚀 **Chuyển Đổi Tin Nhắn Âm Telegram Sang Email Chuyên Nghiệp Tự Động Với AI**

### **Nỗi Đau Của Các Sếp & Nhân Viên**
Các sếp và nhân viên thường phải:
- **Lắng nghe và ghi lại** nội dung tin nhắn âm thanh từ Telegram (thường là yêu cầu, thông báo, hoặc tin nhắn cá nhân).
- **Viết email** để trả lời hoặc chuyển tiếp thông tin, mất thời gian và dễ mắc lỗi chính tả hoặc nội dung không chuyên nghiệp.
- **Quên hoặc trì hoãn** việc trả lời, ảnh hưởng đến hình ảnh chuyên nghiệp của doanh nghiệp.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động chuyển đổi** tin nhắn âm thanh thành văn bản (sử dụng **OpenAI Whisper**).
✅ **Sử dụng AI (GPT-4)** để tự động viết email chuyên nghiệp, bao gồm:
   - Địa chỉ email nhận (thậm chí tự hoàn thành từ đoạn văn bản ngắn).
   - Tiêu đề email phù hợp.
   - Nội dung HTML đẹp mắt, không lỗi chính tả.
✅ **Gửi email tự động** qua Gmail, tiết kiệm thời gian lên tới **90%** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nghe lại tin nhắn âm thanh và viết email thủ công.
- **Chuyên nghiệp hóa liên lạc**: Email luôn được viết bởi AI với **nội dung chính xác, không lỗi chính tả**, và **định dạng HTML đẹp**.
- **Hoạt động liên tục**: Workflow chạy tự động ngay cả khi các sếp **ngủ ngơi**, không bỏ lỡ tin nhắn nào.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, chỉ cần **cấu hình 1 lần** là workflow hoạt động mãi.
- **Dễ dàng mở rộng**: Có thể kết nối với **Slack, Telegram, hoặc hệ thống CRM** khác để tự động hóa thêm các công việc liên quan.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cấu hình bot để **lắng nghe tin nhắn âm thanh** (cần quyền admin trong nhóm/channel nếu cần).
2. **API Key OpenAI**:
   - Đăng ký tài khoản [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Đảm bảo tài khoản có **gói sử dụng đủ** cho Whisper và GPT-4 (đặc biệt là `gpt-4.1-mini`).
3. **Tài khoản Gmail OAuth2**:
   - Cấu hình **OAuth2** trong n8n để workflow có thể gửi email tự động.
   - **Lưu ý**: Gmail có thể yêu cầu **cài đặt ứng dụng không an toàn** (nếu không cấu hình OAuth2).
4. **N8n Self-Hosted** (khuyến nghị):
   - Workflow này **không hoạt động trên n8n Cloud** do giới hạn API và thời gian xử lý.
   - Nên cài đặt trên **VPS** để đảm bảo **ổn định 24/7**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7041) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ file vào **Import Workflow** trong n8n.

**Cách import:**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **From JSON**.
2. Dán nội dung JSON từ file vào và nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **9 node** quan trọng, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Phần 1: Telegram → Tải File Âm Thanh**
1. **Telegram Voice Message Trigger**
   - **Node type**: `telegramTrigger`
   - **Credential**: Chọn **telegramApi** (đã cấu hình bot trên BotFather).
   - **Trigger On**: Chọn **`Message`** (lắng nghe tất cả tin nhắn, bao gồm âm thanh).
   - **Lưu ý**:
     - **Chỉ có 1 Telegram Trigger cho 1 bot** (nếu có nhiều bot, cần tạo workflow riêng).
     - Nếu muốn **chỉ lắng nghe âm thanh**, các sếp có thể **lọc tin nhắn** bằng **Webhook Filter** (nếu cần nâng cao).

2. **Buffer Delay (Pre-Processing)**
   - **Node type**: `wait`
   - **Thời gian**: Để mặc định (5 giây) để tránh **tràn tin nhắn** khi nhiều người gửi cùng lúc.

3. **Download Telegram Voice File**
   - **Node type**: `telegram`
   - **Resource**: Chọn **`file`**.
   - **File ID**: **Không cần điền** (n8n tự lấy từ tin nhắn âm thanh).
   - **Lưu ý**:
     - Đảm bảo **bot có quyền** tải file âm thanh từ Telegram.
     - Nếu file âm thanh quá lớn, có thể **cắt ngắn** bằng cách cấu hình **thời gian tối đa** trong OpenAI Whisper (node sau).

---

##### **🔹 Phần 2: Chuyển Âm Thanh → Văn Bản → Email**
4. **Transcribe Audio to Text (OpenAI Whisper)**
   - **Node type**: `openAi`
   - **Credential**: Chọn **openAiApi** (API Key đã cấu hình).
   - **Operation**: Chọn **`transcribe`**.
   - **Resource**: Chọn **`audio`**.
   - **Lưu ý**:
     - Đảm bảo **file âm thanh được tải đúng** từ node trước.
     - Nếu âm thanh quá dài, có thể **cắt ngắn** bằng cách cấu hình **`max_duration_seconds`** (nếu hỗ trợ).

5. **Buffer Delay (Pre-AI Processing)**
   - **Node type**: `wait`
   - **Thời gian**: Để mặc định (5 giây) để **Whisper hoàn thành** trước khi chuyển sang AI.

6. **Generate Email Content AI AGENT**
   - **Node type**: `agent` (Langchain)
   - **Prompt (cần chỉnh sửa)**:
     ```
     Bạn là một trợ lý email chuyên nghiệp. Dựa vào nội dung sau:
     ```
     {{ $json.text }}
     ```
     Hãy:
     1. **Xác định địa chỉ email nhận** (nếu chỉ có tên, hãy tự hoàn thành, ví dụ: "send to fort.baptiste.pro" → "fort.baptiste.pro@gmail.com").
     2. **Hiểu ý định** của người gửi (thoái việc, yêu cầu, xin lỗi, thông báo...).
     3. **Viết tiêu đề email** phù hợp và chuyên nghiệp.
     4. **Viết nội dung email** trong **HTML**, không có lỗi chính tả, với cấu trúc rõ ràng.
     5. **Trả về kết quả theo schema JSON sau**:
     ```json
     {
       "email": "string",
       "subject": "string",
       "body": "string"
     }
     ```
     ```
   - **Model**: Chọn **`gpt-4.1-mini`** (hoặc `gpt-4` nếu có budget).
   - **Credential**: Chọn **openAiApi** (API Key OpenAI).
   - **Lưu ý**:
     - **Prompt rất quan trọng**! Nếu không viết đúng, AI sẽ trả về kết quả sai.
     - Có thể **test prompt** trước bằng cách chạy **Langchain Playground** (nếu có).

7. **GPT-4 Email Generator Model**
   - **Node type**: `lmChatOpenAi`
   - **Model**: Chọn **`gpt-4.1-mini`** (hoặc `gpt-4`).
   - **Credential**: Chọn **openAiApi**.
   - **Lưu ý**:
     - Nếu budget hạn chế, **gpt-4.1-mini** vẫn cho kết quả tốt.
     - Đảm bảo **tài khoản OpenAI có đủ token** (1 request ≈ 1000 token).

8. **Enforce Email JSON Schema**
   - **Node type**: `outputParserStructured`
   - **JSON Schema**:
     ```json
     {
       "email": "string",
       "subject": "string",
       "body": "string"
     }
     ```
   - **Lưu ý**:
     - Nếu AI trả về **kết quả không đúng schema**, workflow sẽ **báo lỗi**.
     - Có thể **cải thiện prompt** trong node `agent` để đảm bảo AI tuân thủ schema.

9. **Send Email**
   - **Node type**: `gmail`
   - **To**: `{{$json.output.email}}` (địa chỉ email nhận từ AI).
   - **Subject**: `{{$json.output.subject}}` (tiêu đề email).
   - **HTML Body**: `{{$json.output.body}}` (nội dung HTML).
   - **Credential**: Chọn **gmailOAuth2** (đã cấu hình OAuth2).
   - **Lưu ý**:
     - Đảm bảo **Gmail không bị block** (nếu gửi quá nhiều email, có thể bị Gmail đánh dấu là spam).
     - Có thể **thêm CC/BCC** bằng cách **cấu hình thêm fields** trong node `gmail`.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một tin nhắn âm thanh mẫu:
   - Gửi **tin nhắn âm thanh** cho bot Telegram.
   - Kiểm tra **log** trong n8n để xem workflow có chạy đúng không.
   - Nếu có lỗi, **check lại các node** (đặc biệt là **prompt** và **schema JSON**).

2. **Bật Active**:
   - Sau khi test thành công, **bật switch `Active`** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**
   - Sau khi email được gửi, có thể **gửi thông báo** về Slack/Telegram để các sếp biết workflow đã hoàn thành.
   - **Cách làm**:
     - Thêm node **`slack`** hoặc **`telegram`** sau node `gmail`.
     - Gửi tin nhắn: `"Email đã được gửi thành công cho: {{ $json.output.email }}"`.

2. **Lưu Log Tất Cả Email Đã Gửi**
   - Thêm node **`googleSheets`** hoặc **`airtable`** để lưu **tất cả email đã tự động gửi**.
   - **Cách làm**:
     - Sau node `gmail`, thêm node **`googleSheets`** với schema:
       ```json
       {
         "email_sent_at": "datetime",
         "recipient": "string",
         "subject": "string",
         "status": "string"
       }
       ```
   - **Lợi ích**: Dễ dàng **theo dõi và báo cáo** hoạt động của workflow.

3. **Tự Động Xóa Tin Nhắn Âm Thanh Sau Khi Xử Lý**
   - Thêm node **`telegram`** với **`operation: delete`** để xóa tin nhắn âm thanh sau khi chuyển thành email.
   - **Lưu ý**: Cần **cấu hình quyền** cho bot để có thể xóa tin nhắn.

4. **Cấu Hình Thời Gian Chờ Động**
   - Nếu workflow **bị tràn tin nhắn**, có thể **tăng thời gian chờ** trong node `wait` (ví dụ: 10-30 giây).
   - **Cách làm**:
     - Trong node `wait`, thay đổi **`time`** từ `5000ms` (5s) thành `10000ms` (10s).

5. **Sử Dụng AI Agent Tùy Chỉnh**
   - Nếu muốn **AI viết email theo phong cách riêng**, hãy **cập nhật prompt** trong node `agent`:
     - Ví dụ: `"Viết email theo phong cách chính thức của công ty [Tên Công Ty]"`.
     - Hoặc: `"Tránh sử dụng từ ngữ quá thân mật, sử dụng HTML với font Arial 12px"`.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và nhân viên khỏi việc **nghe tin nhắn âm thanh và viết email thủ công**, đồng thời **tăng cường chuyên nghiệp hóa liên lạc** với khách hàng và đồng nghiệp.

**Bước đầu tiên:**
1. **Cài đặt n8n trên VPS** (khuyến nghị).
2. **Import workflow** và **cấu hình các credential** (Telegram, OpenAI, Gmail).
3. **Test với tin nhắn mẫu** và **bật Active**.

**Kết quả:**
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Email luôn chuyên nghiệp**, không lỗi chính tả.
- **Hoạt động 24/7**, không bỏ lỡ tin nhắn nào.

**Hãy áp dụng ngay và tự động hóa liên lạc doanh nghiệp của mình!** 🚀

---
**Cần hỗ