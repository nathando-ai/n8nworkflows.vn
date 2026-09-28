---
title: "🤖 **Tự Động Phân Loại Email Gmail Bằng GPT-4 Mini – Giảm 90% Thời Gian Quản Lý Email**"
description: "Workflow tự động phân loại email Gmail thành 'Business', 'Cold Emails', hoặc 'Meetings' bằng trí tuệ nhân tạo GPT-4 Mini, giúp các sếp tiết kiệm hàng giờ mỗi ngày và duy trì inbox sạch sẽ 24/7."
slug: "tu-dong-phan-loai-email-gmail-bang-gpt-4-mini"
tags: [n8n, automation, gmail, ai, gpt-4-mini, no-code]
keywords: [tự động hóa email gmail, phân loại email bằng ai, gpt-4 mini n8n, quản lý email không code, workflow gmail n8n]
---

# 🚀 **Tự Động Phân Loại Email Gmail Bằng GPT-4 Mini – Giúp Các Sếp Quên Về "Inbox Clutter"**

### **Nỗi Đau Thực Tế Của Các Sếp**
Hàng ngày, các sếp phải mất **từ 1-2 giờ** để:
- **Lọc email** giữa tin nhắn quan trọng (business), email lạnh (cold emails), và thông báo cuộc họp (meetings).
- **Xóa hoặc nhãn** hàng trăm email mỗi ngày, dẫn đến **stress** và **sai sót**.
- **Tìm kiếm lại** email cũ trong một inbox hỗn loạn, mất thời gian và hiệu suất.

**Workflow này giải quyết tất cả đó bằng trí tuệ nhân tạo!** Dựa trên **GPT-4 Mini** (mô hình AI mạnh mẽ của OpenAI), nó tự động phân loại email và **nhãn/đánh dấu** chúng theo danh mục, giúp các sếp **tự động hóa 90% công việc quản lý email**.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 1-2 giờ/ngày** – Không phải mất thời gian lọc email thủ công.
✅ **Inbox sạch sẽ 24/7** – Email được tự động nhãn hóa và xóa (nếu cần).
✅ **Chính xác cao** – GPT-4 Mini phân loại với độ chính xác >90%.
✅ **Hoạt động liên tục** – Không cần can thiệp người dùng.
✅ **Giao diện thân thiện** – Dễ dàng cấu hình, không cần code.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0).
2. **API Key OpenAI** (để sử dụng GPT-4 Mini).
3. **n8n Self-hosted** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**Lưu ý:** Workflow **không hoạt động** nếu sử dụng n8n Cloud (do giới hạn API và tính năng).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```bash
# Cách 1: Import từ file JSON
1. Tải file workflow từ [n8n.io/workflows/7599](https://n8n.io/workflows/7599).
2. Trên n8n Editor, nhấn **Import** và chọn file.
3. Chọn **Create Workflow**.

# Cách 2: Copy/Paste JSON
1. Trên n8n Editor, nhấn **Create Workflow**.
2. Chọn **Import from JSON** và dán mã JSON từ [n8n.io/workflows/7599](https://n8n.io/workflows/7599).
```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này bao gồm **7 node chính**, các sếp cần cấu hình **cẩn thận** như sau:

##### **A. Cấu Hình Gmail OAuth 2.0**
- **Node:** `Gmail Trigger` và `Business`, `Meetings`, `Cold Emails`
- **Hành động:**
  1. Trên n8n, đi đến **Credentials** → **Add Credential** → **Gmail OAuth 2.0**.
  2. Đăng nhập tài khoản Gmail và **cho phép quyền truy cập**.
  3. Lưu credential với tên **`gmailOAuth2`**.

##### **B. Cấu Hình OpenAI API Key**
- **Node:** `OpenAI Chat Model` (gpt-4.1-mini)
- **Hành động:**
  1. Trên [OpenAI Platform](https://platform.openai.com/settings/organization/api-keys), tạo **API Key mới**.
  2. Trên n8n, đi đến **Credentials** → **Add Credential** → **OpenAI API**.
  3. Dán **API Key** vào và lưu với tên **`openAiApi`**.

##### **C. Cấu Hình Node `Text Classifier`**
- **Node:** `Text Classifier` (sử dụng mô hình GPT-4 Mini)
- **Hành động:**
  - **Không cần cấu hình thêm** (n8n tự động sử dụng `openAiApi` đã thiết lập).
  - **Lưu ý:** Nếu muốn thay đổi mô hình, các sếp có thể chỉnh `model` trong **keyParameters** (ví dụ: `gpt-4-1106-preview`).

##### **D. Cấu Hình Nhãn Email (Labels)**
- **Node:** `Business`, `Meetings`, `Cold Emails`
- **Hành động:**
  1. Trên Gmail, tạo **nhãn mới** với tên tương ứng:
     - `Business` (để email quan trọng).
     - `Meetings` (để email về cuộc họp).
     - `Cold Emails` (để email lạnh, có thể xóa sau).
  2. Trong node `Cold Emails`, các sếp có thể **thay đổi hành động** thành `markAsRead` (để giữ email nhưng đánh dấu đã đọc) thay vì `delete`.

##### **E. Test Run & Kích Hoạt**
1. **Test Run** với một email mẫu:
   - Chọn **Run Workflow** và chọn một email trong Gmail.
   - Kiểm tra kết quả phân loại (n8n sẽ nhãn hóa email).
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, chuyển **Active** sang **ON**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**TIẾP CẬN HƠN**]
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi email mới được phân loại.
   - Ví dụ: *"Email mới được phân loại là 'Business' – Kiểm tra ngay!"*

2. **Lưu Log Phân Loại**
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử phân loại.
   - Giúp các sếp **theo dõi hiệu suất** của AI.

3. **Tự Động Xóa Email Lạnh**
   - Thay vì chỉ đánh dấu `delete`, các sếp có thể **xóa sau 7 ngày** bằng cách thêm node **Google Calendar** để lập lịch xóa.

4. **Cải Thiện Mô Hình AI**
   - Nếu độ chính xác không cao, các sếp có thể **tùy chỉnh prompt** trong node `Text Classifier` để mô tả rõ ràng hơn các danh mục.
   - Ví dụ:
     ```json
     "prompt": "Phân loại email này vào danh mục sau:
     - Business: Email liên quan đến công việc, hợp đồng, yêu cầu.
     - Meetings: Email về cuộc họp, lịch trình.
     - Cold Emails: Email từ người lạ, quảng cáo, không liên quan."
     ```

5. **Sử Dụng Workflow cho Nhiều Tài Khoản Gmail**
   - Nếu các sếp quản lý nhiều tài khoản, có thể **tạo credential Gmail mới** và chia sẻ workflow.
   - Sử dụng node **Switch** để chọn tài khoản phù hợp.
:::

---
### 📌 **Kết Luận: Đừng Bị "Inbox Clutter" Lại Đêm Nay!**
Workflow này **giải phóng các sếp khỏi công việc lặp lại** và giúp họ **tập trung vào công việc quan trọng**. Với **GPT-4 Mini**, độ chính xác cao và **tự động hóa hoàn toàn**, các sếp sẽ **không bao giờ phải lo lắng về email rối tung** nữa.

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình Gmail + OpenAI.
3. **Test Run** và **bật Active** để bắt đầu tự động hóa!

**🚀 CÓ THỂ THỬ NGHIÊM TỪ HÔM NAY!** 🚀

---
:::note[**LƯU Ý CUỐI CUNG**]
- Workflow **không hỗ trợ Gmail Business** (chỉ cá nhân).
- Nếu gặp lỗi, kiểm tra **API Key OpenAI** và **quyền OAuth 2.0** của Gmail.
- Để **cải thiện hiệu suất**, các sếp có thể **tăng giới hạn API** của OpenAI.
:::

---
**Bạn có câu hỏi về workflow?** Để lại comment bên dưới hoặc liên hệ với tác giả [Ilyass Kanissi](https://n8n.io/workflows/7599) để hỗ trợ! 💬