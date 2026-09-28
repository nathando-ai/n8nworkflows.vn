---
title: "🚀 Tự động tạo báo cáo sức khỏe doanh nghiệp hàng tuần với Claude AI và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu từ Google Sheets, nhờ Claude AI phân tích xu hướng và gửi báo cáo kinh doanh qua Gmail mỗi sáng thứ Hai."
slug: "tu-dong-tao-bao-cao-suc-khoe-doanh-nghiep-hang-tuan-claude-ai-google-sheets"
tags: [n8n, automation, ai-summarization, google-sheets, claude-ai, gmail]
keywords: [n8n workflow, bao cao kinh doanh tu dong, claude ai automation, google sheets n8n, tao bao cao hang tuan]
---

# 🚀 Tự động tạo báo cáo sức khỏe doanh nghiệp hàng tuần với Claude AI và Google Sheets

Các sếp có còn tốn thời gian vào những buổi sáng thứ Hai đầu tuần để ngồi tổng hợp số liệu, vẽ biểu đồ và viết báo cáo thủ công trên Google Sheets hay Excel không? Việc này không chỉ mất hàng giờ đồng hồ mà đôi khi còn khiến chúng ta bỏ lỡ các biến động quan trọng của doanh nghiệp.

Được thiết kế bởi chuyên gia tự động hóa B2B **Akshay Chug**, workflow n8n này sẽ giải quyết triệt để vấn đề trên. Hệ thống sẽ tự động đọc dữ liệu kinh doanh 7 ngày qua từ Google Sheets, yêu cầu **Claude AI** phân tích xu hướng, cảnh báo rủi ro, ghi nhận các điểm sáng (wins) và gửi một bản báo cáo bằng ngôn ngữ tự nhiên thẳng vào hộp thư của bạn trước khi buổi họp đầu tuần bắt đầu. Hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Loại bỏ hoàn toàn 2-3 tiếng đồng hồ tổng hợp số liệu mỗi sáng thứ Hai.
- **Phân tích sâu sắc bằng AI:** Claude AI giúp so sánh tuần này với tuần trước, phát hiện ngay các chỉ số bất thường (giảm doanh thu, rớt chuyển đổi...).
- **Gợi ý hành động thực tế:** AI không chỉ đưa ra con số khô khan mà còn đề xuất top 3 việc cần làm ngay trong tuần.
- **Lưu trữ lịch sử minh bạch:** Mọi báo cáo chạy tự động đều được log lại vào Google Sheets để tiện theo dõi theo thời gian.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
1. **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
2. **Google Account:** Truy cập vào Google Sheets và Gmail.
3. **Anthropic API Key:** Tài khoản tại [console.anthropic.com](https://console.anthropic.com) để sử dụng Claude AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau cần cấu hình:

- **Weekly Schedule Trigger:** Mặc định lịch chạy là vào 7:00 sáng mỗi thứ Hai hàng tuần. Các sếp có thể đổi lại múi giờ hoặc thời gian tùy theo lịch sinh hoạt của team.
- **Configure Report Settings (Code node):** Mở node này và cấu hình lại tên doanh nghiệp (`YOUR_BUSINESS_NAME`), email nhận báo cáo (`YOUR_REPORT_EMAIL`), và mô tả các chỉ số (`YOUR_METRICS_DESCRIPTION`) để Claude hiểu rõ ý nghĩa các cột dữ liệu trong sheet.
- **Fetch This Week Data & Fetch Last Week Data (Google Sheets nodes):** Kết nối tài khoản Google của bạn, chọn file Google Sheet chứa dữ liệu kinh doanh (mỗi dòng là một ngày, các cột là các chỉ số như Doanh thu, Leads, Cuộc gọi, Chuyển đổi...).
- **Claude Sonnet (lmChatAnthropic node):** Click vào node này, thêm Anthropic API Credential và dán API Key lấy từ Anthropic Console.
- **Send Weekly Report (Gmail node):** Kết nối tài khoản Gmail dùng để gửi báo cáo tự động đến đội ngũ.
- **Log Report Run (Google Sheets node):** Tạo một tab thứ hai trong Google Sheet của bạn tên là `Report Log` với các cột: `Date`, `Summary`, `Status` để ghi nhận nhật ký chạy báo cáo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử nghiệm dữ liệu lần đầu xem email có gửi về đúng định dạng không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh chat:** Ngoài Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bắn bản tóm tắt báo cáo thẳng vào group chat công ty.
- **Tối ưu chi phí AI:** Nếu dữ liệu của doanh nghiệp nhỏ và đơn giản, có thể đổi mô hình Claude Sonnet sang Claude Haiku trong sub-node để tiết kiệm token API.
- **Mở rộng nguồn dữ liệu:** Nối thêm các node kéo dữ liệu từ Stripe, Facebook Ads, hoặc HubSpot trước bước Format Data để có bức tranh kinh doanh toàn diện hơn.

### 📌 Kết luận
Việc tự động hóa báo cáo tuần không chỉ giúp tiết kiệm hàng tá thời gian mà còn giúp ban quản lý nắm bắt chính xác nhịp đập doanh nghiệp ngay từ đầu tuần mà không tốn một giọt mồ hôi làm báo cáo thủ công. Hãy cài đặt ngay workflow này và tận hưởng sức mạnh của AI trong quản trị!