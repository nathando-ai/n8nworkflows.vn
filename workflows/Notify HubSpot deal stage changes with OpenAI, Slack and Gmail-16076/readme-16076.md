---
title: "🚀 Tự Động Hóa Thông Báo Thay Đổi Stage Deal HubSpot Với AI, Slack & Email (N8N)"
description: "Workflow tự động hóa thông báo thay đổi stage deal trong HubSpot bằng AI OpenAI, gửi thông báo Slack cá nhân hóa và email chúc mừng cho deal Won/Lost, đồng thời ghi log vào Google Sheets. Giúp đội ngũ bán hàng luôn cập nhật và tối ưu hóa quy trình bán hàng 24/7."
slug: "tieu-dong-hoa-thong-bao-thay-doi-stage-deal-hubspot-ai-slack-email"
tags: [n8n, automation, hubspot, ai-summarization, slack, gmail, crm, openai, no-code]
keywords: [n8n workflow hubspot, tự động hóa bán hàng, ai trong hubspot, thông báo deal won lost, slack automation, gmail automation, tự động hóa crm]
---

# 🚀 **Tự Động Hóa Thông Báo Thay Đổi Stage Deal HubSpot Với AI, Slack & Email**

### **Giải pháp cho đội ngũ bán hàng:**
Hàng ngày, các sếp và đội ngũ bán hàng phải mất thời gian theo dõi từng deal trong HubSpot, ghi chú tay, và gửi thông báo cá nhân hóa cho từng thành viên. **Workflow này tự động hóa toàn bộ quy trình:**
- **Nhận biết** khi một deal chuyển stage trong HubSpot.
- **Tích hợp AI** để tổng hợp thông tin deal và đề xuất các bước tiếp theo.
- **Gửi thông báo Slack** đến đội ngũ bán hàng và lãnh đạo.
- **Gửi email chúc mừng** cho thành viên khi deal Won.
- **Cảnh báo deal Lost** đến quản lý.
- **Ghi log** tất cả hoạt động vào Google Sheets để theo dõi.
- **Cập nhật HubSpot** với ghi chú tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần theo dõi thủ công từng deal, tự động cập nhật thông tin.
- **Cá nhân hóa thông báo:** Slack và email được gửi với tên thật của contact và owner.
- **Tối ưu hóa quyết định:** AI đề xuất các bước tiếp theo cho deal.
- **Cảnh báo kịp thời:** Deal Lost được gửi cảnh báo ngay đến lãnh đạo.
- **Dữ liệu minh bạch:** Tất cả hoạt động được ghi log vào Google Sheets.
- **Hoạt động liên tục:** Workflow chạy 24/7 mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (API Key + Developer API).
2. **Tài khoản OpenAI** (API Key).
3. **Tài khoản Slack** (Credentials + tên channel: `#sales-team`, `#leadership`).
4. **Tài khoản Gmail** (Credentials để gửi email chúc mừng).
5. **Google Sheets** (Sheet ID để ghi log).
6. **N8n Editor** (cài đặt phiên bản mới nhất).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/16076) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Lưu workflow** với tên **"HubSpot Deal Stage Notifier"** (hoặc tên tùy ý).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình HubSpot Trigger**
- **Node:** `HubSpot Trigger`
  - Chọn **Credentials** của HubSpot (đã cấu hình trước).
  - **Event:** Chọn `deal` và `stage` (để workflow kích hoạt khi stage deal thay đổi).

##### **B. Kiểm tra thay đổi stage thực sự**
- **Node:** `Is Real Stage Change?` (If node)
  - Cấu hình điều kiện để loại bỏ các thay đổi stage không cần thiết (ví dụ: stage `Prospecting` → `Qualified`).

##### **C. Lấy chi tiết deal, contact và owner**
- **Node:** `Get Deal Details` (HubSpot)
  - Chọn **Credentials HubSpot**.
  - **Operation:** `get` → **Resource:** `deal`.
- **Node:** `Get Owner Details` (HTTP Request)
  - **URL:** `https://api.hubapi.com/crm/v3/objects/people/{owner_id}` (lấy từ deal details).
  - **Headers:** Thêm `Authorization: Bearer {HubSpot API Key}`.
- **Node:** `Get Contact Details` (HTTP Request)
  - **URL:** `https://api.hubapi.com/crm/v3/objects/contacts/{contact_id}`.
  - **Headers:** Giống như trên.

##### **D. Tích hợp OpenAI để tổng hợp AI**
- **Node:** `Generate AI Summary` (OpenAI)
  - **Credentials:** Thêm API Key OpenAI.
  - **Prompt:** Sử dụng template mặc định (có thể tùy chỉnh trong **Code Node** `Format Deal Data`).
  - **Model:** Chọn `gpt-3.5-turbo` (hoặc `gpt-4` nếu có budget).

##### **E. Cấu hình Slack & Gmail**
- **Node:** `Slack - Leadership Channel` & `Slack - Sales Team Channel`
  - **Credentials:** Thêm token Slack (tạo từ [Slack API](https://api.slack.com/apps)).
  - **Channel:** Điền tên channel cụ thể (ví dụ: `#sales-team`, `#leadership`).
- **Node:** `Gmail - Congrats to Owner`
  - **Credentials:** Thêm tài khoản Gmail (cần **App Password** nếu sử dụng 2FA).
  - **Email Template:** Sử dụng template mặc định (có thể chỉnh sửa trong **Code Node** `Build Enriched Context`).

##### **F. Ghi log vào Google Sheets**
- **Node:** `Log to Google Sheets`
  - **Credentials:** Thêm API Key Google Sheets.
  - **Sheet ID:** Điền ID sheet (lấy từ liên kết Google Sheets: `https://docs.google.com/spreadsheets/d/{SHEET_ID}/edit`).
  - **Range:** `Sheet1!A1` (hoặc tên sheet tùy ý).

##### **G. Xử lý Deal Won/Lost**
- **Node:** `Won / Lost / Other?` (Switch node)
  - **Cases:**
    - **Closed Won:** Gửi email chúc mừng (`Gmail - Congrats to Owner`).
    - **Closed Lost:** Gửi cảnh báo Slack (`Slack - Loss Alert to Management`).
    - **Khác:** Gửi thông báo Slack thông thường (`Slack - Sales Team Channel`).

##### **H. Cập nhật HubSpot & Cảnh báo lỗi**
- **Node:** `Create HubSpot Note on Deal` & `Associate Note to Deal`
  - **URL:** `https://api.hubapi.com/crm/v3/objects/deals/{deal_id}/notes` (lấy từ `Get Deal Details`).
  - **Headers:** Thêm `Authorization: Bearer {HubSpot API Key}`.
- **Node:** `Slack - Error Alert`
  - **Credentials:** Slack (channel `#error-alerts`).
  - **Message:** Thông báo lỗi chi tiết (ví dụ: lỗi API, thiếu dữ liệu).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một deal mẫu:
   - Chọn **Run Workflow** và nhập **deal ID** từ HubSpot.
   - Kiểm tra:
     - Slack có nhận được thông báo không?
     - Email có được gửi không?
     - Google Sheets có ghi log không?
2. **Bật Active Workflow**:
   - Đảm bảo tất cả node hoạt động bình thường.
   - **Bật Active** để workflow chạy tự động khi deal stage thay đổi.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt AI**:
   - Mở **Code Node** `Format Deal Data` và chỉnh sửa template để AI đề xuất các bước tiếp theo phù hợp với ngành nghề của doanh nghiệp.
   - Ví dụ: Nếu là SaaS, AI có thể đề xuất "Gửi demo sản phẩm" hoặc "Tư vấn về giá cả".

2. **Kết hợp với Zapier/Integromat**:
   - Nếu cần gửi thông báo đến nhiều nền tảng (ví dụ: Telegram, Microsoft Teams), có thể sử dụng **HTTP Request** để gọi API của các nền tảng đó.

3. **Ghi log chi tiết hơn**:
   - Thêm **Google Sheets** để ghi log thêm thông tin như:
     - Thời gian deal chuyển stage.
     - Người tạo deal.
     - Lịch sử stage trước đó.

4. **Tự động gửi báo cáo tuần/month**:
   - Sử dụng **n8n Scheduler** để chạy workflow định kỳ và gửi báo cáo tổng hợp về deal Won/Lost qua Slack hoặc email.

5. **Cảnh báo deal ở stage "Stuck"**:
   - Thêm **Code Node** để kiểm tra deal ở stage `Prospecting` trong >7 ngày và gửi cảnh báo tự động.

---

### 📌 **Kết luận**
Workflow này **giải phóng đội ngũ bán hàng** khỏi việc theo dõi thủ công từng deal, đồng thời **tối ưu hóa quy trình bán hàng** bằng AI và tự động hóa thông báo. **Các sếp hãy áp dụng ngay để:**
✅ **Tiết kiệm thời gian** cho đội ngũ.
✅ **Cải thiện trải nghiệm khách hàng** với thông báo cá nhân hóa.
✅ **Nhận được báo cáo minh bạch** từ Google Sheets.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Bắt đầu tự động hóa ngay hôm nay!** 🚀
Nếu có vấn đề, hãy để lại comment dưới đây hoặc liên hệ với [Avkash Kakdiya](https://itechnotion.com/) (tác giả của workflow).