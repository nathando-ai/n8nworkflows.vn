---
title: "⚽ Tự Động Gửi Cảnh Báo Bàn Thắng Bóng Đá Chống Spoiler Với n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp lấy dữ liệu trận đấu trực tiếp từ API-Football, khớp với độ trễ của các dịch vụ streaming và gửi email qua Gmail mà không lo bị lộ kết quả trước."
slug: "tu-dong-gui-canh-bao-ban-thang-bong-da-chong-spoiler-n8n"
tags: [n8n, automation, no-code, api-football, google-sheets, gmail]
keywords: [n8n workflow, api-football, chống spoiler bóng đá, tự động hóa thông báo bóng đá, n8n google sheets gmail]
---

# ⚽ Tự Động Gửi Cảnh Báo Bàn Thắng Bóng Đá Chống Spoiler Với n8n

Các sếp có bao giờ rơi vào cảnh đang xem bóng đá qua các ứng dụng streaming trực tuyến (như K+, FPT Play, TV360, v.v.) bị trễ từ 30 đến 90 giây so với thực tế, để rồi điện thoại thông báo "VÀOOO!" trước khi mắt kịp chứng kiến bóng lăn vào lưới chưa? Cảm giác đó thực sự rất "tụt mood"!

Giải pháp cho các sếp đây: Workflow n8n siêu việt mang tên **"Delay football goal alerts with API-Football, Google Sheets and Gmail"** do tác giả Mychel Garzon thiết kế sẽ giúp tự động hóa 100% việc bắt nhịp trận đấu, tính toán độ trễ chính xác của stream và gửi thông báo qua Gmail đúng khoảnh khắc hình ảnh hiển thị trên màn hình của các sếp. Không còn nỗi sợ bị "spoiler" nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [An tâm chạy ngầm với VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chống Spoiler hoàn hảo:** Trì hoãn thông báo đúng bằng số giây độ trễ của dịch vụ streaming (30s - 90s).
- **Tối ưu hóa tài nguyên API:** Chỉ gọi API-Football trong khoảng thời gian diễn ra trận đấu (±2 tiếng từ giờ bóng lăn), tiết kiệm 80-90% giới hạn gọi API miễn phí.
- **Tự động hóa thông minh:** Tự động tắt trạng thái theo dõi (Active) khi trận đấu kết thúc (FT, AET, PEN...) để tránh lãng phí lượt gọi trong những ngày không có trận.
- **Cá nhân hóa cao:** Quản lý danh sách người dùng, đội bóng yêu thích và thời gian delay ngay trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc Cloud).
- **Tài khoản Google:** Để kết nối Google Sheets (lưu cấu hình, lịch sử trận đấu) và Gmail (gửi thông báo).
- **API Key API-Football:** Đăng ký tài khoản miễn phí tại [API-Football](https://www.api-football.com/) (gói miễn phí cung cấp 100 request/ngày).
- **Team ID:** ID của đội bóng các sếp muốn theo dõi (lấy từ API-Football).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template (ID: 15675), sau đó copy toàn bộ nội dung JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thành phần sau để hệ thống chạy mượt mà:

- **Google Sheets Nodes (`Load User Preferences`, `Update Notified Goals Log`, `Disable Active Status`):** 
  - Tạo một Google Sheet mới với 8 cột bắt buộc: `User Email`, `Team ID`, `Active`, `Delay Seconds`, `Streaming Service`, `Match Datetime`, `Last Notified Goals`, `Last Notification`.
  - Kết nối `Google Sheets OAuth2 API` credentials.
  - Thay thế `YOUR_SPREADSHEET_ID` bằng ID Google Sheet thực tế của các sếp trong cả 3 node này.
- **HTTP Request Node (`API-Football: Get Live Match`):**
  - Thêm thông tin xác thực `HTTP Header Auth` với API Key được cấp từ API-Football.
- **Gmail Node (`Gmail: Send Goal Alert`):**
  - Kết nối tài khoản `Gmail OAuth2` để cho phép workflow gửi email cảnh báo.
- **Schedule Trigger Node (`Schedule: Every 10 Minutes`):**
  - Mặc định chạy kiểm tra mỗi 10 phút. Node `Setup Validation` và `Check Match Timing Window` sẽ tự động xử lý logic thời gian xem có cần gọi API hay không.

#### 3. Kích hoạt ⚡️
- Điền dữ liệu thử nghiệm vào Google Sheet với cột `Match Datetime` theo định dạng ISO (ví dụ: `2025-06-01T20:00:00Z`) và cột `Active` để là `Yes`.
- Bấm **Execute Workflow** để test thủ công trong khung giờ trận đấu.
- Khi mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** góc trên cùng bên phải.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Gmail, các sếp có thể nhân bản nhánh thông báo sang node **Telegram** hoặc **Slack** để nhận cảnh báo ngay trên điện thoại cho nhanh.
- **Mở rộng nhiều đội bóng:** Thiết kế thêm các hàng trong Google Sheet để theo dõi đồng thời nhiều đội bóng yêu thích trong cùng một mùa giải.
- **Lưu trữ lịch sử:** Tận dụng dữ liệu từ Google Sheets để thống kê lại số lượng bàn thắng đội nhà ghi được qua từng trận.

### 📌 Kết luận
Với workflow n8n này, các sếp không còn phải lo lắng về việc lướt mạng xã hội thấy kết quả trước khi kịp nhìn thấy pha lập công của thần tượng trên TV. Hãy triển khai ngay hôm nay để tận hưởng trọn vẹn từng cảm xúc thăng hoa trên sân cỏ!