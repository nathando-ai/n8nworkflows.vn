---
title: "🚀 Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày Với OpenAI & Perplexity AI – Gửi Trực Tiếp Zalo & Telegram (N8N)"
description: "Workflow tự động hóa tóm tắt tin tức từ RSS Feed hàng ngày bằng AI (OpenAI + Perplexity), sau đó gửi kết quả tóm tắt đến Zalo cá nhân/nhóm và Telegram – tiết kiệm thời gian lên đến 50% cho các sếp quản lý thông tin."
slug: "tu-dong-hoa-tom-tat-tin-tuc-hang-ngay-voi-openai-perplexity"
tags: [n8n, automation, ai-summarization, zalo-telegram, rss-feed, openai, perplexity-ai]
keywords: [n8n workflow tự động hóa, tóm tắt tin tức AI, gửi tin tức Zalo Telegram, tự động hóa thông tin hàng ngày, OpenAI Perplexity N8N]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày Với AI – Gửi Trực Tiếp Zalo & Telegram**

### **Giải pháp cho các sếp bị "ngập" thông tin**
Hàng ngày, các sếp phải mất **30-60 phút** để đọc và tóm tắt tin tức từ nhiều nguồn khác nhau (Vnexpress, BBC, Reuters,...) để cập nhật tình hình thị trường, đối thủ cạnh tranh hoặc xu hướng công nghệ. **Workflow này tự động hóa toàn bộ quy trình** bằng AI, giúp bạn:
✅ **Tiết kiệm 50% thời gian** so với cách làm thủ công.
✅ **Nhận tóm tắt chính xác** từ 20 tin tức mới nhất hàng ngày.
✅ **Cập nhật tức thì** trên Zalo cá nhân/nhóm và Telegram.
✅ **Không cần code** – chỉ cần cấu hình và chạy 24/7.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tóm tắt tin tức tự động**: AI xử lý từ 4 nguồn RSS khác nhau (ví dụ: Vnexpress, BBC, Reuters,...) và đưa ra bản tóm tắt ngắn gọn.
- **Gửi kết quả ngay**: Tin nhắn được gửi tự động đến **Zalo cá nhân/nhóm** và **Telegram** mỗi sáng (hoặc thời gian bạn thiết lập).
- **Duy trì thông tin liên tục**: Không bỏ lỡ tin tức mới nhờ **trigger hàng ngày** và **lọc tin tức mới nhất**.
- **Tích hợp AI tiên tiến**: Sử dụng **OpenAI (GPT-4)** và **Perplexity AI** để đảm bảo chất lượng tóm tắt cao.
- **Hoạt động 24/7**: Workflow chạy tự động trên **n8n self-hosted**, không phụ thuộc vào máy tính cá nhân.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n self-hosted** (khuyến nghị dùng **VPS** để chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **API Keys & Credentials**:
   - **OpenAI API Key** (đăng ký tại [openai.com](https://platform.openai.com/))
   - **Perplexity API Key** (đăng ký tại [perplexity.ai](https://www.perplexity.ai/))
   - **Zalo OAuth2 API Key** (cần tạo trên [Zalo Developer](https://developers.zalo.me/))
   - **Telegram Bot Token** (tạo bot tại [@BotFather](https://t.me/BotFather))

3. **Danh sách RSS Feed**:
   - 4 liên kết RSS Feed của các nguồn tin tức (ví dụ: `https://vnexpress.net/rss/tin-tuc.rss`).

4. **Thiết bị nhận tin**:
   - **Zalo**: Số điện thoại và nhóm Zalo để nhận tin.
   - **Telegram**: Chat ID hoặc nhóm Telegram để nhận tin.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/7627](https://n8n.io/workflows/7627) (chọn **Export as JSON**).
2. Mở **n8n Editor** (trang chủ của workflow n8n).
3. Nhấn **Import** và chọn file JSON vừa tải.
4. Workflow sẽ xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/7627](https://n8n.io/workflows/7627).
2. Trong **n8n Editor**, nhấn **Import** → **Paste JSON**.
3. Chọn **Import** để hoàn tất.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **10 node quan trọng** cần cấu hình cẩn thận:

#### **🔹 Node "Schedule Trigger" (Động cơ kích hoạt hàng ngày)**
- **Cấu hình**:
  - **Schedule**: Chọn thời gian chạy (ví dụ: `0 8 * * *` để chạy lúc 8h sáng hàng ngày).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**: Nếu không thiết lập, workflow sẽ không chạy tự động.

#### **🔹 Node "My RSS 01" đến "My RSS 04" (Đọc RSS Feed)**
- **Cấu hình**:
  - **URL**: Nhập liên kết RSS Feed của nguồn tin (ví dụ: `https://vnexpress.net/rss/tin-tuc.rss`).
  - **Limit**: Đặt số lượng tin tức tối đa (workflow mặc định là **20 tin mới nhất**).
- **Lưu ý**:
  - Thay đổi **URL** cho mỗi node (`My RSS 01`, `My RSS 02`,...) thành nguồn tin khác nhau.
  - Nếu nguồn RSS không hoạt động, kiểm tra lại liên kết.

#### **🔹 Node "Message an assistant" (OpenAI) & "Message a model in Perplexity1" (Perplexity AI)**
- **Cấu hình**:
  - **OpenAI**:
    - **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
    - **Prompt**: Sử dụng prompt mặc định (có thể tùy chỉnh để phù hợp với nhu cầu).
  - **Perplexity AI**:
    - **Credentials**: Chọn `perplexityApi`.
    - **Model**: Chọn `sonar-reasoning` (hoặc model khác nếu muốn).
- **Lưu ý**:
  - Nếu OpenAI/Perplexity AI không trả về kết quả, kiểm tra **API Key** có đúng không.
  - Thay đổi **prompt** để điều chỉnh chất lượng tóm tắt (ví dụ: `"Tóm tắt tin tức này thành 3 câu ngắn gọn, nhấn mạnh điểm quan trọng"`).

#### **🔹 Node "Gửi tin nhắn cá nhân & nhóm1" (Zalo) & "Send a text message" (Telegram)**
- **Cấu hình**:
  - **Zalo**:
    - **Credentials**: Chọn `zaloUserOAuth2Api`.
    - **Recipient**: Nhập số điện thoại hoặc ID nhóm Zalo.
    - **Message**: Sử dụng dữ liệu từ node **Aggregate** (tóm tắt tin tức).
  - **Telegram**:
    - **Credentials**: Chọn `telegramApi`.
    - **Chat ID**: Nhập ID chat hoặc nhóm Telegram (có thể tìm bằng cách gửi tin cho bot `@RawDataBot`).
    - **Message**: Sử dụng dữ liệu từ node **Aggregate**.
- **Lưu ý**:
  - **Kiểm tra quyền**: Đảm bảo tài khoản Zalo/Telegram đã cấp quyền cho bot.
  - **Dạng tin nhắn**: Workflow sẽ gửi **tin tức tóm tắt + liên kết gốc** để dễ dàng truy cập.

#### **🔹 Node "Limit" (Giới hạn 20 tin tức mới nhất)**
- **Cấu hình**:
  - **Limit**: Đặt giá trị **20** (mặc định) để lấy 20 tin tức mới nhất.
- **Lưu ý**: Nếu muốn lấy nhiều tin tức hơn, tăng số lượng (nhưng lưu ý chi phí API).

#### **🔹 Node "Aggregate" (Kết hợp dữ liệu)**
- **Cấu hình**:
  - **Operation**: Chọn `merge` để ghép tất cả tin tức từ các RSS Feed.
  - **Fields**: Chọn các trường cần giữ (ví dụ: `title`, `description`, `link`).
- **Lưu ý**: Nếu dữ liệu không hợp nhất, kiểm tra lại **node Merge** trước đó.

---
### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử)**:
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra kết quả trong **node Aggregate** và **Zalo/Telegram**.
   - Nếu có lỗi, xem **Log** để sửa.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - Workflow sẽ chạy tự động theo **Schedule Trigger**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC TỐT NHẤT]
- **Thêm nguồn RSS mới**: Bạn có thể thêm **node RSS Feed** nữa (ví dụ: `My RSS 05`) và kết nối vào **node Merge**.
- **Tùy chỉnh tin nhắn**: Sử dụng **node Set** để thêm thông tin cá nhân (ví dụ: "Chào buổi sáng, đây là tin tức mới nhất...").
- **Lưu log**: Sử dụng **node StickyNote** để ghi lại lịch sử chạy workflow.
- **Gửi báo cáo định kỳ**: Kết hợp với **node Email** để gửi báo cáo tóm tắt hàng tuần.
- **Sử dụng AI khác**: Thay thế OpenAI bằng **Perplexity AI** hoặc ngược lại để so sánh chất lượng tóm tắt.
- **Duy trì tin tức cũ**: Sử dụng **node MemoryBufferWindow** để lưu trữ lịch sử tóm tắt (nếu cần).
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa việc cập nhật tin tức hàng ngày** mà không cần mất thời gian đọc thủ công. Với **AI tóm tắt chất lượng** và **gửi tin tức tự động** đến Zalo/Telegram, bạn sẽ **tiết kiệm thời gian, giảm stress** và luôn cập nhật thông tin mới nhất.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các **API Key**.
3. **Chạy thử** và **bật tự động** để nhận tin tức mỗi sáng!

👉 **Bắt đầu tự động hóa ngay bây giờ!** 🚀