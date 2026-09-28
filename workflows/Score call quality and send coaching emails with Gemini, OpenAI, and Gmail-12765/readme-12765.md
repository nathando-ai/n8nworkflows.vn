---
title: "🤖 **Tự Động Học Đánh Giá Chất Lượng Cuộc Gọi & Gửi Email Huấn Luyện AI (Gemini + OpenAI + Gmail)**"
description: "Giải pháp tự động hóa hoàn toàn cho trung tâm dịch vụ khách hàng, đánh giá chất lượng cuộc gọi bằng AI, phát hiện rủi ro, và gửi email huấn luyện cá nhân hóa cho nhân viên. Tiết kiệm 80% thời gian kiểm duyệt thủ công!"
slug: "tieu-dong-hoa-danh-gia-chat-luong-cuoc-goi-voi-ai"
tags: [n8n, automation, ai-summarization, call-center, gmail-integration, google-drive, gemini, openai]
keywords: [n8n workflow call center, tự động hóa đánh giá chất lượng cuộc gọi, gemini transcribe, openai gpt-4o đánh giá nhân viên, email huấn luyện tự động]
---

# 🚀 **Tự Động Học Đánh Giá Chất Lượng Cuộc Gọi & Gửi Email Huấn Luyện AI**

### **Giải pháp cho trung tâm dịch vụ khách hàng: Đánh giá cuộc gọi bằng AI, tiết kiệm 80% thời gian kiểm duyệt thủ công**

Hiện nay, việc đánh giá chất lượng cuộc gọi tại trung tâm dịch vụ khách hàng vẫn phụ thuộc vào con người, dẫn đến:
❌ **Thời gian kiểm duyệt lâu** (thường mất 1-2 ngày cho mỗi cuộc gọi)
❌ **Chủ quan trong đánh giá** (mất đồng nhất giữa các evaluator)
❌ **Không phát hiện được rủi ro** (việc gọi vi phạm chính sách, thông tin nhạy cảm)
❌ **Email huấn luyện không cá nhân hóa** (mẫu chung, không phù hợp với từng nhân viên)

**Workflow này giải quyết tất cả vấn đề trên bằng AI!**
- **Chuyển âm thanh cuộc gọi → văn bản** (Gemini)
- **Đánh giá chất lượng** (điểm số, nhận xét chi tiết) bằng AI Agent
- **Phát hiện rủi ro** (vi phạm chính sách, cảm xúc khách hàng)
- **Gửi email huấn luyện tự động** (cá nhân hóa, có gợi ý cải thiện)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với kiểm duyệt thủ công (AI xử lý trong vài giây)
- **Đánh giá khách quan** (AI tuân theo tiêu chí nhất quán, không bị ảnh hưởng cảm xúc)
- **Phát hiện rủi ro tự động** (vi phạm chính sách, thông tin nhạy cảm, cảm xúc tiêu cực)
- **Email huấn luyện cá nhân hóa** (nhận xét chi tiết, gợi ý cải thiện cụ thể)
- **Hoạt động 24/7** (không cần nhân viên giám sát)
- **Kết hợp nhiều mô hình AI** (Gemini + OpenAI GPT-4o cho độ chính xác cao)
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu file âm thanh cuộc gọi)
   - **Folder chia sẻ** (cần quyền đọc ghi) để workflow tự động lấy file mới.
2. **API Key Gemini (Google Palm API)**
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/) và lấy API Key.
3. **API Key OpenAI**
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy API Key.
4. **Tài khoản Gmail** (để gửi email huấn luyện)
   - Cần **OAuth 2.0** để n8n có thể gửi email tự động.
5. **File âm thanh cuộc gọi** (định dạng `.mp3` hoặc `.wav`)
   - Lưu trong folder Google Drive đã chọn.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12765](https://n8n.io/workflows/12765) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **11 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu hình Google Drive**
1. **Node: `Google Drive Trigger`**
   - Chọn **credentials**: `googleDriveOAuth2Api`
   - **Folder ID**: Điền ID folder Google Drive chứa file âm thanh (lấy từ liên kết folder: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
   - **File Type**: Chọn `Audio files` (`.mp3`, `.wav`).

2. **Node: `Download file`**
   - Sử dụng cùng **credentials** `googleDriveOAuth2Api`.
   - **File ID**: Auto lấy từ trigger, không cần chỉnh.

##### **B. Cấu hình AI Transcription (Gemini)**
3. **Node: `Transcribe` (Google Gemini)**
   - **Credentials**: `googlePalmApi` (điền API Key Gemini).
   - **Resource**: Đặt là `audio` (để AI chuyển âm thanh thành văn bản).
   - **Output Format**: Chọn `structured` (để dễ phân tích sau).

##### **C. Cấu hình AI Scoring (OpenAI + Agent)**
4. **Node: `GPT-4o` (OpenAI)**
   - **Credentials**: `openAiApi` (điền API Key OpenAI).
   - **Model**: Chọn `gpt-4o` (mô hình mới nhất của OpenAI).
   - **Prompt**: Workflow đã tự động cấu hình, **không cần chỉnh** (nếu muốn tùy chỉnh, mở node này và chỉnh `input` trong tab `Parameters`).

5. **Node: `AI Quality Analyst` (Agent)**
   - **Credentials**: Không cần (sử dụng API Key đã cấu hình ở trên).
   - **Scoring Criteria**: Workflow mặc định đánh giá theo tiêu chí:
     - **Empathy** (tình cảm)
     - **Solution Quality** (chất lượng giải pháp)
     - **Clarity** (độ rõ ràng)
     - **Policy Adherence** (tuân thủ chính sách)
   - **Lưu ý**: Nếu muốn thay đổi tiêu chí, mở node này và chỉnh `input` trong tab `Parameters`.

6. **Node: `Memory` (Memory Buffer Window)**
   - **Time Window**: Đặt là `1 day` (AI sẽ nhớ kết quả đánh giá trong 24h để so sánh tiến bộ).
   - **Credentials**: Không cần.

##### **D. Cấu hình Email Huấn Luyện (Gmail)**
7. **Node: `Send a message` (Gmail)**
   - **Credentials**: `gmailOAuth2` (cần cấu hình OAuth 2.0 cho tài khoản Gmail).
   - **To**: Điền email của nhân viên cần huấn luyện (hoặc dùng biến `{{ $json["email"] }}` nếu lưu trong file).
   - **Subject**: Mẫu: `"Feedback Huấn Luyện Cuộc Gọi #{{ $json["call_id"] }}"`.
   - **Body**: Workflow tự động tạo nội dung email với:
     - **Điểm số tổng thể**
     - **Nhận xét chi tiết** (điểm mạnh, điểm yếu)
     - **Gợi ý cải thiện**

##### **E. Cấu hình Output Parser (Structured)**
8. **Node: `Structured Output Parser` & `Structured Output Parser1`**
   - **Credentials**: Không cần.
   - **Format**: Chọn `JSON` (để AI phân tích kết quả một cách hệ thống).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow):
   - Nhấn **Run Workflow** và chọn một file âm thanh mẫu.
   - Kiểm tra:
     - File âm thanh có được tải xuống không?
     - AI có transcribe thành văn bản không?
     - Email có được gửi không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Kết hợp với Slack/Telegram**
   - Thêm node `webhook` để gửi kết quả đánh giá lên Slack/Telegram cho team quản lý.
   - **Cách làm**:
     - Tạo một webhook tại Slack/Telegram.
     - Thêm node `Set` sau `Structured Output Parser` để lưu kết quả vào biến `{{ $json }}`.
     - Thêm node `HTTP Request` với URL webhook và payload `{{ $json }}`.

2. **Lưu log đánh giá**
   - Thêm node `Google Sheets` để ghi dữ liệu đánh giá vào bảng tính.
   - **Cách làm**:
     - Cấu hình `Google Sheets OAuth2`.
     - Thêm node `Google Sheets` sau `Structured Output Parser` và chọn sheet muốn ghi.

3. **Gửi báo cáo định kỳ**
   - Sử dụng node `Set Interval` để chạy workflow hàng tuần/month và gửi báo cáo tổng hợp.
   - **Cách làm**:
     - Thêm node `Set Interval` với thời gian chạy (ví dụ: `every week`).
     - Thêm node `Google Sheets` để ghi báo cáo tổng hợp.
     - Thêm node `Gmail` để gửi báo cáo cho quản lý.

4. **Tùy chỉnh tiêu chí đánh giá**
   - Mở node `AI Quality Analyst` và chỉnh `input` trong tab `Parameters` để thêm/bỏ tiêu chí.
   - **Ví dụ**:
     ```json
     {
       "criteria": [
         "empathy",
         "solution_quality",
         "clarity",
         "policy_adherence",
         "time_to_resolution"  // Thêm tiêu chí mới
       ]
     }
     ```

5. **Sử dụng AI khác (Bard, Claude)**
   - Thay thế node `googleGemini` bằng `bard` hoặc `anthropic` (nếu có API Key).
   - **Cách làm**:
     - Cài node `n8n-nodes-base.bard` hoặc `n8n-nodes-base.anthropic`.
     - Thay thế node `Transcribe` bằng node mới và cấu hình API Key tương ứng.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho trung tâm dịch vụ khách hàng muốn tự động hóa đánh giá chất lượng cuộc gọi, tiết kiệm thời gian và cải thiện chất lượng dịch vụ.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với file âm thanh mẫu** trước khi áp dụng toàn bộ.
3. **Tùy chỉnh tiêu chí** để phù hợp với quy trình của doanh nghiệp.
4. **Kết hợp với Slack/Google Sheets** để quản lý dễ dàng hơn.

**🚀 Khởi động tự động hóa ngay hôm nay!** Nếu có vấn đề, để lại comment bên dưới hoặc liên hệ tác giả [Abdullah Al Shishani](https://n8n.io/workflows/12765) để hỗ trợ.

---
**#TựĐộngHóa #CallCenter #AIQualityAssessment #n8nWorkflows**