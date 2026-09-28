---
title: "🚀 Tự động phát hiện Video YouTube Viral bằng AI & Gửi báo cáo Email"
description: "Hướng dẫn cài đặt workflow n8n tự động quét từ khóa YouTube, tính toán điểm viral và sử dụng AI (OpenAI) để tổng hợp báo cáo gửi thẳng vào Gmail mỗi ngày."
slug: "tu-dong-phat-hien-video-youtube-viral-n8n-ai"
tags: [n8n, automation, youtube, ai-agent, openai, gmail]
keywords: [n8n workflow, youtube viral detector, ai summarization, tự động hóa youtube, openai gpt-4o-mini, youtube data api]
---

# 🚀 Tự động phát hiện Video YouTube Viral bằng AI & Báo cáo qua Email

Các sếp đang làm nội dung số, marketing hay nghiên cứu thị trường chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải cày cuốc hàng giờ trên YouTube để tìm kiếm các xu hướng, video đang nổi (viral) trong ngách của mình. Việc lọc thủ công vừa mất thời gian, vừa dễ bỏ lỡ các tín hiệu tăng trưởng sớm của đối thủ.

Giải pháp ở đây là gì? Hãy để tự động hóa lo! Bài viết này sẽ hướng dẫn các sếp triển khai một siêu workflow n8n được thiết kế bởi chuyên gia dữ liệu **gclbck**, giúp tự động quét, phân tích chỉ số bùng nổ, dùng AI (OpenAI) mổ xẻ nội dung và gửi báo cáo chi tiết thẳng vào Gmail của các sếp mỗi ngày. Hoàn toàn tự động 100% và không tốn một giọt mồ hôi thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt trend cực nhanh:** Tự động tìm kiếm các video phổ biến nhất theo từ khóa/ngách mong muốn trong khoảng thời gian tùy chỉnh.
- **Điểm số Viral thông minh:** Tính toán *"Algorithmic Lift Score"* để lọc ra những video có hiệu suất vượt trội so với kênh.
- **Phân tích chiều sâu từ AI:** AI Agent (GPT-4o-mini) tự động phân tích top 5 video tiềm năng nhất và đưa ra các insight đắt giá.
- **Báo cáo tự động tận nơi:** Nhận ngay báo cáo tổng hợp dạng Markdown cực kỳ trực quan qua Gmail theo lịch trình định sẵn (ví dụ: mỗi ngày 1 lần).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **YouTube Data API v3 Key:** Lấy từ Google Cloud Console để truy vấn dữ liệu video.
- **OpenAI API Key:** Để cung cấp năng lượng phân tích cho AI Agent (`gpt-4o-mini`).
- **Tài khoản Gmail:** Kết nối qua OAuth2 để gửi báo cáo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow từ nguồn gốc (`https://n8n.io/workflows/8368`), sau đó vào giao diện n8n Editor, chọn **Import from File** hoặc copy và paste trực tiếp JSON vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 22 nodes được sắp xếp logic. Các sếp cần cấu hình chính xác 3 điểm mấu chốt sau:

- **Node `Setup` (Cấu hình tìm kiếm):** 
  Double-click vào node này để điền các tham số quan trọng:
  - `query`: Từ khóa hoặc ngách các sếp muốn theo dõi (Ví dụ: `"AI"`, `"Marketing"`, `"Productivity"`).
  - `GoogleAPIkey`: Khóa API của YouTube Data API v3. *(Cách lấy: Vào Google Cloud Console -> Tạo project -> Bật "YouTube Data API v3" -> Tạo API Key trong mục Credentials).*
  - `daysback`: Số ngày tính ngược về quá khứ để quét video (Ví dụ: `3` nghĩa là quét video trong 3 ngày gần nhất).
  - `maxResult`: Số lượng video tối đa lấy về để phân tích (Khuyến nghị để dưới `50` để tránh vượt giới hạn Rate Limit).
  - `e-mail`: Địa chỉ nhận báo cáo.

- **Node `OpenAI Chat Model` (Kết nối AI):**
  - Click vào node, dưới phần **Credential**, chọn **Create New**.
  - Dán **OpenAI API Key** của các sếp vào để kết nối. *(Lưu ý: Template mặc định dùng model `gpt-4o-mini` vừa nhanh vừa tiết kiệm).*

- **Node `Send_Report` (Gửi Email qua Gmail):**
  - Click vào node, chọn **Credential** -> **Create New** để liên kết tài khoản Gmail của các sếp qua OAuth2.
  - Kiểm tra trường **Send To** và đảm bảo nó trỏ đúng đến email nhận báo cáo của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** ở node `When clicking ‘Test workflow’` để chạy thử nghiệm và kiểm tra xem email có được gửi về hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ chạy tự động theo lịch của `Schedule Trigger` (mặc định chạy 1 lần/ngày).

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài gửi Gmail, các sếp có thể gắn thêm node **Telegram** hoặc **Slack** để nhận cảnh báo ngay lập tức trên điện thoại khi có một video siêu viral xuất hiện.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** trước bước tổng hợp để lưu lại lịch sử các video viral theo tuần/tháng phục vụ cho việc nghiên cứu nội dung lâu dài.
- **Tùy biến Prompt AI:** Trong cấu hình của `AI Agent`, các sếp có thể tinh chỉnh câu lệnh (prompt) để AI tập trung phân tích sâu hơn về tiêu đề, thumbnail hoặc cách giữ chân người xem của đối thủ.

### 📌 Kết luận
Việc bắt trend YouTube chưa bao giờ trở nên nhàn hạ và chuyên nghiệp đến thế nhờ sức mạnh của n8n kết hợp với AI. Hãy thiết lập ngay workflow này để tối ưu hóa quy trình sáng tạo nội dung của các sếp ngay hôm nay! Chúc các sếp thao tác thành công!