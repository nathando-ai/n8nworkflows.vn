---
title: "🚀 Tự Động Phân Loại Email Gmail Bằng GPT-4o Và Lưu Trữ Vào Mem0 AI"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa quản lý hộp thư đến Gmail, gắn nhãn thông minh bằng GPT-4o và đồng bộ dữ liệu vào hệ thống trí nhớ dài hạn Mem0."
slug: "tu-dong-phan-loai-email-gmail-gpt4o-mem0-n8n"
tags: [n8n, automation, gmail, openai, mem0, ai-summarization]
keywords: [n8n workflow, tự động hóa email, gpt-4o gmail, mem0 ai, quan ly hop thu den, phan loại email tự động]
---

# 🚀 Tự Động Phân Loại Email Gmail Bằng GPT-4o Và Lưu Trữ Vào Mem0 AI

Các sếp có bao giờ cảm thấy ngợp thở mỗi sáng khi mở hộp thư đến với hàng chục, thậm chí hàng trăm email lẫn lộn từ thông cáo marketing, email nội bộ cho đến các yêu cầu quan trọng từ khách hàng? Việc đọc thủ công, gắn nhãn và phân loại từng email ngốn rất nhiều thời gian quý báu.

Giải pháp ở đây là gì? Workflow n8n siêu việt này sẽ thay các sếp "trấn giữ" hộp thư 24/7. Sử dụng sức mạnh của **GPT-4o**, hệ thống sẽ tự động làm sạch nội dung, phân loại mục đích, gắn nhãn (label) trực tiếp trên Gmail và thậm chí đẩy dữ liệu cấu trúc vào hệ thống trí nhớ dài hạn **Mem0** để tra cứu về sau. Không cần code phức tạp, tự động hóa hoàn toàn 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian quản lý email:** Hộp thư được phân loại và gắn nhãn tự động ngay khi vừa có email mới đến.
- **Trí tuệ nhân tạo thông minh:** Sử dụng `[LLM]: GPT-4o` để đọc hiểu ngữ cảnh, tóm tắt ý chính và trích xuất thông tin cực kỳ chính xác.
- **Hệ thống hóa tri thức (Mem0):** Lưu trữ lịch sử tương tác email vào bộ nhớ dài hạn, giúp dễ dàng truy vấn thông tin khi cần.
- **Hoạt động liên tục 24/7:** Chạy ngầm ổn định trên n8n, đảm bảo không bỏ lỡ bất kỳ email quan trọng nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản & Credentials:**
  - **Gmail (OAuth2):** Để đọc, gắn nhãn và quản lý email.
  - **OpenAI API Key:** Cho model `[LLM]: GPT-4o`.
  - **Mem0 API (hoặc HTTP Header Auth tương đương):** Để đẩy dữ liệu vào kho lưu trữ dài hạn.
  - **JigsawStack API (Tùy chọn):** Dùng làm cơ chế dự phòng (fallback classifier) khi AI chính gặp sự cố.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add Workflow** -> **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:

- **`[Trigger]: Watch Inbox (5m)`**: Kết nối tài khoản Gmail của các sếp qua OAuth2 để trigger quét email mới mỗi 5 phút.
- **`[LLM]: GPT-4o`**: Thêm OpenAI Credentials và đảm bảo model được chọn là `chatgpt-4o-latest`.
- **`[Router]: Triage Streams` (Switch Node)**: Điểm cực kỳ quan trọng! Các sếp nhớ cập nhật rule để nhận diện **tên miền nội bộ của công ty** (ví dụ: `@your-business.com`) nhằm tránh xử lý nhầm các email nội bộ.
- **`[Python]: Format Mem0 V2 Schema` & `[API]: Push to Mem0 Long-term`**: Cấu hình endpoint và API key của Mem0 để đẩy dữ liệu trích xuất vào kho lưu trữ.
- **Nhãn Gmail (Labels)**: Đảm bảo các nhãn như "Marketing", tên danh mục tùy chỉnh đã được tạo sẵn trong Gmail của các sếp hoặc sử dụng node `Create Gmail Simple` có sẵn trong workflow để tự động tạo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với dữ liệu mẫu (hoặc gửi một email test vào inbox).
- Kiểm tra kết quả hiển thị trên các nhánh và đảm bảo nhãn đã được gắn đúng trên Gmail.
- Gạt công tắc sang **Active** để workflow chính thức tự động vận hành.

---

## Mở rộng & Tùy chỉnh (Tùy chọn)
- **Prompt chính (`[AI]: Main Branch Extractor`)**: Các sếp có thể tùy chỉnh thêm các danh mục mong muốn (ví dụ: Thêm nhãn "Khách hàng VIP", "Báo giá", "Hỗ trợ kỹ thuật" kèm hướng dẫn ngắn gọn cho AI).
- **Nhánh phụ (Optional Branch)**: Workflow có sẵn nhánh phụ dành riêng cho các sếp làm side-hustle cần các quy tắc trích xuất riêng biệt. Chỉ cần bật lên và nối vào node `[Batch]: Process Emails`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack sau bước xử lý thành công để nhận thông báo ngay lập tức trên điện thoại khi có email quan trọng từ khách hàng lớn.
- **Ghi log lỗi:** Sử dụng nhánh `Error Details` để lưu vết các email bị lỗi xử lý vào Google Sheets nhằm kiểm tra và tối ưu prompt sau này.

### 📌 Kết luận
Workflow này là một "vũ khí" tối thượng giúp automat hóa toàn bộ quy trình xử lý email rườm rà. Hãy triển khai ngay hôm nay để giải phóng thời gian và tập trung vào những công việc mang lại giá trị cao hơn cho doanh nghiệp của các sếp!