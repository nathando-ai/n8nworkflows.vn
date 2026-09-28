---
title: "🚀 Tự động giám sát đánh giá thấp trên WooCommerce bằng n8n, Google Sheets, Slack và OpenAI"
description: "Hướng dẫn xây dựng workflow n8n tự động quét đánh giá WooCommerce định kỳ, lọc đánh giá 1-2 sao, dùng OpenAI viết nội dung cảnh báo thông minh và bắn thông báo tức thì lên Slack."
slug: "giam-sat-danh-gia-woocommerce-openai-slack-n8n"
tags: [n8n, automation, woocommerce, openai, slack, google-sheets, ai-summarization]
keywords: [n8n workflow, tự động hóa woocommerce, giám sát đánh giá khách hàng, openai n8n, slack alert, google sheets automation]
---

# 🚀 Tự động giám sát đánh giá thấp trên WooCommerce với OpenAI và Slack

Các sếp đang kinh doanh thương mại điện tử trên WooCommerce chắc chắn hiểu rằng: **Đánh giá 1 hoặc 2 sao từ khách hàng chính là "quả bom nổ chậm"** nếu không được xử lý kịp thời. Việc kiểm tra thủ công danh sách đánh giá mỗi ngày cực kỳ tốn thời gian và rất dễ bỏ sót những phản hồi tiêu cực, dẫn đến việc mất khách hàng vĩnh viễn.

Giải pháp là gì? Hãy để **n8n** tự động hóa toàn bộ quy trình này! Workflow này sẽ tự động quét các đánh giá mới từ WooCommerce, lọc ra những đánh giá thấp điểm, sử dụng **OpenAI** để phân tích và soạn tin nhắn cảnh báo chuyên nghiệp, sau đó bắn thẳng lên **Slack** đồng thời lưu trữ/cập nhật dữ liệu vào **Google Sheets** một cách mượt mà. Không cần code, hoạt động 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản ứng chớp nhoáng:** Phát hiện ngay lập tức đánh giá tiêu cực (1-2 sao) để đội ngũ chăm sóc khách hàng xử lý khủng hoảng truyền thông kịp thời.
- **AI thông minh hóa cảnh báo:** Sử dụng OpenAI để tóm tắt và tạo thông điệp cảnh báo súc tích, chuyên nghiệp thay vì chỉ gửi một đống dữ liệu khô khan lên Slack.
- **Chống trùng lặp thông minh:** Kiểm tra dữ liệu cũ trên Google Sheets trước khi gửi thông báo, tự động cập nhật nếu đánh giá có sự thay đổi.
- **Lưu trữ lịch sử minh bạch:** Mọi phản hồi của khách hàng đều được đồng bộ hóa vào Google Sheets để làm báo cáo định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
1. **n8n Instance** (Self-hosted hoặc n8n Cloud).
2. **WooCommerce Store** với quyền truy cập REST API (Consumer Key & Consumer Secret).
3. **Google Sheets** chứa sẵn một file template để lưu log review.
4. **OpenAI Account** (Lấy API Key từ platform.openai.com).
5. **Slack Workspace** và một Webhook/Bot Token để gửi tin nhắn cảnh báo vào kênh Support.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n, sau đó tại giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và credentials cho các node sau:

- **Trigger on schedule time**: Mặc định workflow được thiết lập chạy định kỳ mỗi 5 giờ để quét đánh giá mới. Các sếp có thể tùy chỉnh lại thời gian theo nhu cầu thực tế.
- **Fetch woocommerce reviews**: 
  - Cần cấu hình `Credentials` loại **HTTP Basic Auth** với Username là WooCommerce Consumer Key và Password là Consumer Secret.
  - Điền URL API của cửa hàng WooCommerce (ví dụ: `https://your-store.com/wp-json/wc/v3/reviews`).
- **Normalize review data** & **Process reviews one by one**: Các node trung gian giúp làm sạch dữ liệu và xử lý từng đánh giá riêng biệt (`Split in Batches`) nhằm tránh quá tải hệ thống.
- **Check review approval** & **Check low rating**: Các node điều kiện (`IF`) giúp lọc ra chỉ những đánh giá **đã được phê duyệt** (Approved) và **có điểm số thấp** (ví dụ: 1 hoặc 2 sao) mới đi tiếp vào luồng xử lý cảnh báo.
- **Find review in sheet**, **Log new review**, **Update existing review**: 
  - Cần kết nối `Google Sheets OAuth2 API`.
  - Chọn đúng File Google Sheet và Sheet Name đã chuẩn bị.
  - Node *Find review in sheet* sẽ tra cứu theo Review ID để kiểm tra xem đánh giá này đã tồn tại trên hệ thống hay chưa.
- **Is new review?**: Node `IF` phân loại: Nếu chưa có -> Coi là đánh giá mới (`Log new review`); Nếu đã có -> Cập nhật thông tin (`Update existing review`).
- **Genrate Alert message**: 
  - Kết nối `OpenAiApi`.
  - Thiết lập Prompt để AI viết một đoạn thông báo ngắn gọn, chuyên nghiệp, làm nổi bật tên sản phẩm, điểm số và nội dung phàn nàn của khách.
- **Send slack alert**: 
  - Kết nối `SlackApi`.
  - Chỉ định kênh (Channel) nhận thông báo trên Slack của công ty và truyền nội dung tin nhắn được tạo ra từ node OpenAI vào.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test Run) với một vài bản ghi mẫu, kiểm tra xem dữ liệu có được đẩy lên Google Sheets và Slack chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa quy trình chăm sóc khách hàng, các sếp có thể mở rộng workflow:
1. **Tích hợp thêm Email/Telegram:** Ngoài Slack, có thể gửi thêm email cảnh báo tự động cho Quản lý cửa hàng hoặc bắn tin nhắn qua Telegram Bot.
2. **Tự động tạo Ticket hỗ trợ:** Kết nối thêm với các hệ thống Helpdesk như Zendesk, Freshdesk hoặc Jira để tự động tạo ticket xử lý khiếu nại cho đội ngũ CSKH.
3. **Phân tích cảm xúc (Sentiment Analysis):** Mở rộng prompt của OpenAI để phân tích thêm mức độ tức giận của khách hàng, từ đó gắn nhãn mức độ ưu tiên (Khẩn cấp / Bình thường) trên Slack.

### 📌 Kết luận
Việc tự động hóa giám sát đánh giá WooCommerce bằng n8n, OpenAI và Slack không chỉ giúp doanh nghiệp tiết kiệm hàng giờ kiểm tra thủ công mỗi tuần mà còn đảm bảo không bỏ sót bất kỳ phản hồi tiêu cực nào của khách hàng. Hãy cài đặt ngay hôm nay để nâng cao chất lượng dịch vụ và bảo vệ uy tín thương hiệu của các sếp!