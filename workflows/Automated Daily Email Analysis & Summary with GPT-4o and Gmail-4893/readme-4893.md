---
title: "🚀 Tự động gửi email hàng ngày với GPT‑4o-mini: Tóm tắt & Phân tích dữ liệu Gmail"
description: "Giải pháp tự động hóa 100% không code: lấy dữ liệu Gmail, tóm tắt bằng GPT‑4o-mini và gửi báo cáo qua email mỗi ngày."
slug: "tang-dong-gmail-gpt4o-mini"
tags: [n8n, automation, no-code, AI, email]
keywords: [n8n workflow, tự động hóa, GPT‑4o, email automation, summarization]
---

# 🚀 Tự động gửi email hàng ngày với GPT‑4o-mini

Bạn đang phải lướt qua hàng trăm email mỗi ngày để tìm ra những thông tin quan trọng? Việc đọc, tóm tắt và gửi lại báo cáo cho đồng nghiệp là một công việc tốn thời gian và dễ gây sai sót.  
Workflow **Automated Daily Email Analysis & Summary with GPT‑4o and Gmail** của Zach @Ajenta giúp bạn:

- Lấy toàn bộ email trong ngày qua Gmail API.
- Dùng GPT‑4o-mini để tóm tắt nội dung, phân loại và trích xuất dữ liệu quan trọng.
- Tự động gửi email báo cáo đã được định dạng đẹp, dễ đọc cho người nhận.

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ đọc email xuống vài phút tóm tắt.
- **Độ chính xác cao**: GPT‑4o-mini hiểu ngữ cảnh, giảm sai sót trong báo cáo.
- **Tự động 24/7**: Workflow chạy theo lịch, không cần can thiệp thủ công.
- **Cá nhân hóa**: Định dạng email, tiêu đề, nội dung linh hoạt theo nhu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** có bật API OAuth2.  
  - Cài đặt **Gmail OAuth2** trong n8n (Credentials → Gmail OAuth2).  
  - Cần quyền `https://www.googleapis.com/auth/gmail.readonly` và `https://www.googleapis.com/auth/gmail.send`.
- **API Key OpenAI** (được cung cấp khi đăng ký tài khoản OpenAI).  
  - Cài đặt **OpenAI API** trong n8n (Credentials → OpenAI API).  
- **VPS hoặc máy chủ n8n** (để chạy workflow 24/7).  
  - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
  - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ trang gốc: <https://n8n.io/workflows/4893>.  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** để hoàn tất.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình chính | Lưu ý |
|------|----------|-----------------|-------|
| 1 | **Schedule Trigger** | *Cron*: `0 8 * * *` (tùy chỉnh thời gian). | Đặt thời gian phù hợp với múi giờ công ty. |
| 2 | **Gmail** (getAll) | *Operation*: `getAll`, *Max Results*: `1000`, *Filter*: `after:{{now - 1d}}` | Đảm bảo lấy email trong ngày hôm qua. |
| 3 | **Date Transformer** (code) | `return [{ json: { today: new Date().toISOString().split('T')[0] } }];` | Trả về ngày hiện tại để dùng trong email. |
| 4 | **AI Agent** | *Prompt*: “Summarize the following emails and extract key points.” | Đặt prompt chi tiết, có thể thêm yêu cầu định dạng. |
| 5 | **OpenAI Chat Model** | *Model*: `gpt-4o-mini`, *Temperature*: `0.7` | Sử dụng credential OpenAI đã cài. |
| 6 | **Aggregate** | *Mode*: `Merge`, *Key*: `emailId` | Kết hợp các kết quả từ AI Agent. |
| 7 | **Email Cleanup** (code) | Loại bỏ attachments, chuyển nội dung sang plain text | Đảm bảo email không bị lỗi khi gửi. |
| 8 | **Format HTML** (code) | Tạo HTML thân thiện với email (table, tiêu đề). | Kiểm tra preview trước khi gửi. |
| 9 | **Send Message** (gmail) | *To*: `{{ $json["recipient"] }}`, *Subject*: `Daily Email Summary - {{ $json["today"] }}`, *Body*: `{{ $json["html"] }}` | Đặt credential Gmail OAuth2. |

> **Tip**: Nếu muốn gửi tới nhiều người, thay `{{ $json["recipient"] }}` bằng danh sách email ngăn cách bằng dấu phẩy.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute Workflow”). Kiểm tra output ở từng node.  
2. **Bật Active**: Sau khi xác nhận mọi thứ đúng, chuyển workflow sang trạng thái **Active**.  
3. **Theo dõi logs**: Kiểm tra “Execution” để đảm bảo không có lỗi. Nếu có lỗi, điều chỉnh node tương ứng.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram Notification**: Thêm node Slack hoặc Telegram để nhận thông báo khi workflow chạy thành công hoặc có lỗi.  
- **Lưu Log vào Google Sheet**: Dùng node Google Sheets để ghi lại lịch sử email đã gửi, giúp theo dõi lịch sử.  
- **Scheduled Reports**: Thêm node “Schedule Trigger” khác để gửi báo cáo vào cuối tuần hoặc khi có sự kiện đặc biệt.  
- **Custom Prompt**: Thay đổi prompt trong AI Agent để lấy dữ liệu cụ thể (ví dụ: “Extract action items” hoặc “Generate meeting agenda”).  

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian, giảm sai sót và tăng tính minh bạch trong quản lý email. Bạn chỉ cần cài đặt một vài credential và bật workflow, mọi thứ sẽ tự động chạy theo lịch.  
Hãy thử ngay và cảm nhận sự khác biệt!