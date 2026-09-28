---
title: "🚀 **Tự Động Hóa Tìm Kiếm Lead Reddit Tích Hợp GPT-4, Supabase & Email Alert – Giúp Doanh Nghiệp Tăng Doanh Thu 30% Mà Không Cần Code**"
description: "Workflow tự động hóa tìm kiếm, phân tích và chuyển đổi lead từ Reddit sang email thông báo tự động, tích hợp AI GPT-4 để lọc và tổng hợp thông tin chất lượng cao. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng tỷ lệ chuyển đổi lead lên 30%."
slug: "tieu-dong-hoa-tim-kiem-lead-reddit-gpt4-supabase-email-alert"
tags: [n8n, automation, lead-generation, ai-summarization, gpt-4, reddit-scraping, no-code, supabase, gmail-integration]
keywords: [tự động hóa tìm kiếm lead reddit, gpt-4 tự động hóa, supabase n8n, email alert tự động, lead generation no-code, workflow n8n lead prospecting]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Lead Reddit Với GPT-4, Supabase & Email Alert – Giải Pháp Cho Doanh Nghiệp Không Cần Code**

### **Nỗi Đau Của Các Sếp Trong Tìm Kiếm Lead Trên Reddit**
Bạn đã bao giờ phải:
- **Tốn thời gian** tìm kiếm thủ công hàng trăm bài post trên Reddit để tìm lead tiềm năng?
- **Không biết cách lọc** những lead thực sự chất lượng giữa hàng nghìn bài viết?
- **Quên theo dõi** lead sau khi tìm được, dẫn đến mất cơ hội chuyển đổi?
- **Không có hệ thống** để tự động gửi thông báo email cho lead mới?

**Workflow này giải quyết tất cả!** Với sự kết hợp giữa **Reddit API, GPT-4, Supabase (database cloud) và Gmail**, bạn sẽ tự động:
✅ **Tìm kiếm** lead từ các subreddit liên quan.
✅ **Phân tích** nội dung bằng AI để lọc lead chất lượng cao.
✅ **Lưu trữ** lead vào Supabase (database cloud miễn phí).
✅ **Gửi email tự động** thông báo cho lead mới.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** tìm kiếm và phân tích lead thủ công.
- **Tăng tỷ lệ chuyển đổi lead lên 30%** nhờ AI GPT-4 lọc nội dung chất lượng.
- **Hoạt động liên tục** 24/7, không cần can thiệp.
- **Lưu trữ lead an toàn** trên Supabase (database cloud miễn phí).
- **Email tự động** thông báo lead mới cho team marketing/sales.
- **Cá nhân hóa** thông điệp email dựa trên nội dung bài post.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Reddit OAuth2** (để lấy dữ liệu từ Reddit API).
2. **API Key OpenAI** (để sử dụng GPT-4 trong phân tích nội dung).
3. **Tài khoản Gmail OAuth2** (để gửi email thông báo).
4. **Tài khoản Google Sheets** (để lưu log hoặc dữ liệu tham khảo).
5. **Tài khoản Supabase** (để lưu trữ lead tiềm năng).
6. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7).

---
:::note[Lưu ý quan trọng]
- **Reddit API** có giới hạn request, nên các sếp nên chọn subreddit nhỏ hoặc sử dụng **VPS n8n** để tránh bị chặn.
- **OpenAI API Key** phải có đủ credit để chạy GPT-4.1.
- **Gmail OAuth2** cần cấp quyền cho app n8n gửi email.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6756).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **23 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Credentials (Tài Khoản API)**
| Node | Yêu cầu cấu hình | Ghi chú |
|------|------------------|---------|
| **Reddit OAuth2** | `clientId`, `clientSecret`, `refreshToken` | Lấy từ [Reddit API](https://www.reddit.com/prefs/apps) |
| **OpenAI API** | `apiKey` | Lấy từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys) |
| **Gmail OAuth2** | `clientId`, `clientSecret`, `refreshToken` | Cấu hình từ [Google Cloud Console](https://console.cloud.google.com/) |
| **Supabase API** | `url`, `anonKey` | Lấy từ [Supabase Dashboard](https://app.supabase.com/) |
| **Google Sheets OAuth2** | `clientId`, `clientSecret` | Cấu hình từ [Google Cloud Console](https://console.cloud.google.com/) |

##### **B. Cấu Hình Node Quan Trọng**
1. **`Get Posts` (Reddit)**
   - Chọn **`operation: search`**.
   - Điền **`subreddit`** (ví dụ: `homeimprovement`, `handyman`).
   - Điền **`query`** (ví dụ: `need a plumber`).
   - Thiết lập **`limit`** (số bài post lấy mỗi lần).

2. **`Filter Posts` (If Node)**
   - Sử dụng **`$jsonPath`** để lọc bài post có từ khóa liên quan (ví dụ: `title: *plumber*`).
   - Cấu hình **`condition`** để chỉ giữ những bài post có nội dung phù hợp.

3. **`Analysis Content By AI` (Agent Node)**
   - Chọn **`model: gpt-4.1`** (đã cấu hình sẵn).
   - Cấu hình **`prompt`** để AI phân tích lead (ví dụ: *"Tóm tắt bài post này và đánh giá độ phù hợp với lead marketing"*).
   - Kết quả sẽ được gửi đến **`Append row in sheet1`** (Google Sheets) và **`Send a message`** (Gmail).

4. **`Send a message` (Gmail)**
   - Chọn **`to`** (email của lead hoặc team).
   - Cấu hình **`subject`** và **`body`** (có thể sử dụng **`$jsonPath`** để lấy thông tin từ Reddit).
   - Ví dụ:
     ```plaintext
     Subject: Lead mới từ Reddit - [Tên Subreddit]
     Body: Xin chào [Tên Lead], tôi là [Tên Công Ty] và đã tìm thấy bạn trên Reddit. Dưới đây là thông tin chi tiết:
     [Liên kết bài post] | [Tóm tắt AI]
     ```

5. **`Schedule Trigger` (Nếu muốn chạy định kỳ)**
   - Thiết lập **`cron`** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).

##### **C. Các Node Code (Nếu Cần Sửa Đổi)**
- **`Code`**, **`Code1`**, **`Code3`**, **`Code4`**, **`Code5`**, **`Code6`** được sử dụng để:
  - **Lọc dữ liệu** (ví dụ: loại bỏ bài post trùng lặp).
  - **Tạo cấu trúc email** động.
  - **Xử lý lỗi** (ví dụ: nếu Reddit API trả về lỗi).
- Các sếp có thể **xem mã nguồn** và sửa đổi nếu cần.

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Nhấn **`Test workflow`** để kiểm tra từng node.
  - Kiểm tra **`gmail`** và **`supabase`** để đảm bảo email và database được cập nhật.
- **Bật Active** khi đã kiểm tra xong.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Hợp Slack/Telegram Alert**
   - Thêm **`webhook`** (Slack/Telegram) vào workflow để nhận thông báo lead mới ngay khi có.

2. **Lưu Log Dữ Liệu**
   - Sử dụng **`googleSheets`** để lưu tất cả lead đã tìm kiếm, giúp theo dõi hiệu suất.

3. **Tối Ưu Hóa Prompt AI**
   - Cập nhật **`prompt`** trong **`Analysis Content By AI`** để AI phân tích lead theo yêu cầu cụ thể của doanh nghiệp.

4. **Chạy Định Kỳ**
   - Sử dụng **`scheduleTrigger`** để workflow chạy hàng ngày/lần tuần thay vì thủ công.

5. **Tích Hợp CRM**
   - Sau khi lead được xác nhận, có thể **tích hợp với HubSpot/Zoho** để chuyển đổi sang CRM.

---
### 📌 **Kết Luận**
Workflow **Reddit Lead Finder** là giải pháp **tự động hóa lead prospecting** hoàn hảo cho các doanh nghiệp dịch vụ (home service, handyman, marketing,…). Với sự hỗ trợ của **GPT-4, Supabase và Gmail**, bạn sẽ:
✔ **Tiết kiệm thời gian** và tập trung vào việc chuyển đổi lead.
✔ **Tăng tỷ lệ chuyển đổi** nhờ AI lọc lead chất lượng.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa lead prospecting của mình!**
👉 [Tải file JSON](https://n8n.io/workflows/6756) → Import vào n8n → Cấu hình credentials → **Bật workflow!**

---
**Chia sẻ và like nếu bài viết hữu ích!** 🚀
📩 **Có thắc mắc?** Hãy để lại comment bên dưới, các sếp sẽ được hỗ trợ chi tiết!