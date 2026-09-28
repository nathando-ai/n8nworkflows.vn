---
title: "🚀 Tự Động Hóa Tạo Ảnh 9:16 Cho Mạng Xã Hội Từ Nội Dung & Bộ Nhận Diện Thương Hiệu Với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình lấy nội dung từ Airtable, kết hợp OpenAI và Leonardo.ai để tạo bộ ảnh 9:16 chuẩn thương hiệu."
slug: "tu-dong-hoa-tao-anh-9-16-tu-noi-dung-va-thuong-hieu-n8n"
tags: [n8n, automation, ai, marketing, airtable, openai, leonardo-ai]
keywords: [n8n workflow, tao anh tu dong, leonardo ai n8n, airtable automation, ai marketing automation]
---

# 🚀 Tự Động Hóa Tạo Ảnh 9:16 Cho Mạng Xã Hội Từ Nội Dung & Bộ Nhận Diện Thương Hiệu

Việc sản xuất hình ảnh dọc tỷ lệ 9:16 (cho TikTok, Reels, YouTube Shorts) đồng nhất với bộ nhận diện thương hiệu (Brand Guidelines) thường tốn rất nhiều thời gian của các nhà sáng tạo nội dung và Marketer. Các sếp thường phải đọc nội dung bài viết, tóm tắt ý chính, nghĩ câu lệnh (prompt) tạo ảnh, rồi lọ mọ vào các công cụ AI generate từng cái một rồi tải về. Vừa tốn thời gian, vừa dễ lệch tông màu thương hiệu!

Workflow n8n được thiết kế bởi chuyên gia **Alex Kim** này chính là vị cứu tinh giúp tự động hóa 100% quy trình trên: Lấy nội dung từ Airtable, dùng OpenAI để chuẩn bị kịch bản/prompt, sau đó gọi API của Leonardo.ai để tạo hàng loạt ảnh 9:16 chuẩn sắc nét và tự động lưu ngược lại Airtable.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Biến văn bản (Blog, Content) thành hàng loạt hình ảnh 9:16 chất lượng cao chỉ với 1 cú click.
- **Đồng bộ thương hiệu**: Tự động áp dụng Brand Guidelines thông qua Airtable và OpenAI để hình ảnh luôn nhất quán.
- **Tích hợp AI mạnh mẽ**: Ứng dụng OpenAI (`Script Prep`, `Wikipedia`) kết hợp mô hình tạo ảnh đỉnh cao Leonardo.ai Phoenix 1.0.
- **Tiết kiệm 90% thời gian**: Không còn phải thủ công copy/paste prompt hay chờ đợi render từng tấm ảnh một.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
1. **n8n Instance**: Đã cài đặt sẵn (Khuyên dùng Self-hosted trên VPS).
2. **Airtable Account**: Tạo sẵn Base theo mẫu của tác giả để lưu trữ Content, Brand Guidelines và SEO Keywords.
3. **OpenAI API Key**: Dành cho các node xử lý ngôn ngữ (`Script Prep`).
4. **Leonardo.ai API Key**: Dành cho các HTTP Request nodes gọi model tạo ảnh Phoenix 1.0.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này hoặc tải file từ nguồn cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong các node:

- **Các node kết nối Airtable (`Get Brand Guidelines`, `Get SEO Keywords`, `Get Content`, `Add Asset Info`, `Add Asset Info1`)**:
  - Chọn `airtableTokenApi` credentials của sếp.
  - Trỏ đúng đến Base Airtable mẫu (tham khảo mẫu của tác giả: [Airtable Base Link](https://airtable.com/appRDq3E42JNtruIP/shrnc9EzlxpCq7Vxe)).
- **Node `Script Prep` (OpenAI)**:
  - Cấu hình `openAiApi` credentials.
  - Kiểm tra lại system prompt để đảm bảo AI hiểu cách phân chia kịch bản, trích xuất cảnh quay (Scenes) và viết prompt tạo ảnh 9:16 phù hợp.
- **Các node gọi API Leonardo.ai (`Leo - Improve Prompt`, `Leo - Generate Image`, v.v.)**:
  - Các node này sử dụng `httpCustomAuth`. Các sếp cần cấu hình Header chứa API Key của Leonardo.ai.
  - Đảm bảo body request truyền đúng model ID của Leonardo.ai Phoenix 1.0 và thiết lập tỉ lệ khung hình (Aspect Ratio) là `9:16`.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** tại node `When clicking ‘Test workflow’` để chạy thử với dữ liệu mẫu từ Airtable.
- Kiểm tra kết quả trả về ở các node trung gian và Airtable đích.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối workflow để bot bắn tin nhắn báo cáo kèm link ảnh ngay khi quá trình render hoàn tất.
- **Tự động hóa theo lịch (Cron):** Thay thế node `manualTrigger` bằng `Schedule Trigger` để hệ thống tự động quét bài viết mới trên Airtable và tạo ảnh mỗi ngày.
- **Mở rộng dung lượng batch**: Điều chỉnh node `Limit` hoặc `Split In Batches` nếu các sếp muốn xử lý số lượng bài viết lớn hơn trong một lần chạy.

### 📌 Kết luận
Workflow tạo ảnh 9:16 tự động từ Content kết hợp Brand Guidelines là mảnh ghép hoàn hảo giúp các đội ngũ Marketing scale-up nội dung video ngắn một cách chuyên nghiệp và tiết kiệm nguồn lực tối đa. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp!