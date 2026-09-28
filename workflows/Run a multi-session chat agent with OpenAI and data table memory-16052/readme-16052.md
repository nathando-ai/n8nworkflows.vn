---
title: "🤖 **Tự Động Hóa Chatbot AI Nhớ Lịch Sử Hẹn Trước - Không Cần Code!**"
description: "Workflow này giúp chatbot AI nhớ lại lịch sử hội thoại của người dùng giữa các phiên chat khác nhau, tự động lưu trữ thông tin trên bảng dữ liệu n8n (Data Table) - không cần cơ sở dữ liệu bên ngoài. Giúp người dùng không phải lặp lại thông tin, cải thiện trải nghiệm và tiết kiệm thời gian."
slug: "tieu-dong-hoa-chatbot-ai-nhom-lich-su-het-truong"
tags: [n8n, automation, ai-chatbot, no-code, long-term-memory]
keywords: [n8n workflow chatbot, tự động hóa chatbot nhớ lịch sử, AI nhớ người dùng, data table n8n, OpenAI tự động hóa]
---

# 🚀 **Chatbot AI Nhớ Lịch Sử Hẹn Trước - Giải Pháp Tự Động Hóa Miễn Cần Code**

### **Nỗi Đau Của Doanh Nghiệp & Người Dùng**
Bạn đã bao giờ phải **lặp lại cùng một thông tin** cho chatbot AI ở mỗi phiên chat mới? Hay **mất mát bối cảnh** giữa các cuộc trò chuyện? Đặc biệt với các ứng dụng hỗ trợ khách hàng, **AI không nhớ lịch sử** khiến trải nghiệm trở nên **khó chịu và không chuyên nghiệp**.

Hầu hết các giải pháp hiện nay yêu cầu:
❌ **Cơ sở dữ liệu bên ngoài** (tốn kém, phức tạp)
❌ **API gọi liên tục** (chậm, không hiệu quả)
❌ **Người dùng phải điền form** (gián tiếp, mất thời gian)

**Workflow này giải quyết tất cả!** Sử dụng **n8n Data Table** (bảng dữ liệu tích hợp sẵn) làm bộ nhớ dài hạn, **không cần cơ sở dữ liệu bên ngoài**, giúp chatbot AI **nhớ lại lịch sử hội thoại** của người dùng giữa các phiên chat khác nhau, **tự động lưu trữ thông tin** từ cuộc trò chuyện, và **không bao giờ làm người dùng phải lặp lại**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính riêng tư và hiệu suất tối ưu**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Người dùng **không phải lặp lại thông tin** ở mỗi phiên chat mới.
- **Trải nghiệm cá nhân hóa**: Chatbot **nhớ lại lịch sử** và tiếp tục cuộc trò chuyện từ điểm dừng cuối cùng.
- **Bảo mật & riêng tư**: **Không bao giờ lộ thông tin người dùng** cho người khác (dù họ có cùng tên).
- **Không cần cơ sở dữ liệu bên ngoài**: Sử dụng **n8n Data Table** tích hợp sẵn, **không tốn chi phí API**.
- **Hoạt động liên tục**: Cài trên VPS, workflow **chạy 24/7** mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✅ **API Key OpenAI** (để kết nối với mô hình AI)
✅ **Bảng dữ liệu n8n (Data Table)** có tên `chat_sessions_data` với các cột sau:
| Cột | Loại Dữ liệu | Mô Tả |
|------|--------------|--------|
| `session_id` | Text | ID duy nhất cho mỗi phiên chat |
| `channel` | Text | Kênh trò chuyện (ví dụ: "web", "slack") |
| `channel_id` | Text | ID cụ thể của kênh (ví dụ: "12345") |
| `user_id` | Text | ID người dùng (nếu có) |
| `first_name` | Text | Tên đầu tiên của người dùng |
| `last_name` | Text | Tên cuối của người dùng |
| `company` | Text | Công ty/doanh nghiệp (nếu có) |
| `last_topic` | Text | Chủ đề cuối cùng được thảo luận |
| `last_intent` | Text | Ý định cuối cùng của người dùng |
| `unresolved_question` | Text | Câu hỏi chưa được giải quyết |
| `conversation_stage` | Text | Bước tiến của cuộc trò chuyện |
| `last_session_date` | DateTime | Thời gian phiên chat cuối |
| `interested_in` | Text | Điểm quan tâm của người dùng |
| `chat_history` | Text | Lịch sử cuộc trò chuyện |
| `execution_time` | DateTime | Thời gian thực thi |
| `current_time` | DateTime | Thời gian hiện tại (tự động) |

✅ **Thời gian múi giờ (Timezone)** của workflow (để lưu timestamp chính xác).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấp vào **"Import"** (hoặc **"Create new workflow"**).
3. Chọn **"Import from JSON"** và dán nội dung JSON từ [link gốc](https://n8n.io/workflows/16052).
4. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/16052/download) và chọn **"Upload JSON file"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **cần cấu hình** các node quan trọng sau:

##### **A. Cấu Hình Bảng Dữ liệu (Data Table)**
- **Tên bảng**: `chat_sessions_data` (phải khớp với tên trong workflow).
- **Cấu trúc cột**: Đảm bảo bảng có **tất cả các cột** như trong bảng trên (nếu thiếu, workflow sẽ lỗi).

##### **B. Node `OpenAI Chat Model`**
- **API Key OpenAI**:
  - Đi đến **Settings → Credentials → Add Credential**.
  - Chọn **OpenAI API** và nhập **API Key** từ tài khoản OpenAI.
  - Trong node `OpenAI Chat Model`, chọn **credentials** là `openAiApi`.
- **Mô hình AI**:
  - Mặc định là `gpt-5.3-chat-latest` (nếu không có, có thể thay bằng `gpt-4` hoặc `gpt-3.5-turbo`).

##### **C. Node `When chat message received` (Chat Trigger)**
- **Kênh trò chuyện**:
  - Nếu muốn kết nối với **Slack/Telegram/Webhook**, cần cấu hình **trigger** tương ứng.
  - Ví dụ: Nếu dùng **webhook**, thêm node **HTTP Request** trước `chatTrigger`.

##### **D. Node `Simple Memory` (Bộ nhớ ngắn hạn)**
- **Sliding Window**: Mặc định là **10 lượt trò chuyện** (có thể điều chỉnh).

##### **E. Node `lookup_past_session_by_email` & `lookup_past_session_by_name`**
- **Trường tìm kiếm**:
  - Đảm bảo bảng `chat_sessions_data` có cột `email` và `first_name`/`last_name`.
  - Nếu không có, cần **thêm cột** hoặc **cập nhật logic** trong node `dataTableTool`.

##### **F. Node `update_chat_session_record`**
- **Cập nhật tự động**: Node này sẽ **ghi đè** thông tin như `name`, `email`, `company` nhưng **thêm vào** `chat_history`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **"Run Workflow"** và gửi một **tin nhắn mẫu** (ví dụ: *"Tôi là John Doe, email john@example.com, tôi muốn hỏi về sản phẩm X"*).
   - Kiểm tra **Data Table** xem liệu thông tin đã được lưu không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển **status** từ **"Inactive"** sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack/Telegram Incoming Webhook** trước `chatTrigger` để nhận tin nhắn từ kênh này.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Notion** để **ghi lại lịch sử hoạt động** của chatbot.

3. **Gửi báo cáo định kỳ**:
   - Tạo một **workflow khác** sử dụng **n8n Schedule Node** để **tổng hợp và gửi báo cáo** về hoạt động của chatbot.

4. **Xóa phiên chat cũ**:
   - Thêm node **n8n-nodes-base.date** để **xóa phiên chat cũ** sau một thời gian (ví dụ: 30 ngày).

5. **Thay đổi mô hình AI**:
   - Nếu muốn dùng **Anthropic Claude** hoặc **Google Gemini**, thay thế node `lmChatOpenAi` bằng node tương ứng.

6. **Sử dụng ID điện thoại thay vì email**:
   - Cập nhật logic trong `lookup_past_session_by_email` để tìm kiếm theo **số điện thoại** thay vì email.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn **tự động hóa chatbot AI nhớ lịch sử**, **cải thiện trải nghiệm người dùng**, và **tiết kiệm thời gian** mà **không cần code**.

**Hãy áp dụng ngay!**
1. **Cài đặt n8n trên VPS** (để đảm bảo ổn định).
2. **Import workflow** và **cấu hình** như hướng dẫn.
3. **Test với dữ liệu mẫu** và **bật hoạt động**.
4. **Mở rộng** với các tính năng nâng cao như **Slack/Telegram** hoặc **báo cáo tự động**.

**Chatbot của bạn sẽ trở nên thông minh hơn bao giờ hết!** 🚀