---
title: "🚀 Tự Động Scrape Đánh Giá Trustpilot + Phân Tích Sentiment với DeepSeek & OpenAI (Không Cần Code)"
description: "Workflow tự động scrape tất cả đánh giá Trustpilot của doanh nghiệp, trích xuất thông tin chi tiết, phân tích cảm xúc (sentiment) và tổng hợp báo cáo tự động lên Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng và nhận được insights khách hàng chính xác."
slug: "tự-dộng-scrape-trustpilot-deepseek-openai"
tags: [n8n, automation, no-code, ai-marketing, sentiment-analysis, deepseek, openai, google-sheets]
keywords: [scrape trustpilot n8n, tự động hóa đánh giá khách hàng, phân tích sentiment với openai, deepseek chatbot, google sheets automation, workflow marketing]
---

# 🚀 **Tự Động Scrape & Phân Tích Đánh Giá Trustpilot Cho Doanh Nghiệp**

### **Nỗi Đau Của Các Sếp**
Làm thủ công scrape đánh giá Trustpilot của doanh nghiệp là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**:
- **Tốn nhiều giờ** để copy-paste từng đánh giá từ trang web.
- **Không cập nhật kịp thời** khi có đánh giá mới.
- **Không phân tích được cảm xúc** (sentiment) của khách hàng để cải thiện dịch vụ.
- **Không lưu trữ hệ thống** để theo dõi xu hướng phản hồi.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Scrape tự động** tất cả đánh giá mới từ Trustpilot.
✅ **Trích xuất thông tin chi tiết** (tên khách hàng, ngày đánh giá, nội dung, rating).
✅ **Phân tích sentiment** với **DeepSeek** (mô hình AI tiên tiến) và **OpenAI** để biết khách hàng cảm thấy như thế nào.
✅ **Lưu trữ tự động** lên **Google Sheets** với định dạng chuyên nghiệp.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
- **Nhận được báo cáo sentiment** để hiểu rõ hơn về trải nghiệm khách hàng.
- **Cập nhật tự động** khi có đánh giá mới (không cần check thủ công).
- **Lưu trữ dữ liệu sạch sẽ** trên Google Sheets, dễ dàng phân tích với Excel/Google Data Studio.
- **Cải thiện dịch vụ** bằng cách phản hồi kịp thời với khách hàng không hài lòng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Trustpilot** của doanh nghiệp (để scrape).
✔ **API Key OpenAI** (để sử dụng mô hình **DeepSeek** và **GPT-3.5/4**).
✔ **Google Sheets OAuth2 API Key** (để lưu trữ dữ liệu).
✔ **Tên Sheet Google** (để lưu kết quả scrape).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không cần API Key Trustpilot** vì scrape từ frontend (an toàn và không vi phạm chính sách).
- **DeepSeek** được sử dụng để trích xuất thông tin chi tiết từ đánh giá (mô hình mạnh hơn OpenAI trong việc xử lý văn bản tiếng Anh).
- **OpenAI** được sử dụng để phân tích sentiment (có thể thay thế bằng mô hình DeepSeek nếu muốn).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào n8n Editor:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2792).
2. Trong n8n Editor, nhấn **"Import"** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **"Import Workflow"** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng**:

##### **A. Cấu Hình "Get reviews" (Scrape Trustpilot)**
- **Node:** `Get reviews` (HTTP Request)
- **Tham số cần chỉnh:**
  - **URL:** `https://www.trustpilot.com/review/www.[tên-doanh-nghiệp].com` (thay `tên-doanh-nghiệp` bằng tên công ty của bạn).
  - **Headers:**
    ```
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
    Accept-Language: en-US,en;q=0.9
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
    ```
  - **Method:** `GET`

##### **B. Cấu Hình "Set Parameters" (Limiter số trang scrape)**
- **Node:** `Limit1` (Limit)
- **Tham số cần chỉnh:**
  - **Limit:** Đặt số lượng **trang tối đa** muốn scrape (ví dụ: `5` trang).

##### **C. Cấu Hình "Google Sheets" (Lưu dữ liệu)**
- **Node:** `Get Google Sheets` và `Update sheet` (Google Sheets)
- **Tham số cần chỉnh:**
  - **Spreadsheet ID:** ID của Google Sheet bạn muốn lưu dữ liệu (tham khảo [cách lấy ID](https://support.google.com/docs/answer/3093333)).
  - **Sheet Name:** Tên tab trong Google Sheet (ví dụ: `Trustpilot_Reviews`).
  - **Credentials:** Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).

##### **D. Cấu Hình "DeepSeek Chat Model" (Trích Xuất Thông Tin)**
- **Node:** `DeepSeek Chat Model` (LM Chat OpenAI)
- **Tham số cần chỉnh:**
  - **Model:** `deepseek-reasoner` (không cần thay đổi).
  - **API Key:** Chọn `openAiApi` (đã cấu hình trước).
  - **Prompt:**
    ```plaintext
    Extract the following information from the review text:
    - Customer name (if available)
    - Date of review
    - Rating (1-5 stars)
    - Review text
    - Sentiment (positive/negative/neutral)
    Format the output as JSON:
    {
      "customer_name": "string",
      "date": "string",
      "rating": "number",
      "review_text": "string",
      "sentiment": "string"
    }
    ```

##### **E. Cấu Hình "Sentiment Analysis" (Phân Tích Cảm Xúc)**
- **Node:** `Sentiment Analysis` (Sentiment Analysis)
- **Tham số cần chỉnh:**
  - **Model:** Chọn `deepseek-reasoner` (nếu muốn) hoặc `text-embedding-ada-002` (OpenAI).
  - **API Key:** Chọn `openAiApi`.

##### **F. Cấu Hình "If" (Kiểm Tra Trùng Lặp)**
- **Node:** `If` (Conditional)
- **Tham số cần chỉnh:**
  - **Condition:** Kiểm tra xem review đã tồn tại trong Google Sheets chưa (tránh trùng lặp).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Test Workflow"** để kiểm tra các node hoạt động như thế nào.
   - Kiểm tra **Google Sheets** xem dữ liệu có được lưu đúng không.
2. **Bật Active Workflow:**
   - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram để báo cáo tự động:**
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `Update sheet` để thông báo khi có review mới.
2. **Lưu Log vào Google Drive:**
   - Sử dụng node **Google Drive** để lưu log hoạt động của workflow.
3. **Tự động gửi báo cáo định kỳ:**
   - Kết hợp với **n8n Scheduler** để gửi báo cáo sentiment hàng tuần qua email.
4. **Sử dụng mô hình DeepSeek khác:**
   - Nếu muốn, thay thế `deepseek-reasoner` bằng `deepseek-coder` (nếu cần phân tích mã nguồn hoặc logic).

---
### 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa hoàn toàn quá trình scrape và phân tích đánh giá Trustpilot**, tiết kiệm thời gian và nhận được **insights khách hàng chính xác**. Bằng cách kết hợp **DeepSeek (trích xuất thông tin) và OpenAI (phân tích sentiment)**, các sếp có thể **hiểu rõ hơn về trải nghiệm khách hàng** và **cải thiện dịch vụ một cách dữ liệu-driven**.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa marketing của mình!** 🚀

---
:::tip[Gợi Ý Tiếp Theo]
- Nếu muốn **scrape nhiều trang web khác**, có thể mở rộng workflow với node **HTTP Request** và **Loop**.
- Để **tối ưu hóa hiệu suất**, các sếp có thể chạy workflow trên **VPS** thay vì n8n.cloud.
:::

---
**Cảm ơn các sếp đã đọc!** Nếu có thắc mắc, hãy để lại comment dưới đây. 👇