---
title: "🤖 🏠 Tự Động Hoạt Động Thiết Bị SwitchBot Qua Chat AI - Không Cần Code!"
description: "Hướng dẫn tự động hóa điều khiển thiết bị SwitchBot thông qua chatbot AI bằng n8n, giúp các sếp chỉ cần nói là thiết bị tự động thực hiện - tiết kiệm thời gian, tăng tính tiện lợi cho cuộc sống thông minh."
slug: "tự-dộng-hoạt-dộng-switchbot-qua-chat-ai"
tags: [n8n, automation, no-code, ai-chatbot, smart-home, switchbot]
keywords: [tự động hóa SwitchBot, chatbot điều khiển thiết bị, n8n workflow AI, tự động hóa nhà thông minh, OpenRouter API]
---

# 🚀 **Tự Động Hoạt Động Thiết Bị SwitchBot Qua Chat AI - Không Cần Code!**

### **Giải pháp nào giúp các sếp chỉ cần nói "Tắt đèn phòng khách" là thiết bị tự động thực hiện?**
Hiện nay, việc điều khiển thiết bị thông minh như SwitchBot vẫn còn phụ thuộc vào việc mở ứng dụng, chọn thiết bị và nhấn nút. **Nhưng với workflow này, các sếp chỉ cần nói với AI là thiết bị sẽ tự động thực hiện theo yêu cầu!**

Dù là muốn tắt đèn, điều chỉnh nhiệt độ, mở cửa hay đóng cửa, **chỉ cần gửi tin nhắn qua chatbot**, AI sẽ phân tích yêu cầu, lấy danh sách thiết bị và gửi lệnh điều khiển tự động đến SwitchBot. **Không cần viết một dòng code nào cả!**

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở app, chọn thiết bị và nhấn nút mỗi lần.
- **Tiện lợi tuyệt đối**: Điều khiển thiết bị bằng giọng nói hoặc chatbot 24/7.
- **Chính xác cao**: AI phân tích yêu cầu và gửi lệnh chính xác đến thiết bị.
- **Hoạt động liên tục**: Tự động hóa hoàn toàn, không phụ thuộc vào người dùng.
- **Dễ dàng mở rộng**: Thêm nhiều thiết bị hoặc tích hợp với các dịch vụ khác.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản SwitchBot** và **API Token + Secret**:
   - Mở app SwitchBot → **Profile → Preferences → App Version** → Nhấn **10 lần** để lộ token và secret.
2. **Tài khoản OpenRouter API** (hoặc thay thế bằng mô hình LLM khác):
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
3. **n8n Self-hosted** (không dùng phiên bản cloud):
   - Để workflow hoạt động 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15566](https://n8n.io/workflows/15566) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **7 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node 1: "When chat message received" (chatTrigger)**
- **Không cần chỉnh sửa**, node này sẽ bắt đầu workflow khi nhận được tin nhắn từ chatbot n8n.

##### **🔹 Node 2: "Set Credentials" (set)**
- **Thêm credentials mới**:
  - Nhấn **Add Credential** → Chọn **SwitchBot API Token** và **Secret**.
  - Điền vào:
    - `token`: API Token từ SwitchBot (lấy từ app).
    - `secret`: API Secret từ SwitchBot (lấy từ app).
  - Lưu credentials với tên **`switchbotAuth`**.

##### **🔹 Node 3: "Get Auth" (code)**
- **Không cần chỉnh sửa**, node này tự động tạo **HMAC-SHA256** cho yêu cầu API của SwitchBot.

##### **🔹 Node 4: "Get Device List" (httpRequest)**
- **Không cần chỉnh sửa**, node này lấy danh sách tất cả thiết bị SwitchBot đã đăng ký.
- **Lưu ý**: Nếu không có thiết bị nào, node này sẽ trả về lỗi. Các sếp cần **đăng ký ít nhất 1 thiết bị** trước khi chạy.

##### **🔹 Node 5: "OpenRouter Chat Model" (lmChatOpenRouter)**
- **Thêm credentials OpenRouter**:
  - Nhấn **Add Credential** → Chọn **OpenRouter API**.
  - Điền **API Key** từ OpenRouter vào.
  - **Không cần chỉnh sửa model** (sử dụng `openai/gpt-oss-120b:free` mặc định).
- **Lưu ý**: Nếu muốn sử dụng mô hình khác, chỉnh sửa ở **keyParameters → model**.

##### **🔹 Node 6: "Generate API Request with AI" (agent)**
- **Không cần chỉnh sửa**, node này sẽ:
  - Đọc **danh sách thiết bị** từ node trước.
  - Phân tích **yêu cầu của người dùng** (ví dụ: "Tắt đèn phòng khách").
  - **Tự động sinh lệnh API** cho SwitchBot.

##### **🔹 Node 7: "Send Device Command" (httpRequest)**
- **Không cần chỉnh sửa**, node này sẽ gửi **lệnh điều khiển** đến SwitchBot.
- **Lưu ý**: Nếu gặp lỗi, kiểm tra:
  - Credentials SwitchBot có đúng không?
  - Thiết bị có được đăng ký trên SwitchBot không?

#### **3. Kích hoạt ⚡️**
- **Test run** với một yêu cầu đơn giản (ví dụ: "Mở cửa phòng ngủ").
- Nếu thành công, **bật Active workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng **n8n-nodes-slack** hoặc **n8n-nodes-telegram** để chatbot hoạt động trên Slack/Telegram thay vì n8n chat.
2. **Lưu log hoạt động**:
   - Thêm node **n8n-nodes-base.googleSheets** để ghi lại lịch sử lệnh đã gửi.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.email** để gửi báo cáo sử dụng thiết bị hàng ngày.
4. **Thay thế mô hình AI**:
   - Nếu OpenRouter không phù hợp, thay thế bằng **Mistral, Llama2** hoặc mô hình khác trên OpenRouter.
5. **Tự động hóa theo thời gian**:
   - Sử dụng **n8n-nodes-base.date** để tự động gửi lệnh (ví dụ: "Tắt tất cả đèn lúc 22h").
:::

---

### 📌 **Kết luận**
Workflow này giúp **tự động hóa hoàn toàn việc điều khiển SwitchBot chỉ bằng chatbot AI**, tiết kiệm thời gian và tăng tính tiện lợi cho cuộc sống thông minh. **Không cần code, không cần kỹ thuật cao**, chỉ cần **cài đặt và chạy** là xong!

👉 **Hãy thử ngay và chia sẻ kết quả với các sếp nhé!** Nếu gặp vấn đề, để lại comment dưới đây, các sếp sẽ được hỗ trợ chi tiết.

---