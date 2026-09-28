---
title: "🎙️ Tự Động Chuyển Âm Thanh Sang Văn Bản với OpenAI GPT-4o-mini (API Speech-to-Text) - N8n"
description: "Workflow tự động hóa chuyển âm thanh thành văn bản bằng OpenAI GPT-4o-mini chỉ với 4 node, không cần viết code. Giúp doanh nghiệp tiết kiệm thời gian ghi chép, cải thiện chính xác và cá nhân hóa dịch vụ. Hoạt động 24/7 trên VPS riêng."
slug: "tieu-dong-chuyen-am-than-sang-van-ban-openai-gpt4o-mini-n8n"
tags: [n8n, automation, speech-to-text, OpenAI, no-code, AI, document-extraction]
keywords: [n8n workflow speech to text, tự động hóa chuyển âm thanh sang văn bản, OpenAI API, GPT-4o-mini transcribe, tự động hóa văn phòng, API webhook]
---

# 🚀 **Tự Động Chuyển Âm Thanh Sang Văn Bản Với OpenAI GPT-4o-mini (API Speech-to-Text)**

## **Giới Thiệu**
Bạn đã từng phải tốn thời gian ghi chép lại những cuộc gọi, cuộc họp, hoặc âm thanh từ các file audio? Hay phải đối mặt với những bản ghi không chính xác, mất nhiều thời gian? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **n8n**, bạn có thể xây dựng một **API Speech-to-Text hoàn toàn tự động** chỉ trong vài phút, sử dụng **OpenAI GPT-4o-mini** để chuyển đổi âm thanh thành văn bản với độ chính xác cao. Không cần viết một dòng code nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 và không bị gián đoạn, các sếp nên **cài đặt n8n trên VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải nghe lại và ghi chép thủ công.
- **Chính xác cao**: Sử dụng mô hình AI tiên tiến của OpenAI.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
- **Cá nhân hóa**: Tích hợp dễ dàng với các ứng dụng khác (Slack, Email, CRM...).
- **Giảm lỗi**: Tránh sai sót khi ghi chép bằng tay.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** và **API Key** của OpenAI.
2. **VPS** để cài đặt n8n (không cần nếu dùng n8n Cloud, nhưng không ổn định).
3. **Trang web hoặc ứng dụng** để gọi API (có thể là một frontend đơn giản như ví dụ dưới đây).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io](https://n8n.io/workflows/5925) hoặc copy JSON từ trang này.
- **Bước 2**: Mở **n8n Editor** và chọn **"Import Workflow"** (hoặc paste JSON vào).
- **Bước 3**: Chọn **"Active"** để kích hoạt workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Webhook (Nhận file âm thanh)**
- **Tên node**: `Webhook containing audio to transcribe`
- **Cấu hình**:
  - **HTTP Method**: `POST`
  - **Path**: `audio-to-transcribe` (không cần thay đổi)
  - **Credentials**: Không cần thiết (n8n tự động tạo URL).

##### **🔹 Node 2: Transcribe with OpenAI (Chuyển âm thanh thành văn bản)**
- **Tên node**: `Transcribe with OpenAI`
- **Cấu hình**:
  - **Credentials**: Thêm `openAiApi` (nếu chưa có, tạo mới).
  - **API Key**: Điền **API Key** của OpenAI (tìm trong tài khoản OpenAI).
  - **URL**: `https://api.openai.com/v1/audio/transcriptions`
  - **Headers**:
    - `Authorization`: `Bearer {API_KEY}`
    - `Content-Type`: `multipart/form-data`
  - **Body**:
    - **File**: `audio_file` (n8n sẽ tự động gửi file âm thanh từ Webhook).
    - **Model**: `gpt-4o-mini` (mô hình AI của OpenAI).
    - **Response Format**: `json` (để nhận kết quả dưới dạng JSON).

##### **🔹 Node 3: Extract transcript (Lấy văn bản từ kết quả)**
- **Tên node**: `Extract transcript`
- **Cấu hình**:
  - **Operation**: `Set`
  - **Property**: `Transcript` (n8n sẽ lấy phần `text` từ kết quả API và đặt vào biến `Transcript`).

##### **🔹 Node 4: Respond to Webhook (Trả về văn bản cho frontend)**
- **Tên node**: `Respond to Webhook with transcript`
- **Cấu hình**:
  - **Response**: Chọn `Transcript` (biến chứa văn bản đã chuyển đổi).
  - **Format**: `JSON` (để frontend dễ dàng đọc kết quả).

#### **3. Kích hoạt ⚡️**
- **Bước 1**: Test run với một file âm thanh mẫu (ví dụ: một file `.mp3` hoặc `.wav`).
- **Bước 2**: Bật **Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sau khi chuyển đổi thành văn bản, gửi kết quả lên Slack/Telegram thông qua **n8n Slack Node** hoặc **Telegram Bot Node**.

2. **Lưu log và báo cáo**:
   - Sử dụng **n8n Google Sheets Node** để lưu tất cả các bản ghi chuyển đổi vào một bảng Excel tự động.

3. **Tự động gửi email kết quả**:
   - Kết hợp với **n8n Email Node** để gửi văn bản chuyển đổi qua email cho các thành viên nhóm.

4. **Tối ưu hóa mô hình AI**:
   - Thay đổi mô hình từ `gpt-4o-mini` sang `whisper-1` (nếu muốn tiết kiệm chi phí).

---

### 📌 **Kết luận**
Workflow này giúp **tự động hóa hoàn toàn quá trình chuyển âm thanh thành văn bản**, tiết kiệm thời gian và giảm thiểu lỗi. **Không cần viết code**, chỉ cần cài đặt và chạy trên VPS!

**Hãy áp dụng ngay và nâng cao hiệu suất làm việc của doanh nghiệp!** 🚀

---
**🔹 Xem thêm:**
- [Tutorial cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-vps/)
- [Tài liệu API OpenAI](https://platform.openai.com/docs/api-reference/audio/createTranscription)