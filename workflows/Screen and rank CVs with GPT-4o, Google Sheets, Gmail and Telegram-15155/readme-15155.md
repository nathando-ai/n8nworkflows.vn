---
title: "🤖 **Tự Động Xếp Hạng & Lọc CV với GPT-4o, Google Sheets, Gmail & Telegram – Giải Pháp HR Không Code**"
description: "Workflow tự động hóa lọc, xếp hạng và xử lý ứng viên dựa trên CV (PDF/DOCX) với AI GPT-4o, gửi email mời phỏng vấn hoặc từ chối, đồng thời báo cáo ngay cho HR qua Telegram. Tiết kiệm 80% thời gian tuyển dụng!"
slug: "tieu-dong-xep-hang-cv-voi-gpt-4o-google-sheets-gmail-telegram"
tags: [n8n, automation, hr, ai-summarization, gpt-4o, google-sheets, gmail, telegram]
keywords: [n8n workflow tuyển dụng, tự động hóa lọc cv, gpt-4o xếp hạng ứng viên, gửi email tự động từ chối mời phỏng vấn, báo cáo hr qua telegram]
---

# 🚀 **Tự Động Xếp Hạng & Lọc CV với AI GPT-4o – Giải Pháp HR Không Code**

### **Nỗi Đau Của Các Sếp Trong Việc Tuyển Dụng**
Hàng ngày, bộ phận HR phải:
✅ **Quét hàng trăm CV** (PDF/DOCX) thủ công để tìm kiếm ứng viên phù hợp.
✅ **Xếp hạng và đánh giá** dựa trên yêu cầu công việc, mất nhiều thời gian.
✅ **Gửi email mời phỏng vấn/từ chối** một cách cá nhân hóa, dễ gây lỗi.
✅ **Báo cáo cho lãnh đạo** về tình hình tuyển dụng, nhưng thường bị trì hoãn.

**Workflow này giải quyết tất cả!** Sử dụng **AI GPT-4o** để tự động:
- **Lọc và xếp hạng** CV theo yêu cầu công việc.
- **Gửi email tự động** mời phỏng vấn (hoặc từ chối) cho ứng viên.
- **Báo cáo ngay cho HR** qua Telegram khi có ứng viên ưu tiên.
- **Lưu trữ dữ liệu** vào Google Sheets để theo dõi và phân tích.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong việc lọc CV thủ công.
- **Xếp hạng chính xác** dựa trên AI GPT-4o, không bị chủ quan.
- **Gửi email tự động** (mời phỏng vấn/từ chối) với nội dung cá nhân hóa.
- **Báo cáo ngay cho HR** qua Telegram khi có ứng viên ưu tiên.
- **Lưu trữ dữ liệu** vào Google Sheets để phân tích sau này.
- **Không cần code**, chỉ cần cấu hình đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để kết nối **Google Sheets** và **Gmail**).
✔ **API Key OpenAI** (để sử dụng **GPT-4o** trong việc lọc CV).
✔ **Bot Telegram** (để báo cáo cho HR).
✔ **Địa chỉ email chính thức** (để gửi email mời/từ chối).

---
:::note[Cách lấy API Key]
- **OpenAI API Key**:
  - Đăng ký tại [OpenAI](https://platform.openai.com/) → **API Keys** → Copy key.
- **Google Sheets OAuth2**:
  - Tạo dự án tại [Google Cloud Console](https://console.cloud.google.com/) → **APIs & Services** → **Credentials** → **Create OAuth Client ID**.
- **Gmail OAuth2**:
  - Cùng bước như Google Sheets, nhưng chọn **Gmail API**.
- **Telegram Bot Token**:
  - Trên Telegram, tìm bot `@BotFather` → `/newbot` → Nhận **API Token**.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/15155](https://n8n.io/workflows/15155) → **Import** vào n8n Editor.
- **Copy JSON** từ link trên → **Paste** vào n8n Editor (tab **Import/Export**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **16 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

##### **A. Cấu Hình Webhook Nhận CV (Receive CV Webhook)**
- **Node**: `Receive CV Webhook`
- **Cấu hình**:
  - **HTTP Method**: `POST`
  - **Path**: `cv-screening` (không đổi)
  - **Credentials**: Không cần (sử dụng URL mặc định của n8n).

**Lưu ý**:
- Các ứng viên sẽ gửi CV qua **URL này** (ví dụ: `https://tên-vps-của-bạn.n8n.workers.dev/cv-screening`).
- **Test**: Gửi một file mẫu (PDF/DOCX) từ Postman hoặc ứng dụng nội bộ để kiểm tra.

##### **B. Kết Nối Gmail (Send Interview Invite / Rejection Email)**
- **Node**: `Send Interview Invite Email` & `Send Rejection Email`
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
  - **Email From**: Địa chỉ email chính thức của công ty.
  - **Template Email**:
    - **Mời phỏng vấn**:
      ```plaintext
      Chào [Tên Ứng Viên],

      Chúng tôi rất vui mừng thông báo rằng CV của bạn đã được lọc vào danh sách ứng viên ưu tiên cho vị trí [Tên Công Việc].

      Thời gian phỏng vấn: [Ngày/Giờ]
      Địa điểm: [Địa chỉ/Nội dung]

      Xin cảm ơn và chúc bạn một ngày tốt lành!
      ```
    - **Từ chối**:
      ```plaintext
      Chào [Tên Ứng Viên],

      Sau khi đánh giá kỹ lưỡng, chúng tôi quyết định không tiếp tục quá trình tuyển dụng với bạn cho vị trí [Tên Công Việc].

      Chúng tôi rất trân trọng thời gian của bạn và mong bạn sẽ thành công trong tương lai!
      ```

##### **C. Kết Nối Google Sheets (Read/Append Data)**
- **Node**: `Read Job Requirements` & `Append Top Candidates` & `Archive Candidate Data`
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Tạo một sheet mới với **các cột**:
    - `Job Title` (Tên công việc)
    - `Candidate Name` (Tên ứng viên)
    - `Score` (Điểm xếp hạng)
    - `Status` (Mời/From chối)
    - `Email` (Email liên lạc)
    - `CV File` (Link file CV)
  - **Operation**:
    - `Read Job Requirements`: Chọn **tab "Yêu cầu công việc"** (để AI so sánh).
    - `Append Top Candidates`: Chọn **tab "Ứng viên ưu tiên"**.
    - `Archive Candidate Data`: Chọn **tab "Lịch sử ứng viên"**.

##### **D. Kết Nối OpenAI (AI Screening Model)**
- **Node**: `AI Screening Model`
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `gpt-4o` (hoặc `gpt-4` nếu không có).
  - **Prompt Template** (cần chỉnh sửa để phù hợp):
    ```plaintext
    Bạn là một chuyên gia tuyển dụng. Đọc yêu cầu công việc sau và CV của ứng viên. Xếp hạng ứng viên từ 1-10 dựa trên phù hợp với yêu cầu.

    **Yêu cầu công việc**:
    {{jobRequirements}}

    **CV của ứng viên**:
    {{candidateCV}}

    **Cách đánh giá**:
    - Kỹ năng: 40%
    - Kinh nghiệm: 30%
    - Trình độ ngôn ngữ: 20%
    - Động cơ: 10%

    **Kết quả phải trả về dưới dạng JSON**:
    {
      "score": [số điểm từ 1-10],
      "feedback": "Lý do xếp hạng (tối đa 200 ký tự)"
    }
    ```

##### **E. Cấu Hình Telegram (Send HR Alert)**
- **Node**: `Send HR Alert on Telegram`
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi`.
  - **Chat ID**: ID của bot Telegram (để tìm, gửi tin nhắn cho bot và copy ID từ phản hồi).
  - **Message Template**:
    ```plaintext
    🚨 **Ứng viên mới ưu tiên** 🚨
    - **Tên**: {{candidateName}}
    - **Điểm**: {{score}}/10
    - **Vị trí**: {{jobTitle}}
    - **Email**: {{email}}
    - **CV**: [Link]({{cvFile}})
    ```

##### **F. Node Code (Parse DOCX/PDF & Validate Input)**
- **Node**: `Parse DOCX CV`, `Parse PDF CV`, `Generate CV Text`, `Validate CV Input`, `Check for Duplicates`
- **Lưu ý**:
  - Các node này **không cần chỉnh sửa** (n8n tự động xử lý).
  - **Validate CV Input**: Kiểm tra file có đúng định dạng (PDF/DOCX) hay không.
  - **Check for Duplicates**: So sánh email/ten ứng viên đã tồn tại trong Google Sheets.

##### **G. Cấu Hình Score Threshold (Check Score Threshold)**
- **Node**: `Check Score Threshold`
- **Cấu hình**:
  - **Condition**: `{{$json["score"]}} >= [số điểm ngưỡng]` (ví dụ: `>= 7`).
  - **Nếu đúng**: Chuyển sang **Send Interview Invite**.
  - **Nếu sai**: Chuyển sang **Send Rejection Email**.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một file CV mẫu (PDF/DOCX) qua Webhook.
  - Kiểm tra:
    - AI có xếp hạng đúng không?
    - Email có được gửi không?
    - Telegram có báo cáo không?
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và chia sẻ **URL Webhook** cho ứng viên gửi CV.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi báo cáo hàng tuần** cho HR:
   - Sử dụng **node `set`** để lưu ngày tháng.
   - Thêm **node `schedule`** (n8n Pro) để gửi báo cáo định kỳ.

2. **Kết hợp với Slack**:
   - Thay vì Telegram, có thể báo cáo qua **Slack** bằng node `slack`.

3. **Lưu log chi tiết**:
   - Thêm **node `stickyNote`** để ghi lại lỗi hoặc thông tin debug.

4. **Cải thiện Prompt AI**:
   - Nếu AI xếp hạng không chính xác, **cập nhật lại Prompt** trong node `AI Screening Model`.

5. **Tự động xóa CV sau khi xử lý**:
   - Thêm **node `deleteFile`** (n8n Pro) để xóa file CV sau khi xử lý.

---

### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của bộ phận HR trong việc lọc CV thủ công. Với **AI GPT-4o**, các sếp có thể:
✅ **Xếp hạng chính xác** ứng viên dựa trên yêu cầu công việc.
✅ **Gửi email tự động** (mời/from chối) một cách cá nhân hóa.
✅ **Báo cáo ngay cho HR** qua Telegram khi có ứng viên ưu tiên.
✅ **Lưu trữ dữ liệu** để phân tích sau này.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các API.
3. **Test với file CV mẫu** và bắt đầu tự động hóa tuyển dụng!

**🚀 Cùng tự động hóa HR của bạn ngay hôm nay!** 🚀