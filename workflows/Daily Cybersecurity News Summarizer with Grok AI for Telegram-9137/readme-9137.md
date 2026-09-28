---
title: "🚀 Tự Động Hóa Tóm Tắt Tin An Toàn Máy Tính Hàng Ngày Với Grok AI & Telegram (N8N)"
description: "Workflow tự động hóa lấy tin tức an toàn mạng từ RSS, tóm tắt bằng AI Grok-4 và gửi kết quả qua Telegram hàng ngày - tiết kiệm 5+ giờ công mỗi tuần cho các sếp IT."
slug: "tuy-dong-hoa-tom-tat-tin-an-toan-may-tinh-hang-ngay"
tags: [n8n, automation, cybersecurity, ai, telegram, grok-ai]
keywords: [n8n workflow tự động hóa, tóm tắt tin tức an toàn mạng, grok ai, telegram bot, tự động hóa content, rss feed automation]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin An Toàn Máy Tính Hàng Ngày Với Grok AI & Telegram**

### **🔍 Nỗi Đau Của Các Sếp IT Hàng Ngày**
Các sếp IT, chuyên gia an toàn mạng hoặc người quản lý hệ thống phải dành **5-10 giờ mỗi tuần** để:
- Theo dõi tin tức an toàn mạng từ nhiều nguồn khác nhau (Bleeping Computer, Hacker News, ZDNet...).
- Lọc bỏ tin tức không liên quan hoặc quảng cáo.
- Tóm tắt nội dung dài thành những điểm chính để review nhanh.
- Gửi kết quả cho đội nhóm hoặc bản thân để cập nhật kiến thức.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động lấy tin tức** từ RSS hàng ngày (9h sáng).
✅ **Lọc bỏ quảng cáo & nội dung không liên quan** bằng AI.
✅ **Tóm tắt bằng Grok-4 (AI của xAI)** với chất lượng cao.
✅ **Gửi kết quả qua Telegram** dưới dạng tin nhắn hoặc ảnh tóm tắt.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** cho việc theo dõi tin tức thủ công.
- **Nội dung được tóm tắt chính xác** bởi AI Grok-4 (không bỏ sót chi tiết quan trọng).
- **Cập nhật tức thời** qua Telegram, không cần mở nhiều tab.
- **Lọc bỏ quảng cáo & tin không liên quan** tự động.
- **Hoạt động liên tục** ngay cả khi các sếp nghỉ ngơi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **API Token Telegram Bot**:
   - Tạo bot Telegram tại [@BotFather](https://t.me/BotFather) và lấy `API Token`.
   - Thêm bot vào nhóm hoặc chat cá nhân để nhận tin tức.
2. **API Key OpenRouter** (miễn phí cho mô hình `x-ai/grok-4-fast:free`):
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy API Key.
3. **N8N Self-Hosted** (không dùng phiên bản cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
4. **Nguồn RSS tin tức an toàn mạng** (Workflow sử dụng Bleeping Computer, nhưng có thể thay đổi).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/9137](https://n8n.io/workflows/9137).
  2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
- **Cách 2: Copy/Paste JSON**
  1. Mở n8n Editor → Nhấn **Import** → Chọn **Paste JSON**.
  2. Dán toàn bộ JSON từ [n8n.io/workflows/9137](https://n8n.io/workflows/9137) vào ô.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "9 AM - Schedule Trigger" (n8n-nodes-base.scheduleTrigger)**
- **Thiết lập thời gian chạy**: 9h sáng hàng ngày (cài đặt trong `cron` expression: `0 9 * * *`).
- **Lưu ý**: Nếu sử dụng VPS ở khu vực khác (ví dụ: Singapore), điều chỉnh giờ theo múi giờ của mình.

##### **🔹 Node "Bleeping Computer Security Bulletin" (n8n-nodes-base.rssFeedRead)**
- **URL RSS**: `https://www.bleepingcomputer.com/rss/`
  - *Lưu ý*: Nếu muốn lấy từ nguồn khác (ví dụ: Hacker News), thay đổi URL này.
- **Tham số `maxItems`**: Đặt giá trị **10-20** để lấy đủ tin tức mới nhất.

##### **🔹 Node "OpenRouter Chat Model" (n8n-nodes-langchain.lmChatOpenRouter)**
- **Model**: Chọn `x-ai/grok-4-fast:free` (miễn phí).
- **API Key**: Điền vào **Credentials** của node (tạo mới trong n8n: `Settings > Credentials > Add Credential > OpenRouter API`).
- **Prompt mẫu** (có thể tùy chỉnh):
  ```json
  "prompt": "Tóm tắt tin tức này về an toàn mạng thành 3 điểm chính, không bao gồm quảng cáo. Nếu có liên kết quan trọng, hãy nhắc đến. Dữ liệu: {{$json.body}}"
  ```

##### **🔹 Node "Send a photo message" (n8n-nodes-base.telegram)**
- **Credentials**: Chọn `telegramApi` (đã tạo trước đó).
- **Chat ID**: Lấy từ bot Telegram (gửi tin nhắn `/get_id` cho bot).
- **Tham số `photo`**: Sử dụng kết quả từ node `Filter Image Links From Body` (nếu muốn gửi ảnh tóm tắt).

##### **🔹 Node "Sponsored Removal" (n8n-nodes-base.if)**
- **Điều kiện lọc**: Kiểm tra xem tin tức có chứa từ khóa quảng cáo như `"sponsored"`, `"ad"`, `"promo"` hay không.
- *Lưu ý*: Nếu cần lọc thêm, chỉnh sửa điều kiện trong `if` node.

##### **🔹 Node "AI Agent" (n8n-nodes-langchain.agent)**
- **Tham số `tools`**: Đảm bảo các công cụ (như `lmChatOpenRouter`) được liên kết đúng.
- **Prompt mặc định**: Workflow đã cấu hình tự động, nhưng các sếp có thể chỉnh sửa trong `agentConfig`.

##### **🔹 Node "Simple Memory" (n8n-nodes-langchain.memoryBufferWindow)**
- **Thời gian lưu trữ**: Đặt `windowSize` = `7` (lưu 7 tin tức gần nhất để AI có thể so sánh và tổng hợp).
- *Lưu ý*: Nếu muốn lưu lâu hơn, tăng giá trị này.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node `Bleeping Computer Security Bulletin` để lấy tin tức mẫu.
   - Kiểm tra node `OpenRouter Chat Model` có trả về tóm tắt hợp lý không.
   - Gửi tin nhắn qua Telegram để xác nhận.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Thêm nhiều nguồn RSS**:
   - Thay đổi node `rssFeedRead` để lấy từ nhiều nguồn như:
     - [Hacker News](https://news.ycombinator.com/rss) (tin tức tech an toàn).
     - [Krebs on Security](https://krebsonsecurity.com/feed/) (tin tức an toàn mạng chuyên sâu).
   - Sử dụng node `merge` để kết hợp tất cả tin tức.

2. **Gửi báo cáo định kỳ**:
   - Thêm node `telegram` mới để gửi **báo cáo tuần/month** tổng hợp tất cả tin tức đã tóm tắt.
   - Ví dụ: Gửi 1 tin nhắn hàng tuần với tiêu đề `"Tóm tắt tin tức an toàn mạng tuần này"`.

3. **Lưu log vào Google Sheets/Notion**:
   - Thêm node `googleSheets` hoặc `notion` để lưu toàn bộ tin tức và tóm tắt vào bảng dữ liệu.
   - Cách làm:
     1. Tạo bảng mới trên Google Sheets/Notion.
     2. Thêm node `googleSheets` sau node `merge`.
     3. Chọn sheet và cấu hình cột dữ liệu.

4. **Cảnh báo tin tức cấp thiết**:
   - Sử dụng node `if` kết hợp với `telegram` để gửi **tin nhắn ưu tiên** nếu tin tức chứa từ khóa như `"ransomware"`, `"zero-day"`, `"data breach"`.

5. **Tùy chỉnh Grok-4**:
   - Nếu muốn Grok-4 trả lời chi tiết hơn, chỉnh sửa prompt trong node `lmChatOpenRouter`:
     ```json
     "prompt": "Tóm tắt tin tức này về an toàn mạng với 5 điểm chính, bao gồm:
     1. Tóm tắt ngắn gọn về sự kiện.
     2. Nguyên nhân/nguồn gốc (nếu có).
     3. Ảnh hưởng tiềm năng.
     4. Giải pháp khắc phục (nếu có).
     5. Liên kết quan trọng.
     Dữ liệu: {{$json.body}}"
     ```

6. **Dùng Slack thay vì Telegram**:
   - Thay thế node `telegram` bằng `slack` (n8n-nodes-base.slack) để gửi tin tức vào Slack.

---

### 📌 **Kết Luận**
Workflow **Daily Cybersecurity News Summarizer** là giải pháp **tự động hóa hoàn chỉnh** cho các sếp IT, giúp:
✔ **Tiết kiệm thời gian** từ việc theo dõi tin tức thủ công.
✔ **Cập nhật kiến thức** một cách nhanh chóng và chính xác.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận tin tức tóm tắt hàng ngày!

**🚀 Cảm ơn các sếp đã thử nghiệm!** Nếu có vấn đề, hãy comment bên dưới hoặc liên hệ qua Telegram `@n8n_automation`. Chúc các sếp thành công! 💻🔒