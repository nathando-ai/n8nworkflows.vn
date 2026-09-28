---
title: "🚀 Tự Động Hóa Tìm Việc Freelance Từ RSS + GPT-4.1: Nhận Cảnh Báo Telegram & Lưu Trữ Google Sheets"
description: "Workflow tự động hóa tìm kiếm và phân tích công việc freelance từ RSS, sử dụng trí tuệ nhân tạo GPT-4.1 để lọc, đánh giá và tạo đề xuất ứng tuyển. Các sếp nhận cảnh báo Telegram thực thời và dữ liệu được lưu trữ sạch sẽ trên Google Sheets."
slug: "tieu-dong-hoa-tim-viec-freelance-rss-gpt-4-1"
tags: [n8n, automation, freelance, ai, google-sheets, telegram-bot, gpt-4-1, no-code]
keywords: [tự động hóa tìm việc freelance, n8n workflow gpt-4, cảnh báo công việc mới telegram, lọc công việc chất lượng cao, google sheets tự động hóa]
---

# 🚀 **Tự Động Hóa Tìm Việc Freelance: Nhận Cảnh Báo Telegram & Lưu Trữ Google Sheets Với GPT-4.1**

### **🔍 Nỗi Đau Của Các Sếp Trong Tìm Việc Freelance**
Mỗi ngày, các sếp phải:
- **Quét hàng chục trang web** (Upwork, Freelancer, RSS) để tìm công việc phù hợp.
- **Lọc thủ công** những công việc chất lượng thấp, trùng lặp hoặc không phù hợp với kỹ năng.
- **Tốn thời gian** viết đề xuất ứng tuyển từ đầu, dù có nhiều công việc tương tự.
- **Quên hoặc bỏ lỡ** những cơ hội hấp dẫn vì không được cảnh báo kịp thời.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4.1 + n8n**, nó sẽ:
✅ **Tự động quét** công việc mới từ RSS (ví dụ: Freelancer.com).
✅ **Lọc và đánh giá** chất lượng công việc bằng AI.
✅ **Tạo đề xuất ứng tuyển** cá nhân hóa.
✅ **Gửi cảnh báo Telegram** ngay khi có công việc mới phù hợp.
✅ **Lưu trữ tất cả dữ liệu** trên Google Sheets để theo dõi.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** không phải quét và lọc công việc thủ công.
- **Nhận cảnh báo Telegram** ngay khi có công việc mới phù hợp với kỹ năng và từ khóa mong muốn.
- **Dữ liệu sạch sẽ** trên Google Sheets: Không trùng lặp, được đánh giá chất lượng và phân loại.
- **Đề xuất ứng tuyển tự động** bằng GPT-4.1, cá nhân hóa cho từng công việc.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để chạy 24/7):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy `sk-...` (đảm bảo có tiền để sử dụng GPT-4.1).

3. **Tài khoản Google Sheets**:
   - Một file Google Sheets để lưu trữ lịch sử công việc (cần chia sẻ với n8n).

4. **Bot Telegram**:
   - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy `API_TOKEN`.
   - Gửi tin nhắn `/start` cho bot để lấy `chat_id` (sử dụng cho cảnh báo).

5. **Danh sách từ khóa và "wishlist"**:
   - Các từ khóa công việc mong muốn (ví dụ: "Python", "UI/UX").
   - Danh sách liên kết công việc đã xem (tránh trùng lặp).

6. **Nguồn RSS**:
   - Link RSS của trang web công việc (ví dụ: [Freelancer.com RSS](https://www.freelancer.com/rss/)).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9270) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **15 node**, nhưng các node quan trọng cần cấu hình kỹ như sau:

##### **A. Cấu Hình Nguồn RSS (Fetch Freelancer.com RSS)**
- **Node**: `Fetch Freelancer.com RSS` (type: `rssFeedRead`)
  - **URL**: Điền link RSS của trang công việc (ví dụ: `https://www.freelancer.com/rss/`).
  - **Test**: Nhấn **Execute Node** để kiểm tra dữ liệu đầu vào.

##### **B. Cấu Hình Từ Khóa & Wishlist (Settings)**
- **Node**: `Settings (Keyword & Wishlist)` (type: `set`)
  - **Tham số**:
    - `keywords`: Danh sách từ khóa (ví dụ: `["Python", "Web Development", "AI"]`).
    - `wishlist`: Danh sách URL công việc đã xem (tránh trùng lặp).
  - **Lưu ý**: Nếu không có dữ liệu ban đầu, có thể bỏ trống và để workflow tự động cập nhật.

##### **C. Cấu Hình AI Job Analyzer (Agent)**
- **Node**: `AI Job Analyzer` (type: `agent`)
  - **Tham số**:
    - **Model**: Chọn `gpt-4-1106-preview` (hoặc phiên bản mới nhất của GPT-4).
    - **Prompt**: Workflow đã định sẵn, nhưng các sếp có thể tùy chỉnh để phù hợp với yêu cầu cụ thể (ví dụ: yêu cầu AI đánh giá mức lương, kỹ năng cần thiết).
  - **API Key**: Điền `sk-...` từ OpenAI vào **Credentials** của node `OpenAI`.

##### **D. Cấu Hình Google Sheets**
- **Node**: `Log to Google Sheets` (type: `googleSheets`)
  - **Credentials**: Thiết lập kết nối với Google Sheets (nhấn **Add New** → Đăng nhập Google → Chọn file Sheets).
  - **Sheet Name**: Đặt tên sheet (ví dụ: `Freelance_Jobs`).
  - **Headers**: Đảm bảo cột đầu tiên là `Date`, `Job Title`, `Description`, `Score`, `Proposal`, `Link`.

- **Node**: `Load Seen Links (Google Sheets)` (type: `googleSheets`)
  - **Credentials**: Sử dụng cùng kết nối Google Sheets.
  - **Sheet Name**: Đặt tên sheet lưu trữ danh sách URL đã xem (ví dụ: `Seen_Links`).

##### **E. Cấu Hình Telegram Alert**
- **Node**: `Send Telegram Alert` (type: `telegram`)
  - **Credentials**: Thiết lập kết nối với bot Telegram:
    1. Nhấn **Add New** → Điền `API_TOKEN` từ `@BotFather`.
    2. Điền `chat_id` của tài khoản Telegram muốn nhận cảnh báo (lấy từ `/start`).
  - **Message Template**: Workflow đã định sẵn, nhưng các sếp có thể tùy chỉnh nội dung cảnh báo (ví dụ: thêm link trực tiếp đến công việc).

##### **F. Cấu Hình Schedule Trigger**
- **Node**: `Schedule: Every 5 Minutes` (type: `scheduleTrigger`)
  - **Interval**: Đặt thành `5 minutes` để workflow chạy liên tục.
  - **Lưu ý**: Nếu muốn chạy ít hơn, giảm xuống `15 minutes` để tiết kiệm tài nguyên.

##### **G. Cấu Hình AI Proposal Generator**
- **Node**: `AI Proposal Generator` (type: `openAi`)
  - **Model**: Chọn `gpt-4-1106-preview`.
  - **Prompt**: Workflow đã định sẵn để tạo đề xuất ứng tuyển, nhưng các sếp có thể chỉnh sửa để phù hợp với phong cách cá nhân.

##### **H. Cấu Hình De-duplicate & Filter**
- **Node**: `De-duplicate by Link` (type: `filter`)
  - **Condition**: Kiểm tra nếu `job.link` **không** trong danh sách `wishlist` (tránh trùng lặp).
- **Node**: `Gate: Score ≥` (type: `if`)
  - **Condition**: Chỉ cho phép công việc có `score` từ AI ≥ 7/10 (hoặc điều chỉnh theo yêu cầu).

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **Execute Workflow** và chọn **Test Run** với dữ liệu mẫu từ RSS.
   - Kiểm tra:
     - Cảnh báo Telegram có được gửi không?
     - Dữ liệu có được lưu vào Google Sheets không?
     - AI có phân tích và tạo đề xuất không?

2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Prompt cho AI**:
   - Mở node `AI Job Analyzer` và chỉnh sửa prompt để AI đánh giá các yếu tố cụ thể (ví dụ: yêu cầu AI kiểm tra mức lương, thời gian hoàn thành, kỹ năng cần thiết).

2. **Lưu Log Chi Tiết**:
   - Thêm node `Set` sau `Log to Google Sheets` để lưu thêm thông tin như `user_id` (nếu có nhiều người dùng) hoặc `status` (đã ứng tuyển hay chưa).

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node `ScheduleTrigger` để chạy workflow hàng tuần và gửi báo cáo tổng hợp qua Email (thêm node `Email` từ `n8n-nodes-base.email`).

4. **Kết Nối Với Slack**:
   - Thay vì Telegram, các sếp có thể cấu hình node `Slack` để cảnh báo trong kênh Slack (cần `webhook_url` từ Slack).

5. **Tự Động Xóa Công Việc Đã Xem**:
   - Thêm node `GoogleSheets` sau `Send Telegram Alert` để xóa công việc đã xem khỏi sheet `Seen_Links` (tránh trùng lặp trong lần chạy tiếp theo).

---
### 📌 **Kết Luận**
Workflow này là **công cụ tự động hóa hoàn hảo** cho các sếp freelance muốn tiết kiệm thời gian và không bỏ lỡ cơ hội. Với **GPT-4.1 + n8n**, nó không chỉ lọc và đánh giá công việc mà còn **tạo đề xuất ứng tuyển cá nhân hóa** và **cảnh báo Telegram thực thời**.

**Hành động ngay!**
1. **Chuẩn bị tài nguyên** (VPS, API Key, Google Sheets, Telegram Bot).
2. **Import workflow** và cấu hình các node quan trọng.
3. **Bật Active** và bắt đầu tự động hóa cuộc sống freelance của mình!

---
**💡 Chia sẻ & phản hồi**:
Nếu các sếp có bất kỳ câu hỏi hoặc muốn tùy chỉnh workflow thêm, hãy liên hệ với tác giả [Sulieman Said](https://aufcopilot.de/) hoặc để lại bình luận dưới đây. **Hãy tự động hóa cuộc sống của mình ngay hôm nay!** 🚀