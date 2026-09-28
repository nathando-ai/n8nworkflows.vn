---
title: "🤖 **AI Trợ Lý Slack Toàn Dạng: Xử Lý Văn Bản, Âm Thanh, Hình Ảnh & Video Tự Động**"
description: "Workflow tự động hóa AI giúp các sếp xử lý yêu cầu từ Slack với âm thanh, hình ảnh và video thông qua OpenAI, Google Gemini và Claude, trả lời nhanh chóng và chính xác 24/7. Giảm thiểu công việc thủ công, tăng cường hiệu suất và cá nhân hóa tương tác."
slug: "ai-troly-slack-toan-dang-xuly-am-than-hinh-anh-video"
tags: [n8n, automation, no-code, ai-multimodal, slack-bot, openai, google-gemini, claud-ai]
keywords: [n8n workflow slack ai, tự động hóa xử lý âm thanh hình ảnh video, ai trợ lý multimodal, chatbot doanh nghiệp, xử lý file đa dạng trong slack]
---

# 🚀 **AI Trợ Lý Slack Toàn Dạng: Xử Lý Âm Thanh, Hình Ảnh & Video Tự Động**

### **Giải pháp cho các sếp:**
Hãy tưởng tượng một trợ lý AI luôn sẵn sàng trong Slack của bạn, không chỉ xử lý văn bản mà còn **nghe** âm thanh, **nhìn** hình ảnh và **phân tích** video để trả lời chính xác và nhanh chóng. **Không cần code**, không cần kỹ thuật viên, chỉ cần một workflow n8n và một chút cấu hình, bạn đã có một **trợ lý AI toàn năng** hoạt động 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Điều này đảm bảo tính riêng tư, tốc độ cao và khả năng mở rộng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý AI nhanh)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần phải chuyển đổi giữa các công cụ để xử lý âm thanh, hình ảnh và video.
- **Tương tác đa dạng:** Trợ lý AI có thể **nghe** ghi âm, **nhìn** hình ảnh và **phân tích** video để trả lời chính xác.
- **Cá nhân hóa:** Điều chỉnh hệ thống prompt của AI để phù hợp với nhu cầu cụ thể của team.
- **Hoạt động liên tục:** Workflow chạy tự động 24/7, không cần can thiệp thủ công.
- **Tích hợp Slack:** Trả lời ngay trong kênh Slack, không cần chuyển đổi giữa các ứng dụng.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Slack** và **bot Slack** (đã cấp quyền `chat:write`, `files:read`, `files:write`).
2. **API Key** của các mô hình AI sau:
   - **OpenAI** (để transcribe âm thanh).
   - **Google Gemini** (để phân tích hình ảnh và video).
   - **Claude (Anthropic)** (để làm việc với AI Agent).
3. **Tài khoản n8n** (self-hosted hoặc n8n.cloud).
4. **File mẫu** (âm thanh, hình ảnh, video) để test.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/9149) hoặc sao chép JSON từ trang này.
2. Trong n8n Editor, nhấn **Import** và dán JSON vào.
3. Chọn **Create Workflow** để hoàn tất.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Slack Trigger**
- Mở node **Slack Trigger** và tạo **credentials** mới:
  - Nhập **API Token** của bot Slack (đã cấp quyền trước).
  - Lưu lại.

#### **B. Cấu hình API Keys cho AI**
1. **OpenAI (Transcribe âm thanh):**
   - Mở node **Transcribe a recording** → Tạo credentials mới.
   - Nhập **API Key** từ tài khoản OpenAI.
   - Chọn **model** phù hợp (ví dụ: `whisper-1`).

2. **Google Gemini (Phân tích hình ảnh/video):**
   - Mở node **Analyze an image** và **Analyze video** → Tạo credentials mới.
   - Nhập **API Key** từ tài khoản Google Cloud (đã kích hoạt API Gemini).

3. **Claude (Anthropic) - AI Agent:**
   - Mở node **Anthropic Chat Model** → Tạo credentials mới.
   - Nhập **API Key** từ tài khoản Claude.
   - Chọn mô hình `claude-sonnet-4-20250514`.

#### **C. Cấu hình AI Agent**
- Mở node **AI Agent** và điều chỉnh **system prompt** để phù hợp với nhu cầu của team. Ví dụ:
  ```
  Bạn là một trợ lý AI chuyên nghiệp, hỗ trợ xử lý yêu cầu từ Slack.
  Khi nhận được âm thanh, hãy transcribe và trả lời nội dung.
  Khi nhận được hình ảnh/video, hãy phân tích và cung cấp kết quả chi tiết.
  ```

#### **D. Cấu hình bộ nhớ (Memory Buffer Window)**
- Mở node **Simple Memory** và thiết lập số lượng **messages** AI có thể đọc lại (ví dụ: 5).

#### **E. Kết nối các node xử lý file**
- Các node **Get Audio File**, **Get a Picture File**, **Get Video File** sẽ tự động lấy file từ Slack khi có yêu cầu.
- Đảm bảo các node này được kết nối với **Slack Trigger** và **AI Agent**.

### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Gửi một tin nhắn trong Slack với **âm thanh**, **hình ảnh** hoặc **video** để test.
   - Kiểm tra kết quả trả lời từ AI Agent.
2. **Bật Active:**
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với các kênh khác:**
   - Sử dụng **HTTP Request** để kết nối với **Telegram**, **Email** hoặc **Google Drive** để lưu kết quả phân tích.

2. **Lưu log hoạt động:**
   - Thêm node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử tương tác và phân tích hiệu suất.

3. **Tự động gửi báo cáo:**
   - Sử dụng **Date & Time Tool** để gửi báo cáo định kỳ (ví dụ: hàng ngày) về hoạt động của AI Agent.

4. **Cải thiện hệ thống prompt:**
   - Thử nghiệm với các mô hình AI khác (ví dụ: **Anthropic Claude 3**) để tối ưu hóa kết quả.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa tương tác AI trong Slack với **âm thanh, hình ảnh và video**. Không cần code, không cần kỹ thuật viên, chỉ cần một chút cấu hình, bạn đã có một **trợ lý AI toàn năng** hoạt động 24/7!

**Hãy thử ngay và tiết kiệm thời gian, tăng hiệu suất cho team của mình!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/9149)**
**📌 [Hướng dẫn chi tiết cấu hình](https://docs.n8n.io/)**