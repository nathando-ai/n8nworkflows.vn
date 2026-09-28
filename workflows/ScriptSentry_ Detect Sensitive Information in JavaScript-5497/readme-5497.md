---
title: "🔍 ScriptSentry: Tự Động Phát Hiên Thông Tin Nhạy Cảm Trong JavaScript (AI + Puppeteer)"
description: "Workflow tự động quét, phát hiện và báo cáo thông tin nhạy cảm (API keys, PII, email) trong mã JavaScript của trang web, gửi báo cáo tự động qua email với AI hỗ trợ. Giúp các sếp bảo mật website, tuân thủ GDPR, CCPA mà không cần code."
slug: "script-sentry-tu-dong-phat-hien-thong-tin-nhay-cam-trong-javascript"
tags: [n8n, automation, security, ai, puppeteer, seo, no-code]
keywords: [n8n workflow bảo mật, phát hiện API key tự động, quét mã nguồn website, GDPR compliance, AI tự động hóa, tự động hóa seo]
---

# 🚀 **ScriptSentry: Bảo Vệ Website Bằng AI Phát Hiên Thông Tin Nhạy Cảm**

### **Nỗi Đau Của Các Sếp**
Bạn đã bao giờ lo lắng về:
- **Mã JavaScript** của website chứa **API keys**, **thông tin cá nhân (PII)** hoặc **email** công khai?
- **Vi phạm GDPR/CCPA** vì không phát hiện kịp thời thông tin nhạy cảm?
- **Tốn thời gian** phải quét thủ công hàng trăm trang web?
- **Không biết** liệu đối thủ cạnh tranh đã "lấy" thông tin của bạn từ mã nguồn?

**ScriptSentry** là giải pháp **tự động hóa 100% không code** giúp các sếp:
✅ **Quét toàn bộ mã JavaScript** trên trang web (đơn trang hoặc toàn bộ domain).
✅ **Phát hiện tự động** API keys, email, số điện thoại, và thông tin nhạy cảm khác.
✅ **Sử dụng AI (GPT-4.1-mini)** để tổng hợp báo cáo chi tiết.
✅ **Gửi báo cáo qua email** định kỳ (hoặc ngay khi phát hiện).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho Puppeteer + AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-20 giờ/ngày** so với quét thủ công.
- **Bảo mật cao**: Phát hiện API keys, token trước khi bị hacker lợi dụng.
- **Tuân thủ pháp luật**: GDPR, CCPA, HIPAA (nếu áp dụng).
- **AI tự động hóa**: GPT-4.1-mini tổng hợp báo cáo với ngữ cảnh chuyên nghiệp.
- **Hoạt động liên tục**: Chạy tự động hàng ngày, tuần, hoặc khi có sự thay đổi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (để gửi báo cáo):
   - Cấu hình **OAuth2** trong n8n (Settings → Credentials → Add OAuth2).
   - Điền **email nhận** (của bạn hoặc team) trong node **Send a message1**.

✔ **API Key OpenAI** (để sử dụng GPT-4.1-mini):
   - Tạo tại [OpenAI Platform](https://platform.openai.com/).
   - Thêm vào n8n dưới **openAiApi** (Settings → Credentials).

✔ **Puppeteer** (để quét trang web):
   - Cài đặt trong **Community Nodes** (Settings → Community Nodes → Search "Puppeteer").
   - **Lưu ý**: Puppeteer yêu cầu **RAM ít nhất 2GB** để chạy ổn định.

✔ **URL trang web** cần quét:
   - Sau khi import, truy cập **Form Trigger URL** (node **Landing Page Url1**) để nhập link.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5497](https://n8n.io/workflows/5497) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Node `Form Trigger` (Landing Page Url1)**
- **Chức năng**: URL này sẽ được dùng để **khởi động workflow** khi bạn nhập link trang web.
- **Cách sử dụng**:
  1. Click **Execute Workflow** → Copy link từ node này.
  2. Mở link trong trình duyệt → Nhập **URL trang web** cần quét (ví dụ: `https://tudonghoa.vn`).
  3. Click **Submit** để bắt đầu quét.

##### **B. Node `Puppeteer1`**
- **Chức năng**: Quét toàn bộ mã JavaScript trên trang web.
- **Lưu ý**:
  - Nếu trang web **chặn bot**, workflow có thể không hoạt động.
  - **Thời gian chạy**: Trang web nhỏ (5-10s), trang web lớn (30s-2min).
  - **RAM**: Yêu cầu **ít nhất 2GB** để tránh crash.

##### **C. Node `JavaScript Extractor1` (Code)**
- **Chức năng**: Lọc ra **thông tin nhạy cảm** như:
  - API keys (`sk-abc123`, `AIza...`).
  - Email (`user@example.com`).
  - Số điện thoại (`+84123456789`).
- **Không cần chỉnh sửa** (n8n đã cấu hình sẵn).

##### **D. Node `OpenAI Chat Model` (AI Tổng Hợp Báo Cáo)**
- **Chức năng**: Sử dụng **GPT-4.1-mini** để **tổng hợp báo cáo** với ngữ cảnh chuyên nghiệp.
- **Lưu ý**:
  - Đảm bảo **API Key OpenAI** đã điền đúng trong **credentials**.
  - **Prompt mặc định** đã tối ưu, **không cần chỉnh sửa** trừ khi cần thay đổi cách AI trả lời.

##### **E. Node `Send a message1` (Gmail)**
- **Chức năng**: Gửi báo cáo qua email.
- **Cách cấu hình**:
  1. Trong **credentials**, chọn **gmailOAuth2**.
  2. Điền **email nhận** (của bạn hoặc team) trong **To**.
  3. **From**: Điền email của bạn (đã cấu hình OAuth2).
  4. **Subject**: Thay đổi thành `"Báo cáo bảo mật website: [Tên Website]"` (ví dụ: `"Báo cáo bảo mật website: tudonghoa.vn"`).

##### **F. Node `JavaScript Search Agent w/Email Template1` (Agent AI)**
- **Chức năng**: **Tối ưu hóa quá trình** bằng AI, giúp phát hiện thông tin nhạy cảm hiệu quả hơn.
- **Không cần chỉnh sửa** (n8n đã cấu hình sẵn).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập **URL mẫu** (ví dụ: `https://example.com`) vào **Form Trigger**.
   - Chạy workflow và kiểm tra **email nhận** có báo cáo không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Quét Định Kỳ (Cron Job)**
- Sử dụng **n8n Cron Trigger** để chạy workflow **hàng ngày/tuần**.
- **Cách làm**:
  1. Thêm node **Cron Trigger** vào workflow.
  2. Cấu hình lịch (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  3. Kết nối với node **Form Trigger** để tự động nhập URL.

#### **2. Lưu Log Vào Google Sheets**
- Thêm node **Google Sheets** để **lưu lịch sử phát hiện** (giúp theo dõi xu hướng vi phạm).
- **Cách làm**:
  1. Thêm node **Google Sheets** sau **Send a message1**.
  2. Cấu hình sheet với cột: `Ngày quét`, `URL`, `Thông tin nhạy cảm phát hiện`.

#### **3. Gửi Báo Cáo Vào Slack/Telegram**
- Thay thế node **Gmail** bằng **Slack Webhook** hoặc **Telegram Bot** để báo cáo tức thời.
- **Cách làm**:
  1. Thêm node **Slack** hoặc **Telegram**.
  2. Cấu hình **webhook URL** từ Slack/Telegram.

#### **4. Phát Hiên Thông Tin Nhạy Cảm Trong Code GitHub**
- Nếu website sử dụng **GitHub**, bạn có thể:
  1. Thêm node **GitHub API** để lấy mã nguồn.
  2. Chạy **Puppeteer** trên file `.js` trong repo.
  3. Gửi báo cáo cho **team DevOps**.

---

### 📌 **Kết Luận**
**ScriptSentry** là **công cụ tự động hóa bảo mật** hoàn hảo cho các sếp:
✔ **Không cần code** nhưng hiệu quả như chuyên gia.
✔ **Phát hiện API keys, PII, email** trong JavaScript.
✔ **Gửi báo cáo tự động** qua email với AI hỗ trợ.
✔ **Tuân thủ GDPR/CCPA** mà không tốn thời gian.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Quét website** của bạn để phát hiện thông tin nhạy cảm.
3. **Cài đặt định kỳ** để bảo mật liên tục.

👉 [Tải workflow ngay từ n8n.io](https://n8n.io/workflows/5497) và bảo vệ website của bạn **hôm nay**! 🚀

---
**Chia sẻ ý kiến** của các sếp về workflow này trong comment dưới đây! 👇