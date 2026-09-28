---
title: "🚀 Tự động tổng hợp lịch họp Outlook hàng ngày và gửi email tóm tắt"
description: "Workflow n8n lấy các sự kiện Outlook trong ngày, tạo bản tóm tắt HTML và gửi qua email, giúp các sếp tiết kiệm thời gian và không bỏ lỡ cuộc họp."
slug: "tu-dong-tong-hop-lich-hop-outlook-hang-ngay"
tags: [n8n, automation, no-code, outlook, email, schedule]
keywords: [n8n workflow, tự động hóa, Outlook, email digest, lịch họp]
---

# 🚀 Tự động tổng hợp lịch họp Outlook hàng ngày và gửi email tóm tắt

Bạn có bao giờ phải mở Outlook, lướt qua hàng chục cuộc họp, rồi mới kịp ghi chú lại?  
Việc này không chỉ tốn thời gian mà còn dễ gây nhầm lẫn, đặc biệt khi lịch thay đổi liên tục.  

**Automated Daily Outlook Calendar Meeting Digest** là giải pháp 100 % không cần code, tự động:

1. Lấy toàn bộ sự kiện Outlook trong ngày.  
2. Tạo bản tóm tắt dạng HTML đẹp mắt.  
3. Gửi ngay qua email cho bạn và đội ngũ.  

Kết quả: các sếp luôn nắm bắt lịch họp, không còn “bắt trễ” hay “quên lịch”.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không cần mở Outlook, chỉ nhận email tóm tắt.  
- **Độ chính xác 100 %**: Dữ liệu lấy trực tiếp từ Outlook API.  
- **Cá nhân hoá**: Nội dung email có thể tùy chỉnh theo nhu cầu.  
- **Hoạt động liên tục**: Tự động chạy mỗi ngày mà không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Microsoft Outlook** có quyền truy cập API (OAuth2).  
- **Credential “microsoftOutlookOAuth2Api”** được tạo trong n8n.  
- **SMTP server** (hoặc dịch vụ email) để gửi email, kèm credential “smtp”.  
- **Địa chỉ email người gửi** và **địa chỉ email người nhận** (có thể là danh sách).  
- **Quyền truy cập internet** cho n8n để gọi Outlook API và gửi email.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file workflow (hoặc copy/paste JSON vào ô).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hướng dẫn cấu hình |
|------|-------------------|
| **Schedule Trigger** | - Mở node, vào tab **Settings** → **Cron**.<br>- Đặt **Time** theo ghi chú “## Update Time” (ví dụ: `08:00` mỗi ngày). |
| **Microsoft Outlook** | - Chọn **Credentials → microsoftOutlookOAuth2Api**.<br>- Đảm bảo **Resource** là `event` (đã được preset). |
| **Code** (đầu tiên) | - Không cần thay đổi nếu bạn chỉ muốn lọc sự kiện trong ngày. Nếu muốn thay đổi khoảng thời gian, chỉnh `startDate` và `endDate` trong script. |
| **Edit Fields (Set)** | - Đặt các trường cần hiển thị trong email (ví dụ: `subject`, `start`, `end`, `location`). |
| **Generate HTML** (Code) | - Script tạo HTML cho danh sách sự kiện. Bạn có thể tùy chỉnh giao diện (thêm logo, màu sắc). |
| **Send Email** | - Chọn **Credentials → smtp**.<br>- Điền **From Email** (địa chỉ người gửi) và **To Email** (địa chỉ người nhận).<br>- Chủ đề email có thể để: `📅 Tóm tắt lịch họp ngày {{ $today }}`.<br>- Trong phần **HTML**, chọn **Expression** và nhập `{{$node["Generate HTML"].json["html"]}}`. |
| **Sticky Note** | - Chỉ là ghi chú hướng dẫn, không cần cấu hình. |

> **Lưu ý:** Đảm bảo mọi node đều **Enabled** và **Active**. Nếu có lỗi “Authentication”, kiểm tra lại OAuth token và quyền API.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra dữ liệu mẫu.  
2. Kiểm tra email nhận được, xác nhận nội dung HTML hiển thị đúng.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy mỗi ngày theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi bản tóm tắt ngay vào kênh nhóm.  
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** để ghi lại số lượng cuộc họp, thời gian bắt đầu/kết thúc, giúp phân tích hiệu suất làm việc.  
- **Báo cáo tuần**: Tạo một workflow phụ, chạy vào cuối tuần, tổng hợp các email ngày trong tuần và gửi báo cáo tổng hợp.  
- **Định dạng thời gian**: Sử dụng **Moment.js** trong node **Code** để chuyển múi giờ hoặc định dạng hiển thị (VD: `DD/MM/YYYY HH:mm`).  

### 📌 Kết luận
Với **Automated Daily Outlook Calendar Meeting Digest**, các sếp sẽ không còn lo lắng về việc bỏ lỡ cuộc họp quan trọng. Chỉ cần một lần thiết lập, workflow sẽ tự động thu thập, định dạng và gửi bản tóm tắt mỗi ngày, giúp tăng năng suất và giảm thiểu sai sót. Hãy triển khai ngay hôm nay để trải nghiệm tự động hoá thực sự!