---
title: "📅 **Tự Động Hóa Lịch Google Sang Telegram Với Claude 3.5 Sonnet - Không Cần Code!**"
description: "Workflow tự động hóa lấy lịch sự kiện Google Calendar hàng ngày, tổng hợp và chuyển đổi thành tin nhắn cá nhân hóa bằng Claude 3.5 Sonnet, gửi trực tiếp qua Telegram. Giúp các sếp quản lý thời gian hiệu quả, không bỏ lỡ bất kỳ sự kiện quan trọng nào."
slug: "tieu-dong-hoa-lich-google-sang-telegram-claude-3-5"
tags: [n8n, automation, google-calendar, telegram-bot, ai-chatbot, claude-3-5, productivity]
keywords: [n8n workflow google calendar telegram, tự động hóa lịch sự kiện, Claude 3.5 Sonnet n8n, gửi tin nhắn lịch hàng ngày, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Lịch Google Calendar Sang Telegram Với Claude 3.5 Sonnet**

### **Giải pháp cho các sếp bị "lịch" chìm trong đống email và cuộc gọi**
Bạn có bao giờ cảm thấy **lịch Google Calendar** của mình trở thành một "bẫy thời gian" không thể thoát? Sự kiện này trùng với sự kiện khác, thông báo lặp đi lặp lại, và cuối cùng bạn phải **quét qua hàng chục tin nhắn** mỗi sáng để biết ngày hôm nay có gì quan trọng? **Workflow này sẽ giải quyết tất cả!**

Với **Daily Calendar Digest**, các sếp sẽ:
✅ **Tự động lấy tất cả sự kiện Google Calendar** của ngày hôm nay (hoặc ngày cụ thể).
✅ **Sử dụng Claude 3.5 Sonnet** (mô hình AI tiên tiến của Anthropic) để **tổng hợp, sắp xếp và cá nhân hóa** thông tin lịch.
✅ **Gửi tin nhắn Telegram** với **định dạng chuyên nghiệp**, giúp bạn **không bỏ lỡ bất kỳ sự kiện quan trọng nào** trong ngày.

**Kết quả?** **Tiết kiệm 30 phút mỗi ngày**, giảm stress, và **quản lý thời gian như một chuyên gia**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải mở Google Calendar hàng ngày.
- **Tin nhắn cá nhân hóa**: Claude 3.5 Sonnet **tự động sắp xếp và mô tả** sự kiện một cách logic.
- **Không bỏ lỡ sự kiện**: Nhận thông báo **định kỳ** (ví dụ: 7h sáng) qua Telegram.
- **Hoạt động liên tục**: Workflow chạy **mỗi ngày tự động**, không cần can thiệp.
- **Dễ dàng mở rộng**: Thêm/loại sự kiện, thay đổi định dạng tin nhắn một cách đơn giản.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Calendar** (để lấy dữ liệu lịch).
✔ **API Key Anthropic** (để sử dụng Claude 3.5 Sonnet).
✔ **Bot Telegram** (để gửi tin nhắn tự động).
✔ **n8n Self-hosted** (để chạy workflow 24/7).

**Lưu ý:**
- **API Key Anthropic**: Mở tài khoản tại [Anthropic](https://www.anthropic.com/) và lấy `API Key`.
- **Bot Telegram**: Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy `API Token`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7266) và import vào n8n Editor.
- **Copy JSON** từ file và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy)**
- **Tham số cần chỉnh:**
  - **Time:** Đặt thời gian muốn nhận tin nhắn (ví dụ: **7h sáng**).
  - **Time Zone:** Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Repeat:** Chọn **Daily** để chạy hàng ngày.

##### **🔹 Node 2: Get many events (Lấy sự kiện Google Calendar)**
- **Tham số cần chỉnh:**
  - **Credentials:** Chọn `googleCalendarOAuth2Api` (đã cấu hình trước).
  - **Operation:** Đặt là `getAll`.
  - **Time Range:** Để trống để lấy **tất cả sự kiện ngày hôm nay**.

##### **🔹 Node 3: ID, Summary, Time (Lọc thông tin cần thiết)**
- **Tham số cần chỉnh:**
  - **Set Data:** Chọn các trường cần giữ (ví dụ: `id`, `summary`, `start`, `end`).

##### **🔹 Node 4: Combine data (Kết hợp dữ liệu)**
- **Tham số cần chỉnh:**
  - **Aggregate:** Chọn `join` để ghép tất cả sự kiện thành một chuỗi JSON.

##### **🔹 Node 5: Get string (Định dạng dữ liệu)**
- **Tham số cần chỉnh:**
  - **Set Data:** Chuyển dữ liệu thành **dạng chuỗi** để Claude 3.5 Sonnet xử lý.

##### **🔹 Node 6: Event extractor (Trích xuất thông tin)**
- **Tham số cần chỉnh:**
  - **Credentials:** Chọn `anthropicApi`.
  - **Model:** Đặt là `claude-3-5-sonnet-20241022`.
  - **Prompt:** Sử dụng **template mặc định** (n8n sẽ tự động lấy từ node `stickyNote`).
  - **Input:** Điền **chuỗi sự kiện** từ node trước.

##### **🔹 Node 7: Send a text message (Gửi tin nhắn Telegram)**
- **Tham số cần chỉnh:**
  - **Credentials:** Chọn `telegramApi`.
  - **Chat ID:** Điền **ID chat của bot Telegram** (lấy từ `@BotFather`).
  - **Text:** Chọn **output của node Event extractor** (đã được Claude 3.5 Sonnet xử lý).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow một lần để kiểm tra **tin nhắn Telegram** có đúng định dạng không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để nó chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm/Loại Sự Kiện**:
   - Sử dụng **node `Set`** để **lọc bỏ** sự kiện không cần thiết (ví dụ: cuộc họp nội bộ).
2. **Thay Đổi Định Dạng Tin Nhắn**:
   - Cập nhật **prompt** trong node `Event extractor` để Claude 3.5 Sonnet **tạo ra tin nhắn theo phong cách riêng** của các sếp.
3. **Gửi Báo Cáo Định Kỳ**:
   - Thêm **node `Schedule Trigger`** khác để gửi **tin nhắn tổng kết tuần** vào thứ 7.
4. **Lưu Log Dữ Liệu**:
   - Sử dụng **node `StickyNote`** để lưu **lịch sử sự kiện** để theo dõi.
5. **Kết Nối Với Slack**:
   - Thay vì Telegram, các sếp có thể **gửi tin nhắn qua Slack** bằng node `slack`.

---
### 📌 **Kết luận**
**Workflow này không chỉ giúp các sếp quản lý lịch hiệu quả mà còn làm cho việc theo dõi sự kiện trở nên **thú vị và cá nhân hóa** nhờ Claude 3.5 Sonnet.** Hãy **cài đặt ngay** và **tận hưởng sự tự do thời gian** mà nó mang lại!

**Bắt đầu từ hôm nay, không còn lo lắng về việc "quên lịch" nữa!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Hỏi trên [Community n8n](https://community.n8n.io/)**.
- **Đăng ký VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow 24/7.