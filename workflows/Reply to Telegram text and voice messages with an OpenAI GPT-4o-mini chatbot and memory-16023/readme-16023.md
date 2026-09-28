---
title: "🤖 **Tự Động Hóa Chatbot Telegram AI với GPT-4o-mini: Trả Lời Tin Nhắn Văn Bản & Âm Thanh + Nhớ Lịch Sử Hỏi Đáp**"
description: "Workflow này tự động trả lời tất cả tin nhắn văn bản và âm thanh trên Telegram bằng AI GPT-4o-mini, tích hợp công cụ tra cứu Wikipedia, tính toán và nhớ lịch sử hội thoại. Giúp doanh nghiệp hỗ trợ khách hàng 24/7 mà không cần nhân viên."
slug: "tieu-dong-hoa-chatbot-telegram-ai-gpt-4o-mini"
tags: [n8n, automation, telegram-bot, ai-chatbot, openai-gpt-4o-mini, google-sheets-logging]
keywords: [tự động hóa chatbot telegram, gpt-4o-mini tự động trả lời, nhớ lịch sử hội thoại ai, tra cứu wikipedia trong chatbot, tính toán tự động trong telegram]
---

# 🚀 **Chatbot Telegram AI Tự Động Hóa với GPT-4o-mini: Trả Lời Âm Thanh + Nhớ Lịch Sử**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, khi doanh nghiệp sử dụng Telegram hỗ trợ khách hàng, việc phải **phản hồi từng tin nhắn văn bản hoặc âm thanh thủ công** là một công việc **mệt mỏi và tốn thời gian**. Thêm vào đó, khách hàng thường **quên lịch sử trước đó**, dẫn đến trải nghiệm không mượt mà.

**Workflow này giải quyết tất cả:**
✅ **Trả lời tự động** tất cả tin nhắn văn bản và âm thanh trên Telegram bằng AI GPT-4o-mini.
✅ **Chuyển đổi âm thanh thành văn bản** tự động (OCR) bằng OpenAI.
✅ **Nhớ lịch sử hội thoại** để AI trả lời liên tục và logic hơn.
✅ **Tra cứu Wikipedia & tính toán tự động** khi khách hàng hỏi về kiến thức hoặc toán học.
✅ **Ghi log tất cả hội thoại** vào Google Sheets để theo dõi và phân tích.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** phản hồi khách hàng (không cần nhân viên hỗ trợ 24/7).
- **Trải nghiệm khách hàng chuyên nghiệp** với AI nhớ lịch sử và trả lời logic.
- **Tự động tra cứu Wikipedia** khi khách hàng hỏi về kiến thức (ví dụ: "AI là gì?").
- **Tính toán tự động** (ví dụ: "1000 nhân 50 bằng bao nhiêu?").
- **Báo cáo chi tiết** tất cả hội thoại trong Google Sheets để phân tích.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Các sếp cần có:
✔ **Tài khoản Telegram Bot** (đăng ký tại [@BotFather](https://t.me/BotFather)).
✔ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
✔ **Google Sheets API** (cài đặt tại [Google Cloud Console](https://console.cloud.google.com/)).
✔ **File JSON của workflow** (tải từ [n8n.io/workflows/16023](https://n8n.io/workflows/16023)).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/16023](https://n8n.io/workflows/16023) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và **paste vào "Import Workflow"** trong n8n.

:::note[**Lưu Ý**]
- **Không cần chỉnh sửa cấu trúc** của workflow, chỉ cần **cấu hình các node quan trọng** sau.
:::

---

### **2. Các Bước Cấu Hình Bắt Buộc 📌**

#### **🔹 Node 1: Telegram Trigger (When Message Received)**
- **Chọn credential:** Tạo mới tại `Credentials > Add Credential > Telegram`.
- **Điền:**
  - **Bot Token:** API Key từ BotFather.
  - **Chat ID:** ID của chatbot (lấy từ Telegram bằng cách gửi `/get_id` cho bot).
  - **Update Type:** Chọn `message`.

#### **🔹 Node 2: If Voice Message (Phân Loại Tin Nhắn Âm Thanh)**
- **Không cần chỉnh sửa**, node này tự động phân loại tin nhắn văn bản và âm thanh.

#### **🔹 Node 3: Download Telegram Voice (Tải File Âm Thanh)**
- **Chọn credential:** Sử dụng credential Telegram đã tạo ở trên.
- **Không cần thêm tham số**, node này tự động tải file âm thanh từ Telegram.

#### **🔹 Node 4: Transcribe Voice with OpenAI (Chuyển Âm Thanh Sang Văn Bản)**
- **Chọn credential:** Tạo mới tại `Credentials > Add Credential > OpenAI`.
- **Điền:**
  - **API Key:** API Key OpenAI.
  - **Model:** Chọn `whisper-1` (mặc định).
  - **Language:** Chọn `vi` (Tiếng Việt) hoặc `en` (Tiếng Anh).

#### **🔹 Node 5: OpenAI Chat Model (GPT-4o-mini)**
- **Chọn credential:** Sử dụng credential OpenAI đã tạo.
- **Model:** Đảm bảo chọn `gpt-4o-mini` (hoặc `gpt-4o` nếu có).
- **Temperature:** Giữ mặc định (`0.7`) để AI trả lời logic.

#### **🔹 Node 6: Manage Conversation Memory (Nhớ Lịch Sử Hội Thoại)**
- **Không cần chỉnh sửa**, node này tự động lưu trữ lịch sử hội thoại.
- **Lưu ý:** Nếu muốn **xóa lịch sử cũ**, chỉnh sửa `windowSize` trong node này.

#### **🔹 Node 7: Fetch Information from Wikipedia (Tra Cứu Wikipedia)**
- **Không cần credential**, node này tự động tra cứu Wikipedia.
- **Lưu ý:** Nếu Wikipedia không trả lời được, AI sẽ tự động chuyển sang trả lời bằng GPT-4o-mini.

#### **🔹 Node 8: Perform Calculations (Tính Toán Tự Động)**
- **Không cần credential**, node này tự động tính toán toán học.
- **Ví dụ:** Nếu khách hàng gửi "1000 nhân 50", AI sẽ trả lời `50.000`.

#### **🔹 Node 9: Send Response via Telegram (Gửi Trả Lời Lại Telegram)**
- **Chọn credential:** Sử dụng credential Telegram đã tạo.
- **Không cần thêm tham số**, node này tự động gửi trả lời về Telegram.

#### **🔹 Node 10: Append Log to Sheets (Ghi Log Vào Google Sheets)**
- **Chọn credential:** Tạo mới tại `Credentials > Add Credential > Google Sheets`.
- **Điền:**
  - **Spreadsheet ID:** ID của file Google Sheets (lấy từ liên kết share).
  - **Sheet Name:** Tên sheet muốn ghi log (ví dụ: `Chatbot_Logs`).
  - **Headers:** Chọn `Use first row as headers`.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run:** Chạy thử với một tin nhắn mẫu (ví dụ: "Xin chào, AI là gì?").
2. **Kiểm tra log:** Mở Google Sheets để xem liệu hội thoại đã được ghi lại chưa.
3. **Bật Active:** Nếu test thành công, **bật workflow** để hoạt động 24/7.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối Slack/Telegram Cho Log Thông Báo**
- Thêm node **Slack** hoặc **Telegram** sau node `Append Log to Sheets` để nhận thông báo khi có tin nhắn mới.

### **🔹 Tự Động Gửi Báo Cáo Hàng Ngày**
- Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp hội thoại qua email hoặc Telegram mỗi ngày.

### **🔹 Cải Thiện AI Bằng Prompt Tùy Chỉnh**
- Chỉnh sửa **prompt** trong node `AI Conversation Agent` để AI trả lời phù hợp với ngành nghề của doanh nghiệp.

### **🔹 Sử Dụng Nhiều Tool AI Khác**
- Thêm node **toolCalculator** hoặc **toolWikipedia** khác để AI có thể tra cứu nhiều nguồn hơn.

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn tự động hóa hỗ trợ khách hàng trên Telegram **mà không cần code**. Với **GPT-4o-mini**, AI không chỉ trả lời tin nhắn văn bản mà còn **nhớ lịch sử, tra cứu Wikipedia và tính toán tự động**.

**🚀 Hãy áp dụng ngay và giảm thiểu công việc thủ công!**
Nếu có vấn đề, hãy để lại comment dưới đây, các sếp sẽ được hỗ trợ miễn phí. 😊

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::