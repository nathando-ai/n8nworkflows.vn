---
title: "🔍 Promo Seeker: Tự Động Tìm Kiếm Mã Giảm Giá Chất Lượng Với SerpAPI, Gemini AI & Telegram (Không Cần Code)"
description: "Workflow tự động hóa tìm kiếm mã giảm giá, voucher chính xác từ khắp web, gửi kết quả qua Telegram/Gmail và lưu trữ trong Data Table. Giúp doanh nghiệp tiết kiệm thời gian lên tới 80% trong việc tra cứu giảm giá."
slug: "tieu-dong-tim-kiem-ma-giam-gia-voi-n8n"
tags: [n8n, automation, no-code, ai-multimodal, serpapi, gemini-ai, telegram-bot]
keywords: [tự động hóa tìm mã giảm giá, serpapi n8n, gemini ai tìm voucher, workflow n8n content creation, tự động hóa giảm giá online]
---

# 🚀 **Promo Seeker: Tự Động Tìm Kiếm Mã Giảm Giá Chất Lượng Với SerpAPI, Gemini AI & Telegram**

## 💥 **Nỗi Đau Của Các Sếp Trong Việc Tìm Mã Giảm Giá**
Hàng ngày, các sếp phải mất **30-60 phút** để tra cứu mã giảm giá, voucher từ nhiều trang web khác nhau: Shopee, Lazada, TikTok Shop, hay các website giảm giá chuyên dụng. Thường thì:
- **Không tìm được mã mới nhất** vì phải check thủ công hàng ngày.
- **Mã giả hoặc hết hạn** sau khi áp dụng.
- **Tốn thời gian** để so sánh và lọc ra mã hiệu quả nhất.
- **Không lưu trữ kết quả** để theo dõi mã đã dùng hoặc hết hạn.

**Promo Seeker** là giải pháp **tự động hóa 100% không cần code**, sử dụng **SerpAPI + Gemini AI + Telegram** để:
✅ **Tìm kiếm mã giảm giá mới nhất** từ khắp web chỉ với 1 câu lệnh.
✅ **Lọc bỏ mã giả/hết hạn** bằng trí tuệ nhân tạo.
✅ **Gửi kết quả ngay qua Telegram/Gmail** và lưu trữ trong Data Table.
✅ **Hoạt động 24/7** với trigger định kỳ hoặc thông qua Telegram/Webhook.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với tra cứu thủ công.
- **Chỉnh xác 100%** với AI lọc bỏ mã giả/hết hạn.
- **Cá nhân hóa** theo nhu cầu (mã giảm giá cho điện thoại, laptop, du lịch...).
- **Lưu trữ dài hạn** trong Data Table của n8n.
- **Gửi báo cáo tự động** qua Telegram/Gmail hàng ngày.
- **Hoạt động liên tục** với trigger định kỳ (ví dụ: mỗi sáng 7h).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API & Credentials**:
   - [SerpAPI](https://serpapi.com/) (API Key).
   - [OpenRouter](https://openrouter.ai/) (API Key cho Gemini 2.5 Pro).
   - [Telegram Bot](https://t.me/BotFather) (Bot Token).
   - [Gmail](https://mail.google.com/) (OAuth2 cho gửi email).
2. **Bảng Data Table** trong n8n với **4 cột bắt buộc**:
   - `platform` (string) – Tên trang web (Shopee, Lazada...).
   - `promoCode` (string) – Mã giảm giá.
   - `value` (string) – Giá trị giảm (ví dụ: "10%").
   - `termsConditions` (string) – Điều kiện áp dụng.
   - `validUntil` (dateTime) – Ngày hết hạn.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9172) hoặc copy JSON từ canvas.
- Trong n8n Editor, nhấn **Import Workflow** và dán JSON.
- **Tên workflow**: `Promo Seeker` (hoặc đặt tên tùy ý).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **16 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
| Node               | Thao Tác Cần Thực Hiện                                                                 | Lưu Ý                                                                 |
|--------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| **SerpAPI**        | Tạo **Credentials mới** → Chọn **SerpAPI** → Dán **API Key** từ [SerpAPI](https://serpapi.com/). | Không để trống, nếu sai sẽ không tìm kiếm được kết quả.            |
| **Gemini 2.5 Pro** | Tạo **Credentials mới** → Chọn **OpenRouter API** → Dán **API Key** từ [OpenRouter](https://openrouter.ai/). | Chọn model: `google/gemini-2.5-pro`.                                |
| **Telegram**       | Tạo **Credentials mới** → Chọn **Telegram API** → Dán **Bot Token** từ BotFather.       | Bot cần được thêm vào chat để nhận thông báo.                      |
| **Gmail**          | Tạo **Credentials mới** → Chọn **Gmail OAuth2** → Đăng nhập và cấp quyền.              | Chọn email chính để gửi báo cáo.                                   |

##### **B. Cấu Hình Node Quá Trình**
1. **`Schedule Trigger`** (Trigger định kỳ):
   - Đặt **cron expression** theo nhu cầu (ví dụ: `0 7 * * *` để chạy mỗi sáng 7h).
   - Hoặc **bỏ qua** nếu muốn kích hoạt thủ công qua Telegram/Webhook.

2. **`Telegram Trigger`** (Nhận yêu cầu từ Telegram):
   - Cấu hình **chat ID** của bot Telegram (tìm trong `https://api.telegram.org/bot<BOT_TOKEN>/getUpdates`).
   - **Lưu ý**: Bot phải được thêm vào chat trước khi sử dụng.

3. **`SerpAPI` & `Gemini 2.5 Pro`** (Tìm kiếm & Lọc Mã Giảm Giá):
   - **SerpAPI** sẽ tra cứu từ khóa (ví dụ: "mã giảm giá Shopee tháng 10").
   - **Gemini AI** sẽ phân tích và lọc kết quả, trả về mã **chính xác và mới nhất**.

4. **`Data Table`** (Lưu Trữ Kết Quả):
   - **Tạo bảng mới** trong n8n với **5 cột** như hướng dẫn trên.
   - Node `Get row(s)` sẽ lấy dữ liệu cũ, `Upsert row(s)` sẽ cập nhật hoặc thêm mới.

5. **`Send a message` (Gmail) & `notify telegram`**:
   - **Gmail**: Chọn **email nhận báo cáo** và cấu hình nội dung email.
   - **Telegram**: Chọn **chat ID** để gửi kết quả.

6. **`Webhook`** (Kích Hoạt Thủ Công):
   - Cấu hình **path**: `v1/promo-seeker` và **HTTP Method**: `POST`.
   - **Lưu ý**: Các sếp cần gọi API này từ ứng dụng hoặc script nếu muốn kích hoạt không dùng Telegram.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn qua Telegram với từ khóa (ví dụ: "mã giảm giá laptop").
   - Kiểm tra **Data Table** xem có dữ liệu mới được thêm không.
   - Kiểm tra **email/Telegram** xem có nhận được báo cáo không.

2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Lưu ý**: Nếu dùng `Schedule Trigger`, workflow sẽ chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Gửi Báo Cáo Hàng Ngày**:
   - Sử dụng `Schedule Trigger` để gửi email/Telegram báo cáo tổng hợp mã giảm giá mới mỗi sáng.

2. **Kết Nối Với Slack**:
   - Thay thế node `telegram` bằng `slack` để thông báo trên Slack Team.

3. **Lưu Log & Theo Dõi**:
   - Sử dụng node `stickyNote` để ghi chú các mã đã dùng hoặc hết hạn.

4. **Tìm Kiếm Theo Danh Mục**:
   - Tùy chỉnh từ khóa trong `SerpAPI` để tìm mã giảm giá cho **điện thoại, laptop, du lịch, thực phẩm...**.

5. **Xây Dựng Dữ liệu Toàn Cục**:
   - Kết nối với **Google Sheets** hoặc **Airtable** để lưu trữ mã giảm giá dài hạn.

---

### 📌 **Kết Luận**
**Promo Seeker** là công cụ **tự động hóa siêu mạnh** giúp các sếp:
✔ **Tiết kiệm thời gian** trong việc tra cứu mã giảm giá.
✔ **Nhận mã chính xác** với trí tuệ nhân tạo Gemini AI.
✔ **Lưu trữ và theo dõi** mã giảm giá một cách dễ dàng.
✔ **Hoạt động 24/7** với trigger tự động.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình credentials.
2. **Test với từ khóa** như "mã giảm giá Shopee tháng 10".
3. **Bật Active** và bắt đầu tự động hóa!

👉 [Tải workflow nguyên bản](https://n8n.io/workflows/9172) và **cài đặt ngay** để không bỏ lỡ bất kỳ mã giảm giá nào!

---