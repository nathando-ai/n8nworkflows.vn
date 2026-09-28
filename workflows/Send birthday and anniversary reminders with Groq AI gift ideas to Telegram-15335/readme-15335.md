---
title: "🎂 Tự Động Gửi Lời Chúc Sinh Nhật & Kỷ Niệm + Gợi Ý Quà Tặng AI qua Telegram (Miễn Phí)"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp gửi lời chúc sinh nhật, kỷ niệm và gợi ý quà tặng cá nhân hóa thông qua AI Groq miễn phí, chỉ cần 5 phút setup. Tiết kiệm thời gian, tăng tính chuyên nghiệp và làm cho mọi người cảm thấy được quan tâm."
slug: "tự-dộng-gửi-lời-chúc-sinh-nhật-ai-gift-telegram"
tags: [n8n, automation, no-code, ai-personalization, telegram-bot, google-sheets, groq-ai]
keywords: [tự động hóa sinh nhật, gửi lời chúc sinh nhật telegram, ai gợi ý quà tặng, groq ai miễn phí, n8n workflow sinh nhật, tự động hóa cá nhân hóa]
---

# 🚀 **Tự Động Gửi Lời Chúc Sinh Nhật & Kỷ Niệm + Gợi Ý Quà Tặng AI qua Telegram**

### **Giải quyết vấn đề gì?**
Các sếp đã bao giờ phải nhớ ngày sinh nhật, kỷ niệm của đồng nghiệp, khách hàng hay thành viên gia đình? Hoặc phải tốn thời gian tìm kiếm quà tặng phù hợp? **Workflow này tự động hóa toàn bộ quá trình** bằng cách:
✅ **Lấy danh sách người cần chúc** từ Google Sheets (tự động cập nhật).
✅ **Kiểm tra ngày sinh nhật/kỷ niệm** trong 7 ngày tới.
✅ **Sử dụng AI Groq miễn phí** để tạo **3 gợi ý quà tặng cá nhân hóa** dựa trên sở thích của từng người.
✅ **Gửi thông báo đẹp mắt** qua Telegram với lời chúc và quà tặng, **không cần viết tay**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhớ ngày sinh nhật hoặc tìm quà tặng.
- **Cá nhân hóa hoàn toàn**: AI phân tích sở thích và gợi ý quà phù hợp.
- **Hoạt động liên tục**: Chạy tự động hàng ngày vào 8h sáng (cấu hình được).
- **Trải nghiệm chuyên nghiệp**: Thông báo đẹp mắt với logo, hình ảnh và gợi ý AI.
- **Miễn phí**: Sử dụng API Groq miễn phí (không cần thẻ tín dụng).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Google Sheets**:
   - Tạo một bảng với **các cột bắt buộc**:
     - `name` (tên người)
     - `birthday` (ngày sinh, định dạng **DD/MM**)
     - `role` (vai trò, ví dụ: "Đồng nghiệp", "Bạn bè")
     - `interests` (sở thích, ví dụ: "Đọc sách", "Du lịch", "Thể thao")
   - **Chia sẻ bảng với n8n** (quyền đọc).

2. **Telegram Bot**:
   - Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Tìm **Chat ID** của mình qua [@userinfobot](https://t.me/userinfobot) (gửi tin nhắn "start" cho bot).

3. **Groq API Key**:
   - Đăng ký miễn phí tại [console.groq.com](https://console.groq.com).
   - **Không cần thẻ tín dụng** để sử dụng mô hình `llama-3.1-8b-instant`.

4. **Credentials trong n8n**:
   - **Google Sheets**: Thêm credential mới (type: "Google Sheets").
   - **Telegram**: Thêm credential mới (type: "Telegram").
   - **Groq**: Thêm credential mới (type: "OpenAI") với **base URL**: `https://api.groq.com/openai/v1`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15335](https://n8n.io/workflows/15335) (nút "Export").
- **Cách 1**: Nhấn "Import" trong n8n Editor và chọn file JSON.
- **Cách 2**: Copy toàn bộ JSON và dán vào ô "Import" trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình **các node quan trọng** như sau:

##### **📖 Node "📖 Read People" (Google Sheets)**
- **Credentials**: Chọn credential Google Sheets đã tạo.
- **Sheet Name**: Nhập tên sheet chứa dữ liệu (ví dụ: "PeopleList").
- **Range**: Đặt là `Sheet1!A:D` (giả sử dữ liệu từ cột A đến D).

##### **📅 Node "📅 Check Dates" (Code)**
- **Lưu ý**: Node này **so sánh ngày sinh** với ngày hiện tại.
- **Không cần chỉnh sửa** nếu các sếp muốn lấy **tất cả sinh nhật trong 7 ngày tới**.
- **Nếu muốn thay đổi khoảng ngày**, mở code và chỉnh `lookAheadDays` (ví dụ: `lookAheadDays: 14` để lấy 14 ngày).

##### **🤖 Node "🤖 AI Personalize" (Groq LLM)**
- **Credentials**: Chọn credential Groq đã tạo.
- **Model**: Đã mặc định là `llama-3.1-8b-instant` (miễn phí).
- **Prompt**: Node này **không cần chỉnh sửa** vì đã tối ưu sẵn để lấy:
  - Lời chúc sinh nhật/kỷ niệm.
  - **3 gợi ý quà tặng** dựa trên sở thích (`interests`).

##### **📝 Node "📝 Combine Message" (Code)**
- **Lưu ý**: Node này **định dạng tin nhắn** gửi qua Telegram.
- **Không cần chỉnh sửa** nếu muốn giữ mẫu mặc định (có logo, hình ảnh, và gợi ý AI).
- **Nếu muốn thay đổi mẫu**, mở code và chỉnh `messageTemplate`.

##### **📲 Node "📲 Send Telegram"**
- **Credentials**: Chọn credential Telegram đã tạo.
- **Chat ID**: Nhập **Chat ID** của mình (lấy từ @userinfobot).
- **Message**: Chọn `json` từ node trước (`Combine Message`).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn nút **"▶️ Manual Test"** để chạy thử với dữ liệu mẫu.
  - Kiểm tra Telegram xem tin nhắn có được gửi đúng không.
- **Bật Active**:
  - Đánh dấu **"Active"** ở góc trên bên phải.
  - **Schedule Trigger** (`⏰ Daily 8 AM`) sẽ tự động chạy hàng ngày vào 8h sáng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm hình ảnh cá nhân hóa**:
   - Trong node `Combine Message`, thêm biến `{{ $node["🤖 AI Personalize"].json["imageUrl"] }}` nếu AI trả về URL hình ảnh.

2. **Gửi báo cáo định kỳ**:
   - Thêm node **Google Sheets** sau `Send Telegram` để lưu log tất cả tin nhắn đã gửi.

3. **Kết hợp với Slack**:
   - Thêm node **Slack** để thông báo khi có sinh nhật/kỷ niệm sắp đến.

4. **Thay đổi thời gian chạy**:
   - Trong node `⏰ Daily 8 AM`, chỉnh `cron` thành `0 10 * * *` để chạy vào 10h sáng.

5. **Tối ưu AI**:
   - Nếu muốn AI **gợi ý quà tặng theo ngân sách**, chỉnh prompt trong node `🤖 AI Personalize`:
     ```json
     "prompt": "Generate 3 personalized gift ideas under $50 for {{ $node["📖 Read People"].json["interests"] }}."
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào công việc quan trọng hơn, đồng thời **tăng tính chuyên nghiệp** trong việc chúc mừng sinh nhật/kỷ niệm. **Chỉ cần 5 phút setup**, các sếp đã có một hệ thống tự động hóa hoàn chỉnh, **miễn phí** và **cá nhân hóa**.

**Hành động ngay!**
1. Import workflow.
2. Cấu hình credentials.
3. **Bật Active** và xem AI làm việc như thế nào!

---
**💡 Cần hỗ trợ?**
- Trả lời câu hỏi trong [n8n Community](https://community.n8n.io/).
- Liên hệ tác giả [Muhammad Mahamid](https://github.com/muhammadmahamid) qua GitHub.