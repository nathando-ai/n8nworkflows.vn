---
title: "🚀 Tự động phát hiện đánh giá sản phẩm giả mạo (Fake Review) bằng OpenAI, Airtable và Slack trên n8n"
description: "Xây dựng hệ thống kiểm duyệt đánh giá sản phẩm tự động 100% bằng AI, loại bỏ review ảo, lưu trữ qua Airtable và cảnh báo tức thì lên Slack."
slug: "tu-dong-phat-hien-danh-gia-gia-mao-openai-airtable-slack"
tags: [n8n, automation, no-code, openai, airtable, slack, ai-summarization]
keywords: [n8n workflow, phát hiện review giả, fake review detection, openai n8n, airtable slack automation]
---

# 🚀 Tự động phát hiện đánh giá sản phẩm giả mạo (Fake Review) bằng OpenAI, Airtable và Slack

Các doanh nghiệp thương mại điện tử và người làm Affiliate thường xuyên đau đầu với vấn nạn **đánh giá ảo (fake reviews)**. Việc kiểm tra thủ công hàng nghìn đánh giá mỗi ngày vừa tốn thời gian, vừa kém hiệu quả, dễ bỏ sót các đối thủ chơi xấu hoặc các bài đánh giá rác làm giảm uy tín sản phẩm.

Workflow n8n này chính là giải pháp tự động hóa toàn diện giúp các sếp giải quyết triệt để bài toán trên: tự động lấy dữ liệu đánh giá, băm mã định danh chống trùng lặp, dùng AI (OpenAI) chấm điểm mức độ nghi vấn, lưu trữ vào Airtable và cảnh báo ngay lập tức lên Slack khi phát hiện đánh giá đáng ngờ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Từ khâu nhận dữ liệu sản phẩm, cào review, phân tích đến cảnh báo mà không cần can thiệp thủ công.
- **AI thông minh:** Sử dụng OpenAI để phân tích ngữ cảnh, phát hiện tinh vi các bình luận spam, review ảo hoặc bot.
- **Chống trùng lặp thông minh:** Cơ chế tạo Hash riêng cho từng review giúp Airtable không bị lưu lặp dữ liệu cũ.
- **Cảnh báo tức thì:** Đẩy thẳng thông tin chi tiết (điểm rủi ro, lý do, thông tin reviewer) lên kênh Slack để đội ngũ kiểm duyệt xử lý ngay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản OpenAI API Key** (Sử dụng model `o4-mini` hoặc tương đương để phân tích).
- **Tài khoản Airtable** (Chuẩn bị sẵn Base và Bảng lưu trữ review).
- **Tài khoản Slack** (Tạo Webhook hoặc Bot để gửi tin nhắn cảnh báo vào kênh chỉ định).
- **API Cào Review sản phẩm** (Hoặc nguồn cấp dữ liệu qua Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy file JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng Import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Webhook – Receive Product Payload**: Cấu hình đường dẫn endpoint để nhận dữ liệu sản phẩm từ hệ thống của các sếp.
- **Fetch Product Reviews (HTTP Request)**: Trỏ tới API cào dữ liệu review sản phẩm của các sếp (đảm bảo cấu trúc JSON trả về tương thích với các bước xử lý tiếp theo).
- **List Bases / Search Records by Hash / Create Review Record / Update Review Record (Airtable)**: Kết nối tài khoản Airtable bằng `airtableTokenApi`, sau đó trỏ đến đúng Base và Table chứa dữ liệu review.
- **AI Fake Review Analysis (OpenAI)**: Kết nối credentials `openAiApi`, kiểm tra lại Prompt và chọn model (`o4-mini`) để AI đọc nội dung và trả về điểm rủi ro (Suspicious Score).
- **Check Suspicious Score Threshold (IF)**: Tùy chỉnh hạn mức điểm nghi vấn theo ý muốn (ví dụ: điểm trên 70/100 sẽ được coi là bất thường).
- **Send Moderation Alert (Slack)**: Kết nối credentials `slackApi` và chọn kênh Slack (Channel) sẽ nhận tin nhắn báo động.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với một vài dữ liệu mẫu qua node Webhook.
- Kiểm tra xem Airtable đã lưu đúng bản ghi và Slack đã nhận được thông báo chưa.
- Bật công tắc **Active** để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể gắn thêm node Telegram hoặc Email để nhận cảnh báo đa kênh.
- **Lưu Log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để thông báo về group riêng nếu API cào dữ liệu hoặc OpenAI gặp sự cố.
- **Tự động ẩn review trên Web:** Nếu điểm rủi ro quá cao, có thể gọi tiếp API của website thương mại điện tử để tự động ẩn review đó đi mà không cần chờ con người duyệt.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp tự động hóa khâu kiểm duyệt đánh giá, tiết kiệm hàng chục giờ làm việc thủ công và bảo vệ uy tín thương hiệu trước các làn sóng đánh giá ảo. Hãy import ngay vào n8n và tối ưu hóa hệ thống của các sếp ngay hôm nay!