---
title: "🚀 Tự Động Theo Dõi Lợi Nhuận Agency Đa Nền Tảng với n8n & Google Gemini"
description: "Workflow n8n giúp agency gom dữ liệu từ Facebook Ads, Google Ads, Shopify, Stripe và Clockify, tính toán lợi nhuận và dùng AI phân tích gửi báo cáo tự động lên Slack."
slug: "tu-dong-theo-doi-loi-nhuan-agency-facebook-shopify-stripe-clockify-gemini"
tags: [n8n, automation, ai-summarization, crm, facebook-ads, shopify, slack]
keywords: [n8n workflow, theo dõi lợi nhuận agency, tự động hóa quảng cáo shopify stripe, n8n google gemini, phân tích tài chính agency]
---

# 🚀 Tự Động Theo Dõi Lợi Nhuận Agency Đa Nền Tảng với n8n & Google Gemini

Các sếp chạy agency chắc chắn luôn đau đầu với việc tổng hợp dữ liệu tài chính rải rác ở khắp mọi nơi: tiền chạy quảng cáo nằm ở Facebook và Google, doanh thu về qua Shopify và Stripe, còn thời gian làm việc của team lại nằm ở Clockify. Việc ngồi làm báo cáo thủ công mỗi tuần vừa tốn thời gian, vừa dễ sai sót, lại không kịp thời phát hiện client nào đang lỗ.

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó. Hệ thống sẽ tự động hóa 100% quy trình: kéo dữ liệu từ 5 nền tảng lớn, gom nhóm và tính toán các chỉ số sống còn (ROAS, CAC, biên lợi nhuận, chi phí nhân sự...), nhờ AI (**Google Gemini**) viết bản tóm tắt chiến lược, lưu lịch sử vào **Google Sheets** và bắn thẳng cảnh báo thông minh lên **Slack**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chạy định kỳ hàng tuần nhờ `Schedule Trigger`, không cần đụng tay vào bảng tính Excel.
- **Bức tranh tài chính minh bạch:** Gom toàn bộ chi phí (Ads, lương nhân sự tính qua Clockify, chi phí vận hành) và doanh thu theo từng khách hàng.
- **Cảnh báo thông minh bằng AI:** Google Gemini tự động phân tích và đánh giá sức khỏe tài chính của từng client, chỉ ra những khách hàng đang kéo lùi lợi nhuận agency.
- **Lưu trữ & Báo cáo tức thì:** Dữ liệu lịch sử tự động lưu vào Google Sheets, đồng thời gửi bản tin điều hành (Executive Summary) gọn gàng lên Slack của team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API credentials sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Facebook Graph API Credentials** (Để lấy dữ liệu ad spend).
- **Google Ads OAuth2 API** (Để lấy chi phí chiến dịch Google Ads).
- **Shopify API / Access Token** (Để kéo dữ liệu đơn hàng và doanh thu).
- **Stripe API Keys** (Để kiểm tra số dư và giao dịch).
- **Clockify API Key** (Để tracking thời gian làm việc của team theo từng client).
- **Google Sheets Credentials** (Tài khoản Google OAuth2 để ghi dữ liệu).
- **Slack Bot Token** (Đã được cấp quyền post bài vào kênh mong muốn).
- **Google Gemini (Palm) API Key** (Dùng cho AI Agent phân tích số liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from File** và chọn file JSON vừa tải.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 17 nodes được thiết kế rất thông minh, trong đó có các nodes cốt lõi sau các sếp cần chú ý cấu hình:

- **Các node Mock Set (`Facebook ads1`, `Google ads1`, `Shopify1`, `Stripe1`, `Clockify1`):** 
  :::note[Lưu ý quan trọng]
  Workflow cung cấp sẵn các node Set chứa dữ liệu mẫu để test. Khi đưa vào chạy thật (Go live), các sếp nhớ **xóa các node Set này** và kết nối trực tiếp các node API thật (`Facebook Graph API`, `Get a campaign`, `Get many orders`, `Get a balance`, `Get a time entry`) vào node `Merge1`.
  :::
- **Node `Code in JavaScript`:** Đây là "trái tim" tính toán của workflow. Các sếp hãy mở node này và cập nhật lại đối tượng `CONFIG` (bao gồm: tỷ lệ chi phí chung overhead, chi phí phần mềm, và ngưỡng biên lợi nhuận tối thiểu) cho phù hợp với mô hình thực tế của agency mình.
- **Node `Append row in sheet1` (`Google Sheets`):** Chọn đúng file Google Sheets và Sheet Name dùng để lưu lịch sử báo cáo hàng tuần. Đảm bảo các tiêu đề cột khớp với dữ liệu trả về từ code node.
- **Node `Send a message` (`Slack`):** Chọn Credentials Slack và điền ID kênh Slack (Channel ID) nhận báo cáo. *Đảm bảo Slack Bot đã được mời (invite) vào kênh đó trước.*
- **Node `Google Gemini Chat Model1` & `AI Profit Analyzer1` (`Agent`):** Kết nối Google Gemini API. Các sếp có thể tinh chỉnh lại System Prompt của AI nếu định nghĩa về "hiệu suất tài chính tốt" của agency các sếp có thay đổi.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Execute Workflow**) với một lần fetch dữ liệu mẫu để kiểm tra xem luồng dữ liệu qua các node Merge và Code có mượt mà không, AI có trả về kết quả đúng ý không và dữ liệu đã vào Google Sheets chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch hẹn của `Schedule Trigger1`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo:** Ngoài Slack, các sếp có thể nhân bản nhánh thông báo để bắn thêm một bản tóm tắt qua Telegram Bot cá nhân của Giám đốc tài chính (CFO).
- **Tạo bảng Dashboard trên Looker Studio:** Kết nối Google Sheets do workflow này tạo ra với Google Looker Studio để vẽ biểu đồ trực quan theo dõi biên lợi nhuận theo thời gian thực.
- **Cảnh báo tự động khách hàng lỗ:** Bổ sung điều kiện (If Node) sau đoạn code tính toán, nếu biên lợi nhuận của client nào âm trong 2 tuần liên tiếp, tự động tạo ticket trên Trello/Asana hoặc gửi cảnh báo khẩn cấp cho Account Manager.

### 📌 Kết luận
Việc quản lý tài chính agency sẽ không còn là cơn ác mộng tổng hợp dữ liệu thủ công nữa. Chỉ với một workflow n8n hoàn chỉnh kết hợp sức mạnh phân tích của Google Gemini, các sếp đã có trong tay một hệ thống "CFO ảo" hoạt động 24/7, giúp tối ưu hóa lợi nhuận và ra quyết định kinh doanh sắc bén hơn bao giờ hết. Chúc các sếp cài đặt thành công!