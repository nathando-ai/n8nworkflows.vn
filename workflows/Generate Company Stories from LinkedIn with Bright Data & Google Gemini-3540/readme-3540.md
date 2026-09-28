---
title: "🚀 Tự động tạo câu chuyện doanh nghiệp từ LinkedIn bằng Bright Data & Google Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu công ty từ LinkedIn thông qua Bright Data và sử dụng AI Google Gemini để trích xuất thông tin, viết câu chuyện thương hiệu."
slug: "tu-dong-tao-cau-chuyen-doanh-nghiep-linkedin-bright-data-google-gemini"
tags: [n8n, automation, bright-data, google-gemini, ai, sales, marketing]
keywords: [n8n workflow, bright data linkedin, google gemini ai, tu dong hoa marketing, cào dữ liệu linkedin]
---

# 🚀 Tự động tạo câu chuyện doanh nghiệp từ LinkedIn bằng Bright Data & Google Gemini

Việc nghiên cứu đối thủ, khách hàng tiềm năng hoặc đối tác bằng cách đọc từng trang LinkedIn thủ công tốn rất nhiều thời gian của các đội ngũ Sales và Marketing. Việc này không chỉ nhàm chán mà còn khó tổng hợp thông tin một cách mạch lạc. 

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: cào dữ liệu từ LinkedIn bằng **Bright Data API**, sau đó tận dụng sức mạnh AI của **Google Gemini** để phân tích, trích xuất và biến dữ liệu thô thành những câu chuyện doanh nghiệp hoặc bản tóm tắt cực kỳ chuyên nghiệp mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công tra cứu và tổng hợp thông tin công ty trên LinkedIn nữa.
- **AI thông minh:** Sử dụng Google Gemini để trích xuất dữ liệu có cấu trúc và viết tóm tắt/câu chuyện doanh nghiệp mượt mà.
- **Tự động hóa toàn trình:** Từ khâu gọi API cào dữ liệu, kiểm tra trạng thái, tải về đến xử lý qua AI và gửi thông báo qua Webhook.
- **Linh hoạt tích hợp:** Dễ dàng mở rộng để gửi kết quả về Slack, Telegram hoặc Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data**: Để lấy API Key thực hiện cào dữ liệu LinkedIn (`Perform LinkedIn Web Request`, `Check on the errors`, `Set Snapshot Id`, `Check Snapshot Status`, `Download Snapshot`).
- **Google Gemini API Key**: Cấu hình cho các node LangChain (`Google Gemini Chat Model` và `Google Gemini Chat Model1`).
- **Webhook Endpoint (Tùy chọn)**: Nếu muốn nhận thông báo qua webhook (`Webhook Notifier for Data Extractor`, `Webhook Notifier for Summary Generator`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Sao chép mã nguồn JSON của workflow hoặc tải file JSON về máy.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl + V` để dán trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình kỹ các node quan trọng sau đây để workflow chạy trơn tru:
- **Set LinkedIn URL (`Set LinkedIn URL`)**: Điền đường dẫn trang công ty trên LinkedIn mà các sếp muốn phân tích.
- **Bright Data HTTP Request Nodes (`Perform LinkedIn Web Request`, `Check Snapshot Status`, `Download Snapshot`)**: Điền thông tin xác thực (`httpHeaderAuth`) bằng API token của Bright Data để hệ thống có quyền cào dữ liệu.
- **Google Gemini Chat Models (`Google Gemini Chat Model`, `Google Gemini Chat Model1`)**: Thêm credentials Google Gemini (`googlePalmApi`) và chọn model phù hợp (như *Google Gemini Flash*).
- **Webhook Notifiers (`Webhook Notifier for Data Extractor`, `Webhook Notifier for Summary Generator`)**: Trỏ URL Webhook về nơi các sếp muốn nhận kết quả (ví dụ: Discord, Slack, hoặc hệ thống CRM nội bộ).

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** (`When clicking ‘Test workflow’`) để chạy thử nghiệm với dữ liệu mẫu và kiểm tra kết quả trả về ở từng node.
- Nếu mọi thứ hoạt động chính xác, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Google Sheets**: Thay thế hoặc bổ sung node Webhook bằng node Google Sheets để lưu trữ toàn bộ các câu chuyện doanh nghiệp được tạo tự động vào một bảng tính theo dõi khách hàng.
- **Gửi thông báo qua Telegram/Slack**: Đẩy trực tiếp bản tóm tắt câu chuyện công ty lên group chat nội bộ của team Sales ngay khi quá trình xử lý hoàn tất.
- **Xử lý hàng loạt (Batch Processing)**: Kết hợp thêm một danh sách công ty từ tệp CSV hoặc Google Sheets để workflow tự động cào và viết câu chuyện cho hàng loạt doanh nghiệp cùng lúc.

### 📌 Kết luận
Workflow tích hợp giữa Bright Data và Google Gemini này là vũ khí cực mạnh giúp tự động hóa quá trình nghiên cứu thị trường, làm giàu dữ liệu khách hàng (Data Enrichment) cho đội ngũ Sales và Marketing. Hãy thiết lập ngay hôm nay để tối ưu hóa năng suất cho doanh nghiệp các sếp nhé!