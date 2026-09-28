---
title: "🚀 Tự động tạo bài viết LinkedIn chuyên nghiệp từ Wikipedia bằng AI và Ideogram"
description: "Hướng dẫn sử dụng workflow n8n tự động hóa quy trình viết bài LinkedIn: cào dữ liệu Wikipedia, tóm tắt bằng GPT-4, tạo ảnh minh họa bằng Ideogram và tự động đăng bài."
slug: "tu-dong-tao-bai-viet-linkedin-tu-wikipedia-ai-ideogram"
tags: [n8n, automation, no-code, linkedin, ai-agent, openai, ideogram]
keywords: [n8n workflow, tu dong hoa linkedin, wikipedia scraper, ai agent gpt-4, ideogram image generation]
keywords: [n8n workflow, tự động hóa linkedin, viết bài linkedin tự động, ai agent, gpt-4, ideogram]
---

# 🚀 Tự động tạo bài viết LinkedIn chuyên nghiệp từ Wikipedia bằng AI và Ideogram

Các sếp có tốn hàng giờ mỗi tuần để nghiên cứu chủ đề, viết nội dung thu hút và thiết kế hình ảnh bắt mắt cho LinkedIn không? Việc duy trì nội dung đều đặn trên mạng xã hội chuyên nghiệp này thực sự là một "cực hình" nếu làm thủ công.

Workflow n8n này sẽ giải quyết triệt để bài toán đó cho các sếp. Chỉ cần nhập tên chủ đề hoặc bài viết từ Wikipedia qua một form đơn giản, hệ thống sẽ tự động cào dữ liệu, nhờ AI (GPT-4 / Claude) biên tập thành bài đăng LinkedIn chuẩn chỉnh dưới 2000 ký tự, tạo ảnh minh họa độc quyền qua Ideogram API và tự động xuất bản lên trang cá nhân/doanh nghiệp của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tra cứu, viết lách hay thiết kế đồ họa thủ công nữa.
- **Nội dung chất lượng cao:** Ứng dụng AI Agent thông minh tóm tắt kiến thức sâu sắc, đúng văn phong thu hút người đọc trên LinkedIn.
- **Hình ảnh độc quyền:** Tự động tạo ảnh trực quan thông qua Ideogram API dựa trực tiếp trên nội dung bài viết.
- **Vận hành khép kín:** Tự động hóa từ bước nhập liệu thông qua Form cho đến khi bài viết xuất hiện trên LinkedIn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản và API Key của **OpenAI** (hoặc Anthropic Claude).
- Tài khoản dịch vụ cào dữ liệu web (**Bright Data** API).
- Tài khoản tạo ảnh **Ideogram API**.
- Tài khoản **LinkedIn** và cấu hình LinkedIn OAuth2 API để đăng bài.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ thư viện n8n (Link gốc: [n8n.io/workflows/6433](https://n8n.io/workflows/6433)) và tiến hành Import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được chia thành các phân đoạn rõ rệt, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **📝 On form submission**: Node khởi đầu dạng Form, các sếp có thể tùy chỉnh giao diện nhập liệu tên bài viết/chủ đề từ Wikipedia mà mình muốn khai thác.
- **🌐 HTTP Request / 🌐 🌐 HTTP Request**: Kết nối tới dịch vụ **Bright Data** để cào dữ liệu bài viết Wikipedia dựa theo từ khóa do người dùng nhập. Cần cấu hình API Token chính xác ở đây.
- **Wait for status**, **Check Final Status**, **Wait (1 min)**, **Wikipedia Scrap Post**: Các node xử lý vòng lặp chờ đợi (polling) để đảm bảo Bright Data đã lấy dữ liệu xong xuôi trước khi chuyển sang bước tiếp theo.
- **AI Agent**, **OpenAI Chat Model**, **Anthropic Chat Model**: 
  - Node **OpenAI Chat Model** sử dụng model `gpt-4.1-mini` để đóng vai trò biên tập viên viết bài. Các sếp nhớ kết nối `openAiApi` credentials.
  - Node **Anthropic Chat Model** (`claude-sonnet-4-20250514`) hỗ trợ kiểm tra và sửa lỗi cấu trúc đầu ra nếu cần.
- **Structured Output Parser** & **Auto-fixing Output Parser**: Đảm bảo AI trả về kết quả đúng định dạng JSON chuẩn cấu trúc cho các bước tiếp theo.
- **Image Generate** & **HTTP Request1**: Gọi Ideogram API để tạo ảnh minh họa dựa trên nội dung tóm tắt, sau đó tải file ảnh về chuẩn bị cho bước đăng bài.
- **Create a post** & **LinkedIn URL**: Node đăng bài trực tiếp lên LinkedIn thông qua `linkedInOAuth2Api` và node Code (`LinkedIn URL`) giúp trích xuất link bài viết hoàn chỉnh sau khi đăng thành công.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách submit một chủ đề bất kỳ qua form để kiểm tra toàn bộ luồng dữ liệu từ cào web, AI viết bài, tạo ảnh đến đăng LinkedIn.
- Sau khi test thành công không báo lỗi, hãy bật **Active workflow** để đưa hệ thống vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước kiểm duyệt (Approval):** Thay vì đăng tự động ngay lập tức, các sếp có thể chèn thêm node gửi thông báo về Slack hoặc Telegram kèm nút bấm "Phê duyệt / Từ chối" trước khi gọi node đăng LinkedIn.
- **Lưu trữ lịch sử:** Thêm node Google Sheets hoặc Airtable để lưu lại tiêu đề, nội dung bài viết và link LinkedIn đã đăng nhằm phục vụ việc phân tích hiệu suất nội dung về sau.
- **Đa dạng hóa mạng xã hội:** Nhân bản nhánh cuối để tận dụng nội dung AI viết sẵn đăng đồng thời lên Facebook Page, Twitter/X hoặc X.

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung mạng xã hội chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, AI Agent và các công cụ hiện đại. Hãy cài đặt ngay workflow này để tối ưu hóa thời gian và bùng nổ tương tác trên LinkedIn của các sếp nhé!