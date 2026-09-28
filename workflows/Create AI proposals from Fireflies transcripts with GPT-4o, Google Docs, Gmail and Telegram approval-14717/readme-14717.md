---
title: "🚀 Tự Động Hóa Tạo Báo Giá AI Từ Phiên Bản Ghi Chép Fireflies (GPT-4o + Google Docs + Gmail + Telegram)"
description: "Workflow tự động hóa 100% không code chuyển phiên bản ghi chép cuộc họp từ Fireflies thành báo giá chuyên nghiệp, được AI phân loại và cá nhân hóa, sau đó gửi qua Gmail và yêu cầu phê duyệt qua Telegram. Giúp các sếp tiết kiệm 8+ giờ/tháng và tăng cường độ chính xác trong giao dịch."
slug: "tu-dong-hoa-tao-bao-gia-ai-tu-fireflies"
tags: [n8n, automation, no-code, ai-summarization, fireflies, google-docs, gmail, telegram, sales-automation]
keywords: [tự động hóa báo giá AI, fireflies n8n, gpt-4o tạo báo giá, tự động hóa bán hàng không code, workflow n8n google docs]
---

# 🚀 **Tự Động Hóa Tạo Báo Giá AI Từ Phiên Bản Ghi Chép Fireflies (Không Cần Code!)**

### **🔥 Nỗi Đau Của Các Sếp Trong Bán Hàng & Marketing**
Các sếp thường phải:
- **Ghi chép thủ công** những cuộc họp quan trọng từ Fireflies vào báo giá.
- **Tốn thời gian** viết lại nội dung từ phiên bản ghi chép thành báo giá chuyên nghiệp.
- **Mất nhiều giờ** để cá nhân hóa mỗi báo giá cho khách hàng.
- **Rủi ro sai sót** khi copy-paste thông tin từ cuộc họp vào mẫu báo giá.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Phân loại cuộc họp** (đơn hàng, tư vấn, từ chối) bằng AI.
✅ **Tạo báo giá cá nhân hóa** từ phiên bản ghi chép Fireflies.
✅ **Xuất PDF** và gửi qua Gmail cho khách hàng.
✅ **Yêu cầu phê duyệt** qua Telegram trước khi gửi.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 8+ giờ/tháng** cho đội bán hàng.
- **Giảm sai sót** nhờ AI phân tích và tự động hóa.
- **Cá nhân hóa báo giá** cho từng khách hàng.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Tăng cơ hội thành công** với báo giá chuyên nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Fireflies** (để lấy phiên bản ghi chép cuộc họp).
2. **API Key OpenAI** (để sử dụng GPT-4o phân loại và tạo nội dung).
3. **Google Drive & Google Docs** (mẫu báo giá với placeholder).
4. **Tài khoản Gmail** (để gửi báo giá cho khách hàng).
5. **Bot Telegram** (để phê duyệt báo giá).
6. **VPS Self-hosted n8n** (để workflow chạy 24/7).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14717](https://n8n.io/workflows/14717).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste** JSON vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **25 node**, nhưng các node quan trọng nhất cần cấu hình kỹ:

##### **🔹 Node Webhook (When Transcript Ready)**
- **Path:** `fireflies-transcript`
- **HTTP Method:** `POST`
- **Cấu hình Fireflies:**
  - Vào **Settings > Developer > Webhooks** → Thêm URL webhook từ n8n.
  - Chọn **HTTP Header Auth** với API Key Fireflies.

##### **🔹 Node OpenAI (Classify Meeting Type & Generate Proposal Content)**
- **API Key:** Điền vào **Credentials** của node OpenAI.
- **Prompt AI:**
  - **Phân loại cuộc họp:** Cần chỉnh sửa để phù hợp với tiêu chí của doanh nghiệp.
  - **Tạo báo giá:** Đảm bảo nội dung phù hợp với **brand voice** và cấu trúc báo giá.

##### **🔹 Node Google Docs (Fill Template Placeholders)**
- **Mẫu báo giá cần có:**
  - **Placeholder:** `{{CLIENT_NAME}}, {{CLIENT_COMPANY}}, {{MEETING_DATE}}, ...`
  - **Cách tạo:**
    1. Tạo 1 Google Doc mới.
    2. Thêm các placeholder trên.
    3. **Copy Doc ID** từ URL (ví dụ: `https://docs.google.com/document/d/1AbCdEfGhIjKlMnOpQRsTuVwXyZ/` → `1AbCdEfGhIjKlMnOpQRsTuVwXyZ`).
    4. Điền vào **Copy Proposal Template** node.

##### **🔹 Node Telegram (Send Approval Request & Wait for Approval)**
- **Bot Token & Chat ID:**
  - Tạo bot Telegram → Lấy **API Token** từ `@BotFather`.
  - Lấy **Chat ID** của bạn (gửi tin nhắn cho bot, sau đó check `https://api.telegram.org/bot<TOKEN>/getUpdates`).
  - Điền vào tất cả các node Telegram.

##### **🔹 Node Gmail (Send Proposal Email)**
- **OAuth2 Credential:**
  - Vào **Credentials** → Thêm **Gmail OAuth2**.
  - Chọn **Gmail** → Đăng nhập tài khoản.
  - Chọn **Scopes:** `https://www.googleapis.com/auth/gmail.send`.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy với 1 phiên bản ghi chép mẫu từ Fireflies.
- **Bật Active:** Sau khi kiểm tra thành công, bật workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thay Telegram bằng Slack:**
   - Sử dụng node **Slack** thay vì Telegram để phê duyệt báo giá.
2. **Lưu Log Tất Cả Các Báo Giá:**
   - Thêm node **Google Sheets** để ghi lại lịch sử báo giá.
3. **Gửi Báo Cáo Định Kỳ:**
   - Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp hàng tuần.
4. **Cải Thiện AI với Prompt Tùy Chỉnh:**
   - Đối với **Classify Meeting Type**, thêm điều kiện như:
     ```json
     "Nếu cuộc họp liên quan đến 'dịch vụ marketing', thì đánh dấu là 'Proposal Needed'."
     ```
   - Đối với **Generate Proposal Content**, yêu cầu AI:
     ```json
     "Sử dụng ngôn ngữ chuyên nghiệp, tránh từ lóng, và bao gồm 3 giải pháp cụ thể."
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc bán hàng chứ không phải viết báo giá. **Tự động hóa 100% không code**, kết hợp AI, Google Docs và Telegram để tạo báo giá chuyên nghiệp và nhanh chóng.

**🚀 Hãy áp dụng ngay và giảm thiểu công việc thủ công!**
Nếu cần hỗ trợ thêm, **hãy liên hệ với Devon Toh** qua [cal.com](https://cal.com/devon-toh-vrmdab/30min) để tư vấn chi tiết.

---
**💡 Lưu ý cuối cùng:**
- **Không có mẫu báo giá?** → Tạo ngay 1 Google Doc với placeholder và copy Doc ID.
- **Không biết cấu hình Telegram?** → Tạo bot và lấy Chat ID theo hướng dẫn trên Telegram.
- **Cần tối ưu AI?** → Chỉnh sửa prompt để phù hợp với doanh nghiệp.