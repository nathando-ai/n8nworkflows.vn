---
title: "🚀 Tự động Giám sát Uy tín Thương hiệu trên Reddit chống Khủng hoảng Truyền thông với n8n, Gemini & AI Agent"
description: "Hướng dẫn cài đặt workflow n8n tự động quét Reddit, sử dụng Gemini AI phân tích PR tiêu cực và lưu trữ báo cáo vào Google Sheets 24/7."
slug: "giam-sat-uy-tin-thuong-hieu-reddit-gemini-n8n"
tags: [n8n, automation, ai-agent, gemini, google-sheets, reddit, langChain]
keywords: [n8n workflow, giám sát thương hiệu, pr tiêu cực reddit, gemini ai, langhain n8n, tự động hóa marketing]
---

# 🚀 Tự động Giám sát Uy tín Thương hiệu trên Reddit chống Khủng hoảng Truyền thông với n8n, Gemini & AI Agent

Các sếp có bao giờ đau đầu khi một bài viết chê bai sản phẩm, dịch vụ mọc lên trên Reddit nhưng phát hiện quá muộn? Khủng hoảng truyền thông (Negative PR) trên mạng xã hội lớn như Reddit có thể lan rộng và thổi bay doanh thu chỉ trong vài giờ nếu đội ngũ của các sếp không xử lý kịp thời. Việc ngồi cào dữ liệu thủ công hay lướt Reddit cả ngày là bất khả thi.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ thay các sếp "canh gác" Reddit 24/7, ứng dụng sức mạnh của **Gemini AI (LangChain)** để đọc hiểu, phân tích sắc thái bài viết (sentiment), và tự động ghi nhận các thông tin tiêu cực vào **Google Sheets** để xử lý ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện khủng hoảng sớm:** Tự động quét các bài viết mới nhất trên Reddit theo lịch trình định sẵn mà không cần thao tác tay.
- **AI thông minh lọc nhiễu:** Sử dụng Gemini AI thông qua LangChain để đánh giá chính xác bài viết nào mang tính chất tiêu cực, bôi nhọ hay phàn nàn thật sự.
- **Báo cáo trực quan:** Tự động đồng bộ toàn bộ dữ liệu bài viết, mức độ tiêu cực và tóm tắt nội dung vào Google Sheets để team PR/Marketing xử lý.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên hệ thống n8n của các sếp, không bỏ lỡ bất kỳ khung giờ cao điểm nào.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Self-hosted hoặc n8n Cloud).
- **Google Cloud / Vertex AI Credentials:** Tài khoản kết nối với Google Vertex Chat Model để AI xử lý ngôn ngữ.
- **Google Sheets Account:** Tạo sẵn một bảng tính Google Sheets để lưu thông tin bài viết Reddit.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy mã JSON của workflow (hoặc tải file từ nguồn cấp) và paste trực tiếp vào giao diện n8n Editor của mình. Workflow này được thiết kế bởi tác giả *iamvaar* với tổng cộng 9 nodes kết hợp cực kỳ mượt mà.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Schedule Trigger1**: Cấu hình thời gian chạy tự động (Ví dụ: Chạy mỗi 1 tiếng hoặc 30 phút/lần để quét bài viết mới trên Reddit).
- **Look for Latest posts (HTTP Request Node)**: Thiết lập API hoặc URL endpoint để gọi dữ liệu bài viết mới nhất từ Reddit. Các sếp nhớ điền đúng từ khóa thương hiệu (Brand Keyword) cần theo dõi.
- **Extract Post Metadata1 (Set Node) & Seperate array into individual posts1 (Split Out Node)**: Dùng để lọc các trường dữ liệu quan trọng (Tiêu đề, Link, Tác giả, Thời gian) và tách từng bài viết riêng lẻ để AI xử lý mượt mà.
- **AI Agent & Google Vertex Chat Model**: Node trung tâm ứng dụng LangChain và Gemini (Google Vertex AI). Các sếp cần cấu hình Credential kết nối Google Cloud và viết Prompt yêu cầu AI nhận diện mức độ tiêu cực (Negative Score/Sentiment).
- **Structured Output Parser**: Đảm bảo AI trả về kết quả dưới định dạng cấu trúc chuẩn (JSON) để dễ dàng đẩy dữ liệu xuống bảng tính.
- **Append to Google Sheets**: Kết nối tài khoản Google của các sếp, chọn đúng file Sheet và mapping các trường dữ liệu từ AI trả về vào các cột tương ứng (Tiêu đề, Đường dẫn, Mức độ tiêu cực, Tóm tắt nội dung).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm (Test run) với một vài bài viết mẫu, kiểm tra xem dữ liệu đã đổ về Google Sheets chuẩn xác chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn nữa, các sếp có thể mở rộng thêm:
- **Tích hợp Telegram / Slack Node:** Gửi tin nhắn hú còi cảnh báo ngay lập tức vào group chat nội bộ của team khi phát hiện bài viết có mức độ tiêu cực cao (Negative > 8/10).
- **Lọc từ khóa thông minh (Code Node):** Tinh chỉnh thêm đoạn code JS để lọc bỏ các bài viết rác, quảng cáo không liên quan trước khi đẩy vào AI nhằm tiết kiệm token.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp số lượng phàn nàn trong tuần gửi vào email cho quản lý.

### 📌 Kết luận
Bảo vệ danh tiếng thương hiệu chưa bao giờ dễ dàng và tự động đến thế. Chỉ với vài phút cài đặt workflow n8n kết hợp cùng Gemini AI, các sếp đã có một "lính canh" mẫn cán trực chiến ngày đêm trên mạng xã hội. Lên đồ ngay thôi nào các sếp!