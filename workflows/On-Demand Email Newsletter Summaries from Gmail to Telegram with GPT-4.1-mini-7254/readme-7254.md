---
title: "📧 Tự Động Tóm Tắt Tin Nhắn Gmail Sang Telegram Với GPT-4.1-mini - Không Cần Code!"
description: "Workflow tự động hóa lấy tất cả tin nhắn Gmail, tóm tắt nội dung bằng AI, và gửi dưới dạng tin nhắn Telegram định kỳ - tiết kiệm thời gian lên đến 80% cho công việc quản lý email."
slug: "tieu-dong-tom-tat-tin-nhan-gmail-sang-telegram-voi-gpt-4-1-mini"
tags: [n8n, automation, gmail, telegram, ai, gpt-4.1-mini, no-code]
keywords: [tự động hóa email telegram, gmail telegram ai, tóm tắt tin nhắn bằng gpt, workflow n8n gmail telegram, tự động hóa quản lý email]
---

# 🚀 **Tự Động Tóm Tắt Email Gmail Sang Telegram Với GPT-4.1-mini**

### **Giải pháp hoàn hảo cho các sếp bị "ngập" email hàng ngày**
Hàng ngày, các sếp phải mất **30-60 phút** để đọc, lọc và tóm tắt tin nhắn quan trọng từ Gmail. Workflow này **tự động hóa toàn bộ quá trình** bằng cách:
✅ **Lấy tất cả tin nhắn** từ Gmail (bao gồm tin nhắn nhóm, tin nhắn từ ngày trước).
✅ **Tóm tắt nội dung** bằng **GPT-4.1-mini** (của OpenAI) thành các chủ đề ngắn gọn.
✅ **Gửi kết quả dưới dạng tin nhắn Telegram** định dạng HTML, dễ đọc và chia sẻ.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** quản lý email hàng ngày.
- **Không bỏ lỡ tin nhắn quan trọng** nhờ AI tóm tắt chính xác.
- **Dễ dàng chia sẻ** kết quả với đồng nghiệp qua Telegram.
- **Hoạt động tự động** ngay cả khi các sếp ngủ.
- **Định dạng chuyên nghiệp** với HTML, dễ đọc trên mọi thiết bị.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n).
2. **Tài khoản Telegram** và **bot Telegram** (để nhận tin nhắn tự động).
3. **API Key OpenAI** (để sử dụng GPT-4.1-mini).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/7254) hoặc copy toàn bộ JSON từ đây.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **"Active"** để kích hoạt workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **13 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node "Get many messages" (Gmail)**
- **Credentials:** Chọn `gmailOAuth2` (đã cấu hình trước).
- **Operation:** Đặt là `getAll` để lấy tất cả tin nhắn.

##### **🔹 Node "Telegram Trigger"**
- **Credentials:** Chọn `telegramApi` (API Key của bot Telegram).
- **Lưu ý:** Bot Telegram phải được tạo trước và thêm vào nhóm/đại diện cá nhân.

##### **🔹 Node "Message a model" (OpenAI)**
- **Credentials:** Chọn `openAiApi` (API Key OpenAI).
- **Prompt:** Workflow đã cấu hình sẵn prompt tóm tắt email, **không cần chỉnh sửa** (nếu muốn tối ưu, các sếp có thể thay đổi ở node này).

##### **🔹 Các Node Code (Cần kiểm tra)**
Workflow sử dụng **6 node Code** để xử lý logic:
- **"Get days"**: Lấy ngày từ Telegram Trigger (ví dụ: nếu người dùng gửi số `2`, nó lấy tin nhắn từ 2 ngày trước).
- **"Get message data"**: Lấy chi tiết tin nhắn từ Gmail.
- **"Merge"**: Kết hợp dữ liệu tin nhắn.
- **"Create TG message"**: Tạo tin nhắn Telegram từ dữ liệu tóm tắt.
- **"Sanitize" & "Clean"**: Lọc và định dạng lại nội dung để phù hợp với Telegram.

**Lưu ý quan trọng:**
- Nếu các sếp muốn **thay đổi ngày lấy tin nhắn**, cần chỉnh sửa **node "Get days"** (ví dụ: thay `2` thành `7` để lấy tin nhắn từ 7 ngày trước).
- **Node "Split"** (nếu có) sẽ chia tin nhắn thành nhiều phần nhỏ để phù hợp với giới hạn Telegram (4096 ký tự).

#### **3. Kích hoạt ⚡️**
- **Test Run:** Gửi số `2` đến bot Telegram để lấy tin nhắn từ 2 ngày trước.
- **Active Workflow:** Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động tự động.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ NHẤT]
1. **Tạo bot Telegram riêng** để quản lý tin nhắn tự động (không dùng bot công cộng).
2. **Thêm node "StickyNote"** để ghi chú lỗi hoặc cập nhật prompt cho AI.
3. **Kết hợp với Slack** bằng node Slack để báo cáo lỗi hoặc kết quả.
4. **Lưu log** bằng node **Google Sheets** hoặc **Airtable** để theo dõi lịch sử.
5. **Chạy định kỳ** bằng **n8n Cron** (nếu muốn gửi tin nhắn hàng ngày vào 8h sáng).
:::

---
### **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại quản lý email. **Chỉ cần 10 phút setup**, sau đó AI sẽ tự động tóm tắt và gửi tin nhắn Telegram cho các sếp **mỗi khi có yêu cầu**.

**👉 Hãy thử ngay và tiết kiệm thời gian cho công việc quan trọng hơn!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::