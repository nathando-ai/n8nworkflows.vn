---
title: "🚀 Tự Động Hóa Bot Nhắc Nhở Telegram Thông Minh với GPT-4 Mini & Airtable (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn giúp các sếp quản lý nhắc nhở cá nhân thông qua Telegram, lưu trữ trên Airtable và cho phép hủy bỏ nhắc nhở bằng mã duy nhất - hoạt động 24/7 mà không cần viết dòng code nào."
slug: "tự-dộng-hoa-bot-nhắc-nhở-telegram-gpt-4-mini-airtable"
tags: [n8n, automation, no-code, ai-chatbot, airtable, telegram-bot, gpt-4-mini]
keywords: [tự động hóa nhắc nhở telegram, bot nhắc nhở ai, airtable n8n, gpt-4 mini workflow, tự động hóa cá nhân hóa, cancel code reminder]
---

# 🚀 **Bot Nhắc Nhở Telegram Thông Minh: Tự Động Hóa Quản Lý Nhiệm Vụ Cá Nhân**

### **💡 Giải Pháp Cho Nỗi Đau "Quên Nhiệm Vụ" Của Các Sếp**
Các sếp đã từng phải đối mặt với tình huống:
- **"Quên gọi mẹ vào 6h tối"** → Lúc đó mới nhớ, nhưng đã quá muộn.
- **"Đã đặt nhắc nhở trên điện thoại nhưng không thể quản lý tập trung"** → Nhiều nhắc nhở trùng lặp, khó theo dõi.
- **"Muốn hủy bỏ nhắc nhở nhưng không biết cách"** → Phải nhớ mã hoặc phải nhờ người khác.

**Workflow này giải quyết tất cả!** Với **Telegram + GPT-4 Mini + Airtable**, các sếp có thể:
✅ **Đặt nhắc nhở bằng giọng nói tự nhiên** (ví dụ: *"Remind me at 6pm to call mom"*).
✅ **Hủy nhắc nhở bằng mã duy nhất** (không cần nhớ nội dung).
✅ **Tự động nhắc nhở qua Telegram** khi đến giờ.
✅ **Lưu trữ tất cả nhắc nhở trên Airtable** để theo dõi và phân tích.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập thông tin nhắc nhở thủ công.
- **Chính xác 100%**: GPT-4 Mini tự động phân tích và tạo nhắc nhở theo định dạng chuẩn.
- **Hủy bỏ dễ dàng**: Chỉ cần gửi mã duy nhất qua Telegram.
- **Hoạt động liên tục**: Scheduler tự động kiểm tra và gửi nhắc nhở mỗi 5 phút.
- **Dữ liệu trung tâm**: Tất cả nhắc nhở được lưu trên Airtable, dễ dàng theo dõi và báo cáo.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Bot Telegram (tạo từ [@BotFather](https://t.me/BotFather)).
   - API Token của bot (để kết nối với n8n).
2. **Tài khoản Airtable**:
   - Base mới tên **"REMINDER-TABLE"**.
   - Bảng với các trường bắt buộc:
     - `chat_id` (Text) – ID chat của người dùng.
     - `title` (Text) – Tiêu đề nhắc nhở.
     - `due_at` (Date/Time) – Thời gian nhắc nhở.
     - `code` (Text) – Mã hủy bỏ duy nhất.
   - Token Personal Access của Airtable (để kết nối với n8n).
3. **Tài khoản OpenAI** (tùy chọn nhưng **khuyến nghị**):
   - API Key để sử dụng GPT-4 Mini.
4. **VPS cho n8n** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7921) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi cú pháp).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **16 node** với các cấu hình quan trọng sau:

##### **A. Cấu Hình Telegram**
- **Node "Telegram Trigger"**:
  - Điền **API Token** từ BotFather vào `credentials` (tên: `telegramApi`).
  - Chọn **Update** (để bot lắng nghe tin nhắn mới).
- **Node "Send a text message"**:
  - Sử dụng cùng `credentials` (`telegramApi`) để gửi tin nhắn nhắc nhở.

##### **B. Cấu Hình Airtable**
- **Node "Create a record"**:
  - Điền **Airtable Token** vào `credentials` (tên: `airtableTokenApi`).
  - Đảm bảo bảng **REMINDER-TABLE** có các trường như hướng dẫn.
- **Node "Search records"**:
  - Cấu hình cùng `credentials` (`airtableTokenApi`).
  - Tham số `operation` mặc định là `search`.
- **Node "Delete a record"**:
  - Cấu hình cùng `credentials` (`airtableTokenApi`).
  - Tham số `operation` mặc định là `deleteRecord`.

##### **C. Cấu Hình AI Agent (GPT-4 Mini)**
- **Node "OpenAI Chat Model"**:
  - Điền **API Key OpenAI** vào `credentials` (tên: `openAiApi`).
  - Đảm bảo **model** được chọn là `gpt-4.1-mini`.
- **Node "AI Agent"**:
  - Sử dụng **LangChain Agent** để phân tích tin nhắn tự nhiên thành nhắc nhở có cấu trúc.
  - **Prompt mẫu**:
    ```
    Parse the user's message into a structured reminder with:
    - Title: Description of the task.
    - Due date/time: When the reminder should trigger.
    - Timezone: User's timezone (default: Asia/Ho_Chi_Minh).
    - Generate a unique cancellation code (6 digits).
    ```

##### **D. Cấu Hình Scheduler**
- **Node "Code" (Scheduler)**:
  - Thiết lập **interval** (ví dụ: `5 minutes`) để tự động kiểm tra nhắc nhở đến hạn.
  - Mẫu code:
    ```javascript
    // Fetch all reminders due in the next 5 minutes
    const now = new Date();
    const fiveMinutesLater = new Date(now.getTime() + 5 * 60 * 1000);

    return {
      json: {
        due_at: { "$lt": fiveMinutesLater.toISOString() },
        status: "pending"
      }
    };
    ```

##### **E. Cấu Hình Logic Hủy Nhắc Nhở**
- **Node "CHECK IF CODE IS THERE"**:
  - Kiểm tra xem mã hủy có tồn tại trong Airtable không.
- **Node "CODE FOUND?"**:
  - Nếu mã tồn tại → **xóa nhắc nhở** và gửi tin nhắn xác nhận.
  - Nếu mã không tồn tại → gửi tin nhắn **"Code not found"**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn mẫu:
    ```
    Remind me at 6pm to call mom
    ```
  - Kiểm tra nhắc nhở được tạo trên Airtable và bot Telegram phản hồi.
- **Bật Active**:
  - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để gửi nhắc nhở đến nhiều kênh.
2. **Lưu Log Hoạt Động**:
   - Sử dụng node **StickyNote** để ghi lại lịch sử nhắc nhở và lỗi.
3. **Báo Cáo Định Kỳ**:
   - Tạo một workflow riêng để gửi báo cáo tổng hợp nhắc nhở đã hoàn thành/hủy bỏ.
4. **Cải Thiện Prompt AI**:
   - Tùy chỉnh prompt để AI hiểu rõ hơn về **timezone** hoặc **priorities** (nhắc nhở ưu tiên).
5. **Tích Hợp với Google Calendar**:
   - Sử dụng node **Google Calendar** để đồng bộ nhắc nhở với lịch cá nhân.
:::

---
### 📌 **Kết Luận**
Workflow này không chỉ **giải phóng thời gian** mà còn **cải thiện hiệu suất cá nhân** của các sếp. Với **GPT-4 Mini**, nhắc nhở được tạo tự động từ lời nói tự nhiên; **Airtable** lưu trữ dữ liệu một cách chuyên nghiệp; và **Telegram** đảm bảo các sếp không bao giờ quên nhiệm vụ.

**Hãy áp dụng ngay và trải nghiệm sự khác biệt!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/7921) và bắt đầu tự động hóa nhắc nhở của mình!

---
:::note[CHÚ Ý CUỐI CÙNG]
- Nếu gặp lỗi, hãy kiểm tra lại **credentials** (API Key) và **cấu hình node**.
- Đối với **scheduler**, đảm bảo VPS của bạn **không ngắt kết nối** (n8n cần chạy liên tục).
- Nếu muốn mở rộng, các sếp có thể **tạo phiên bản riêng** với các tính năng như nhắc nhở nhóm hoặc nhắc nhở dựa trên vị trí.
:::

---
**🚀 Cảm ơn các sếp đã theo dõi!** Nếu có thắc mắc, hãy để lại bình luận dưới đây. 👇