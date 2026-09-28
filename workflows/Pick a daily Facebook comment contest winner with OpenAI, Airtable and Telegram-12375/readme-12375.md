---
title: "🎁 **Tự Động Chọn Người Chiến Thắng Cuộc Thi Facebook Hàng Ngày Với AI, Airtable & Telegram**"
description: "Workflow tự động hóa hoàn toàn không cần code để chọn người chiến thắng cuộc thi Facebook hàng ngày một cách công bằng, minh bạch và tự động hóa 100%. Sử dụng AI OpenAI phân tích cảm xúc, Airtable lưu trữ lịch sử và Telegram thông báo kết quả, tiết kiệm thời gian cho các sếp quản lý cộng đồng lên đến 10 giờ/tuần."
slug: "tieu-dong-chon-nguoi-chien-thang-cuoc-thi-facebook-hang-ngay"
tags: [n8n, automation, social-media, ai-summarization, airtable, telegram, openai, no-code]
keywords: [tự động hóa chọn người chiến thắng Facebook, AI phân tích cảm xúc, Airtable lưu trữ lịch sử, Telegram thông báo kết quả, workflow n8n tự động]
---

# 🚀 **Tự Động Chọn Người Chiến Thắng Cuộc Thi Facebook Hàng Ngày Với AI, Airtable & Telegram**

### **Giải pháp cho các sếp quản lý cộng đồng Facebook mệt mỏi với công việc chọn người chiến thắng thủ công**
Hàng ngày, các sếp phải dành **30-60 phút** để:
- **Lọc thủ công** hàng chục bình luận trên bài viết.
- **Phân loại** bình luận spam, không phù hợp.
- **Đảm bảo công bằng** bằng cách tránh chọn người đã thắng trước đó.
- **Gửi thông báo** kết quả cho cộng đồng.

**Workflow này tự động hóa toàn bộ quy trình trong 5 giây mỗi ngày**, đảm bảo:
✅ **Công bằng** (không lặp người thắng trước đó).
✅ **Minh bạch** (AI phân tích cảm xúc, lọc bình luận tích cực).
✅ **Tiết kiệm thời gian** (không cần kiểm tra thủ công).
✅ **Hoạt động 24/7** (không phụ thuộc vào giờ làm việc).

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** cho công việc chọn người chiến thắng.
- **Giảm thiểu sai sót** với AI phân tích cảm xúc thay vì con người.
- **Lưu trữ lịch sử** tất cả người chiến thắng trên Airtable.
- **Thông báo tự động** kết quả qua Telegram (hoặc Slack).
- **Công bằng tuyệt đối** với logic tránh lặp người thắng trước đó.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Facebook Developer** (để lấy **Post ID** và **Graph API Access Token**).
2. **Airtable** (để lưu trữ danh sách người chiến thắng trước đó).
3. **OpenAI API Key** (để sử dụng mô hình **GPT-4o-mini** phân tích cảm xúc).
4. **Telegram Bot Token** (để gửi thông báo kết quả).
5. **Supabase** (để log lỗi nếu có).
6. **Post ID** của bài viết trên Facebook muốn tự động chọn người chiến thắng.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12375](https://n8n.io/workflows/12375) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12375) và dán vào **Create Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **13 node**, các sếp cần chú ý cấu hình **các node sau**:

##### **🔹 Node "Get FB Comments" (HTTP Request)**
- **Tham số quan trọng:**
  - **URL:** `https://graph.facebook.com/v19.0/{POST_ID}/comments?fields=id,from,message&access_token={ACCESS_TOKEN}`
  - **POST_ID:** Thay thế bằng **ID bài viết Facebook** của sếp (có thể lấy từ URL bài viết: `https://www.facebook.com/{POST_ID}`).
  - **ACCESS_TOKEN:** Lấy từ **Facebook Graph API** (cần cấp quyền `pages_read_engagement`).
  - **Method:** `GET`.

##### **🔹 Node "Get Past Winners" (Airtable)**
- **Tham số quan trọng:**
  - **Base ID & Table Name:** Điền vào **Airtable Credentials** (cần tạo trước trên Airtable).
  - **Operation:** `search` (lấy danh sách người đã thắng trước đó).
  - **Filter:** Lọc theo ngày gần nhất (30 ngày) để tránh lặp người.

##### **🔹 Node "OpenAI Chat Model" (lmChatOpenAi)**
- **Tham số quan trọng:**
  - **Model:** `gpt-4o-mini` (mô hình miễn phí, hiệu quả).
  - **Prompt:** Sử dụng mặc định của workflow (phân tích cảm xúc bình luận).
  - **API Key:** Điền vào **OpenAI Credentials** (tạo trên [OpenAI Platform](https://platform.openai.com/)).

##### **🔹 Node "Pick Random Winner" (Code)**
- **Lưu ý:**
  - Workflow tự động **lọc ra người chưa thắng trước đó** và **chọn ngẫu nhiên**.
  - Nếu không có người phù hợp, workflow **dừng lại** và gửi lỗi qua Telegram.

##### **🔹 Node "Create a record" (Airtable)**
- **Tham số quan trọng:**
  - **Fields:** Điền các trường cần lưu (Name, ID, Comment, Date).
  - **Base & Table:** Đảm bảo trùng với **Get Past Winners**.

##### **🔹 Node "Notify Admin (Error)" & "Send a text message" (Telegram)**
- **Tham số quan trọng:**
  - **Chat ID:** Lấy từ Telegram Bot (cách lấy: `@username_bot` → `/start` → copy `chat_id`).
  - **Message:** Sử dụng mặc định (công bố người chiến thắng hoặc lỗi).

##### **🔹 Node "Log Error (Supabase)"**
- **Tham số quan trọng:**
  - **Table Name:** Điền tên bảng trên Supabase để log lỗi.
  - **Credentials:** Điền **Supabase URL & Key** (tạo trên [Supabase](https://supabase.com/)).

#### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy thử với **dữ liệu mẫu** (nếu có) để kiểm tra logic.
- **Bật Active:** Đặt workflow sang **Active** và chọn **Daily Trigger** tại **21:00** (9 PM).

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack** thay vì Telegram:
   - Thay node Telegram bằng **Slack Webhook** để thông báo kết quả.
2. **Lưu log chi tiết** trên Airtable:
   - Thêm trường `Status` (Thành công/Thất bại) và `Reason` (Lý do nếu lỗi).
3. **Gửi báo cáo hàng tuần** qua Email:
   - Sử dụng node **Email** (n8n-nodes-base.email) để gửi tổng hợp người chiến thắng.
4. **Tự động chia sẻ kết quả trên Facebook**:
   - Sử dụng **Facebook Graph API** trong node **HTTP Request** để post tự động.
5. **Cài đặt cảnh báo spam tự động**:
   - Thêm node **Code** để kiểm tra từ khóa spam (ví dụ: "win", "prize", "free") và loại bỏ.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý cộng đồng Facebook, đồng thời **tăng cường minh bạch** với AI phân tích cảm xúc và logic chọn ngẫu nhiên. **Chỉ cần 5 phút setup**, workflow sẽ hoạt động tự động hàng ngày!

👉 **Bắt đầu ngay:**
1. **Cài n8n Self-hosted** trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Bật Active** và xem AI làm việc thay các sếp!

**🎁 Mã giảm giá VPS cho n8n:**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (💰 **Giảm 39%** với mã **VPSN8N**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
**🚀 Hãy tự động hóa ngay hôm nay và dành thời gian cho những việc quan trọng hơn!**