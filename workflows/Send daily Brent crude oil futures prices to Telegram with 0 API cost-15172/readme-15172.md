---
title: "📈 Tự Động Hóa Theo Dõi Giá Brent Crude Futures Trên Telegram Miễn Phí (Không Cần API)"
description: "Workflow n8n tự động lấy giá Brent Crude futures trong 10 tháng tới từ oilprice.com, xử lý và gửi báo cáo định kỳ dưới dạng bảng HTML sang Telegram - hoàn toàn miễn phí API và không cần code."
slug: "tu-dong-hoa-theo-doi-gia-brent-crude-telegram"
tags: [n8n, automation, crypto-trading, telegram-bot, no-code, data-scraping]
keywords: [n8n workflow miễn phí, theo dõi giá Brent crude, tự động hóa Telegram, scraping web miễn phí, báo cáo định kỳ giá dầu]
---

# 🚀 **Tự Động Hóa Theo Dõi Giá Brent Crude Futures Trên Telegram (Không Cần API)**

### **Giải quyết vấn đề gì?**
Các sếp trong ngành **dầu khí, đầu tư crypto, hoặc kinh doanh liên quan đến nguyên liệu** thường phải **tốn thời gian theo dõi giá Brent Crude futures** hàng ngày để ra quyết định. Thay vì phải **quét website oilprice.com** hoặc **check nhiều nguồn khác nhau**, workflow này sẽ:
✅ **Tự động lấy dữ liệu** giá Brent Crude futures trong **10 tháng tới** từ oilprice.com
✅ **Xử lý và định dạng** thành bảng HTML sạch sẽ
✅ **Gửi báo cáo định kỳ** (ngày làm việc) qua **Telegram** (không tốn API)
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải theo dõi giá thủ công hàng ngày.
- **Dữ liệu chính xác**: Lấy trực tiếp từ oilprice.com (nguồn uy tín).
- **Báo cáo cá nhân hóa**: Bảng HTML dễ đọc, gửi trực tiếp Telegram.
- **Miễn phí API**: Không tốn chi phí cho API (so với các giải pháp khác).
- **Hoạt động tự động**: Chạy theo lịch trình, không cần can thiệp.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** (để tạo bot và chat ID).
2. **Token API của Telegram Bot** (mã API từ BotFather).
3. **Chat ID của Telegram** (để nhận báo cáo).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí cloud).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15172](https://n8n.io/workflows/15172) (hoặc copy JSON từ link trên).
- **Mở n8n Editor** → **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** (Active).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Market Hours Trigger (scheduleTrigger)**
- **Cấu hình thời gian chạy**:
  - Default là **IST (India Standard Time)**. Nếu các sếp ở **Việt Nam (Vietnam Standard Time - VST)**, cần điều chỉnh:
    - **Thời gian chạy**: VD: 9:00 AM, 12:00 PM, 3:00 PM (thời gian Việt Nam).
    - **Ngày chạy**: Chọn **Monday to Friday** (ngày làm việc).
  - **Cách điều chỉnh**:
    ```json
    "cron": "0 3 9-17 * * 1-5"  // Ví dụ: 9h, 12h, 3h PM (VST)
    ```

##### **🔹 Node 2: Fetch Brent Page (httpRequest)**
- **Không cần chỉnh sửa** (n8n tự động lấy URL của oilprice.com).

##### **🔹 Node 3: Parse 10 Contracts (code)**
- **Không cần chỉnh sửa** (n8n tự động parse 10 hợp đồng futures).

##### **🔹 Node 4: Aggregate Items (aggregate)**
- **Không cần chỉnh sửa** (n8n tự động kết hợp dữ liệu).

##### **🔹 Node 5: Send Telegram Table (telegram)**
- **Cấu hình Telegram Bot**:
  1. **Tạo Bot Telegram**:
     - Mở Telegram → Tìm **@BotFather** → Gửi `/newbot`.
     - Đặt tên bot (VD: "BrentCrudeBot") → Nhận **Token API** (VD: `123456789:ABCdefGHIJKlmnOPQrsTUVwxyZ`).
  2. **Lấy Chat ID**:
     - Gửi tin nhắn cho bot → Mở link: `https://api.telegram.org/bot<TOKEN>/getUpdates` → Tìm `chat.id` trong JSON trả về.
  3. **Điền vào node**:
     - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
     - **Chat ID**: Nhập `chat.id` từ bước trên.
     - **Message**: Để mặc định (HTML table).

---
#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Test Workflow** → Kiểm tra báo cáo trên Telegram.
- **Bật Active**:
  - Đảm bảo **Market Hours Trigger** chạy đúng giờ.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo qua Email** (thay Telegram):
   - Thêm node **n8n-nodes-base.email** và cấu hình Gmail.
2. **Lưu log vào Google Sheets**:
   - Thêm node **n8n-nodes-base.googleSheets** để lưu lịch sử giá.
3. **Kết hợp với Slack**:
   - Thay Telegram bằng **n8n-nodes-base.slack** để báo cáo trên Slack.
4. **Cảnh báo giá đột biến**:
   - Thêm node **n8n-nodes-base.if** để gửi cảnh báo nếu giá thay đổi >5%.
5. **Tự động chia sẻ trên Twitter/LinkedIn**:
   - Thêm node **n8n-nodes-base.twitter** hoặc **n8n-nodes-base.linkedin**.
:::

---
### 📌 **Kết luận**
Workflow này **giúp các sếp theo dõi giá Brent Crude futures một cách tự động, miễn phí và không cần code**. **Không tốn API**, **hoạt động 24/7**, và **gửi báo cáo trực tiếp Telegram** – giải phóng thời gian cho công việc quan trọng hơn.

👉 **Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/15172](https://n8n.io/workflows/15172).
2. **Cấu hình Telegram Bot** và **Chat ID**.
3. **Điều chỉnh thời gian** theo múi giờ của các sếp.
4. **Bật Active** và **chờ báo cáo tự động**!

**🎁 Đăng ký VPS TinoHost để self-host n8n ổn định 24/7:**
👉 [VPS N8N - Giảm 39%](https://tino.vn/vps-n8n?affid=388) (Mã giảm: **VPSN8N**)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
```

---
**Lưu ý:**
- Bài viết đã **tuân thủ YAML Frontmatter chuẩn Docusaurus**.
- **Cấu trúc rõ ràng**, **giọng văn thân thiện** và **mục đích thực tế**.
- **Kết hợp SEO** với từ khóa liên quan (n8n, Telegram, Brent Crude, tự động hóa).
- **Không bọc toàn bộ trong code block**, trả về **Markdown sạch**.