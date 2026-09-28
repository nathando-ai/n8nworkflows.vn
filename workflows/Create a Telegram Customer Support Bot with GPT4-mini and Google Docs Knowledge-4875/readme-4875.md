---
title: "🤖 Tạo Bot Trợ Lý Hỗ Trợ Khách Hàng Telegram Siêu Thông Minh Với GPT-4o-mini & Google Docs (Không Code)"
description: "Workflow tự động hóa hoàn toàn giúp các sếp xây dựng một bot Telegram hỗ trợ khách hàng thông minh, trả lời câu hỏi phức tạp bằng kiến thức từ Google Docs, hoạt động 24/7 mà không cần viết code."
slug: tao-bot-troly-ho-tro-telegram-gpt4-mini-google-docs
tags: [n8n, automation, ai-agent, support-bot, google-docs, telegram-bot]
keywords: [bot hỗ trợ khách hàng Telegram, tự động hóa hỗ trợ khách hàng, GPT-4o-mini, RAG, Google Docs API, n8n workflow]
---

# 🚀 Bot Trợ Lý Hỗ Trợ Khách Hàng Telegram Siêu Thông Minh Với AI GPT-4o-mini & Kiến Thức Google Docs

### 💡 Giải pháp cho vấn đề gì?
Các sếp đang gặp khó khăn khi phải:
- Trả lời hàng trăm câu hỏi khách hàng hàng ngày một cách chậm chạp và không nhất quán.
- Lo lắng về chất lượng hỗ trợ khi nhân viên không có kiến thức đầy đủ về sản phẩm/dịch vụ.
- Phải chạy nhiều shift để hỗ trợ khách hàng 24/7.

**Workflow này giúp giải quyết tất cả đó!** Một bot Telegram thông minh sẽ:
- Hiểu và trả lời mọi câu hỏi khách hàng bằng ngôn ngữ tự nhiên.
- Trích xuất kiến thức từ Google Docs (FAQ, SOP, chính sách) để trả lời chính xác.
- Ghi nhớ lịch sử chat để tương tác như con người.
- Hoạt động tự động 24/7 mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định và không bị gián đoạn, các sếp nên cài đặt n8n trên máy chủ riêng (Self-hosted) với tài nguyên tối thiểu:
- **CPU:** 2 nhân
- **RAM:** 4GB
- **Đĩa cứng:** 20GB SSD

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Bot trả lời tự động hàng trăm câu hỏi mỗi ngày, giảm tải cho đội ngũ hỗ trợ.
- **Chất lượng cao:** Trả lời chính xác và chi tiết nhờ trích xuất kiến thức từ Google Docs.
- **Hoạt động 24/7:** Không cần nhân viên trực ca đêm nữa.
- **Tương tác tự nhiên:** Giữ lịch sử chat để trả lời liên tục và logic hơn.
- **Dễ mở rộng:** Có thể kết nối với Slack, WhatsApp hoặc email sau này.
:::

---

### 🔧 Yêu cầu cần thiết
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot:**
   - Tạo bot Telegram thông qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào nhóm hoặc chat cá nhân để test.

2. **Tài khoản Google Cloud:**
   - Tạo dự án Google Cloud và kích hoạt API **Google Docs API**.
   - Tạo **Service Account** và tải xuống **JSON Key File** để kết nối với Google Docs.

3. **Tài khoản OpenAI:**
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key** cho model **gpt-4o-mini**.

4. **Google Doc chứa kiến thức:**
   - Chuẩn bị một Google Doc với nội dung hỗ trợ khách hàng (FAQ, SOP, chính sách...).
   - Chia nhỏ nội dung thành các phần rõ ràng để AI dễ trích xuất.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/4875](https://n8n.io/workflows/4875).
2. Mở **n8n Editor** và nhấn **Import** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Telegram Trigger**
- **Credentials:**
  - Nhập **API Token** của bot Telegram (lấy từ @BotFather).
  - Chọn **Chat ID** của nhóm hoặc chat cá nhân muốn kích hoạt bot.
- **Key Parameters:**
  - Đảm bảo **Update Type** là `message` để bắt tất cả tin nhắn mới.

##### **B. Google Docs Tool**
- **Credentials:**
  - Nhập **JSON Key File** từ Google Cloud (tải xuống trước).
  - Chọn **Project ID** và **Service Account Email** từ file JSON.
- **Key Parameters:**
  - Điền **Document ID** của Google Doc chứa kiến thức hỗ trợ (tìm thấy trong URL của doc).
  - Chọn **Operation** là `get` để lấy toàn bộ nội dung.

##### **C. OpenAI Chat Model (gpt-4o-mini)**
- **Credentials:**
  - Nhập **API Key** từ OpenAI.
- **Key Parameters:**
  - Đảm bảo **Model** là `gpt-4o-mini` (đã được thiết lập mặc định).

##### **D. Customer Support AI Agent**
- **Credentials:**
  - Không cần thiết, nhưng có thể cấu hình **Temperature** (0.7) để điều chỉnh độ sáng tạo của AI.
- **Key Parameters:**
  - Đảm bảo **Memory Buffer** được kết nối với node **Simple Memory** để lưu lịch sử chat.

##### **E. Telegram (Send Response)**
- **Credentials:**
  - Sử dụng cùng **API Token** của bot Telegram như trong node **Telegram Trigger**.
- **Key Parameters:**
  - Chọn **Chat ID** tương ứng để gửi phản hồi.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Gửi một tin nhắn test đến bot Telegram và kiểm tra phản hồi.
   - Nếu có lỗi, kiểm tra lại các **credentials** và **key parameters** của các node.

2. **Bật Workflow:**
   - Nhấn **Active** để workflow chạy liên tục.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Cập nhật kiến thức thường xuyên:**
   - Khi Google Doc được cập nhật, bot sẽ tự động lấy nội dung mới sau khi chạy lại.

2. **Kết nối với Slack/Email:**
   - Sử dụng node **Slack** hoặc **Email** để mở rộng bot hỗ trợ trên nhiều kênh.

3. **Lưu log hoạt động:**
   - Thêm node **StickyNote** hoặc **Google Sheets** để ghi lại tất cả các câu hỏi và phản hồi của bot.

4. **Tối ưu hóa model AI:**
   - Thử nghiệm với các model khác như `gpt-4o` (nếu budget cho phép) để cải thiện chất lượng trả lời.

5. **Tạo menu hỗ trợ:**
   - Sử dụng **Telegram Keyboard** để cho phép khách hàng chọn các câu hỏi phổ biến (ví dụ: "Hỏi về sản phẩm", "Hỏi về giao hàng").

---

### 📌 Kết luận
Workflow này là giải pháp **tự động hóa hoàn toàn** để các sếp xây dựng một bot hỗ trợ khách hàng thông minh, hoạt động 24/7 mà không cần viết code. Với khả năng trích xuất kiến thức từ Google Docs và sử dụng AI GPT-4o-mini, bot sẽ trả lời mọi câu hỏi một cách chính xác và tự nhiên.

**Hành động ngay hôm nay!**
- Import workflow và bắt đầu test với bot Telegram của mình.
- Cập nhật kiến thức trong Google Docs để bot trở nên thông minh hơn mỗi ngày.
- Mở rộng sang Slack, WhatsApp hoặc email để hỗ trợ khách hàng trên nhiều kênh.

👉 [Xem video hướng dẫn chi tiết](https://www.youtube.com/@Automatewithmarc) để hiểu rõ hơn về cách cấu hình và tối ưu hóa bot!