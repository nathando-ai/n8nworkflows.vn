---
title: "🎤 Thực hành Phỏng vấn Tiếng Việt với AI Gemini Voice Interviewer - Tự động hóa Phỏng vấn Hiệu quả 100% Không Code"
description: "Workflow tự động hóa phỏng vấn tiếng Việt bằng AI Gemini, giúp các sếp thực hành phỏng vấn với giọng nói tự nhiên, hỏi theo logic và lưu lịch sử hội thoại. Giúp chuẩn bị sẵn sàng cho các cuộc phỏng vấn thực tế một cách hiệu quả."
slug: "thuc-hanh-phong-van-voi-ai-gemini-voice-interviewer"
tags: [n8n, automation, ai-chatbot, google-gemini, phong-van-tieng-viet, no-code]
keywords: [n8n workflow phỏng vấn, AI Gemini tự động hóa, phỏng vấn tiếng Việt, chatbot phỏng vấn, tự động hóa nhân sự]
---

# 🎤 Thực hành Phỏng vấn Tiếng Việt với AI Gemini Voice Interviewer

## 🔍 Nỗi đau thực tế của các sếp khi chuẩn bị phỏng vấn
Chuẩn bị cho các cuộc phỏng vấn là một quá trình tốn thời gian và căng thẳng. Các sếp thường phải:
- **Lặp đi lặp lại** các câu hỏi phỏng vấn thông thường, không thể thực hành theo logic thực tế.
- **Không có phản hồi cá nhân hóa**, chỉ có thể tự trả lời và tự đánh giá.
- **Không lưu lịch sử hội thoại**, dẫn đến việc không thể học hỏi từ các lỗi sai trước đó.
- **Phải tự viết câu hỏi phức tạp**, mất nhiều thời gian và công sức.

Workflow này là **giải pháp hoàn hảo** để các sếp thực hành phỏng vấn bằng giọng nói tự nhiên, với AI Gemini hỏi theo logic và lưu toàn bộ lịch sử hội thoại. Bạn sẽ không chỉ trả lời câu hỏi, mà còn **học hỏi từ các phản hồi thông minh** của AI, giống như một cuộc phỏng vấn thực tế!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thực hành phỏng vấn bằng giọng nói tự nhiên** (không cần gõ bàn phím).
- **AI hỏi theo logic**, từ câu hỏi cơ bản đến câu hỏi phức tạp dựa trên lịch sử hội thoại.
- **Lưu toàn bộ lịch sử phỏng vấn**, giúp các sếp học hỏi và cải thiện từng lần.
- **Cá nhân hóa phỏng vấn** dựa trên CV và mô tả công việc của từng người dùng.
- **Hoạt động liên tục 24/7**, không giới hạn số lần thực hành.
- **Giảm thời gian chuẩn bị** so với việc tự viết câu hỏi phỏng vấn.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **API Key của Google Gemini**:
   - Miễn phí từ [Google AI Studio](https://makersuite.google.com/app/apikey).
   - Thêm credential vào node **"Google Gemini Chat Model"** trong n8n.
2. **Frontend HTML** (để chuyển giọng nói thành văn bản và đọc lại câu trả lời):
   - Tải mã nguồn từ [GitHub repository](https://github.com/sarthak1999/voice-interview) (cần cài đặt Node.js và chạy `npm install`).
3. **Mô tả công việc (Job Description)** và **CV (Resume)** của người dùng (gửi từ frontend).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải workflow** từ [n8n.io/workflows/6614](https://n8n.io/workflows/6614) hoặc tải file JSON đã cung cấp.
- Mở **n8n Editor** và chọn **"Import"** → Chọn file JSON hoặc **copy/paste** JSON vào ô nhập liệu.
- **Lưu workflow** với tên **"Gemini Voice Interviewer"** (hoặc tên khác tùy thích).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

##### **A. Cấu hình Credential Google Gemini**
1. Vào node **"Google Gemini Chat Model"**.
2. Nhấp vào **"Add Credential"** → Chọn **"googlePalmApi"**.
3. Nhập **API Key** từ Google AI Studio (đã chuẩn bị ở trên).
4. **Lưu credential** và quay lại node.

##### **B. Cấu hình Webhook**
1. Vào node **"Webhook"**.
2. **Không cần thay đổi gì** (n8n sẽ tự động tạo URL cho frontend).
3. **Sau khi lưu workflow**, nhấp vào node **"Webhook"** → Chọn **"Copy Production URL"**.
4. **Dán URL này vào file `voice-interview.html`** (tại phần `<script>window.webhookUrl = "YOUR_URL_HERE";</script>`).

##### **C. Cấu hình Prompts (Câu hỏi AI)**
Workflow tự động tạo **2 loại prompt**:
- **Prompt đầu tiên** (câu hỏi khởi đầu): Dựa trên CV và mô tả công việc.
- **Prompt tiếp theo** (câu hỏi theo logic): Dựa trên lịch sử hội thoại.
Các sếp **không cần chỉnh sửa** nếu muốn sử dụng mặc định.

##### **D. Kích hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một request POST từ frontend (từ file HTML) với dữ liệu mẫu:
     ```json
     {
       "resume": "Tôi có kinh nghiệm 5 năm trong lĩnh vực marketing digital...",
       "jobDescription": "Chuyên viên Marketing Digital - Quản lý chiến dịch SEO, quảng cáo Google Ads..."
     }
     ```
   - Kiểm tra phản hồi từ AI trong **n8n Editor** (node **"Respond to Webhook"**).
2. **Bật Active workflow** bằng cách nhấp vào nút **"Active"** ở góc trên bên phải.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ NHẤT]
1. **Tạo nhiều phiên phỏng vấn khác nhau**:
   - Sử dụng **mô tả công việc khác nhau** (ví dụ: Developer, Designer, Sales) để thực hành cho nhiều vị trí.
   - **Lưu lịch sử phỏng vấn** trong Google Sheets (thêm node **Google Sheets** sau node **"Merge"** để lưu dữ liệu).

2. **Kết hợp với Slack/Telegram**:
   - Sau khi hoàn thành phỏng vấn, **gửi kết quả** về Slack/Telegram bằng node **Slack** hoặc **Telegram Bot**.
   - Ví dụ:
     ```json
     {
       "text": "🎤 Phỏng vấn hoàn tất!\nCV: [Tên người dùng]\nCâu hỏi cuối cùng: [Câu hỏi AI]\nLời khuyên: [Phản hồi từ AI]"
     }
     ```

3. **Thêm tính năng đánh giá tự động**:
   - Sử dụng **node LLM Chain** để phân tích câu trả lời của người dùng và **đánh giá điểm số** (ví dụ: 1-10).
   - Ví dụ prompt:
     ```
     "Đánh giá câu trả lời sau của người dùng (1-10 điểm) dựa trên sự chính xác, logic và chuyên nghiệp:
     Câu trả lời: '[Câu trả lời người dùng]'
     Mô tả công việc: '[Job Description]'
     ```

4. **Tạo báo cáo định kỳ**:
   - Sử dụng **node Schedule** (n8n Pro) để gửi **báo cáo tổng hợp** về tiến độ học tập mỗi tuần.
   - Ví dụ:
     ```
     "Tổng số phỏng vấn thực hành: 15
     Trung bình điểm: 8.2/10
     Thiếu sót thường gặp: [Danh sách lỗi]"
     ```

5. **Chuyển đổi giọng nói sang văn bản tự động**:
   - Nếu frontend không hỗ trợ, các sếp có thể sử dụng **node Web Speech API** (JavaScript) hoặc dịch vụ như **Google Speech-to-Text** để chuyển giọng nói thành văn bản trước khi gửi đến n8n.

---

### 📌 Kết luận
Workflow **"Practice Job Interviews with Voice-based Google Gemini AI Interviewer"** là **giải pháp hoàn hảo** để các sếp:
✅ **Thực hành phỏng vấn tiếng Việt một cách tự nhiên** (giống như cuộc phỏng vấn thực tế).
✅ **Học hỏi từ AI** với câu hỏi logic và phản hồi cá nhân hóa.
✅ **Lưu lịch sử phỏng vấn** để cải thiện từng lần.
✅ **Tiết kiệm thời gian** so với việc tự viết câu hỏi phỏng vấn.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình Google Gemini API.
3. **Tải frontend** từ GitHub và kết nối với backend.
4. **Bắt đầu thực hành phỏng vấn** và chuẩn bị sẵn sàng cho các cuộc phỏng vấn thực tế!

🚀 **Chúc các sếp thành công trong việc chuẩn bị phỏng vấn!** Nếu có bất kỳ câu hỏi nào, hãy để lại bình luận dưới đây. 👇