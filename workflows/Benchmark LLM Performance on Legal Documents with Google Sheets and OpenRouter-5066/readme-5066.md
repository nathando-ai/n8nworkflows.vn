---
title: "🤖 Benchmark Hiệu Suất LLM Trên Tài Liệu Pháp Lý: Tự Động Hoá So Sánh AI với Google Sheets & OpenRouter"
description: "Workflow tự động hóa so sánh hiệu suất các mô hình LLM (AI) trên tài liệu pháp lý bằng cách tải PDF từ Google Drive, xử lý nội dung và đánh giá kết quả qua OpenRouter. Giúp các sếp tiết kiệm thời gian so sánh thủ công, tối ưu hóa mô hình AI và lưu kết quả vào Google Sheets để phân tích dài hạn."
slug: "benchmark-llm-tren-tai-lieu-phap-ly"
tags: [n8n, automation, ai, google-sheets, openrouter, legal-tech, no-code]
keywords: [benchmark llm, tự động hóa so sánh ai, google sheets automation, openrouter api, đánh giá hiệu suất llm, tài liệu pháp lý]
---

# 🚀 Benchmark Hiệu Suất LLM Trên Tài Liệu Pháp Lý: Giải Pháp Tự Động Hoá Cho Các Sếp

## **Nỗi Đau Thực Tế Của Các Sếp**
Hiện nay, khi muốn đánh giá hiệu suất của các mô hình LLM (AI) trên tài liệu pháp lý phức tạp như hợp đồng, điều lệ công ty hay văn bản pháp luật, các sếp phải thực hiện thủ công:
- **Tải và xử lý hàng loạt tài liệu PDF** từ Google Drive.
- **Ghi nhớ và nhập dữ liệu** vào Google Sheets để so sánh kết quả.
- **Đánh giá thủ công** xem mô hình AI trả lời chính xác hay không, mất nhiều thời gian và dễ bị sai sót.
- **Không có hệ thống tự động hóa** để cập nhật và phân tích kết quả theo thời gian.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình: từ tải tài liệu, xử lý nội dung, đánh giá AI cho đến lưu kết quả vào Google Sheets. **Kết quả? Các sếp tiết kiệm 80% thời gian so sánh, đảm bảo độ chính xác và có thể mở rộng cho nhiều mô hình AI khác nhau.**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần nhập liệu thủ công, giảm thiểu sai sót.
- **Đánh giá chính xác**: Sử dụng mô hình AI (OpenRouter) để phân tích và lý giải kết quả.
- **Lưu trữ dữ liệu**: Kết quả được ghi vào Google Sheets, dễ dàng theo dõi và phân tích dài hạn.
- **Mở rộng linh hoạt**: Thay đổi mô hình LLM (ví dụ: GPT-4, Claude) chỉ bằng một cú nhấp chuột.
- **Hoạt động liên tục**: Workflow chạy tự động khi có tài liệu mới, không phụ thuộc vào thời gian làm việc của người dùng.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets và Google Drive).
2. **API Key OpenRouter** (để sử dụng mô hình LLM).
3. **Google Sheet mẫu** (có cấu trúc như trong [bài viết gốc](https://docs.google.com/spreadsheets/d/10l_gMtPsge00eTTltGrgvAo54qhh3_twEDsETrQLAGU/edit?usp=sharing)).
4. **Tài liệu PDF** (đã upload lên Google Drive và liên kết trong Google Sheet).
5. **n8n Self-hosted** (để chạy workflow 24/7).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/5066) (chọn "Export Workflow").
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Cấu hình Credentials**
1. **Google Sheets & Google Drive**:
   - Đi đến **Credentials** → Tạo mới **Google Sheets OAuth2** và **Google Drive OAuth2**.
   - Chọn **"Google Sheets"** và **"Google Drive"** trong danh sách.
   - Nhấn **"Connect"** và theo hướng dẫn để cấp quyền cho n8n.

2. **OpenRouter API**:
   - Đi đến **Credentials** → Tạo mới **OpenRouter API**.
   - Nhập **API Key** từ tài khoản OpenRouter của mình.
   - Chọn **"lmChatOpenRouter"** trong danh sách.

##### **B. Cấu hình Node "Get Tests" (Google Sheets)**
- Trong node **"Get Tests"**, chọn **Google Sheet** chứa danh sách test (ví dụ: [Sheet mẫu](https://docs.google.com/spreadsheets/d/10l_gMtPsge00eTTltGrgvAo54qhh3_twEDsETrQLAGU/edit?usp=sharing)).
- Chọn **Sheet Name** là **"Tests"** (hoặc tên tương ứng).
- Chọn **Range** là **"A1:F"** (để lấy tất cả dữ liệu).

##### **C. Cấu hình Node "OpenRouter Chat Model"**
- Trong node **"OpenRouter Chat Model"**, chọn mô hình LLM muốn sử dụng (ví dụ: `"openai/gpt-4.1"`).
- Cấu hình **Prompt** để đánh giá kết quả (các sếp có thể tùy chỉnh prompt theo yêu cầu cụ thể).

##### **D. Cấu hình Node "Update Results" (Google Sheets)**
- Chọn **Google Sheet** kết quả (ví dụ: **"Results"**).
- Chọn **Range** là `"A1:G"` (để ghi kết quả vào cột tương ứng).

##### **E. Cấu hình Node "Webhook"**
- Node **"Webhook"** sẽ được kích hoạt khi có yêu cầu HTTP POST đến URL:
  ```
  https://[your-n8n-domain]/webhook/1cbce320-d28e-4e97-8663-bf2c6a36a358
  ```
- Các sếp có thể **bỏ qua node này** nếu chỉ muốn chạy workflow tự động từ **"Manual Trigger"**.

#### 3. Kích hoạt ⚡️
- Nhấn **"Execute Workflow"** (không phải nút dưới webhook).
- Chọn **"Test workflow"** để chạy thử với dữ liệu mẫu.
- Sau khi kiểm tra thành công, bật **Active workflow**.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh Prompt cho LLM**:
   - Các sếp có thể thay đổi **Prompt** trong node **"OpenRouter Chat Model"** để đánh giá theo tiêu chí riêng (ví dụ: độ chính xác, logic pháp lý, tính toàn diện).

2. **Lưu Log & Báo Cáo**:
   - Sử dụng node **"Set"** để lưu dữ liệu vào **Google Sheets** hoặc **Google Drive** để theo dõi lịch sử.
   - Tạo một **Google Sheet báo cáo** để tổng hợp kết quả của nhiều mô hình LLM.

3. **Kết hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram** để thông báo kết quả khi workflow hoàn thành.

4. **Batching Requests**:
   - Node **"Limit (for testing)"** có thể được bỏ qua hoặc điều chỉnh để xử lý nhiều tài liệu cùng một lúc.

5. **Mở rộng cho nhiều mô hình AI**:
   - Thay đổi **model** trong node **"OpenRouter Chat Model"** để so sánh hiệu suất giữa GPT-4, Claude, hoặc mô hình khác.

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc đánh giá hiệu suất LLM trên tài liệu pháp lý. **Không cần viết code**, chỉ cần cấu hình vài bước là có thể tiết kiệm thời gian, đảm bảo độ chính xác và mở rộng cho nhiều mô hình AI khác nhau.

**Hãy áp dụng ngay và bắt đầu tự động hóa quy trình của mình!** 🚀
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, các sếp có thể tham khảo [dокументация chính thức của n8n](https://docs.n8n.io/) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community).