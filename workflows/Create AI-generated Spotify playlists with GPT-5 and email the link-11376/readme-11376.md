---
title: "🎵 Tự Động Tạo Playlist Spotify AI Chuyên Nghiệp Với GPT-5 & Gửi Link Email (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo playlist Spotify cá nhân hóa dựa trên sự kiện, khách mời và sở thích, sau đó gửi link trực tiếp qua email chỉ trong vài giây. Giảm thời gian thủ công từ 30 phút xuống 0!"
slug: "tay-dong-tao-playlist-spotify-ai-gpt-5-email"
tags: [n8n, automation, no-code, spotify-api, openai, email-automation, ai-playlist]
keywords: [tự động hóa playlist spotify, tạo playlist spotify bằng ai, gpt-5 spotify, tự động hóa email spotify, workflow n8n spotify, api spotify tự động]
---

# 🎵 **Tự Động Tạo Playlist Spotify AI Chuyên Nghiệp Với GPT-5 & Gửi Link Email (Không Cần Code)**

## **🔥 Nỗi Đau Của Các Sếp Khi Tạo Playlist Spotify Thường Xuyên**
Mỗi khi chuẩn bị cho một sự kiện (đám cưới, sinh nhật, hội nghị), các sếp phải:
- **Tốn thời gian** tìm kiếm và chọn nhạc phù hợp (thường mất 30-60 phút).
- **Không đảm bảo tính cá nhân hóa** vì dựa vào cảm nhận chủ quan.
- **Quên gửi link** cho khách mời hoặc đồng nghiệp sau khi hoàn thành.
- **Không thể tự động hóa** do thiếu kiến thức về API hoặc code.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-5** để tạo playlist chuyên nghiệp từ mô tả sự kiện, sau đó tự động tạo trên Spotify và gửi link qua email **một cách hoàn toàn tự động**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** từ 30 phút xuống **0 giây** – chỉ cần nhập mô tả sự kiện.
✅ **Playlist cá nhân hóa** dựa trên sự kiện, khách mời và sở thích (do AI phân tích).
✅ **Tự động gửi link** qua email cho khách mời hoặc đồng nghiệp.
✅ **Hoạt động liên tục** 24/7, không cần can thiệp thủ công.
✅ **Không cần code** – chỉ cần cấu hình API và email.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Spotify Developer** và **OAuth2 Credentials** (Client ID & Secret).
2. **API Key của OpenAI** (để sử dụng GPT-5).
3. **Dịch vụ SMTP** (hoặc tài khoản Gmail/Outlook) để gửi email tự động.
4. **n8n Self-hosted** (không dùng phiên bản miễn phí để tránh giới hạn).

**Chi tiết cấu hình chi tiết ở phần sau!**
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11376) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.
- Workflow sẽ tự động xuất hiện trên canvas.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **14 node** quan trọng, các sếp cần cấu hình như sau:

#### **A. Cấu Hình API & Credentials**
1. **Spotify OAuth2 Credentials** (để kết nối với Spotify API):
   - Tạo tài khoản tại [Spotify Developer Dashboard](https://developer.spotify.com/dashboard).
   - Nhập **Client ID** và **Client Secret** vào n8n dưới **Credentials** → **Add Credential** → **Spotify OAuth2**.
   - **Quá trình authorize**:
     - Sau khi tạo credential, nhấn **"Authorize"** trong n8n → Đăng nhập Spotify → Chọn quyền cần thiết (thường là `user-library-modify`, `playlist-modify-public`).

2. **OpenAI API Key** (để sử dụng GPT-5):
   - Tạo API Key tại [OpenAI Platform](https://platform.openai.com/settings/organization/api-keys).
   - Trong n8n, thêm **OpenAI API** credential và dán key vào.

3. **SMTP Email Service** (hoặc Gmail/Outlook):
   - **Cách 1 (SMTP):**
     - Nếu dùng SMTP (Gmail, SendGrid, etc.), thêm credential mới trong n8n với:
       - **Host**: `smtp.gmail.com` (hoặc host của dịch vụ SMTP).
       - **Port**: `587` (hoặc `465`).
       - **Username & Password**: Tài khoản email và mật khẩu (hoặc app password nếu dùng Gmail).
       - **Sender Email**: Email bạn muốn hiển thị khi gửi.
   - **Cách 2 (Gmail/Outlook Node):**
     - Thay thế node `emailSend` bằng node **Gmail** hoặc **Outlook** và cấu hình tương tự.

#### **B. Cấu Hình Node Quan Trọng**
| **Node** | **Lưu Ý Cần Chỉnh** |
|----------|----------------------|
| **On form submission** | Cấu hình form với các trường: `event_name`, `guests`, `mood`, `special_requests` (ví dụ). |
| **OpenAI Chat Model1** | Đảm bảo **model** được chọn là `gpt-5` (hoặc model mới nhất của OpenAI). |
| **AI Agent** | Kiểm tra **prompt** đã được cấu hình để AI tạo playlist phù hợp với mô tả. |
| **Search Spotify for Song** | Đảm bảo **credentials** là `spotifyOAuth2Api` và **query** được truyền từ AI. |
| **Create Spotify Playlist** | Nhập **name** và **description** từ dữ liệu form (ví dụ: `Playlist cho Đám Cưới của [Tên Khách Hàng]`). |
| **Send email** | Kiểm tra **to**, **subject**, và **body** email (có link playlist). |

#### **C. Test Run & Kích Hoạt**
1. **Test với dữ liệu mẫu**:
   - Nhập vào form (ví dụ: `Đám cưới, 50 khách, nhạc pop hiện đại, không có nhạc rock`).
   - Chạy workflow và kiểm tra:
     - AI có tạo playlist hợp lý không?
     - Spotify có tạo playlist và thêm nhạc không?
     - Email có gửi link thành công không?
2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** trên workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi playlist cho nhiều người**:
   - Sử dụng node **Merge** để kết hợp nhiều email từ form (ví dụ: `email_guest1`, `email_guest2`).
   - Thêm node **Loop** để gửi email cho từng khách mời.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử playlist đã tạo (tên sự kiện, ngày tạo, link).

3. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi playlist hoàn thành.

4. **Cập nhật playlist định kỳ**:
   - Sử dụng **n8n Scheduler** để tự động thêm nhạc mới vào playlist sau một thời gian.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tạo playlist thủ công, đồng thời **tăng trải nghiệm khách hàng** với nhạc cá nhân hóa. **Chỉ cần nhập mô tả sự kiện, AI và Spotify sẽ làm tất cả!**

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
2. **Cấu hình API và email** theo hướng dẫn trên.
3. **Import workflow** và test với dữ liệu mẫu.
4. **Bật Active** và chia sẻ với đồng nghiệp!

**🚀 Cần hỗ trợ thêm?**
- Liên hệ tác giả: [ufuk@neorebels.com](mailto:ufuk@neorebels.com)
- Theo dõi trên [LinkedIn](https://www.linkedin.com/in/ufuk-oeren/)

---
**Chúc các sếp thành công với playlist Spotify AI hoàn toàn tự động!** 🎶🤖