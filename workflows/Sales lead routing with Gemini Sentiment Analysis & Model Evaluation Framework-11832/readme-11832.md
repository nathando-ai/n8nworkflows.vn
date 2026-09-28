---
title: "🚀 **Tự Động Hóa Xử Lý Lead Sales Với Phân Tích Sentiment AI & Khung Đánh Giá Model Gemini - N8n**"
description: "Workflow tự động phân loại và phân phối lead sales từ email dựa trên phân tích cảm xúc AI, đồng thời cung cấp khung đánh giá hiệu suất model Gemini để tối ưu hóa quyết định marketing. Giúp các sếp tiết kiệm 80% thời gian xử lý lead thủ công và nâng cao tỷ lệ chuyển đổi."
slug: "tieu-ly-lead-sales-voi-gemini-sentiment-analysis"
tags: [n8n, automation, no-code, lead-generation, ai-sentiment-analysis, google-gemini, email-automation]
keywords: [n8n workflow lead sales, tự động hóa phân tích lead, sentiment analysis gemini, đánh giá model ai, tối ưu marketing email]
---

# 🚀 **Tự Động Hóa Xử Lý Lead Sales Với Phân Tích Sentiment AI & Khung Đánh Giá Model Gemini**

## **🔥 Nỗi Đau Của Các Sếp Trong Xử Lý Lead Sales**
Hàng ngày, các sếp phải:
- **Lọc và phân loại** hàng trăm email lead thủ công, dẫn đến mất thời gian và khả năng bỏ sót lead có giá trị.
- **Không biết lead nào thực sự "hot"** vì thiếu công cụ phân tích cảm xúc tự động.
- **Không thể so sánh hiệu suất** giữa các model AI (Gemini Lite, Flash, Pro) để chọn lựa tối ưu.
- **Rủi ro gửi lead sai nhãn** (positive/negative/neutral) gây mất niềm tin với khách hàng.

**Workflow này giải quyết tất cả đó!** Với **AI Gemini** phân tích cảm xúc và **khung đánh giá model**, các sếp sẽ:
✅ **Tự động phân loại lead** theo độ ưu tiên (hot/medium/cold).
✅ **So sánh hiệu suất model** để chọn model phù hợp với ngân sách.
✅ **Đánh giá chính xác** kết quả AI so với ground truth (dữ liệu tham chiếu).
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phân loại lead** theo cảm xúc (positive/negative/neutral) và độ ưu tiên.
- **So sánh 3 model Gemini** (Flash Lite, Flash, Pro) để chọn model tối ưu về **tốc độ + độ chính xác**.
- **Khung đánh giá model** so sánh kết quả AI với ground truth (dữ liệu tham chiếu).
- **Gửi thông báo email tự động** cho team sales khi có lead "hot".
- **Lưu lịch sử đánh giá** để theo dõi hiệu suất dài hạn.
- **Không cần code**, chỉ cần cấu hình trong n8n Editor.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để nhận và gửi email lead).
2. **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
3. **n8n Data Table** (để lưu dữ liệu đánh giá model).
4. **Dữ liệu tham chiếu (Golden Dataset)** (các email đã được nhãn định trước để đánh giá model).

---
:::info[CHUẨN BỊ]
- **Gmail OAuth2**: Cấu hình trong n8n Credentials (để gửi/receive email).
- **Google Palm API**: Thêm API Key trong Credentials (để kết nối với Gemini).
- **n8n Data Table**: Tạo bảng dữ liệu với cột `input_text` (nội dung email) và `expected_sentiment` (nhãn cảm xúc).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/11832](https://n8n.io/workflows/11832) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào n8n Editor (tab "Import").

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **2 đường dẫn chính**:
- **Production Path** (xử lý lead thực tế).
- **Evaluation Path** (đánh giá model).

##### **A. Cấu Hình Credentials**
| Node | Yêu Cầu Cấu Hình |
|------|------------------|
| **Gmail Trigger** | Chọn `gmailOAuth2` credentials (đã cấu hình OAuth2). |
| **Send Hot Lead Email / Follow-up Notification** | Chọn cùng `gmailOAuth2` credentials. |
| **Google Gemini 3 PRO / Flash / Flash Lite** | Chọn `googlePalmApi` credentials (điền API Key). |

##### **B. Cấu Hình Data Table (Evaluation Path)**
- Tạo **n8n Data Table** với 2 cột:
  - `input_text` (nội dung email).
  - `expected_sentiment` (nhãn cảm xúc: `positive`, `negative`, `neutral`).
- Kết nối **Evaluation Trigger** với Data Table này.

##### **C. Chọn Model Gemini**
- Workflow hỗ trợ **3 model**:
  - `Google Gemini 3 PRO` (độ chính xác cao nhất).
  - `Google Gemini 2.5 Flash` (tốc độ cao).
  - `Google Gemini 2.5 Flash Lite` (rẻ nhất).
- Các sếp có thể **thay đổi model** trong node `Sentiment Analysis` để so sánh hiệu suất.

##### **D. Safety Gate (Đảm Bảo Không Gửi Email Thực Tế Trong Đánh Giá)**
- Các node `Check Positive/Neutral/Negative` sẽ **chặn email thực tế** khi đang trong chế độ đánh giá.
- Khi hoàn tất đánh giá, các sếp cần **bật chế độ Production** bằng cách điều chỉnh logic trong `evaluationTrigger`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một email test vào Gmail Trigger.
   - Kiểm tra kết quả phân loại sentiment.
2. **Bật Active Workflow**:
   - Đảm bảo tất cả credentials đã đúng.
   - Kích hoạt **Gmail Trigger** và **Evaluation Trigger** (nếu muốn đánh giá model).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo lead "hot" ngay lập tức.
2. **Lưu Log Đánh Giá**:
   - Sử dụng node `stickyNote` để ghi lại kết quả đánh giá model vào một file CSV.
3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một workflow phụ để gửi báo cáo hiệu suất model cho team marketing hàng tuần.
4. **Tối ưu Model**:
   - Thử nghiệm với **các prompt khác nhau** trong node `lmChatGoogleGemini` để cải thiện độ chính xác.

---
### 📌 **Kết Luận**
Workflow này không chỉ **tự động hóa xử lý lead** mà còn **cung cấp khung đánh giá model AI** để các sếp luôn chọn lựa tối ưu. **Không cần code**, chỉ cần cấu hình trong n8n Editor!

**Hành động ngay:**
1. **Import workflow** và cấu hình credentials.
2. **Test với dữ liệu mẫu** trước khi áp dụng toàn bộ.
3. **So sánh hiệu suất model** và chọn model phù hợp.

**🚀 Cải thiện hiệu suất marketing chỉ trong vài phút!**