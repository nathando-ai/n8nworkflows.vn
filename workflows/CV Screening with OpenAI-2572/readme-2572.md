---
title: "🚀 Tự động hóa sàng lọc CV và chấm điểm ứng viên bằng OpenAI với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tải CV, trích xuất văn bản PDF, phân tích và chấm điểm ứng viên bằng OpenAI API hoàn toàn tự động."
slug: "tu-dong-hoa-sang-loc-cv-openai-n8n"
tags: [n8n, automation, ai, openai, hr, recruitment]
keywords: [n8n workflow, cv screening, ai recruitment, tự động hóa hr, openai api n8n]
---

# 🚀 Tự động hóa sàng lọc CV và chấm điểm ứng viên bằng OpenAI với n8n

Việc đọc và sàng lọc hàng trăm bộ hồ sơ (CV) thủ công mỗi khi tuyển dụng là một "cực hình" đối với các nhà quản lý nhân sự (HR) và các startup. Các sếp thường phải mất nhiều giờ để đọc, đánh giá mức độ phù hợp và so sánh kỹ năng ứng viên với mô tả công việc (Job Description).

Giải pháp gì để tiết kiệm 90% thời gian cho khâu này? Workflow **CV Screening with OpenAI** (được chia sẻ bởi chuyên gia Mark Shcherbakov từ cộng đồng 5minAI) sẽ giúp các sếp tự động hóa toàn bộ quy trình: từ tải CV, đọc file PDF, phân tích chuyên sâu qua AI đến trả về điểm số và đánh giá chi tiết mà không cần tốn một giọt mồ hôi nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** AI tự động đọc CV và chấm điểm chỉ trong vài giây.
- **Đánh giá khách quan:** Cung cấp điểm số (matching score), tóm tắt điểm mạnh, điểm yếu và lý do phù hợp dựa trên tiêu chí công việc.
- **Chuẩn hóa dữ liệu:** Trích xuất thông tin ứng viên dưới định dạng JSON có cấu trúc rõ ràng, sẵn sàng lưu trữ vào Database.
- **Hoạt động linh hoạt:** Dễ dàng tích hợp vào hệ thống tuyển dụng hiện tại của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Tài khoản OpenAI có sẵn số dư để gọi mô hình GPT (GPT-4o hoặc GPT-4o-mini).
- **Đường dẫn CV (Direct Link):** Link trực tiếp tải file PDF của CV (từ Google Drive, Dropbox, Supabase Storage, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n.io (Workflow 2572)](https://n8n.io/workflows/2572) hoặc sao chép mã JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các node sau:

- **Node `When clicking ‘Test workflow’` (Manual Trigger):** 
  - Đây là điểm khởi đầu thủ công để kiểm tra. Các sếp có thể thay thế bằng *Webhook*, *Google Drive Trigger* hoặc *Email Trigger* khi đưa vào vận hành thực tế.
- **Node `Set Variables`:** 
  - Nơi các sếp khai báo đường dẫn trực tiếp tới file CV (`cv_url`) và đoạn mô tả công việc (`job_description`) để AI có căn cứ đối chiếu.
- **Node `Download File` (HTTP Request):** 
  - Thực hiện tải nội dung file CV từ URL đã được truyền vào từ bước trước.
- **Node `Extract Document PDF` (Extract From File):** 
  - Trích xuất toàn bộ văn bản thô (raw text) từ định dạng PDF của CV ứng viên.
- **Node `OpenAI - Analyze CV` (HTTP Request):** 
  - **Credentials:** Chọn kết nối OpenAI API của các sếp.
  - **Body / Prompt:** Cấu hình gửi text CV và Job Description sang OpenAI, kết hợp sử dụng **JSON Schema** để ép AI trả về kết quả theo cấu trúc chuẩn (Điểm số, Điểm mạnh, Điểm yếu, Nhận xét chung).
- **Node `Parsed JSON` (Set):** 
  - Xử lý và định dạng lại kết quả trả về từ OpenAI để sẵn sàng lưu trữ hoặc chuyển sang bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với một file CV mẫu, kiểm tra kỹ phần JSON trả về từ OpenAI.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết nối thêm node **Supabase** hoặc **Google Sheets** ở cuối workflow để tự động lưu thông tin ứng viên và điểm số vào database.
- **Thông báo qua Telegram/Slack:** Thêm node gửi tin nhắn tự động về nhóm HR ngay khi có ứng viên nộp CV và vượt qua vòng chấm điểm của AI.
- **Tự động gửi email phản hồi:** Tích hợp Gmail node để gửi email cá nhân hóa (thư mời phỏng vấn hoặc thư cảm ơn lịch sự) dựa theo số điểm AI chấm.

### 📌 Kết luận
Tự động hóa sàng lọc CV với n8n và OpenAI là bước tiến lớn giúp bộ phận nhân sự tối ưu hóa năng suất, không bỏ lỡ các nhân tài sáng giá. Hãy áp dụng ngay vào quy trình tuyển dụng của doanh nghiệp các sếp nhé!