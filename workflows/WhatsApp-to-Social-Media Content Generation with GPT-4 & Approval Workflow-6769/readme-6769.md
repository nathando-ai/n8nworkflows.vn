---
title: "🚀 Tự động hóa nội dung mạng xã hội từ WhatsApp với GPT-4 & quy trình phê duyệt"
description: "Hướng dẫn tự động hóa nội dung mạng xã hội từ WhatsApp với GPT-4 và quy trình phê duyệt trong n8n. Tiết kiệm thời gian và nâng cao hiệu suất nội dung."
slug: "tu-dong-hoa-noi-dung-mang-xa-hoi-tu-whatsapp-voi-gpt-4"
tags: [n8n, automation, no-code, social media, ai]
keywords: [n8n workflow, tự động hóa nội dung, GPT-4, mạng xã hội, tự động hóa]
---

# 🚀 Tự động hóa nội dung mạng xã hội từ WhatsApp với GPT-4 & quy trình phê duyệt

[Các sếp đang gặp khó khăn khi phải tạo nội dung cho nhiều nền tảng mạng xã hội khác nhau từ một nguồn tin duy nhất. Với workflow này, các sếp có thể tự động hóa quy trình này hoàn toàn, tiết kiệm thời gian và đảm bảo nội dung nhất quán trên tất cả các nền tảng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tạo nội dung cho 4 nền tảng (LinkedIn, Instagram, Facebook, X) chỉ trong vài phút.
- Nâng cao hiệu suất: Đảm bảo nội dung nhất quán và phù hợp với từng nền tảng.
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi thiết lập.
- Tích hợp AI: Sử dụng GPT-4 để tạo nội dung chất lượng cao.
- Quy trình phê duyệt: Đảm bảo nội dung được kiểm duyệt trước khi đăng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp để nhận tin nhắn đầu vào.
- API keys cho các dịch vụ sau:
  - OpenAI API Key (https://auth.openai.com/log-in)
  - Google Studio API Key (https://aistudio.google.com/app/apikey)
  - SERP API Key (https://serpapi.com/)
  - Gmail OAuth (https://docs.n8n.io/integrations/builtin/credentials/google/)
  - imgbb API (https://imgbb.com/)
- Credentials cho các nền tảng mạng xã hội (LinkedIn, Instagram, Facebook, X).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào "Import from URL" và dán link workflow: https://n8n.io/workflows/6769.
3. Hoặc tải file JSON về và import thủ công.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Social Media Content Factory**: Đây là node trung tâm tạo nội dung cho các nền tảng. Các sếp cần điều chỉnh prompts để phù hợp với nhu cầu cá nhân hoặc doanh nghiệp.
- **Google Gemini LLM & gpt-4o LLM**: Các node này sử dụng mô hình ngôn ngữ để tạo nội dung. Các sếp cần đảm bảo API keys được cấu hình đúng.
- **pollinations.ai**: Node này tạo hình ảnh cho bài đăng. Các sếp có thể thay đổi prompt để tạo hình ảnh phù hợp.
- **Instagram Image & Instragram Post**: Các node này xử lý hình ảnh và đăng bài lên Instagram. Các sếp cần cấu hình credentials cho Instagram.
- **X Post, Facebook Post, LinkedIn Post**: Các node này đăng bài lên các nền tảng tương ứng. Các sếp cần cấu hình credentials cho từng nền tảng.
- **Approve Final Post Content**: Node này gửi email phê duyệt nội dung. Các sếp cần cấu hình Gmail OAuth.
- **Is Approved?**: Node này kiểm tra xem nội dung có được phê duyệt hay không. Các sếp có thể điều chỉnh logic phê duyệt.
- **Gmail Results**: Node này gửi kết quả cuối cùng qua email. Các sếp cần cấu hình Gmail OAuth.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Telegram Bot để nhận thông báo khi có bài đăng mới (https://docs.n8n.io/integrations/builtin/credentials/telegram/).
- Lưu log các bài đăng để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về hiệu suất nội dung.
- Tích hợp với các công cụ phân tích mạng xã hội để theo dõi tương tác.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình tạo nội dung mạng xã hội từ WhatsApp, tiết kiệm thời gian và đảm bảo nội dung chất lượng. Các sếp chỉ cần nhập tin nhắn vào WhatsApp và workflow sẽ tự động tạo nội dung, tạo hình ảnh, đăng bài và gửi email phê duyệt. Hãy áp dụng ngay để nâng cao hiệu suất nội dung mạng xã hội của bạn!