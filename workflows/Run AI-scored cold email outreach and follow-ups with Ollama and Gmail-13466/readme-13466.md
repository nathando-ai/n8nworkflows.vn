---
title: "🚀 Tự Động Hóa Outreach Lạnh AI với Ollama & Gmail: Scoring, Email Cá Nhân Hóa & Follow-up Tự Động"
description: "Workflow tự động hóa hoàn toàn pipeline outreach lạnh: nghiên cứu lead, đánh giá AI, viết email cá nhân hóa, gửi email, theo dõi phản hồi và tự động hóa follow-up - tất cả từ Google Sheets. Giúp tiết kiệm 10+ giờ/tuần cho các sếp bán hàng và marketing."
slug: "tieu-dong-hoa-outreach-lanh-ai-ollama-gmail"
tags: [n8n, automation, lead-nurturing, ai-summarization, ollama, gmail, telegram-notification, google-sheets]
keywords: [n8n workflow outreach lạnh, tự động hóa email cá nhân hóa, scoring lead AI, follow-up tự động, Ollama với n8n, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Outreach Lạnh AI: Scoring Lead, Email Cá Nhân Hóa & Follow-up Tự Động**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Làm thủ công** việc nghiên cứu lead, viết email cá nhân hóa và theo dõi phản hồi?
- **Tốn thời gian** để đánh giá lead phù hợp và quyết định ai là khách hàng tiềm năng thực sự?
- **Quên follow-up** sau khi gửi email đầu tiên, dẫn đến mất cơ hội?
- **Không biết** liệu email của mình đã được đọc hay không?

Workflow này **tự động hóa toàn bộ quy trình outreach lạnh** từ A đến Z, giúp bạn:
✅ **Tiết kiệm 10+ giờ/tuần** bằng cách loại bỏ công việc lặp đi lặp lại.
✅ **Tăng tỷ lệ chuyển đổi** với email cá nhân hóa dựa trên dữ liệu nghiên cứu.
✅ **Đánh giá lead chính xác** bằng AI (scoring từ 0-100).
✅ **Theo dõi phản hồi tự động** và ngừng tiếp xúc với lead đã trả lời.
✅ **Nhận thông báo Telegram** tại mỗi bước quan trọng (gửi email, phản hồi, bỏ qua lead).

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% pipeline outreach lạnh** (không cần viết code).
- **Email cá nhân hóa cao độ** dựa trên thông tin nghiên cứu từ website lead.
- **Scoring lead AI** (đánh giá lead từ 0-100) để tập trung vào khách hàng tiềm năng.
- **Follow-up tự động** (Email 2 sau 3 ngày, Email 3 sau 7 ngày).
- **Phát hiện phản hồi tự động** và ngừng tiếp xúc với lead đã trả lời.
- **Nhận thông báo Telegram** tại mỗi bước (gửi email, phản hồi, bỏ qua lead).
- **Lưu trữ dữ liệu** trên Google Sheets để theo dõi toàn bộ quá trình.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với bảng dữ liệu chứa các cột:
   - `Lead Name` (Tên lead)
   - `Email` (Email lead)
   - `Company` (Công ty)
   - `Website` (Website của lead)
   - `Role/Title` (Vị trí/Chức vụ)
   - `Status` (Trạng thái: "New", "Sent", "Follow-up", "Replied", "Skipped")
   - `Reply Date` (Ngày phản hồi)
   - `Reply Subject` (Chủ đề phản hồi)
   - `Reply Snippet` (Đoạn trích phản hồi)

2. **Tài khoản Gmail** (để gửi email) với **OAuth2** được cấu hình trong n8n.
3. **Tài khoản Telegram** để nhận thông báo (cần `CHAT_ID`).
4. **Ollama** (hoặc OpenAI/Anthropic) với mô hình AI đã cài đặt (ví dụ: `llama3`).
5. **Thời gian** để cấu hình và test workflow (khoảng 30-60 phút).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13466](https://n8n.io/workflows/13466) (chọn "Export as JSON").
2. Trong n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/13466](https://n8n.io/workflows/13466) (chọn "Export as JSON").
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán mã.
3. Chọn **"Import"** để hoàn tất.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và cần cấu hình cẩn thận. Dưới đây là các bước **quan trọng nhất**:

#### **🔹 1. Cấu Hình Credentials**
- **Google Sheets**:
  - Thiết lập credential với quyền truy cập vào bảng dữ liệu.
  - Đảm bảo bảng có **các cột bắt buộc** như trên (nếu thiếu, workflow sẽ lỗi).

- **Gmail**:
  - Cấu hình OAuth2 với tài khoản Gmail sẽ gửi email.
  - **Lưu ý**: Đặt **sender name** trong node **"Extract Emails"** (line 12) và **"Find Follow-ups"** (line 9) là tên hiển thị của email (ví dụ: "Tony Adijah").

- **Telegram**:
  - Cấu hình credential với `CHAT_ID` của bạn (để nhận thông báo).
  - Thay thế `YOUR_TELEGRAM_CHAT_ID` trong tất cả các node Telegram.

- **Ollama**:
  - Cài đặt mô hình AI (ví dụ: `llama3`) và cấu hình credential.
  - **Lưu ý**: Thay thế `YOUR_MODEL_NAME` trong node **"Ollama Scorer"** và **"Ollama Writer"** thành tên mô hình của bạn (ví dụ: `llama3`).

#### **🔹 2. Cấu Hình AI Lead Scorer & Email Writer**
Workflow sử dụng **AI Agent** để:
- **Đánh giá lead** (scoring từ 0-100).
- **Viết email cá nhân hóa**.

**Cần chỉnh sửa 2 node quan trọng**:
1. **Node "AI Lead Scorer" (Agent)**:
   - Mở node này và chỉnh sửa **system prompt** để phù hợp với:
     - Sản phẩm của bạn.
     - ICP (Ideal Customer Profile) của bạn.
     - Tiêu chí đánh giá lead (ví dụ: "Lead có vai trò quyết định không?", "Công ty có ngân sách không?").

2. **Node "AI Email Writer" (Agent)**:
   - Chỉnh sửa **system prompt** để bao gồm:
     - Tên và vị trí của bạn.
     - Giá trị của sản phẩm/dịch vụ.
     - Cách viết email cá nhân hóa (ví dụ: "Nêu tên công ty và vai trò của lead").

#### **🔹 3. Cấu Hình Threshold Scoring**
- Trong node **"Extract Score"**, thay đổi **threshold** (ngưỡng đánh giá) từ `40` thành số phù hợp với bạn (ví dụ: `50` để chỉ gửi email cho lead có độ phù hợp cao).
- **Lưu ý**: Lead có score < threshold sẽ được **bỏ qua** (status = "Skipped").

#### **🔹 4. Cấu Hình Follow-up**
- Trong node **"Find Follow-ups"**, chỉnh sửa logic để:
  - Email 2 được gửi sau **3 ngày**.
  - Email 3 được gửi sau **7 ngày**.
  - **Lưu ý**: Cần chỉnh sửa **cron schedule** trong node **"Every 2hrs — Follow-ups"** để phù hợp với giờ Việt Nam (ví dụ: `0 0/2 * * 1-5` để chạy từ thứ 2 đến thứ 6).

#### **🔹 5. Cấu Hình Reply Detection**
- Trong node **"Filter Active Leads"** và **"Check Reply Results"**, thay thế `your-email@gmail.com` thành **email của bạn** để workflow **không nhầm lẫn email của bạn với phản hồi**.
- **Lưu ý**: Nếu email của bạn có tên miền khác (ví dụ: `tony@company.com`), thay thế hoàn toàn.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Thêm 1-2 lead vào Google Sheets với trạng thái `"New"`.
   - Chạy workflow và kiểm tra:
     - Email có được gửi không?
     - AI có đánh giá lead không?
     - Telegram có thông báo không?

2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho workflow.
   - Kiểm tra **log** trong n8n để đảm bảo không có lỗi.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thay vì chỉ Telegram, thêm **Slack** để nhận thông báo trong nhóm công việc.

2. **Lưu log hoạt động**:
   - Sử dụng node **StickyNote** để lưu trữ log của workflow (ví dụ: "Email gửi vào lúc 9:00 AM").

3. **Báo cáo định kỳ**:
   - Tạo một **báo cáo hàng tuần** tự động (ví dụ: "Tỷ lệ mở email", "Tỷ lệ phản hồi") và gửi qua email.

4. **Tích hợp CRM**:
   - Nếu dùng **HubSpot, Salesforce** hoặc **Zoho CRM**, thay thế Google Sheets bằng API của CRM để đồng bộ dữ liệu.

5. **Chỉnh sửa mô hình AI**:
   - Nếu Ollama không phù hợp, thử **OpenAI (GPT-4)** hoặc **Anthropic (Claude)** với node `@n8n/n8n-nodes-openai`.

6. **Tự động hóa thêm**:
   - Thêm **node "ScheduleTrigger"** để chạy workflow vào giờ làm việc (ví dụ: 8h sáng).
   - Thêm **node "Webhook"** để nhận lead từ form website và tự động thêm vào Google Sheets.
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng bạn khỏi công việc outreach lạnh mệt mỏi**, giúp tập trung vào **quan trọng hơn**: xây dựng mối quan hệ và đóng gói deal.

**Bắt đầu ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Cấu hình credentials** và chỉnh sửa AI prompts.
3. **Test và bật workflow** để tự động hóa pipeline outreach của bạn.

:::tip[LƯU Ý CUỐI CUNG]
- **Không có workflow nào hoàn hảo**: Cần điều chỉnh theo nhu cầu cụ thể của bạn.
- **Dữ liệu là vàng**: Luôn cập nhật Google Sheets để workflow hoạt động chính xác.
- **Học từ AI**: Nếu email không hiệu quả, chỉnh sửa **system prompt** của AI để cải thiện.

**Chúc các sếp thành công với outreach lạnh tự động hóa!** 🚀
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::