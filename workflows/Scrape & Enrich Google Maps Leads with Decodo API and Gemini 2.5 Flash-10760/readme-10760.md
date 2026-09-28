---
title: "🚀 Tự Động Hoá Scraping & Tăng Cường Dữ Liệu Google Maps với Decodo API + Gemini 2.5 Flash (AI Tự Động)"
description: "Workflow tự động hóa 100% không code để scrap dữ liệu doanh nghiệp từ Google Maps, tăng cường thông tin bằng AI Gemini 2.5 Flash, và lọc ra leads chất lượng cao (score ≥7) với email outreach sẵn sàng gửi. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng tỷ lệ chuyển đổi lên 30%."
slug: "tieu-dong-hoa-scraping-google-maps-decodo-gemini"
tags: [n8n, automation, lead-generation, ai-summarization, google-maps-scraping, gemini-ai, no-code]
keywords: [n8n workflow google maps, tự động hóa scrap leads, gemini 2.5 flash, tăng cường dữ liệu doanh nghiệp, lọc leads chất lượng cao, outreach email tự động]
---

# 🚀 **Tự Động Hoá Scraping & Tăng Cường Dữ Liệu Google Maps với AI Gemini 2.5 Flash**

### **Giải pháp cho các sếp bán hàng, marketing và sales team:**
Bạn có bao giờ phải mất **5-10 giờ/ngày** để:
- Scrap dữ liệu doanh nghiệp từ Google Maps?
- Lọc ra leads thực sự chất lượng (có số điện thoại, email, địa chỉ chi tiết)?
- Tự động tạo **email outreach cá nhân hóa** sẵn sàng gửi?
- **Gemini 2.5 Flash** sẽ giúp bạn **tự động hóa toàn bộ quy trình** này chỉ với **1 workflow n8n**!

Workflow này **scrap dữ liệu từ Google Maps**, **tăng cường thông tin bằng AI**, **lọc leads chất lượng cao**, và **tự động tạo email outreach** – tất cả **không cần viết một dòng code nào!**

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 10+ giờ/ngày** – Không cần scrap thủ công hoặc sử dụng công cụ trả phí.
✅ **Leads chất lượng cao** – AI Gemini 2.5 Flash **đánh giá score 1-10** cho mỗi lead (score ≥7 mới được lưu).
✅ **Email outreach cá nhân hóa** – AI tự động **tạo nội dung email** phù hợp với từng doanh nghiệp.
✅ **Hoạt động 24/7** – Không cần can thiệp thủ công, workflow chạy tự động mỗi khi có dữ liệu mới.
✅ **Lưu trữ dữ liệu trên Google Sheets** – Dễ dàng theo dõi và quản lý leads.
✅ **Báo lỗi tự động qua Telegram** – Nếu workflow gặp sự cố, bạn sẽ được thông báo ngay.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Decodo API** (để scrap Google Maps):
   - [Đăng ký API Decodo](https://dashboard.decodo.com/web-scraping-api/scraper?target=google_maps) (miễn phí 1000 request/tháng).
   - **API Key** sẽ được sử dụng trong **HTTP Header Auth** của node `Decodo Maps Scraper`.

2. **Tài khoản Google Sheets** (để lưu leads):
   - **Credentials OAuth2** cho Google Sheets (cài đặt trong n8n).

3. **API Key của Google Gemini 2.5 Flash** (để tăng cường dữ liệu):
   - [Đăng ký API Gemini](https://ai.dev/) (miễn phí 3 tháng).
   - **API Key** sẽ được sử dụng trong node `2.5 Flash`.

4. **(Tùy chọn) Bot Telegram** (để nhận báo lỗi):
   - [Tạo bot Telegram](https://t.me/BotFather) và lấy **API Token**.

5. **VPS Self-hosted n8n** (để workflow chạy 24/7):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10760](https://n8n.io/workflows/10760).
- **Import vào n8n Editor**:
  - Nhấn `Import` → Chọn file JSON → Nhấn `Import`.
  - **Hoặc** copy toàn bộ JSON và paste vào `Create Workflow` → `Import JSON`.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Credentials**
| **Node**               | **Credentials**               | **Hướng dẫn**                                                                 |
|------------------------|-------------------------------|---------------------------------------------------------------------------------|
| **Decodo Maps Scraper** | `httpHeaderAuth`              | - **Header Name:** `Authorization`                                            |
|                        |                               | - **Header Value:** `Basic YOUR_DECODO_API_KEY` (đổi `YOUR_DECODO_API_KEY` thành API key từ Decodo) |
| **Google Sheets**       | `googleSheetsOAuth2Api`       | Cài đặt OAuth2 từ Google Cloud Console (đã hướng dẫn trong n8n).              |
| **Gemini 2.5 Flash**   | `googlePalmApi`               | - **API Key:** Lấy từ [ai.dev](https://ai.dev/).                              |
| **Telegram (nếu dùng)**| `telegramApi`                 | - **Token:** Lấy từ [BotFather](https://t.me/BotFather).                        |

#### **B. Cấu hình Search Parameters (Node `Set Search Parameters`)**
- **Query:** Nhập từ khóa tìm kiếm (ví dụ: `"café sữa chua Hà Nội"`).
- **Country:** Chọn quốc gia (ví dụ: `VN`).
- **Language:** Chọn ngôn ngữ (`vi` hoặc `en`).
- **Results Limit:** Đặt số lượng kết quả scrap (gợi ý bắt đầu từ **5** để test).

#### **C. Cấu hình AI Enrichment (Node `2.5 Flash`)**
- **Model:** Chọn `gemini-2.5-flash`.
- **Prompt:** AI sẽ tự động phân tích và tạo **value proposition**, **pain points**, và **outreach hooks**.
- **Output Format:** Đảm bảo trả về **structured data** (JSON) để node `Result Parser` xử lý.

#### **D. Cấu hình Filter Hot Leads (Node `Filter Hot Leads`)**
- **Điều kiện:** Lọc leads có **score ≥7** và **có thông tin liên lạc** (email/số điện thoại).
- **Action:** Leads chất lượng sẽ được **lưu vào Google Sheets** với status `"HOT"`.

#### **E. Cấu hình Error Handling (Node `Error Handler`)**
- **Telegram Bot Token:** Nếu muốn nhận báo lỗi, điền **API Token** của bot Telegram.
- **Message Format:** Node `Format Error Message` sẽ tự động tạo thông báo chi tiết.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra kết quả):
   - Nhấn `Run Workflow` với **resultsLimit = 5**.
   - Kiểm tra **Google Sheets** và **Telegram** (nếu có) để xem kết quả.
2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấn `Active` để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**TIẾP CẬN HƠN**]
1. **Kết hợp với Slack/Email** (thay vì Telegram):
   - Thay node `telegram` bằng `email` hoặc `slack` để gửi báo cáo hàng ngày.
2. **Lưu log hoạt động**:
   - Sử dụng node `set` để lưu **thời gian scrap**, **số lượng leads**, và **status** vào Google Sheets.
3. **Tự động gửi email outreach**:
   - Kết nối với **SendGrid** hoặc **Mailchimp** để tự động gửi email cho leads "HOT".
4. **Tăng cường dữ liệu thêm**:
   - Sử dụng **API khác** (ví dụ: Clearbit) để lấy thông tin thêm về doanh nghiệp.
5. **Tối ưu search query**:
   - Thử các từ khóa khác nhau (ví dụ: `"restaurant vegan TP.HCM"`) để tìm leads phù hợp.
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc scrap thủ công**, **tự động hóa tăng cường dữ liệu bằng AI**, và **lọc ra leads chất lượng cao** – tất cả chỉ với **một workflow n8n**!

**Hành động ngay:**
1. **Đăng ký Decodo API** và **Google Gemini** (nếu chưa có).
2. **Import workflow** và **cấu hình credentials**.
3. **Test với 5 kết quả** và **bật Active** để tự động hóa toàn bộ quy trình!

**🚀 Kết quả:** Tiết kiệm **10+ giờ/ngày**, **tăng tỷ lệ chuyển đổi lên 30%**, và **hoạt động 24/7** mà không cần can thiệp thủ công!

---
**💡 Lưu ý:** Nếu gặp khó khăn, hãy để lại comment dưới đây hoặc liên hệ với cộng đồng n8n để được hỗ trợ!