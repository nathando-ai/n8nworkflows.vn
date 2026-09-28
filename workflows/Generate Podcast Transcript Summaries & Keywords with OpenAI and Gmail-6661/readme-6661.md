---
title: "🎙️ Tự Động Tóm Tắt Transcript Podcast và Trích Xuất Từ Khóa với OpenAI & Gmail"
description: "Biến bản ghi chép podcast thô (transcript) thành bản tóm tắt sắc bén và bộ từ khóa chuẩn SEO chỉ trong vài giây, sau đó tự động gửi kết quả qua Gmail nhờ n8n."
slug: "tu-dong-tom-tat-podcast-transcript-openai-gmail"
tags: [n8n, automation, no-code, openai, gmail, content-creation, ai-summarization]
keywords: [n8n workflow, tóm tắt podcast, trích xuất từ khóa ai, openai gpt-3.5, tự động hóa gmail, content automation]
---

# 🎙️ Tự Động Tóm Tắt Transcript Podcast và Trích Xuất Từ Khóa với OpenAI & Gmail

Các sếp làm sáng tạo nội dung, làm podcast hay nghiên cứu thị trường chắc chắn đã từng "ngán ngẩm" cảnh phải ngồi đọc hàng ngàn từ trong bản transcript thô (raw transcript) để chắt lọc ý chính hay tìm kiếm từ khóa. Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ lỡ các ý tưởng đắt giá.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: nhận văn bản thô, dùng sức mạnh của AI (OpenAI) để phân tích, tóm tắt nội dung và trích xuất từ khóa cốt lõi, cuối cùng gom lại và gửi thẳng vào hộp thư Gmail của các sếp. Không một dòng code nào cần viết!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất 30-45 phút đọc và tổng hợp một tập podcast, AI xử lý xong trong vài giây.
- **Nội dung chuẩn xác, súc tích:** Bản tóm tắt nêu bật các ý chính, giúp các sếp nhanh chóng nắm bắt nội dung hoặc làm nguyên liệu viết bài blog, social media.
- **Tối ưu SEO tự động:** Trích xuất ngay lập tức các từ khóa quan trọng để làm thẻ tag, hashtag hoặc định hướng nội dung.
- **Nhận kết quả tận tay:** Gửi toàn bộ báo cáo gọn gàng trực tiếp qua Gmail cá nhân hoặc email công việc mà không cần mở công cụ phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để kết nối với mô hình AI xử lý ngôn ngữ.
- **Tài khoản Google (Gmail):** Để cấu hình node gửi email kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này (hoặc copy toàn bộ mã nguồn JSON) và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được thiết kế tinh gọn gồm 6 nodes. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Input Raw Transcript` (Set):** Nơi các sếp dán đoạn văn bản transcript thô của tập podcast vào đây để bắt đầu chạy thử.
- **Node `AI: Generate Summary` (OpenAI):** 
  - Chọn Credentials OpenAI của các sếp.
  - Model mặc định sử dụng `gpt-3.5-turbo` (tiết kiệm và cực kỳ nhanh). Các sếp có thể đổi sang `gpt-4o-mini` nếu muốn tối ưu hơn.
  - Viết sẵn System Prompt yêu cầu AI tóm tắt ngắn gọn các ý chính.
- **Node `AI: Extract Keywords` (OpenAI):** 
  - Tương tự node trên, chọn Credentials OpenAI.
  - Cấu hình prompt để yêu cầu AI liệt kê từ khóa nổi bật ngăn cách bởi dấu phẩy.
- **Node `Consolidate Output` (Set):** Node này giúp gộp kết quả từ bản tóm tắt và danh sách từ khóa thành một cấu trúc dữ liệu duy nhất, sạch sẽ trước khi chuyển sang bước gửi mail.
- **Node `Email Results` (Gmail):** 
  - Kết nối tài khoản Gmail cá nhân/doanh nghiệp.
  - Điền địa chỉ email nhận, tiêu đề thư động (lấy từ dữ liệu xử lý) và nội dung email hiển thị kết quả tóm tắt cùng từ khóa.

#### 3. Kích hoạt ⚡️
- Nhấn **Test Step** từng node hoặc **Execute Workflow** để kiểm tra luồng chạy với dữ liệu mẫu trong `Input Raw Transcript`.
- Kiểm tra hộp thư Gmail xem đã nhận được báo cáo chưa.
- Khi mọi thứ mượt mà, gạt công tắc sang **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Nâng cấp & Gợi ý mở rộng
Để workflow thông minh hơn nữa, các sếp có thể "độ" thêm vài tính năng:
- **Thay Manual Trigger bằng Webhook/Google Drive:** Thay vì dán thủ công, hãy tự động kích hoạt khi có file audio mới tải lên Google Drive hoặc khi có link YouTube Podcast mới.
- **Gửi về Telegram/Slack:** Thay vì chỉ gửi Gmail, bắn thông báo tóm tắt vào nhóm chat để team cùng nắm bắt nội dung.
- **Lưu trữ tự động:** Đẩy bản tóm tắt và từ khóa thẳng vào Google Sheets hoặc Notion để làm thư viện content dài hạn.

### 📌 Kết luận
Workflow "Generate Podcast Transcript Summaries & Keywords with OpenAI and Gmail" là một trợ thủ đắc lực giúp các nhà sáng tạo nội dung tối ưu hóa hiệu suất làm việc với AI. Hãy cài đặt ngay hôm nay để biến những tập podcast dài lê thê thành những ý tưởng nội dung sắc bén chỉ trong chớp mắt! Chúc các sếp thao tác thành công!