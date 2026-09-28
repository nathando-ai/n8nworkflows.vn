---
title: "🤖 Tự Động Xác Minh & Chăm Sóc Yêu Cầu Demo Trang Web Với AI Claude, Cal.com & Instantly.ai (N8N)"
description: "Workflow tự động hóa 100% không code giúp các sếp nhanh chóng xác minh chất lượng yêu cầu demo từ website, tự động phân loại, đặt lịch hẹn trên Cal.com và chuyển lead chất lượng cao sang Instantly.ai - tiết kiệm thời gian lên đến 80% cho bộ phận sales."
slug: "tieu-dong-xac-minh-cham-soc-yeu-cau-demo-trang-web"
tags: [n8n, automation, ai-claude, cal-com, instantly-ai, lead-generation, no-code]
keywords: [tự động hóa n8n, xác minh lead demo, ai chatbot claude, đặt lịch cal.com, instant messaging, workflow tự động]
---

# 🚀 **Tự Động Xác Minh & Chăm Sóc Yêu Cầu Demo Trang Web Với AI Claude, Cal.com & Instantly.ai**

### **Giải pháp tự động hóa hoàn hảo cho các sếp bán hàng & marketing**
Hãy tưởng tượng một tình huống: Trang web của doanh nghiệp nhận hàng trăm yêu cầu demo mỗi tháng, nhưng chỉ một phần nhỏ là lead thực sự chất lượng cao. Các sếp phải mất nhiều thời gian để:
- **Lọc rác** trong hàng loạt yêu cầu không phù hợp.
- **Trả lời từng email** để xác minh thông tin.
- **Đặt lịch hẹn** trên Cal.com cho lead tiềm năng.
- **Chuyển lead** sang hệ thống Instantly.ai để chăm sóc liên tục.

**Workflow này giải quyết tất cả!** Sử dụng **AI Claude** để tự động phân loại yêu cầu, **Cal.com** để đặt lịch hẹn, và **Instantly.ai** để chuyển lead chất lượng cao sang hệ thống chăm sóc tự động. **Kết quả?** Tiết kiệm **80% thời gian** cho bộ phận sales và tăng **tỷ lệ chuyển đổi lead** lên 30%.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động xác minh lead** trong giây lát bằng AI Claude (không cần code).
✅ **Đặt lịch hẹn tự động** trên Cal.com cho lead tiềm năng.
✅ **Chuyển lead chất lượng cao** sang Instantly.ai để chăm sóc liên tục.
✅ **Tiết kiệm 80% thời gian** cho bộ phận sales.
✅ **Tăng tỷ lệ chuyển đổi lead** lên 30%+.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API Anthropic** (để sử dụng AI Claude):
   - [Đăng ký API Key Anthropic](https://www.anthropic.com/api) (mã giảm giá: **N8NANTHROPIC**).
   - Thêm credentials trong n8n với tên: `anthropicApi`.

2. **Tài khoản Cal.com** (để đặt lịch hẹn tự động):
   - [Đăng ký Cal.com](https://cal.com/) (mã giảm giá: **N8NCAL**).
   - API Key từ **Settings > API Keys**.

3. **Tài khoản Instantly.ai** (để chuyển lead):
   - [Đăng ký Instantly.ai](https://instantly.ai/) (mã giảm giá: **N8NINSTANT**).
   - API Key từ **Settings > API**.

4. **Webhook URL** (để nhận yêu cầu demo từ trang web):
   - Cấu hình trong trang web hoặc form demo của doanh nghiệp.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/6380](https://n8n.io/workflows/6380) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6380) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **21 node** quan trọng, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "Webhook" (n8n-nodes-base.webhook)**
- **Path:** Đặt theo URL của trang web (ví dụ: `/demo-request`).
- **HTTP Method:** POST (để nhận dữ liệu từ form demo).

##### **🔹 Node "Anthropic Chat Model" (lmChatAnthropic)**
- **Model:** Chọn `claude-sonnet-4-20250514` (hoặc `claude-3-7-sonnet-20250219`).
- **Credentials:** Điền `anthropicApi` (API Key đã đăng ký trước).

##### **🔹 Node "AI Qualification" (agent)**
- **Prompt:** AI sẽ tự động phân loại yêu cầu demo (chất lượng cao/ thấp).
- **Output:** Kết quả sẽ được gửi đến node **Structured Output Parser** để định dạng.

##### **🔹 Node "Check Cal.com For Booking" (httpRequest)**
- **URL:** `https://cal.com/api/calendar/your-calendar-id/events`
- **Headers:** Điền `Authorization: Bearer YOUR_CAL_API_KEY`.
- **Query:** Kiểm tra xem lead có sẵn lịch hẹn không.

##### **🔹 Node "Add to Instantly" (httpRequest)**
- **URL:** `https://api.instantly.ai/leads`
- **Headers:** Điền `Authorization: Bearer YOUR_INSTANTLY_API_KEY`.
- **Body:** Gửi thông tin lead chất lượng cao vào Instantly.ai.

##### **🔹 Node "Respond to Webhook" (respondToWebhook)**
- **Trả lời tự động:** AI sẽ gửi phản hồi cho người gửi yêu cầu demo (ví dụ: "Cảm ơn! Chúng tôi sẽ liên hệ trong 24h").

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một yêu cầu demo từ form website.
   - Kiểm tra log trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active workflow** sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack/Telegram** để thông báo khi có lead chất lượng cao.
   - Cài đặt trong **Node "Respond to Webhook"** hoặc sau node **"Add to Instantly"**.

2. **Lưu log tự động:**
   - Sử dụng node **Set** để lưu dữ liệu vào **Google Sheets** hoặc **Airtable** để theo dõi lịch sử.

3. **Gửi báo cáo định kỳ:**
   - Tạo một workflow riêng để tổng hợp số liệu lead mỗi tuần và gửi qua **Email** hoặc **Slack**.

4. **Cải thiện AI Qualification:**
   - Tùy chỉnh **prompt** trong node **"AI Qualification"** để phù hợp với ngành nghề của doanh nghiệp.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quy trình xác minh và chăm sóc lead demo, giúp các sếp **tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và hoạt động 24/7**. **Hãy thử ngay và xem kết quả như thế nào!**

👉 **Bắt đầu tự động hóa ngay hôm nay!**
- [Tải workflow từ n8n.io](https://n8n.io/workflows/6380)
- [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm giá: **VPSN8N**)

**Chúc các sếp thành công!** 🚀