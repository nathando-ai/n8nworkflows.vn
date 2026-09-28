---
title: "🚀 **Tự Động Hóa Sinh Lên Lead Cho Doanh Nghiệp Cục Bộ Với AI, Mạng Xã Hội & Liên Kết WhatsApp**"
description: "Workflow này tự động tìm kiếm, phân tích và tạo lead cho doanh nghiệp địa phương từ Google Maps, sử dụng AI để phân tích thông tin doanh nghiệp và tạo tin nhắn outreach cá nhân hóa. Kết quả được lưu trữ trên Google Sheets và thông báo ngay lập tức qua Telegram."
slug: "tieu-dong-hoa-sinh-len-lead-doanh-nghiep-cuc-bo-voi-ai"
tags: [n8n, automation, lead-generation, ai-multimodal, google-maps, serpapi, telegram-bot, google-sheets, openrouter]
keywords: [n8n workflow lead generation, tự động hóa sinh lead doanh nghiệp địa phương, AI phân tích doanh nghiệp, SerpAPI Google Maps, Telegram bot thông báo lead, WhatsApp link tự động]
---

# 🚀 **Tự Động Hóa Sinh Lên Lead Cho Doanh Nghiệp Cục Bộ Với AI, Mạng Xã Hội & Liên Kết WhatsApp**

### **Giải Pháp Cho Những Người Sếp Bận Rộn Muốn Tiết Kiệm Thời Gian Tìm Lead**
Bạn đã bao giờ phải tốn hàng giờ mỗi tuần để tìm kiếm thông tin doanh nghiệp địa phương, phân tích đánh giá, và viết tin nhắn outreach cá nhân hóa? Hay phải lo lắng rằng lead được sinh ra không đủ chất lượng để chuyển đổi thành khách hàng? **Workflow này sẽ giúp bạn tự động hóa toàn bộ quy trình đó chỉ với một cú nhấp chuột!**

Dựa trên công nghệ **SerpAPI** để lấy dữ liệu từ Google Maps, **AI OpenRouter** để phân tích và tạo tin nhắn outreach, và **Google Sheets** để lưu trữ lead, workflow này sẽ:
✅ **Tìm kiếm tự động** doanh nghiệp theo từ khóa và vị trí địa lý.
✅ **Phân tích AI** thông tin doanh nghiệp (đánh giá, website, mạng xã hội) và tạo tin nhắn outreach cá nhân hóa.
✅ **Tạo liên kết WhatsApp** để khách hàng dễ dàng liên lạc.
✅ **Gửi thông báo Telegram** ngay khi lead mới được sinh ra.
✅ **Lưu trữ lead** trên Google Sheets với cấu trúc chuyên nghiệp.

Không cần viết một dòng code nào, bạn chỉ cần **cấu hình và chạy** workflow này trên n8n Self-hosted để **tự động hóa lead generation 24/7**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công trên Google Maps hoặc Facebook anymore.
- **Lead chất lượng cao**: AI phân tích đánh giá, website và mạng xã hội để tạo tin nhắn outreach cá nhân hóa.
- **Tăng tỷ lệ chuyển đổi**: Tin nhắn được tối ưu hóa theo từng doanh nghiệp, tăng cơ hội phản hồi.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình, không phụ thuộc vào giờ làm việc của bạn.
- **Dữ liệu tập trung**: Tất cả lead được lưu trữ trên Google Sheets với cấu trúc rõ ràng, dễ theo dõi.
- **Thông báo tức thời**: Nhận thông báo Telegram khi lead mới được sinh ra, không bỏ lỡ cơ hội nào.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **SerpAPI Account**
   - [Đăng ký SerpAPI](https://serpapi.com/) (miễn phí 5000 credit/tháng).
   - Lấy **API Key** từ dashboard SerpAPI.
   - *Lưu ý*: SerpAPI có giới hạn credit, các sếp nên chọn gói phù hợp với nhu cầu.

2. **OpenRouter Account**
   - [Đăng ký OpenRouter](https://openrouter.ai/) (miễn phí 1000 credit/tháng).
   - Lấy **API Key** từ dashboard OpenRouter.
   - *Model được sử dụng*: `google/gemini-2.0-flash-exp:free` (miễn phí).

3. **Telegram Bot**
   - Tạo bot mới trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào chat cá nhân để lấy **Chat ID** (sử dụng [@userinfobot](https://t.me/userinfobot)).

4. **Google Sheets**
   - Sử dụng **template Google Sheets** được cung cấp: [Local Business Lead Generator](https://docs.google.com/spreadsheets/d/1s1N_cAFoKtCsolQh4v3QZpqr8KmVzi7agKHr5MdBEBs/edit?usp=sharing).
   - Cấu hình **n8n Google Sheets Credential** trong n8n Editor.

5. **Google Maps API (không bắt buộc nhưng khuyến nghị)**
   - Nếu muốn lấy dữ liệu chi tiết hơn, các sếp có thể thêm **Google Maps API Key** vào node `HTTP Request` (để lấy dữ liệu website).
   - *Lưu ý*: Google Maps API có giới hạn free tier, các sếp nên xem xét gói phù hợp.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo hai cách:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6925) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào n8n Editor (chọn **Import Workflow** > **Paste JSON**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

##### **A. Cấu Hình Node `Schedule Trigger`**
- **Thời gian chạy**: Đặt theo lịch trình phù hợp (ví dụ: chạy hàng ngày lúc 8h sáng).
- *Lưu ý*: Workflow sẽ chạy theo lịch trình này để lấy dữ liệu mới từ Google Maps.

##### **B. Cấu Hình Node `HTTP Request` (SerpAPI)**
- **URL**: `https://serpapi.com/search`
- **Query Parameters**:
  - `engine`: `google_maps`
  - `q`: `{keyword}` (được lấy từ Google Sheets).
  - `location`: `{location}` (được lấy từ Google Sheets).
  - `api_key`: `{serpapi_api_key}` (điền API Key từ SerpAPI).
- *Lưu ý*: Các sếp cần đảm bảo `keyword` và `location` được truyền từ Google Sheets vào node này.

##### **C. Cấu Hình Node `Google Sheets` (Get/Update Row)**
- **Sheet Name**: Đảm bảo sử dụng **template** được cung cấp.
- **Credentials**: Chọn credential Google Sheets đã cấu hình trước.
- **Range**: Đặt theo cấu trúc trong template (ví dụ: `Keywords!A1:B100`).
- *Lưu ý*: Các sheet cần có tên chính xác như trong template (`Keywords`, `Results`, `Analysis`, `Social Media`).

##### **D. Cấu Hình Node `OpenRouter Chat Model`**
- **Model**: `google/gemini-2.0-flash-exp:free` (đã được đặt sẵn).
- **API Key**: Điền `openrouter_api_key` từ OpenRouter.
- **Prompt**: Các sếp có thể điều chỉnh prompt trong node `Basic LLM Chain` để tối ưu hóa kết quả phân tích.

##### **E. Cấu Hình Node `Telegram`**
- **Bot Token**: Điền `telegram_bot_token`.
- **Chat ID**: Điền `chat_id` của bot (lấy từ @userinfobot).
- **Message**: Tin nhắn thông báo lead mới (có thể tùy chỉnh).

##### **F. Cấu Hình Node `Code` (Regex Extraction)**
- Các sếp cần kiểm tra và điều chỉnh **regex** trong node `Code` để trích xuất thông tin từ website (ví dụ: liên kết Instagram, TikTok).
- *Lưu ý*: Nếu website có cấu trúc khác, các sếp cần cập nhật regex phù hợp.

##### **G. Cấu Hình Node `Limit`**
- Đặt số lượng lead được xử lý mỗi lần (ví dụ: `5` để tránh quá tải API).

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow với dữ liệu mẫu từ Google Sheets để kiểm tra kết quả.
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa SerpAPI Credit**
   - Sử dụng **gói SerpAPI phù hợp** với nhu cầu (ví dụ: 5000 credit/tháng cho 1000 lead/month).
   - *Mẹo*: Chỉ chạy workflow vào giờ thấp điểm (ví dụ: 2h sáng) để tiết kiệm credit.

2. **Lưu Log & Theo Dõi**
   - Sử dụng node `stickyNote` để ghi chú lỗi hoặc cập nhật.
   - *Gợi ý*: Tạo một sheet `Logs` trong Google Sheets để lưu lịch sử chạy workflow.

3. **Kết Hợp Với WhatsApp Business API**
   - Nếu muốn gửi tin nhắn WhatsApp thay vì chỉ tạo liên kết, các sếp có thể thêm node `WhatsApp Business API` (cần API Key từ Meta).

4. **Tự Động Gửi Báo Cáo Hàng Tuần**
   - Sử dụng node `Schedule Trigger` để chạy workflow định kỳ (ví dụ: hàng tuần) và gửi báo cáo tổng hợp qua Telegram.

5. **Phân Loại Lead Theo Đánh Giá**
   - Sử dụng node `If` để phân loại lead theo đánh giá (ví dụ: lead có rating >4 sao được ưu tiên).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa lead generation cho doanh nghiệp cục bộ mà không cần viết code. Với sự kết hợp giữa **AI, Google Maps, Telegram và Google Sheets**, bạn sẽ tiết kiệm **hàng giờ mỗi tuần** và tăng **tỷ lệ chuyển đổi lead** đáng kể.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** (SerpAPI, OpenRouter, Telegram, Google Sheets).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để AI làm việc cho bạn!

Nếu có bất kỳ vấn đề nào trong quá trình cấu hình, các sếp có thể tham khảo [hướng dẫn chi tiết của tác giả](https://n8n.io/workflows/6925) hoặc liên hệ cộng đồng n8n để hỗ trợ.

---
**🚀 Chúc các sếp thành công với việc tự động hóa lead generation!**