---
title: "🤖 **Tự Động Hóa Trợ Lý AI Tìm Hiểu Lịch Sử Slack Bằng Ngôn Ngữ Tự Nhiên (OpenAI + n8n)**"
description: "Workflow này giúp các sếp tự động hóa việc phân tích lịch sử tin nhắn Slack bằng AI, trả lời các câu hỏi phức tạp bằng ngôn ngữ tự nhiên (ví dụ: 'Tóm tắt quyết định sprint vừa rồi', 'Ai là người bị blocker nhiều nhất?'). Thay vì tra cứu thủ công, AI tổng hợp thông tin chính xác từ dữ liệu thực tế trong channel."
slug: "tự-dộng-hoa-trợ-ly-ai-slack-openai-n8n"
tags: [n8n, automation, ai-rag, slack, openai, no-code, chatbot]
keywords: [tự động hóa slack, ai chatbot, query slack history, openai n8n, tự động hóa công việc văn phòng, chatbot ai cho doanh nghiệp]
---

# 🚀 **Trợ Lý AI Tự Động Phân Tích Lịch Sử Slack Bằng Ngôn Ngữ Tự Nhiên**

## **🔍 Nỗi Đau Của Các Sếp Và Giải Pháp**
Trong môi trường làm việc hiện đại, các team thường phải **tra cứu thủ công lịch sử tin nhắn Slack** để:
- Tóm tắt quyết định trong các cuộc họp.
- Xác định ai là người được giao nhiệm vụ và tiến độ thực hiện.
- Nhận biết các vấn đề "blocker" cần giải quyết ưu tiên.
- Tìm kiếm thông tin chia sẻ (file, link) trong thời gian cụ thể.

**Thủ công?** Tốn thời gian, dễ sai sót, và không thể phân tích toàn bộ dữ liệu. **Workflow này giải quyết vấn đề bằng cách:**
✅ **Tự động lấy lịch sử tin nhắn Slack** (24h, 1 tuần, tùy chọn).
✅ **Trả lời bằng AI** (OpenAI GPT-4o-mini) dựa trên **dữ liệu thực tế** trong channel (không hư cấu).
✅ **Cung cấp câu trả lời chi tiết** bằng ngôn ngữ tự nhiên (ví dụ: "Tóm tắt 5 điểm chính trong 24h qua").

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên Slack.
- **Chính xác 100%**: AI trả lời **chỉ dựa trên dữ liệu thực tế** trong channel (không hư cấu).
- **Tích hợp AI RAG**: Sử dụng **OpenAI GPT-4o-mini** để phân tích sâu dữ liệu lịch sử.
- **Hoạt động liên tục**: Workflow chạy tự động, không cần can thiệp người dùng.
- **Câu trả lời cá nhân hóa**: Trả lời các câu hỏi phức tạp như "Ai là người được nhắc nhiều nhất tuần này?".
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI**:
   - [Tạo API Key OpenAI](https://platform.openai.com/api-keys) (đã nạp tiền để sử dụng).
2. **App Slack**:
   - [Tạo App Slack](https://api.slack.com/apps) với **scopes** sau:
     - `channels:history`, `groups:history`, `im:history`, `mpim:history` (đọc lịch sử tin nhắn).
     - `channels:read`, `groups:read`, `users:read` (đọc thông tin channel và người dùng).
     - `chat:write` (nếu muốn bot trả lời lại Slack).
   - **Lấy Bot User OAuth Token** sau khi cài đặt app vào workspace.
3. **Channel Slack**:
   - **Channel ID** của channel muốn phân tích (có thể tìm bằng cách gửi tin nhắn `/api.test` trong channel và copy ID từ kết quả).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7669](https://n8n.io/workflows/7669) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7669) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **A. Node `Slack History` (Lấy lịch sử tin nhắn)**
- **Credentials**:
  - Chọn **Slack OAuth2 API** (đã tạo từ bước chuẩn bị).
- **Parameters**:
  - **Channel ID**: Nhập ID của channel cần phân tích (ví dụ: `C123456789`).
  - **Limit**: Thiết lập số lượng tin nhắn lấy (mặc định 1000, có thể điều chỉnh).
  - **Including timestamps**: Bật để AI phân tích theo thời gian.

##### **B. Node `OpenAI Chat Model` (Trả lời bằng AI)**
- **Credentials**:
  - Chọn **OpenAI API** (đã tạo từ bước chuẩn bị).
- **Parameters**:
  - **Model**: Chọn `gpt-4o-mini` (mặc định).
  - **Temperature**: Giá trị mặc định (0.7) để AI trả lời logic.
  - **System Prompt** (nếu cần chỉnh sửa):
     ```json
     "You are an AI assistant that answers questions based ONLY on the Slack channel history provided. Do not make assumptions or provide information outside of what's in the messages."
     ```

##### **C. Node `Chat with Slack` (Gửi câu hỏi từ Slack)**
- **Credentials**:
  - Chọn **Slack OAuth2 API** (cùng với node `Slack History`).
- **Parameters**:
  - **Channel ID**: Nhập ID channel tương tự như node `Slack History`.
  - **Text**: Đây là **câu hỏi người dùng** (ví dụ: "Tóm tắt 5 điểm chính trong 24h qua").

##### **D. Node `Slack Channel Chatbot` (Agent AI)**
- **Credentials**:
  - Chọn **OpenAI API** và **Slack OAuth2 API**.
- **Parameters**:
  - **Agent Name**: Đặt tên tùy ý (ví dụ: `SlackAIAssistant`).
  - **Memory**: Bật để AI nhớ các câu hỏi trước đó (nếu cần).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một **câu hỏi mẫu** vào node `Chat with Slack` (ví dụ: `"Give me a 5-bullet summary of the last 24 hours."`).
  - Kiểm tra AI trả lời có **chính xác** không (so với lịch sử tin nhắn thực tế).
- **Bật Active**:
  - Sau khi test thành công, bật **Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack Bot Trả Lời Tự Động**:
   - Sử dụng **node `Slack Tool`** để bot trả lời lại Slack khi được gọi (ví dụ: `/ai summarize`).
2. **Lưu Log Phân Tích**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử câu hỏi và câu trả lời.
3. **Báo Cáo Định Kỳ**:
   - Sử dụng **node `Set Interval`** để tự động gửi báo cáo tuần/month về các vấn đề "blocker" hoặc tiến độ task.
4. **Cải Thiện Prompt AI**:
   - Chỉnh sửa **System Prompt** trong node OpenAI để AI trả lời **cụ thể hơn** (ví dụ: yêu cầu AI liệt kê thời gian cụ thể của mỗi quyết định).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tra cứu thủ công trên Slack, đồng thời **tăng cường hiệu quả team** bằng cách phân tích dữ liệu một cách **tự động và chính xác**. **Thử ngay** với các câu hỏi mẫu:
- *"Tóm tắt 5 điểm chính trong 24h qua."*
- *"Ai là người được nhắc nhiều nhất tuần này?"*
- *"Hiển thị tin nhắn có từ khóa 'blocker' trong 2 ngày qua."*

**🚀 Áp dụng ngay để làm việc thông minh hơn!** 🚀

---
:::note[Lưu Ý Quan Trọng]
- **Giám sát AI**: Đôi khi AI có thể trả lời không chính xác (do dữ liệu lịch sử không đầy đủ). Các sếp nên **kiểm tra lại** trước khi dựa vào kết quả.
- **Giám sát Slack**: Nếu channel có nhiều tin nhắn, **giảm `Limit`** trong node `Slack History` để tránh timeout.
- **Mở rộng**: Workflow có thể **tích hợp với Microsoft Teams** hoặc **Discord** bằng cách thay thế node Slack.
:::

---
**🔗 [Xem workflow gốc trên n8n.io](https://n8n.io/workflows/7669)**
**📧 Có thắc mắc?** Liên hệ [Robert Breen](mailto:robert@ynteractive.com) để hỗ trợ tùy chỉnh!