---
title: "🔍 Tự Động Hóa Tìm Kiếm Web Bằng Brave Search Engine Trên Telegram (Không Cần Code)"
description: "Workflow này tự động hóa quá trình tìm kiếm thông tin từ Brave Search Engine qua Telegram chỉ với lệnh /brave + từ khóa, tiết kiệm thời gian và nâng cao hiệu suất làm việc hàng ngày. Hỗ trợ 24/7, không cần can thiệp thủ công."
slug: "tu-dong-hoa-tim-kiem-brave-search-telegram"
tags: [n8n, automation, telegram-bot, brave-search, no-code]
keywords: [n8n workflow brave search, tự động hóa tìm kiếm web, telegram bot tìm kiếm, brave search api, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Web Bằng Brave Search Engine Trên Telegram**

### **Giải pháp nào giúp các sếp tìm kiếm thông tin nhanh chóng chỉ với một lệnh Telegram?**
Hãy tưởng tượng: Bạn đang làm việc, cần tìm kiếm thông tin nhanh chóng về một chủ đề nào đó. Thay vì mở trình duyệt, nhập từ khóa và chờ đợi kết quả, **chỉ cần gửi tin nhắn `/brave [từ khóa]` trên Telegram**, workflow sẽ tự động tra cứu trên **Brave Search Engine** và trả về kết quả ngay trong chat!

Workflow này **không cần code**, hoạt động **24/7**, và hoàn toàn tự động hóa quá trình tìm kiếm web thông qua Telegram. Đặc biệt, nó sử dụng **Brave Search Engine** – một công cụ tìm kiếm nhanh, bảo mật và không theo dõi người dùng, phù hợp cho các doanh nghiệp và cá nhân yêu thích tính riêng tư.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở trình duyệt, chỉ cần gửi lệnh Telegram là có kết quả ngay.
- **Tiện lợi & cá nhân hóa**: Tìm kiếm từ bất kỳ thiết bị nào (điện thoại, máy tính) chỉ với Telegram.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.
- **Bảo mật & nhanh chóng**: Sử dụng Brave Search Engine – công cụ tìm kiếm không theo dõi người dùng và tốc độ cao.
- **Dễ dàng mở rộng**: Có thể kết hợp với nhiều công cụ khác như Slack, Email, hoặc lưu log kết quả.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật và ổn định).
2. **Node MCP** (n8n-nodes-mcp) để tương tác với Brave Search API.
   - Cài đặt theo [hướng dẫn này](https://github.com/nerding-io/n8n-nodes-mcp).
3. **API Key của Brave Search**:
   - Đăng ký tại [Brave Search API](https://brave.com/search/api/).
4. **Token API của Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy token.
5. **Chat ID của Telegram** (để workflow gửi kết quả về).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow JSON** từ [đây](https://n8n.io/workflows/3231) hoặc copy toàn bộ mã JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **7 node chính**, các sếp cần cấu hình kỹ các phần sau:

##### **A. Cấu hình MCP Brave Tools**
1. **Node "List Brave Tools"**:
   - Tạo **credentials mới** với tên `mcpClientApi`.
   - Trong trường **Environment**, nhập:
     ```
     BRAVE_API_KEY=your-api-key
     ```
     (Thay `your-api-key` bằng API Key của Brave Search bạn đã đăng ký).

2. **Node "Exec Brave tool"**:
   - Sử dụng cùng credentials `mcpClientApi` như trên.
   - Node này sẽ thực thi lệnh tìm kiếm khi người dùng gửi `/brave [từ khóa]`.

##### **B. Cấu hình Telegram**
1. **Node "Get Message" (Telegram Trigger)**:
   - Sử dụng credentials `telegramApi` (token bot Telegram).
   - Chỉ hoạt động khi nhận được tin nhắn bắt đầu bằng `/brave`.

2. **Node "Send message"**:
   - Sử dụng cùng credentials `telegramApi`.
   - Node này sẽ gửi kết quả tìm kiếm về chat.

##### **C. Node "Clean query" (Code)**
- Node này **xóa lệnh `/brave`** khỏi tin nhắn người dùng để chỉ giữ lại từ khóa tìm kiếm.
- Mở node → Chọn **JavaScript** → Sửa code như sau:
  ```javascript
  // Xóa "/brave" và các ký tự thừa
  const cleanedQuery = $input.all().text.trim().replace('/brave', '').trim();
  return [{ text: cleanedQuery }];
  ```

##### **D. Node "Search with Brave?" (If)**
- Node này **kiểm tra** nếu tin nhắn bắt đầu bằng `/brave` thì mới thực hiện tìm kiếm.
- Đảm bảo **condition** là `$input.all().text.startsWith('/brave')`.

##### **E. Node "Get Text" (Set)**
- Node này **lấy lại từ khóa đã được làm sạch** từ node "Clean query" để truyền vào Brave Search.

---

#### **3. Kích hoạt ⚡️**
1. **Test run**:
   - Gửi tin nhắn `/brave [từ khóa]` (ví dụ: `/brave "tự động hóa n8n"`) trên Telegram.
   - Kiểm tra kết quả trả về có chính xác không.

2. **Bật Active workflow**:
   - Nhấn **Active** trên tab workflow để workflow bắt đầu hoạt động 24/7.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO HỆ THỐNG]
1. **Lưu log kết quả**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử tìm kiếm.
   - Ví dụ: Sau khi Brave Search trả kết quả, lưu vào Google Sheets với thời gian, từ khóa và kết quả.

2. **Kết hợp với Slack**:
   - Thay vì Telegram, có thể gửi kết quả về Slack bằng node **Slack Webhook**.
   - Cài đặt node `n8n-nodes-base.slack` và cấu hình credentials.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule** (n8n-nodes-base.schedule) để gửi báo cáo tổng hợp tìm kiếm hàng tuần/month.

4. **Cải thiện UI kết quả**:
   - Sử dụng node **Code** để định dạng kết quả trước khi gửi về Telegram (ví dụ: thêm tiêu đề, danh sách liên kết).
   - Ví dụ:
     ```javascript
     // Định dạng kết quả trước khi gửi
     const results = $input.all().json;
     const formattedText = `**Kết quả tìm kiếm: ${$input.all().text}**
     ${results.map(r => `- ${r.title}\n${r.url}\n`).join('\n')}`;
     return [{ text: formattedText }];
     ```

5. **Bảo mật thêm**:
   - Sử dụng **Sticky Note** (node `n8n-nodes-base.stickyNote`) để lưu lại API Key và không để lộ trong code.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc tìm kiếm thông tin nhanh chóng, chỉ với một lệnh Telegram. Không cần code, không cần mở trình duyệt, và kết quả luôn chính xác, nhanh chóng.

**Hãy áp dụng ngay để nâng cao hiệu suất làm việc!**
- **Bắt đầu với n8n Self-hosted** để đảm bảo bảo mật và ổn định.
- **Tạo bot Telegram** và bắt đầu test với lệnh `/brave [từ khóa]`.
- **Mở rộng hệ thống** bằng cách kết hợp với Google Sheets, Slack hoặc các công cụ khác.

👉 **Nếu cần hỗ trợ**, liên hệ với tác giả Davide qua [LinkedIn](https://linkedin.com/in/davideboizza) hoặc email **info@n3w.it**.

---