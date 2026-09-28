---
title: "🤖 Tự Động Hoá Email Digest AI: Tóm Tắt Tất Cả Email Theo Nhãn Gmail Với OpenAI O4-Mini (Không Cần Code)"
description: "Workflow tự động hóa 100% không code giúp các sếp tóm tắt và gửi email theo nhãn Gmail hàng ngày bằng trí tuệ nhân tạo OpenAI O4-Mini, tiết kiệm thời gian và giảm thiểu thông tin quá tải. Đặc biệt phù hợp cho content creator, chuyên gia marketing và người quản lý nhiều nguồn tin tức."
slug: "tieu-dong-hoa-email-digest-ai-gmail-openai-o4-mini"
tags: [n8n, automation, no-code, ai-summarization, gmail, openai, email-digest]
keywords: [n8n workflow email digest, tự động hóa email với AI, OpenAI O4-Mini, tóm tắt email hàng ngày, giảm thông tin quá tải, Gmail automation]
---

# 🚀 **Tự Động Hoá Email Digest AI: Tóm Tắt Tất Cả Email Theo Nhãn Gmail Với OpenAI O4-Mini**

### **Giải pháp hoàn hảo cho các sếp bị "chìm" trong hàng trăm email hàng ngày!**
Hàng ngày, các sếp phải mất **30-60 phút** để đọc, lọc và tóm tắt email từ các nhãn quan trọng như *Newsletter*, *Project Updates*, hoặc *Industry News*. Kết quả? **Thông tin quá tải**, **sự chú ý phân tán**, và **sự mệt mỏi** khi phải xử lý thủ công.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Lấy tất cả email mới** theo nhãn Gmail trong vòng 24h
✅ **Tóm tắt bằng AI** với OpenAI O4-Mini (mô hình tiên tiến, chi phí thấp)
✅ **Gửi email tổng hợp** hàng ngày (9h sáng) với định dạng HTML đẹp mắt
✅ **Không cần code**, chỉ cần cấu hình vài bước đơn giản

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 1-2 giờ/ngày** để tập trung vào công việc chính.
- **Giảm thông tin quá tải** với email tổng hợp ngắn gọn, có cấu trúc.
- **Không bỏ lỡ tin tức quan trọng** nhờ AI tóm tắt chính xác.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Cá nhân hóa** với định dạng email chuyên nghiệp, dễ đọc.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** với **OAuth2** được cấu hình (để n8n truy cập email).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
3. **Nhãn Gmail** để phân loại email cần tóm tắt (ví dụ: *Newsletter*, *Project Updates*).
4. **Email nhận digest** (cần thiết để gửi email tổng hợp).
5. **VPS Self-hosted n8n** (để workflow chạy 24/7 ổn định).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/5839) (hoặc copy JSON từ trang này).
2. Mở **n8n Editor** và nhấn **Import Workflow** (hoặc **Create New Workflow** > **Import from JSON**).
3. Dán JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **11 node**, các sếp cần chú ý cấu hình các node sau:

#### **A. Node "Get mails (last 24h)" (Gmail)**
- **Cấu hình OAuth2**:
  - Đăng nhập vào Gmail và cấp quyền cho n8n.
  - Tham khảo: [Cách cấu hình Gmail OAuth2](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/#authentication).
- **Tham số quan trọng**:
  - **Label ID**: Điền **ID của nhãn Gmail** bạn muốn tóm tắt (ví dụ: `newsletter` → tìm ID trong URL khi mở nhãn).
  - **Time Range**: Đặt là **24h** (mặc định).
  - **Operation**: Đặt là **getAll** (lấy tất cả email mới).

#### **B. Node "OpenAI Chat Model" (lmChatOpenAi)**
- **API Key OpenAI**:
  - Đăng nhập vào [OpenAI](https://platform.openai.com/) và lấy **API Key**.
  - Trong node, chọn **Credentials** → **New Credential** → Điền API Key.
- **Model**: Đặt là **o4-mini** (mô hình hiệu quả, chi phí thấp).

#### **C. Node "Summarization Mails" (chainSummarization)**
- **Prompt mặc định**:
  ```plaintext
  You are an AI assistant that summarizes emails in a concise and readable format.
  For each email, provide:
  1. A short subject line (max 30 characters).
  2. A bullet-point summary of the key points.
  3. Preserve all links and format them properly.
  ```
  - Các sếp có thể **thay đổi prompt** để phù hợp với nhu cầu (ví dụ: tóm tắt dài hơn, ngắn hơn).

#### **D. Node "Send Digested mail" (Gmail)**
- **Cấu hình OAuth2**:
  - Sử dụng cùng tài khoản Gmail như node lấy email (hoặc tài khoản khác).
- **Tham số quan trọng**:
  - **To**: Điền email nhận digest (ví dụ: `sếp@example.com`).
  - **Subject**: Đặt là **"Daily Email Digest - [Ngày]"**.
  - **HTML Body**: Workflow tự động tạo định dạng HTML đẹp.

#### **E. Node "Schedule Trigger" (scheduleTrigger)**
- **Thời gian chạy mặc định**: **9h sáng** (thay đổi theo nhu cầu).
- **Format**: Đặt là **cron** → `0 9 * * *` (9h sáng hàng ngày).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual trigger** để kiểm tra workflow với email mẫu.
   - Kiểm tra **log** trong node **No Operation** để debug lỗi.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **Active** trên workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi có email mới.
2. **Lưu Log Email**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử email đã tóm tắt.
3. **Tùy chỉnh Digest**:
   - Sử dụng node **Code** để thêm header/footer cá nhân hóa.
4. **Lọc Email theo Từ Khóa**:
   - Thêm node **If** để bỏ qua email không quan trọng (ví dụ: email spam).
5. **Gửi Digest Định Kỳ**:
   - Thay đổi **scheduleTrigger** để gửi hàng tuần/tháng.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa email digest** với AI, tiết kiệm thời gian và giảm thông tin quá tải. **Không cần code**, chỉ cần cấu hình vài bước đơn giản.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận email tổng hợp hàng ngày!

**Nếu gặp vấn đề**, các sếp có thể tham gia **Discord n8n** hoặc **Forum Cộng Đồng** để hỗ trợ:
👉 [Discord n8n](https://discord.com/invite/XPKeKXeB7d)
👉 [Forum n8n](https://community.n8n.io/)

---
**Happy Automating!** 🚀