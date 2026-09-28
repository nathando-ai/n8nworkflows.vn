---
title: "📧 Tự Động Hoàn Tất Gmail: Xóa Tất Cả Email Không Được Đánh Dấu (Ngoại Trừ Đã Đánh Sao) Mỗi Ngày"
description: "Workflow tự động hóa Gmail giúp các sếp xóa tất cả email không được đánh dấu sao từ Inbox vào mỗi buổi sáng, giữ lại chỉ những tin nhắn quan trọng. Tiết kiệm thời gian quản lý email hàng ngày và duy trì Inbox sạch sẽ 100%."
slug: "tự-dộng-hoàn-tất-gmail-xoa-email-không-danh-dau"
tags: [n8n, automation, gmail, email-management, no-code]
keywords: [tự động hóa gmail, xóa email tự động, lưu trữ email, quản lý inbox, workflow n8n gmail]
---

# 🚀 **Tự Động Hoàn Tất Gmail: Xóa Tất Cả Email Không Được Đánh Dấu (Ngoại Trừ Đã Đánh Sao) Mỗi Ngày**

### **Nỗi Đau Của Các Sếp Với Inbox Gmail**
Hàng ngày, các sếp phải mất **30-60 phút** để quét và xóa email không cần thiết từ Inbox. Nhưng với **n8n**, bạn có thể **tự động hóa toàn bộ quy trình** này chỉ trong vài phút! Workflow này sẽ:
- **Xóa tất cả email không được đánh dấu sao** vào mỗi buổi sáng (hoặc vào buổi chiều).
- **Giữ lại chỉ những tin nhắn quan trọng** (đã đánh sao) trong Inbox.
- **Giảm thiểu rác rưởi** và giúp bạn tập trung vào công việc thực sự.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 1-2 giờ/ngày** quản lý email thủ công.
- **Inbox luôn sạch sẽ**, chỉ giữ lại những tin nhắn quan trọng.
- **Hoạt động tự động**, không cần can thiệp của con người.
- **Không mất email quan trọng** vì chỉ xóa những tin nhắn không đánh dấu sao.
- **Không cần viết code**, chỉ cần copy/paste workflow và cấu hình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (nên là tài khoản chính của công ty hoặc cá nhân).
- **API Key OAuth2 cho Gmail** (cấu hình trong n8n).
- **Thời gian chạy**: Workflow sẽ hoạt động vào **một giờ cố định hàng ngày** (ví dụ: 8h sáng).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2146](https://n8n.io/workflows/2146) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **Import** → Dán hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Gmail OAuth2**
- Vào **Credentials** → Thêm **Gmail OAuth2**.
- Đăng nhập tài khoản Gmail cần tự động hóa.
- **Chọn quyền**:
  - `https://www.googleapis.com/auth/gmail.readonly` (đọc email).
  - `https://www.googleapis.com/auth/gmail.modify` (xóa email).
- **Xác thực** và lưu.

##### **B. Cấu Hình Lịch Trình Chạy (Schedule Trigger)**
- Node **"At midnight every work day"** (hoặc thời gian bạn muốn).
- **Chỉnh sửa lịch trình**:
  - Nếu muốn chạy vào **8h sáng**, thay đổi thành:
    ```json
    {
      "cron": "0 8 * * 1-5", // Chạy vào 8h sáng từ thứ 2 đến thứ 6
      "timeZone": "Asia/Ho_Chi_Minh" // Đặt múi giờ phù hợp
    }
    ```
- **Lưu lại**.

##### **C. Cấu Hình Lọc Email (Filter)**
- Node **"Keep only starred emails in inbox"** sẽ **lọc giữ lại chỉ email đã đánh sao**.
- **Không cần chỉnh sửa gì** vì logic đã được thiết kế sẵn.

##### **D. Kiểm Tra & Test**
- **Run workflow** với một email mẫu (đánh sao và không đánh sao).
- Kiểm tra:
  - Email **đã đánh sao** vẫn ở Inbox.
  - Email **không đánh sao** đã được chuyển sang **Archive**.

---

#### **3. Kích Hoạt ⚡️**
- Sau khi cấu hình xong, **bật nút Active** ở góc trên bên phải.
- **Chờ workflow chạy** vào thời gian đã đặt (ví dụ: 8h sáng).
- **Kiểm tra Inbox** để xác nhận email đã được xóa tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack/Telegram** để thông báo khi workflow chạy thành công/thất bại.
   - Ví dụ: *"Workflow xóa email tự động đã hoàn tất! Đã xóa [X] email không cần thiết."*

2. **Lưu Log Lịch Sử**
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại danh sách email đã xóa.
   - Giúp theo dõi và phục hồi nếu cần.

3. **Chỉnh Lịch Trình Chạy Theo Múi Giờ**
   - Nếu làm việc theo múi giờ khác (ví dụ: UTC+7), điều chỉnh **timeZone** trong Schedule Trigger.

4. **Tự Động Xóa Email Cũ Hơn 30 Ngày**
   - Thêm node **Filter** để lọc email cũ hơn 30 ngày và xóa chúng.

5. **Kết Hợp với Zapier/Make**
   - Nếu muốn thêm tính năng khác (ví dụ: chuyển email quan trọng sang Trello), có thể kết hợp với **Zapier** hoặc **Make**.

---

### 📌 **Kết Luận**
Workflow này giúp **giải phóng thời gian** của các sếp khỏi công việc lặp lại quản lý email. **Chỉ cần cấu hình 1 lần**, workflow sẽ hoạt động **mỗi ngày tự động**, giữ Inbox của bạn **sạch sẽ và chuyên nghiệp**.

**Hãy thử ngay và cảm nhận sự khác biệt!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/2146) và **cài đặt trên VPS** để chạy 24/7.

---
**Chia sẻ ý kiến của bạn về workflow này!** 🚀