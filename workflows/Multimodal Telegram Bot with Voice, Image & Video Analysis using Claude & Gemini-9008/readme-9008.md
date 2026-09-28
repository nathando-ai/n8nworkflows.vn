---
title: "🤖 **Tự Động Hóa Bot Telegram Multimodal: Phân Tích Âm Thanh, Hình Ảnh & Video Với Claude & Gemini (Không Cần Code!)**"
description: "Workflow này tự động nhận dạng và phân tích nội dung từ tin nhắn âm thanh, hình ảnh và video trên Telegram, trả về kết quả phân tích chi tiết từ Claude (Anthropic) và Gemini (Google) thông qua AI Agent. Giúp các sếp tiết kiệm thời gian phân tích nội dung đa phương tiện một cách nhanh chóng và chính xác."
slug: "tieu-dong-hoa-bot-telegram-multimodal-ai"
tags: [n8n, automation, no-code, ai-multimodal, telegram-bot, claude-ai, google-gemini, content-creation]
keywords: [tự động hóa bot telegram, phân tích âm thanh hình ảnh video, claude sonnet, google gemini, n8n workflow, ai agent, no-code automation]
---

# 🚀 **Bot Telegram Multimodal: Phân Tích Âm Thanh, Hình Ảnh & Video Với AI Claude & Gemini**

## **💡 Giới thiệu: Giải pháp tự động hóa phân tích nội dung đa phương tiện cho doanh nghiệp**
Hiện nay, việc phân tích âm thanh, hình ảnh và video thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Các sếp thường phải:
- **Lắng nghe và ghi chép** nội dung từ file âm thanh dài.
- **Mô tả và phân tích** hình ảnh/video một cách chủ quan.
- **Tốn công sức** để tổng hợp kết quả từ nhiều nguồn khác nhau.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động nhận dạng** âm thanh, hình ảnh và video từ Telegram.
✅ **Phân tích sâu** nội dung bằng **Claude (Anthropic)** và **Gemini (Google)**.
✅ **Trả về kết quả** dưới dạng tin nhắn Telegram, giúp các sếp **tiết kiệm thời gian lên đến 80%** trong quá trình phân tích.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần nghe/nhìn thủ công, AI làm tất cả.
- **Chính xác cao**: Phân tích bằng AI Claude và Gemini với độ chính xác gần như con người.
- **Tích hợp hoàn hảo**: Kết quả được gửi trực tiếp qua Telegram, dễ theo dõi và lưu trữ.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp của con người.
- **Cá nhân hóa**: Có thể điều chỉnh **System Prompt** của AI Agent để phù hợp với nhu cầu cụ thể của doanh nghiệp.
:::

---
## **🔧 Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản Telegram & Token API**
- Tạo **bot Telegram** mới:
  - Tìm **@BotFather** trên Telegram.
  - Gửi lệnh `/newbot` và theo hướng dẫn tạo bot.
  - Lưu **API Token** của bot (sẽ cần dùng để cấu hình trong n8n).

### **2. API Keys cho các mô hình AI**
| **Dịch vụ AI**       | **Mô hình sử dụng**       | **Hướng dẫn lấy API Key**                                                                 |
|----------------------|---------------------------|------------------------------------------------------------------------------------------|
| **OpenAI**           | Transcribe âm thanh       | [Tạo tài khoản OpenAI](https://platform.openai.com/) → Mua credits → Lấy API Key.         |
| **Anthropic (Claude)** | Chat & phân tích văn bản  | [Tạo tài khoản Claude](https://www.anthropic.com/) → Mua credits → Lấy API Key.          |
| **Google Gemini**     | Phân tích hình ảnh/video   | [Tạo tài khoản Google Cloud](https://cloud.google.com/) → Bật API Gemini → Lấy API Key. |

### **3. Cài đặt n8n (Self-hosted)**
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/9008) (hoặc sao chép JSON từ trang này).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON đã tải.
3. Chọn **Create New Workflow** và nhấn **Import**.

#### **Phương pháp 2: Sao chép JSON trực tiếp**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** → Dán toàn bộ JSON từ [trang workflow](https://n8n.io/workflows/9008).
3. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **16 node**, nhưng các bước quan trọng nhất cần chú ý:

#### **🔹 Cấu hình Credentials (API Keys)**
| **Node**               | **Credentials cần thiết**       | **Hướng dẫn điền**                                                                 |
|------------------------|----------------------------------|--------------------------------------------------------------------------------------|
| **Telegram Trigger**   | `telegramApi`                    | Dán **API Token** của bot Telegram (đã tạo ở trên).                                |
| **Transcribe a recording** | `openAiApi`               | Dán **API Key OpenAI** (đã mua credits).                                            |
| **Anthropic Chat Model** | `anthropicApi`            | Dán **API Key Claude** (Anthropic).                                                  |
| **Analyze video/image** | `googlePalmApi`              | Dán **API Key Google Gemini** (đã kích hoạt API trên Google Cloud).                |

#### **🔹 Cấu hình AI Agent (Node "AI Agent")**
- Node này là **cốt lõi** của workflow, giúp tổng hợp kết quả từ các mô hình AI.
- **Cấu hình quan trọng:**
  - **System Prompt**: Điều chỉnh để phù hợp với nhu cầu phân tích của doanh nghiệp.
    Ví dụ:
    ```plaintext
    Bạn là một trợ lý AI chuyên phân tích nội dung đa phương tiện.
    Sau khi nhận được kết quả từ OpenAI (âm thanh), Google Gemini (hình ảnh/video), hãy tổng hợp và trả về:
    1. Tóm tắt nội dung chính.
    2. Điểm mạnh/điểm yếu (nếu là video).
    3. Gợi ý cải tiến (nếu là hình ảnh).
    ```
  - **Memory Buffer Window**: Chỉ định số lượng tin nhắn AI Agent nhớ (ví dụ: 5 tin nhắn trước đó).

#### **🔹 Cấu hình Switch (Node "Switch")**
- Node này **xác định loại tin nhắn** người dùng gửi (âm thanh, hình ảnh, video).
- **Không cần chỉnh sửa**, workflow sẽ tự động phân loại.

#### **🔹 Cấu hình Telegram (Node "Send Regular Message")**
- Node này **gửi kết quả phân tích** về Telegram.
- **Không cần chỉnh sửa**, nhưng có thể thêm **stickers, emoji** để làm đẹp tin nhắn.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **âm thanh, hình ảnh hoặc video** từ Telegram đến bot.
   - Kiểm tra kết quả phân tích trên Telegram.
2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor.

---
## **✍️ Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Email**
- Thay vì chỉ gửi kết quả qua Telegram, các sếp có thể **gửi báo cáo định kỳ** qua Slack hoặc Email bằng node **Slack** hoặc **Email**.
- **Cách làm:**
  - Thêm node **Slack** hoặc **Email** sau node **Send Regular Message**.
  - Cấu hình **credentials** và **template** cho tin nhắn.

### **2. Lưu log phân tích**
- Sử dụng node **Google Sheets** hoặc **Notion** để **lưu tất cả kết quả phân tích** vào bảng dữ liệu.
- **Cách làm:**
  - Thêm node **Google Sheets** sau node **Merge**.
  - Cấu hình **Sheet Name** và **credentials** của Google.

### **3. Cải tiến System Prompt cho AI Agent**
- Nếu muốn **AI Agent trả về kết quả chi tiết hơn**, các sếp có thể điều chỉnh **System Prompt** như sau:
  ```plaintext
  Bạn là một chuyên gia phân tích nội dung đa phương tiện.
  Sau khi nhận kết quả từ các mô hình AI, hãy:
  1. Trích dẫn **tất cả điểm chính** trong âm thanh/hình ảnh/video.
  2. Đánh giá **độ phù hợp** với mục tiêu doanh nghiệp.
  3. Gợi ý **cách cải thiện** nội dung (nếu có).
  ```

### **4. Sử dụng Multiple LLM**
- Nếu muốn **so sánh kết quả** từ nhiều mô hình AI khác nhau (ví dụ: Claude + Mistral), các sếp có thể:
  - Thêm node **lmChatMistral** (nếu có API Key).
  - Sử dụng node **Merge** để tổng hợp kết quả từ nhiều mô hình.

---
## **📌 Kết luận**
Workflow **Bot Telegram Multimodal** này là **giải pháp hoàn hảo** để các sếp tự động hóa việc phân tích âm thanh, hình ảnh và video một cách **nhanh chóng, chính xác và không cần code**.

👉 **Hành động ngay:**
1. **Cài đặt n8n** trên VPS (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API Keys.
3. **Test Run** với dữ liệu mẫu.
4. **Bật Active** và bắt đầu tự động hóa!

**Chúc các sếp thành công với việc tự động hóa công việc phân tích nội dung!** 🚀