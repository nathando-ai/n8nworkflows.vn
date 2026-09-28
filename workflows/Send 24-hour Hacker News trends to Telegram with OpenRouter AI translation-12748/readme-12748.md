---
title: "🚀 Tự Động Hóa Báo Cáo Xu Hướng Hacker News 24h Sang Telegram Với AI Dịch Tự Động (OpenRouter)"
description: "Workflow tự động hóa lấy dữ liệu xu hướng Hacker News trong 24h, lọc bỏ nội dung không quan trọng, tổng hợp và gửi báo cáo định kỳ sang Telegram bằng AI dịch sang nhiều ngôn ngữ (Tiếng Tây Ban Nha, Pháp, Trung, Nhật). Giúp các sếp tiết kiệm thời gian theo dõi xu hướng công nghệ hàng ngày."
slug: "tieu-dong-hoa-bao-cao-xu-huong-hacker-news-telegram-ai"
tags: [n8n, automation, ai, telegram, market-research, openrouter, algolia, no-code]
keywords: [tự động hóa hacker news, ai dịch tự động, telegram bot, xu hướng công nghệ, n8n workflow, openrouter gemini]
---

# 🚀 **Tự Động Hóa Báo Cáo Xu Hướng Hacker News 24h Sang Telegram Với AI Dịch Tự Động**

### **Giải Pháp Cho Các Sếp Theo Dõi Xu Hướng Công Nghệ Hàng Ngày**
Theo dõi xu hướng trên **Hacker News** thủ công là một công việc tốn thời gian và dễ bỏ lỡ những bài viết hot. Các sếp phải:
- **Lọc thủ công** hàng trăm bài viết mỗi ngày để tìm ra những xu hướng thực sự quan trọng.
- **Dịch và tổng hợp** nội dung sang nhiều ngôn ngữ để chia sẻ với đội ngũ quốc tế.
- **Bỏ lỡ cơ hội** vì không theo dõi liên tục 24/7.

**Workflow này tự động hóa toàn bộ quá trình:**
✅ **Lấy dữ liệu** từ API Hacker News trong 24h qua.
✅ **Lọc bỏ nội dung không quan trọng** (post mới <1h, tương tác thấp).
✅ **Tính toán xu hướng** dựa trên độ phổ biến (like, comment).
✅ **Dịch tự động** sang **Tiếng Tây Ban Nha, Pháp, Trung, Nhật** bằng AI (Google Gemini).
✅ **Gửi báo cáo định kỳ** (mỗi 4h) sang **Telegram** cho các sếp theo dõi.

---
## :::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng ngày.
- **Tính chính xác cao**: Lọc bỏ post không quan trọng tự động.
- **Tổng hợp đa ngôn ngữ**: Dịch sang **4 ngôn ngữ** (Tây Ban Nha, Pháp, Trung, Nhật) bằng AI.
- **Hoạt động liên tục**: Chạy tự động mỗi 4h, không bỏ lỡ xu hướng.
- **Tích hợp Telegram**: Nhận báo cáo ngay trên nhóm/channel.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Tạo **bot** qua [@BotFather](https://t.me/BotFather) và lưu **Token** vào credentials `telegramApi`.
   - Lấy **Chat ID**:
     - **Cá nhân**: Gửi `/get_id` cho bot `@userinfobot`.
     - **Channel**: Bot phải là **Admin**, Chat ID là suffix của link channel (vd: `-100123456789`).
2. **API Key OpenRouter**:
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lưu vào credentials `openRouterApi`.
3. **Không cần API Hacker News**: Workflow sử dụng API Algolia của Hacker News (miễn phí).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12748) hoặc copy toàn bộ JSON từ canvas.
- Mở **n8n Editor** → **Import Workflow** → Chọn file hoặc paste JSON.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Telegram**
- **Node "Send a text message"**:
  - Chọn `telegramApi` trong **Credentials**.
  - Điền **Chat ID** của nhóm/channel (vd: `-100123456789`).
  - **Lưu ý**: Bot phải có quyền **post message** trong channel.

##### **B. Cấu hình OpenRouter (AI Dịch)**
- **Node "OpenRouter Chat Model1"**:
  - Chọn `openRouterApi` trong **Credentials**.
  - **Model mặc định**: `google/gemini-2.5-flash-lite` (tốt cho dịch và tổng hợp).
  - **Không cần thay đổi** `keyParameters` trừ khi muốn thử model khác.

##### **C. Cấu hình Lọc Xu Hướng (Code Nodes)**
- **Node "Filter"**:
  - **Rule mặc định**:
    ```json
    {
      "jsonpath": "$[?(@.created_at < (now - 1h) && @.score < 3)]"
    }
    ```
    → **Bỏ post mới <1h và score <3** (nhỏ).
  - **Cần chỉnh** nếu muốn thay đổi ngưỡng lọc.

- **Node "Recalculate popularity score"**:
  - **Logic mặc định**:
    ```javascript
    // Tính điểm phổ biến dựa trên like/comment
    const popularityScore = data.likes + (data.num_comments * 0.5);
    return { ...data, popularityScore };
    ```
  - **Không cần chỉnh** trừ khi muốn thay đổi công thức tính điểm.

##### **D. Cấu hình Schedule Trigger**
- **Node "Schedule Trigger"**:
  - **Thời gian chạy**: Mặc định **mỗi 4h**.
  - **Lookback**: **24h** (lấy dữ liệu trong ngày qua).
  - **Không cần chỉnh** nếu muốn giữ nguyên.

##### **E. Cấu hình Dịch (Agent Node)**
- **Node "Translate"**:
  - **Prompt mặc định**:
    ```text
    Dịch bài viết này sang {ngôn ngữ mục tiêu} một cách ngắn gọn và chuyên nghiệp.
    ```
  - **Ngôn ngữ mục tiêu**: Thay đổi trong **Node "Combine message templates"** (xem phần sau).

##### **F. Kết hợp Template (Code Node)**
- **Node "Combine message templates"**:
  - **Thay đổi ngôn ngữ dịch** trong `template`:
    ```javascript
    const languageMap = {
      "es": "español",  // Tây Ban Nha
      "fr": "français", // Pháp
      "zh": "中文",     // Trung
      "ja": "日本語"     // Nhật
    };
    const language = "es"; // Thay đổi thành ngôn ngữ cần dịch
    ```
  - **Lưu ý**: Chỉ cần thay đổi `language` trong `languageMap`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Tab** → Chạy workflow với dữ liệu mẫu.
   - Kiểm tra **Telegram** có nhận được báo cáo không.
2. **Active Workflow**:
   - Bật **Active** trên tab chính.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logs cho Debug**:
   - Sử dụng **Node "StickyNote"** để ghi lại dữ liệu lọc hoặc lỗi.
   - Ví dụ:
     ```json
     {
       "content": "Post filtered: " + JSON.stringify(data)
     }
     ```

2. **Gửi Báo Cáo Định Kỳ Sang Email**:
   - Thêm **Node Email** (n8n-nodes-base.email) sau Telegram để gửi báo cáo cho team.

3. **Tích Hợp Slack**:
   - Thay thế Telegram bằng **Node Slack** để gửi báo cáo vào channel Slack.

4. **Cập Nhật Xu Hướng Mới**:
   - Thêm **Node Webhook** để nhận phản hồi từ Telegram và cập nhật lại workflow.

5. **Tối Ưu Hiệu Suất**:
   - Nếu dữ liệu quá lớn, sử dụng **Node "Set"** để lưu trữ tạm thời trong **n8n Database**.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp theo dõi xu hướng công nghệ hàng ngày mà không cần code. Với **AI dịch tự động** và **lọc thông minh**, bạn sẽ nhận được báo cáo **đa ngôn ngữ, chính xác và định kỳ** ngay trên Telegram.

**Hành động ngay!**
1. Import workflow vào n8n của mình.
2. Cấu hình Telegram và OpenRouter.
3. **Bật Active** và bắt đầu theo dõi xu hướng 24/7!

---
**💡 Lưu ý cuối cùng**: Nếu muốn thay đổi ngôn ngữ dịch, chỉ cần chỉnh `language` trong **Node "Combine message templates"**. Workflow hỗ trợ **Tiếng Tây Ban Nha, Pháp, Trung, Nhật** mà không cần cấu hình thêm!