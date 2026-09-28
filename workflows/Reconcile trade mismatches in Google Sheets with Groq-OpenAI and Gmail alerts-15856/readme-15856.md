---
title: "🔍 **Tự Động Hóa Khớp Lại Giao Dịch (Reconciliation) Trên Google Sheets Với AI Groq-OpenAI & Cảnh Báo Email Tự Động**"
description: "Workflow này tự động khớp lại giao dịch giữa hệ thống nội bộ và bên thứ ba bằng Google Sheets, phát hiện sai sót (giá, số lượng, số tiền), phân loại mức độ nghiêm trọng, và sử dụng AI Groq-OpenAI để phân tích lý do và đề xuất giải pháp. Kết quả được cập nhật tự động và gửi cảnh báo email chi tiết để các sếp tiết kiệm thời gian và giảm thiểu lỗi thủ công."
slug: "tieu-dong-hoa-khop-lai-giao-dich-google-sheets-groq-openai"
tags: [n8n, automation, google-sheets, groq-openai, ai-summarization, reconciliation, gmail-alerts]
keywords: [tự động hóa khớp lại giao dịch, n8n workflow google sheets, groq openai trong n8n, cảnh báo email tự động, giải quyết sai sót giao dịch, AI phân tích dữ liệu tài chính]
---

# 🚀 **Tự Động Hóa Khớp Lại Giao Dịch (Reconciliation) Trên Google Sheets Với AI Groq-OpenAI**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất nhiều thời gian thủ công để khớp lại giao dịch giữa hệ thống nội bộ và bên thứ ba (như ngân hàng, đối tác thương mại). Các sai sót như giá, số lượng, hoặc số tiền không khớp thường được phát hiện muộn, gây ra rủi ro tài chính và mất thời gian giải quyết. Ngoài ra, việc phân tích lý do sai sót và đề xuất giải pháp cũng là một công việc phức tạp, đòi hỏi sự chuyên môn cao.

Workflow này **giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình khớp lại giao dịch**, sử dụng AI Groq-OpenAI để phân tích và đề xuất giải pháp, đồng thời gửi cảnh báo email chi tiết để các sếp có thể xử lý nhanh chóng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công khớp lại hàng ngàn giao dịch mỗi tháng.
- **Chính xác 100%**: Phát hiện sai sót ngay từ đầu, giảm thiểu lỗi tài chính.
- **Phân tích AI sâu**: Groq-OpenAI tự động phân tích lý do sai sót và đề xuất giải pháp.
- **Cảnh báo email tự động**: Nhận thông báo chi tiết về các giao dịch không khớp hoặc thiếu.
- **Dữ liệu được cập nhật tự động**: Kết quả khớp lại được ghi lại trên Google Sheets, dễ theo dõi và kiểm tra.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng tính **Internal Trades** (gồm cột `trade_id`, `price`, `quantity`, `amount`, `date`).
   - Một bảng tính **External Trades** (cấu trúc tương tự, dùng để so sánh với Internal Trades).
   - **API Key OAuth 2.0** cho Google Sheets (cài đặt tại [Google Cloud Console](https://console.cloud.google.com/)).

2. **Tài khoản Gmail**:
   - Tài khoản Gmail để gửi cảnh báo email tự động (cần **OAuth 2.0 API Key**).

3. **API Key Groq/OpenAI**:
   - **Groq API Key** (đăng ký tại [Groq](https://groq.com/)).
   - Model được sử dụng: `openai/gpt-oss-120b` (mô hình AI mạnh mẽ để phân tích).

4. **N8n Self-Hosted**:
   - Để workflow hoạt động 24/7, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/15856](https://n8n.io/workflows/15856).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong Editor.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **18 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

#### **🔹 Node "Groq Chat Model" (AI Groq-OpenAI)**
- **Credentials**: Chọn `groqApi` (đã cấu hình trước khi import).
- **Model**: Đảm bảo chọn `openai/gpt-oss-120b` (không thay đổi).
- **Prompt**: Workflow tự động cấu hình, các sếp không cần chỉnh sửa (nếu muốn tùy chỉnh, cần biết code Python).

#### **🔹 Node "Fetch Internal Trades" & "Fetch External Trades" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Điền tên chính xác của bảng tính (ví dụ: `Internal_Trades` và `External_Trades`).
- **Range**: Điền `Sheet1!A:Z` (hoặc phạm vi dữ liệu cụ thể).
- **Lưu ý**: Cột `trade_id` **phải trùng khớp** giữa hai bảng để workflow so sánh được.

#### **🔹 Node "Merge Internal & External Trades" (Merge)**
- Workflow tự động gộp hai bảng theo `trade_id`, các sếp không cần chỉnh sửa.

#### **🔹 Node "Detect Trade Breaks" & "Classify Severity" (Code)**
- Đây là **hai node JavaScript** tự động phát hiện sai sót và phân loại mức độ nghiêm trọng (Low/Medium/High).
- **Không cần chỉnh sửa** nếu dữ liệu đầu vào đúng cấu trúc.

#### **🔹 Node "Generate AI Reconciliation Insight" (Agent)**
- Node này gửi dữ liệu sai sót đến **Groq-OpenAI** để AI phân tích lý do và đề xuất giải pháp.
- **Lưu ý**: Nếu API Groq gặp lỗi, kiểm tra lại **API Key** và **quota** (Groq có giới hạn free tier).

#### **🔹 Node "Send Trade Break Alert Email" & "Send Missing Trade Alert Email" (Gmail)**
- **Credentials**: Chọn `gmailOAuth2`.
- **To**: Điền email của người nhận cảnh báo (ví dụ: `team@doanhnghiep.com`).
- **Subject**: Workflow tự động cấu hình, các sếp có thể chỉnh sửa nếu muốn.
- **Body**: Nội dung email bao gồm:
  - **Trade ID** không khớp.
  - **Lý do sai sót** (do AI Groq phân tích).
  - **Mức độ nghiêm trọng** (Low/Medium/High).
  - **Giải pháp đề xuất**.

#### **🔹 Node "Update Internal Trades Sheet" & "Update External Trades Sheet" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Range**: Điền `Sheet1!A:Z` (phạm vi cập nhật).
- **Lưu ý**: Workflow sẽ **cập nhật cột `status`** (ví dụ: `Reconciled`, `Mismatch`, `Missing`).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và chọn **Manual Trigger**.
   - Kiểm tra các node quan trọng (AI, Gmail, Google Sheets) có hoạt động không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ `Inactive` sang `Active`.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì chỉ gửi email, các sếp có thể **gửi cảnh báo trên Slack/Telegram** bằng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
   - **Cách làm**: Thêm node `Slack Webhook` sau node `Gmail` và cấu hình webhook từ Slack.

2. **Lưu Log Lịch Sử**:
   - Sử dụng node `n8n-nodes-base.database` (SQLite) hoặc `n8n-nodes-base.googleDrive` để lưu lại lịch sử khớp lại giao dịch.
   - **Lợi ích**: Dễ dàng theo dõi và phân tích xu hướng sai sót.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng node `n8n-nodes-base.cron` để chạy workflow **hàng ngày/tuần** và gửi báo cáo tổng hợp qua email.
   - **Cách làm**: Thêm node `Cron` trước `Manual Trigger` và cấu hình lịch chạy.

4. **Tùy Chỉnh AI Prompt**:
   - Nếu muốn AI Groq phân tích chi tiết hơn, các sếp có thể chỉnh sửa **prompt** trong node `lmChatGroq` bằng code JavaScript (node `Code`).
   - **Ví dụ**:
     ```javascript
     // Thêm vào node "Detect Trade Breaks" hoặc "Classify Severity"
     const prompt = `Analyze the following trade mismatch:
     - Trade ID: {{ $node["Merge Internal & External Trades"].json["$nodeId"].trade_id }}
     - Internal Price: {{ $node["Merge Internal & External Trades"].json["$nodeId"].internal_price }}
     - External Price: {{ $node["Merge Internal & External Trades"].json["$nodeId"].external_price }}
     - Difference: {{ $node["Merge Internal & External Trades"].json["$nodeId"].difference }}
     Provide a detailed explanation of the cause and suggest a resolution.`;
     ```
:::

---

## 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn tự động hóa quy trình khớp lại giao dịch**, giúp các sếp:
✅ **Tiết kiệm thời gian** (không cần thủ công khớp lại hàng ngàn giao dịch).
✅ **Giảm thiểu lỗi** (AI phát hiện và phân tích sai sót chính xác).
✅ **Cập nhật dữ liệu tự động** (Google Sheets luôn đồng bộ).
✅ **Nhận cảnh báo kịp thời** (email/Slack với chi tiết giải pháp).

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test run** và bật **Active** để tự động hóa khớp lại giao dịch!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/15856) và bắt đầu tự động hóa ngay!