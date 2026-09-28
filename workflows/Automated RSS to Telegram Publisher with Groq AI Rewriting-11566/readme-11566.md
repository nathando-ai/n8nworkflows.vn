---
title: "🤖 **Tự Động Hóa RSS → Telegram Với Groq AI: Tạo Nội Dung AI Chuyên Nghiệp Mỗi 30 Phút**"
description: "Workflow tự động hóa lấy tin tức từ RSS, tái tạo nội dung bằng AI Groq và gửi đến Telegram với định dạng chuyên nghiệp. Giúp các sếp tiết kiệm 10+ giờ/tháng viết bài, đồng thời đảm bảo nội dung luôn mới mẻ và cá nhân hóa."
slug: "tieu-dong-hoa-rss-telegram-groq-ai"
tags: [n8n, automation, no-code, telegram-bot, groq-ai, rss-feed, ai-content-rewriting]
keywords: [tự động hóa rss telegram, groq ai viết bài, tự động hóa nội dung social media, workflow n8n telegram, ai rewrite content, tự động hóa blog]
---

# 🚀 **Tự Động Hóa RSS → Telegram Với Groq AI: AI Viết Bài Cho Bạn Mỗi 30 Phút**

### **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
- **Thời gian vô cùng**: Phải thủ công theo dõi tin tức từ nhiều nguồn RSS (như TechCrunch, VnExpress, Forbes), sao chép và viết tóm tắt.
- **Nội dung lặp lại**: Các bài viết gốc từ RSS thường dài và không phù hợp để chia sẻ trên Telegram.
- **Không chuyên nghiệp**: Nội dung không được tối ưu hóa, thiếu cá nhân hóa, khiến người dùng mất quan tâm.
- **Không hoạt động liên tục**: Phải tự động hóa để cập nhật tin tức 24/7 mà không cần can thiệp thủ công.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tin tức mới** từ RSS (TechCrunch, VnExpress, Forbes, ...).
✅ **Tái tạo nội dung** bằng AI Groq (miễn phí) để ngắn gọn, chuyên nghiệp và hấp dẫn.
✅ **Gửi đến Telegram** mỗi 30 phút, giúp bạn **tiết kiệm 10+ giờ/tháng** và **luôn có nội dung mới**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Không cần viết tóm tắt thủ công, AI làm tất cả.
- **Nội dung chuyên nghiệp**: Groq AI tái tạo bài viết ngắn gọn, đọc dễ dàng và hấp dẫn.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi 30 phút, không cần can thiệp.
- **Cá nhân hóa**: Bạn có thể chỉnh sửa prompt AI để phù hợp với phong cách riêng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để chạy 24/7 ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Hai bảng dữ liệu n8n**:
   - **`rss_list`** (cột `rss` chứa URL RSS cần theo dõi).
   - **`post_links`** (cột `link` lưu trữ các bài viết đã được xử lý để tránh lặp lại).

3. **Groq API Key**:
   - Đăng ký miễn phí tại [Groq API](https://console.groq.com/) và thêm vào n8n dưới **Credentials → groqApi**.

4. **Telegram Bot Token & User ID**:
   - Tạo bot Telegram tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Lấy **User ID** của mình bằng cách gửi tin nhắn cho bot và kiểm tra URL (vd: `https://t.me/YOURBOTNAME?start=ID`).
   - Thêm vào n8n dưới **Credentials → telegramApi**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11566](https://n8n.io/workflows/11566) hoặc copy JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 node**, nhưng các node quan trọng nhất cần cấu hình kỹ:

##### **A. Cấu Hình Bảng Dữ liệu n8n**
- **`rss_list`** (danh sách RSS cần theo dõi):
  - Cột `rss` phải chứa URL RSS (vd: `https://feeds.feedburner.com/TechCrunch`).
  - **Lưu ý**: Nếu bảng chưa có, tạo bảng mới trong n8n với cột `rss` (kiểu `string`).

- **`post_links`** (lưu trữ link đã xử lý):
  - Cột `link` lưu trữ URL bài viết đã được gửi để tránh lặp lại.
  - **Lưu ý**: Nếu bảng chưa có, tạo bảng mới với cột `link` (kiểu `string`).

##### **B. Cấu Hình Groq AI**
- Node **`Groq Chat Model`**:
  - **Model**: Đặt là `groq/compound-mini` (miễn phí).
  - **Prompt**: Workflow tự động sử dụng prompt mặc định của tác giả (tái tạo nội dung ngắn gọn). Nếu muốn thay đổi, chỉnh sửa ở node **`Rewrite Post`** (type: `agent`).

##### **C. Cấu Hình Telegram**
- Node **`Send post to user`**:
  - **Chat ID**: Điền **User ID** của bạn (lấy từ bước trên).
  - **Message**: Workflow tự động gửi nội dung tái tạo từ Groq.

##### **D. Cấu Hình Schedule**
- Node **`Every 30 minutes`**:
  - Đảm bảo **Active** và không cần chỉnh sửa gì.

##### **E. Cấu Hình Tránh Lặp Lại**
- Node **`If link not in table`** (type: `dataTable`):
  - **Operation**: Đặt là `rowNotExists` (kiểm tra link có tồn tại trong `post_links` không).
  - **Table**: Chọn `post_links` và cột `link`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra:
     - RSS được lấy đúng không?
     - AI tái tạo nội dung có hợp lý không?
     - Telegram có nhận được tin nhắn không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động mỗi 30 phút.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM NÀY ĐỂ TỐT HƠN**]
1. **Thêm nhiều RSS nguồn**:
   - Thêm URL RSS mới vào bảng `rss_list` để workflow theo dõi nhiều nguồn hơn.

2. **Tùy chỉnh prompt AI**:
   - Mở node **`Rewrite Post`** (type: `agent`) và chỉnh sửa **Prompt** để AI viết theo phong cách riêng (vd: "Viết tóm tắt ngắn gọn, phong cách chuyên nghiệp, không quá 200 từ").

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **`telegram`** để gửi tin nhắn thông báo khi có bài viết mới (vd: "📢 Tin tức mới từ TechCrunch đã được gửi!").

4. **Lưu log hoạt động**:
   - Thêm node **`stickyNote`** sau node **`Send post to user`** để ghi lại lịch sử gửi tin nhắn.

5. **Kết hợp với Slack**:
   - Thay vì chỉ Telegram, bạn có thể thêm node **`slack`** để gửi tin tức đến Slack cùng lúc.

---

### 📌 **Kết Luận**
Workflow **Automated RSS to Telegram Publisher with Groq AI** là giải pháp **tự động hóa hoàn toàn** để các sếp:
✔ **Tiết kiệm thời gian** viết tóm tắt tin tức.
✔ **Nội dung chuyên nghiệp** nhờ AI Groq tái tạo.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Cài n8n Self-hosted** trên VPS (để chạy ổn định).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và xem AI làm việc cho bạn!

👉 [**Tải workflow nguyên bản**](https://n8n.io/workflows/11566) và bắt đầu tự động hóa ngay! 🚀