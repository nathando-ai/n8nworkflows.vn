---
title: "🚀 Tự động hóa báo cáo doanh số hàng tuần với Google Sheets, Gemini AI và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp dữ liệu doanh số từ Google Sheets, phân tích bằng Google Gemini AI và gửi báo cáo HTML trực quan qua Gmail mỗi tuần."
slug: "tu-dong-hoa-bao-cao-doanh-so-hang-tuan-n8n-gemini-gmail"
tags: [n8n, automation, no-code, google-sheets, google-gemini, gmail]
keywords: [n8n workflow, tu dong hoa bao cao doanh so, google sheets gemini ai, automation gmail report]
---

# 🚀 Tự động hóa báo cáo doanh số hàng tuần với Google Sheets, Gemini AI và Gmail

Các sếp có đang mất hàng giờ mỗi tuần để copy/paste dữ liệu doanh số từ Google Sheets, loay hoay tính toán tăng trưởng tuần này so với tuần trước, rồi lại ngồi viết báo cáo gửi sếp lớn hoặc đội ngũ? Việc làm thủ công này không chỉ tẻ nhạt, dễ sai sót mà còn ngốn rất nhiều thời gian quý giá lẽ ra dành cho chiến lược kinh doanh.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa **100%** quy trình: Lấy dữ liệu, làm sạch, phân tích thông minh bằng AI, vẽ biểu đồ trực quan và gửi email báo cáo định kỳ mà không cần một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không còn phải cộng trừ số liệu hay viết báo cáo dài dòng mỗi tuần.
- **Phân tích thông minh bằng AI**: Google Gemini AI tự động tóm tắt các điểm nổi bật và xu hướng kinh doanh cốt lõi.
- **Biểu đồ trực quan sinh động**: Tự động sinh biểu đồ so sánh hiệu suất danh mục sản phẩm thông qua QuickChart.
- **Hoạt động tự động 24/7**: Lên lịch chạy tự động đúng giờ hẹn, báo cáo đẹp mắt gửi thẳng vào hộp thư Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets**: File chứa dữ liệu bán hàng (Sales Data) theo tuần.
- **Google Gemini API Key**: Để AI phân tích và viết tóm tắt kinh doanh.
- **Tài khoản Gmail**: Dùng để gửi email báo cáo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste cấu trúc JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 9 nodes chính hoạt động nhịp nhàng, các sếp cần cấu hình các điểm sau:
- **Schedule Trigger1**: Cài đặt mốc thời gian chạy định kỳ hàng tuần (ví dụ: Thứ Hai lúc 8:00 sáng).
- **Get row(s) in sheet1** (Google Sheets Node): Kết nối tài khoản Google của các sếp, chọn đúng file Google Sheet và Sheet chứa dữ liệu doanh số.
- **Message a model** (Google Gemini Node): Thêm credentials API Key của Google Gemini để AI bắt đầu "làm việc".
- **Format Email1** (Set Node): Tùy chỉnh tiêu đề email, tên người nhận hoặc style hiển thị HTML nếu muốn.
- **Send Email1** (Gmail Node): Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp để gửi email báo cáo đi.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử nghiệm với dữ liệu mẫu xem email gửi về có mượt mà không.
- Nếu mọi thứ hiển thị đẹp đẽ, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ gửi qua Gmail, các sếp có thể gắn thêm node Slack hoặc Telegram để bắn thông báo tóm tắt doanh số ngay lập tức vào group chat công ty.
- **Lưu lịch sử báo cáo**: Thêm một bước ghi lại kết quả phân tích của AI vào một sheet riêng biệt (`Weekly_Reports_Log`) để dễ dàng tra cứu lịch sử về sau.
- **Tùy biến Prompt AI**: Tinh chỉnh prompt trong node Gemini AI để đổi giọng văn báo cáo (chuyên nghiệp, hài hước, hoặc tập trung sâu vào các chỉ số KPI cụ thể).

### 📌 Kết luận
Tự động hóa báo cáo doanh số chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, Google Sheets và Gemini AI. Hãy áp dụng ngay hôm nay để giải phóng thời gian cho đội ngũ và tối ưu hóa vận hành doanh nghiệp các sếp nhé!