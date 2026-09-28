---
title: "🚀 Tự động hóa bản tin công nghệ hàng ngày với Google News và Llama AI trong n8n"
description: "Xây dựng hệ thống tự động cào tin tức công nghệ từ Google News, sử dụng Llama AI tóm tắt xu hướng và gửi báo cáo qua email mỗi ngày."
slug: "tu-dong-hoa-ban-tin-cong-nghe-google-news-llama-ai"
tags: [n8n, automation, ai-agent, ollama, llama, google-news]
keywords: [n8n workflow, tự động hóa bản tin, AI tóm tắt tin tức, Llama AI, Google News scraper, n8n email]
---

# 🚀 Tự động hóa bản tin công nghệ hàng ngày với Google News và Llama AI

Các sếp có thấy mệt mỏi khi mỗi sáng phải tốn hàng giờ đồng hồ lướt web, đọc hàng chục trang báo công nghệ để cập nhật xu hướng mới nhất? Việc tổng hợp thông tin thủ công không chỉ ngốn thời gian mà còn dễ bỏ sót các tin tức quan trọng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ xịn sò được thiết kế bởi **Oneclick AI Squad**. Hệ thống này sẽ tự động hóa 100% quy trình: cào tin tức công nghệ từ Google News, dùng **Llama AI** để phân tích, tóm tắt các xu hướng nổi bật và gửi thẳng bản tin gọn gàng vào hộp thư đến của các sếp mỗi sáng. Không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Tự động hóa hoàn toàn quy trình điểm tin mỗi sáng lúc 8:00 AM mà không cần can thiệp thủ công.
- **Nắm bắt xu hướng nhanh chóng:** AI (Llama 3.2) lọc bỏ thông tin nhiễu, cô đọng các tin tức công nghệ nóng hổi nhất thành một bản tóm tắt súc tích.
- **Cá nhân hóa báo cáo:** Nhận trực tiếp báo cáo phân tích chuyên sâu qua Email cá nhân hoặc doanh nghiệp dưới định dạng đẹp mắt.
- **Vận hành anng toàn:** Tích hợp cơ chế kiểm tra dữ liệu và gửi thông báo lỗi (`Send Error Alert`) nếu có sự cố xảy ra trong quá trình cào tin.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Hệ thống n8n** (Self-hosted hoặc n8n Cloud).
2. **Ollama** đã được cài đặt và cấu hình mô hình `llama3.2-16000:latest` (hoặc kết nối qua API endpoint tương thích).
3. **Tài khoản SMTP** (Gmail, SendGrid, Resend, v.v.) để gửi email thông báo và báo cáo lỗi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình. Workflow này bao gồm 9 nodes chính được liên kết chặt chẽ với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp nhớ cấu hình kỹ các node sau:

- **Schedule Daily Tech News Trigger**: Node này mặc định đặt lịch chạy hàng ngày. Các sếp có thể chỉnh lại múi giờ hoặc giờ chạy (ví dụ: 8:00 AM mỗi sáng) cho phù hợp với thói quen đọc tin.
- **Fetch Google Tech News (`httpRequest`)**: Kiểm tra URL Google News mục công nghệ (ví dụ: Google News India - Tech Category hoặc tuỳ chỉnh theo khu vực các sếp muốn theo dõi).
- **Extract Tech News Articles (`html`)**: Cấu hình các thông số trích xuất (`extractHtmlContent`) để lấy chính xác tiêu đề, nguồn tin và thời gian đăng bài từ mã HTML trả về.
- **AI Tech News Analyzer (`agent`) & LLM - Tech News Model (`lmChatOllama`)**: 
  - Kết nối thông tin xác thực `ollamaApi` để liên kết với Ollama local hoặc Cloud của các sếp.
  - Đảm bảo tên model được điền chính xác là `llama3.2-16000:latest` (hoặc model tương đương mà sếp đang host).
- **Check if News Found (`if`)**: Node điều kiện kiểm tra xem có bài báo nào được trích xuất thành công hay không. Nếu không, hệ thống sẽ chuyển hướng để chạy node báo lỗi.
- **Send Tech News Email & Send Error Alert (`emailSend`)**: Cấu hình thông tin xác thực SMTP (`smtp`) và điền địa chỉ email nhận báo cáo của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** trên từng node để kiểm tra luồng dữ liệu mẫu chạy qua ổn định.
- Sau khi test thành công không báo lỗi, hãy bật nút **Active** ở góc trên bên phải để n8n tự động chạy ngầm 24/7 cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống thông minh và tiện ích hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng sau:
1. **Đa kênh thông báo:** Thay vì chỉ nhận qua Email, hãy thêm node **Telegram** hoặc **Slack** để bắn tin nhắn tóm tắt vào nhóm chat của công ty ngay lập tức.
2. **Lưu trữ lịch sử:** Thêm node **Google Sheets** hoặc **Notion** để lưu lại toàn bộ các bản tóm tắt tin tức theo ngày, tạo thành một cơ sở dữ liệu tri thức công nghệ riêng cho team.
3. **Phân loại nâng cao:** Prompting cho Llama AI phân loại tin tức theo chủ đề cụ thể (AI, Startup, Cybersecurity, Hardware) để dễ dàng tra cứu theo nhu cầu cá nhân.

### 📌 Kết luận
Với workflow **Daily Tech News Digest from Google News Summarized with Llama AI**, việc cập nhật tin tức công nghệ chưa bao giờ dễ dàng và tự động đến thế. Hãy cài đặt ngay hôm nay để tiết kiệm hàng giờ đồng hồ mỗi tuần và luôn đi đầu trong kỷ nguyên số hóa!