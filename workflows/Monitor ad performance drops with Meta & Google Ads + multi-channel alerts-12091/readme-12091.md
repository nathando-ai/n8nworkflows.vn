---
title: "🚀 Tự động cảnh báo sụt giảm hiệu suất quảng cáo Meta & Google Ads với n8n"
description: "Giám sát hiệu suất Google Ads và Meta Ads tự động mỗi ngày, phát hiện sớm sụt giảm CTR/ROAS và gửi cảnh báo tức thì qua Slack, Gmail, WhatsApp."
slug: "tu-dong-canh-bao-hieu-suat-quang-cao-meta-google-ads"
tags: [n8n, automation, marketing, google-ads, meta-ads, slack, ai]
keywords: [n8n workflow, tự động hóa quảng cáo, monitor ad performance, google ads automation, meta ads alert]
---

# 🚀 Tự động cảnh báo sụt giảm hiệu suất quảng cáo Meta & Google Ads với n8n

Các sếp chạy quảng cáo chắc chắn đã từng trải qua cảnh tài khoản bị lỗi, chiến dịch "chết" ngầm hoặc chi phí tăng vọt mà không ra đơn, đến cuối tháng nhìn lại báo cáo thì ngân sách đã bay màu? Việc kiểm tra thủ công hàng chục chiến dịch trên cả Meta Ads và Google Ads mỗi ngày cực kỳ tốn thời gian và rất dễ bỏ sót.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình giám sát, phát hiện sụt giảm hiệu suất (CTR, ROAS, chi phí...) và bắn cảnh báo đa kênh (Slack, Gmail, WhatsApp) ngay lập tức, đồng thời lưu log chi tiết vào Google Sheets. Không cần code, không sợ đốt tiền oan!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tự động quét dữ liệu quảng cáo mỗi ngày mà không cần mở Ads Manager thủ công.
- **Phát hiện sớm rủi ro:** Nhận cảnh báo ngay khi chiến dịch có dấu hiệu tụt ROAS, tụt CTR hoặc tiêu tiền mà không ra chuyển đổi.
- **Đa kênh thông báo:** Team Marketing nhận tin tức thì qua Slack, Email (Gmail) hoặc WhatsApp.
- **Lưu trữ minh bạch:** Tự động lưu lịch sử cảnh báo và trạng thái chiến dịch vào Google Sheets để tiện phân tích và review.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản và quyền truy cập API của **Meta Ads** (Access Token, Ad Account ID).
- Tài khoản **Google Ads** (Developer Token, Client ID, Client Secret).
- Tài khoản **Slack** (để gửi thông báo channel/group).
- Tài khoản **Gmail** hoặc cấu hình SMTP để gửi email.
- Tài khoản **WhatsApp Business API** (hoặc nhà cung cấp API WhatsApp tương thích).
- **Google Sheets** (file mẫu để lưu log).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (Link: [Monitor ad performance drops](https://n8n.io/workflows/12091)) hoặc copy trực tiếp đoạn JSON dán vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Daily Ad Check2 & Daily Ad Check3 (`scheduleTrigger`):** Cấu hình thời gian chạy định kỳ mỗi ngày (ví dụ: 8h sáng hàng ngày để quét dữ liệu của ngày hôm trước).
- **Fetch Meta Ads Data (`httpRequest`):** Điền Endpoint API của Meta Marketing API cùng với Access Token hợp lệ để kéo dữ liệu chiến dịch (impressions, clicks, spend, conversion values).
- **Get many campaigns (`googleAds`):** Kết nối tài khoản Google Ads của các sếp và chọn Customer ID cần giám sát.
- **Set Benchmarks & Set Benchmarks4 (`set`):** Thiết lập các ngưỡng tiêu chuẩn (benchmark) cho CTR, ROAS hoặc chi phí tối đa.
- **Detect Performance Drop & Code in JavaScript (`code`):** Viết hoặc tinh chỉnh logic so sánh dữ liệu thực tế với benchmark, gắn nhãn trạng thái (Performance Status) và lý do tụt giảm (Drop Reason).
- **Send a message (`slack`), Send a message4 (`gmail`), Send message1 (`whatsApp`):** Cấu hình credentials tương ứng và chọn channel/người nhận cảnh báo.
- **your-google-sheets-name (`googleSheets`):** Liên kết tới file Google Sheets của các sếp và chọn operation `appendOrUpdate` để lưu lại log cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu xem các node có hoạt động mượt mà không.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI phân tích nguyên nhân:** Kết nối thêm node OpenAI/Claude để AI đọc chỉ số tụt giảm và tự động đưa ra gợi ý tối ưu chiến dịch (ví dụ: đổi tệp target, làm mới creative...).
- **Thêm nút Pause Campaign:** Tích hợp thêm bước gọi API tạm dừng chiến dịch ngay lập tức nếu chỉ số tụt quá ngưỡng nguy hiểm để tránh thất thoát ngân sách lớn.
- **Báo cáo tuần tổng hợp:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp toàn bộ log từ Google Sheets và gửi báo cáo tóm tắt tình hình sức khỏe tài khoản quảng cáo cho sếp lớn.

### 📌 Kết luận
Việc tối ưu quảng cáo không còn là nỗi ám ảnh phải canh trực 24/7 nữa. Hãy cài đặt ngay workflow này để bảo vệ ngân sách marketing của doanh nghiệp và để công nghệ làm thay những việc lặp đi lặp lại!