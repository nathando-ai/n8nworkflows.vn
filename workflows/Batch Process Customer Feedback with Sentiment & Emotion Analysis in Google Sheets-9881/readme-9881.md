---
title: "🤖 Tự Động Hóa Phân Tích Sentiment & Emotion cho Phản Hồi Khách Hàng trên Google Sheets với AI (OpenAI)"
description: "Workflow tự động hóa phân tích, gán nhãn và phân loại cảm xúc cho hàng ngàn phản hồi khách hàng trên Google Sheets chỉ trong vài phút, tiết kiệm thời gian lên đến 90% so với cách làm thủ công. Kết quả bao gồm tags, phân tích sentiment từ 'Very Negative' đến 'Very Positive', và phát hiện cảm xúc chính/phụ (happy, frustrated, grateful...)."
slug: "tieu-dong-hoa-phan-tich-sentiment-emotion-google-sheets"
tags: [n8n, automation, ai-summarization, google-sheets, openai, sentiment-analysis, no-code, market-research]
keywords: [n8n workflow tự động hóa, phân tích cảm xúc khách hàng, sentiment analysis google sheets, tự động gán nhãn phản hồi, openai n8n, tự động hóa market research]
---

# 🚀 **Tự Động Hóa Phân Tích Sentiment & Emotion cho Phản Hồi Khách Hàng trên Google Sheets**

## **💥 Nỗi Đau Của Các Sếp: Phân Tích Hàng Ngàn Phản Hồi Khách Hàng Thủ Công?**
Hàng ngày, các sếp phải đối mặt với **hàng trăm phản hồi khách hàng** trên Google Forms, email, hoặc hệ thống CRM. Để phân tích và gán nhãn (tagging) chúng thủ công là **một công việc tẻ nhạt, mất thời gian, và dễ sai sót**. Kết quả thường chỉ là một danh sách dài không phân loại, không thể đưa ra quyết định nhanh chóng.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động hóa 100% quá trình phân tích** với AI OpenAI
✅ **Gán nhãn tự động** cho phản hồi với **sentiment** (từ "Very Negative" đến "Very Positive") và **cảm xúc chính/phụ** (happy, frustrated, grateful...)
✅ **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công
✅ **Cập nhật kết quả ngay trên Google Sheets**, sẵn sàng để phân tích sâu hơn

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phân tích từng phản hồi một, AI làm việc 24/7.
- **Chính xác cao**: Phân tích sentiment và cảm xúc dựa trên mô hình AI tiên tiến của OpenAI.
- **Cá nhân hóa & phân loại**: Mỗi phản hồi được gán **3 nhãn chính** và **2 nhãn phụ** (nếu cần).
- **Hoạt động liên tục**: Bật chế độ tự động (Schedule Trigger) để cập nhật mới mỗi 60 phút.
- **Dữ liệu sẵn sàng phân tích**: Kết quả được lưu trên Google Sheets với định dạng chuẩn, dễ dàng export vào Power BI, Tableau, hoặc Notion.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với **2 bảng dữ liệu**:
   - **Bảng "Tags"**: Danh sách các nhãn (tags) cho phép phân tích (ví dụ: "Hài lòng", "Không hài lòng", "Yêu cầu cải thiện").
   - **Bảng "Feedbacks"**: Danh sách phản hồi khách hàng (cột `Feedbacks` chứa nội dung phản hồi, cột `Status` để theo dõi trạng thái).
2. **API Key OpenAI**: Đăng ký tại [OpenAI](https://platform.openai.com/) và thêm vào n8n dưới tên `openAiApi`.
3. **Credentials Google Sheets OAuth2**: Cấu hình trong n8n dưới tên `googleSheetsOAuth2Api`.
4. **File mẫu Google Sheets**: [Tải template](https://docs.google.com/spreadsheets/d/1y7B3u5vgQLDidf-NdfPgAiBuQxP9Qa7RvdgsTPG14Fs/edit?usp=sharing) và sao chép để sử dụng.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/9881](https://n8n.io/workflows/9881) (chọn "Download JSON").
- **Nhập vào n8n**:
  - Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON vừa tải.
  - Hoặc copy toàn bộ JSON và dán vào **"Import Workflow"** trong n8n.

:::note[LƯU Ý]
- **Không sao chép toàn bộ JSON trong mảng `{ "output": ... }`**, chỉ copy phần cấu trúc workflow.
- Nếu import từ file, **không cần chỉnh sửa JSON** nếu đã sao chép template Google Sheets chính xác.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **📌 Node "Fetch Allowed Tags" (Lấy Danh Sách Nhãn Cho Phép)**
- **Cấu hình**:
  - **Google Sheets URL**: Điền link của bảng **"Tags"** (cột duy nhất là `Tags`).
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Điền tên của sheet (ví dụ: `"Tags"`).
  - **Range**: Điền `"Tags!A:A"` (giả sử cột A chứa danh sách nhãn).
- **Kiểm tra**: Chạy node này riêng để đảm bảo lấy được danh sách nhãn.

#### **📌 Node "Fetch New Feedbacks" (Lấy Phản Hồi Mới)**
- **Cấu hình**:
  - **Google Sheets URL**: Điền link của bảng **"Feedbacks"**.
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Điền tên của sheet (ví dụ: `"Feedbacks"`).
  - **Range**: Điền `"Feedbacks!A:Z"` (lấy toàn bộ dữ liệu).
  - **Filter**: Thêm điều kiện `Status = ""` (chỉ lấy phản hồi chưa được phân tích).
- **Kiểm tra**: Chạy node này riêng để đảm bảo lấy được phản hồi mới.

#### **📌 Node "Tag Feedbacks with OpenAI" (Phân Tích với AI)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `gpt-3.5-turbo` (hoặc `gpt-4` nếu có budget).
  - **System Prompt**: Sử dụng prompt mặc định (nếu muốn thay đổi, cập nhật ở đây):
    ```json
    "You are a sentiment and emotion analysis assistant. Your task is to analyze customer feedback and tag it with up to 3 allowed tags from the provided list. If no allowed tags match, suggest up to 2 new tags. Also, classify sentiment (Very Negative to Very Positive) and detect primary and secondary emotions."
    ```
  - **Input Format**: Chọn `JSON` (đảm bảo dữ liệu đầu vào là mảng JSON).
  - **Output Format**: Chọn `JSON` (đảm bảo kết quả là JSON).
- **Lưu ý**:
  - **Batch Size**: Mặc định là 10 phản hồi/lần gọi API (tối ưu hóa chi phí).
  - **Multilingual Support**: Workflow hỗ trợ phân tích phản hồi bằng nhiều ngôn ngữ, bao gồm **Tiếng Việt, Tiếng Anh, Tiếng Pháp, Tiếng Nhật...**

#### **📌 Node "Update Google Sheet (Tagged)" (Cập Nhật Kết Quả)**
- **Cấu hình**:
  - **Google Sheets URL**: Điền link của bảng **"Feedbacks"**.
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Điền tên của sheet (ví dụ: `"Feedbacks"`).
  - **Range**: Điền `"Feedbacks!A:Z"` (cập nhật toàn bộ cột).
  - **Operation**: Chọn `update`.
  - **Update Columns**: Chọn tất cả cột cần cập nhật (`Tag 1`, `Tag 2`, `Tag 3`, `AI Tag 1`, `Sentiment`, `Primary Emotion`, `Secondary Emotion`, `Status`, `Updated Date (N8N)`).
- **Kiểm tra**: Chạy node này riêng để đảm bảo cập nhật dữ liệu chính xác.

#### **📌 Node "Schedule Trigger" (Chế Độ Tự Động)**
- **Cấu hình**:
  - **Schedule**: Chọn `Every 60 minutes` (hoặc điều chỉnh theo nhu cầu).
  - **Timezone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - **Không cần kích hoạt ngay**, chỉ kích hoạt khi đã kiểm tra toàn bộ workflow.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (kiểm tra dữ liệu mẫu):
   - Chạy node **"Manual Trigger"** để kiểm tra workflow với một batch nhỏ (ví dụ: 3-5 phản hồi).
   - Kiểm tra kết quả trên Google Sheets:
     - Cột `Status` sẽ được cập nhật thành `"Updated"` (nếu thành công) hoặc `"Needs Review"` (nếu AI không tìm thấy nhãn phù hợp).
     - Cột `Tag 1-3` và `AI Tag 1-2` sẽ chứa kết quả phân tích.
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, kích hoạt **Schedule Trigger** để workflow chạy tự động mỗi 60 phút.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Hợp với Slack/Telegram để Báo Cáo Kết Quả**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node **"Update Google Sheet"** để gửi thông báo khi có phản hồi mới được phân tích.
- **Cách làm**:
  1. Thêm node **Slack Webhook** (hoặc **Telegram Bot**).
  2. Cấu hình với URL Webhook của Slack/Telegram.
  3. Sử dụng template thông báo:
     ```json
     "New feedback analyzed! 🚀\nSentiment: {{ $node["Tag Feedbacks with OpenAI"].json()["sentiment"] }}\nPrimary Emotion: {{ $node["Tag Feedbacks with OpenAI"].json()["primary_emotion"] }}"
     ```

### **🔹 Lưu Log Kết Quả vào Google Drive**
- Thêm node **Google Drive** sau node **"Update Google Sheet"** để lưu file Excel/CSV chứa tất cả phản hồi đã phân tích.
- **Cách làm**:
  1. Thêm node **Google Drive Create File**.
  2. Chọn loại file: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet` (Excel).
  3. Điền tên file: `Feedback_Analysis_$(date:YYYY-MM-DD).xlsx`.
  4. Điền nội dung từ Google Sheets (sử dụng `{{ $json }}`).

### **🔹 Gửi Báo Cáo Định Kỳ qua Email**
- Thêm node **Email** (n8n-nodes-base.email) để gửi báo cáo tổng hợp hàng tuần.
- **Cách làm**:
  1. Thêm node **Email**.
  2. Cấu hình SMTP (ví dụ: Gmail, SendGrid).
  3. Sử dụng node **Code** trước node Email để tổng hợp dữ liệu:
     ```javascript
     // Tính tổng số phản hồi theo sentiment
     const sentimentCounts = {};
     $input.all().forEach(item => {
       const sentiment = item.json()["sentiment"];
       sentimentCounts[sentiment] = (sentimentCounts[sentiment] || 0) + 1;
     });
     return [{ json: { sentimentCounts } }];
     ```
  4. Gửi email với nội dung:
     ```html
     <h1>Báo cáo Phân Tích Phản Hồi Khách Hàng</h1>
     <p>Tổng số phản hồi: {{ $input.all().length }}</p>
     <p>Phân bố sentiment:</p>
     <ul>
       {{ $node["Code"].json()["sentimentCounts"].map(item => `<li>${Object.keys(item)[0]}: ${item[Object.keys(item)[0]]} phản hồi</li>`).join("") }}
     </ul>
     ```

### **🔹 Tối Ưu Hóa Batch Size**
- Nếu có **hàng ngàn phản hồi**, tăng **batch size** lên 20-50 để giảm số lần gọi API (tiết kiệm chi phí).
- **Cách làm**:
  1. Mở node **"Process Feedbacks in Batches"**.
  2. Cập nhật `batchSize` từ `10` thành `20` (hoặc giá trị phù hợp).

### **🔹 Sử Dụng Google Apps Script để Tự Động Cập Nhật Template**
- Nếu template Google Sheets thay đổi, sử dụng **Google Apps Script** để tự động cập nhật cấu trúc cột trong workflow.
- **Cách làm**:
  1. Tạo một script Google Apps Script để kiểm tra và cập nhật cột trong bảng.
  2. Thêm node **HTTP Request** trong n8n để gọi script này trước khi chạy workflow.

---

## 📌 **Kết Luận: Áp Dụng Ngay để Tiết Kiệm Thời Gian & Tăng Cường Hiệu Quả**

Workflow này **giải phóng thời gian** của các sếp để tập trung vào việc **phân tích chiến lược** thay vì làm việc thủ công. Với **AI OpenAI**, phản hồi khách hàng được phân tích chính xác, nhanh chóng, và tự động gán nhãn theo sentiment và cảm xúc.

**Hành động ngay hôm nay:**
1. **Sao chép template Google Sheets** và cấu hình credentials trong n8n.
2. **Import workflow** và chạy test với dữ liệu mẫu.
3. **Bật chế độ tự động** để workflow chạy mỗi 60 phút.
4. **Kết hợp với Slack/Email** để nhận báo cáo tự động.

👉 **Bắt đầu tự động hóa ngay bây giờ và xem phản hồi khách hàng của mình trở nên thông minh hơn bao giờ hết!**

---
:::note[CHÚ Ý]
- **Chi phí OpenAI**: Workflow này sử dụng **gpt-3.5-turbo**, chi phí khoảng **$0.002/1000 token**. Với batch size 10, mỗi lần chạy ~$0.0002 (rất rẻ).
- **Rate Limit**: Nếu gọi API quá nhiều, OpenAI có thể block. Đảm bảo **batch size không quá 100** và **chờ 5-10 giây** giữa các batch.
- **D