---
title: "🚀 Tự động hóa Tuyển dụng LinkedIn: Tìm kiếm và Xếp hạng Ứng viên bằng AI với GPT-4o"
description: "Xây dựng hệ thống Talent Pipeline tự động 100%: Nhập Mô tả công việc, AI tìm kiếm profile LinkedIn phù hợp, trích xuất dữ liệu, chấm điểm và lưu kết quả vào Google Sheets."
slug: "linkedin-talent-pipeline-ai-gpt4o-n8n"
tags: [n8n, automation, no-code, ai, hr, recruitment, gpt-4o]
keywords: [n8n workflow, tuyển dụng tự động, linkedin talent pipeline, gpt-4o hr, ai tuyển dụng, google sheets automation]
---

# 🚀 Tự động hóa Tuyển dụng LinkedIn: Tìm kiếm và Xếp hạng Ứng viên bằng AI với GPT-4o

Các sếp trong ngành nhân sự (HR) chắc chắn hiểu rõ cảm giác mệt mỏi khi phải lướt qua hàng trăm profile trên LinkedIn, đọc CV thủ công và đối chiếu xem ứng viên nào thực sự khớp với mô tả công việc (Job Description - JD). Công việc này vừa tốn thời gian, vừa dễ bỏ lỡ nhân tài.

Workflow n8n này ra đời như một trợ lý AI đắc lực, giải quyết triệt để bài toán trên. Các sếp chỉ cần nhập JD, hệ thống sẽ tự động quét, lọc hồ sơ, chấm điểm thông minh bằng GPT-4o và trả về bảng danh sách ứng viên tiềm năng được sắp xếp gọn gàng trong Google Sheets!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian sàng lọc:** Tự động hóa toàn bộ quy trình từ tìm kiếm profile trên LinkedIn đến chấm điểm tương thích.
- **Đánh giá khách quan, chuẩn xác:** AI (GPT-4o) phân tích sâu kỹ năng, kinh nghiệm dựa trực tiếp trên yêu cầu của JD.
- **Tập trung vào nhân tài cốt lõi:** Danh sách ứng viên được chấm điểm sẵn và lưu ngay vào Google Sheets giúp các sếp dễ dàng gọi phỏng vấn những người điểm cao nhất.
- **Hoạt động linh hoạt:** Kích hoạt dễ dàng qua giao diện chat bất cứ khi nào có vị trí tuyển dụng mới.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản cloud hoặc self-hosted).
- **OpenAI API Key:** Sử dụng cho các node LangChain, Agent và LLM Scoring (GPT-4o).
- **Google Custom Search API:** Để thực hiện tìm kiếm các profile LinkedIn phù hợp với từ khóa.
- **Apify Account & API Token:** Dùng để cào dữ liệu chi tiết từ các profile LinkedIn.
- **Google Sheets:** Tài khoản Google có quyền tạo và chỉnh sửa file Sheets để lưu danh sách ứng viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow (hoặc tải file JSON từ nguồn) và chọn **Import from File / Paste JSON** trong giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống trơn tru, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Job Description Input (`chatTrigger`) & Extract Job Details (`agent` / `OpenAI Chat Model`):** Kết nối credentials OpenAI của các sếp. Node này sẽ nhận diện yêu cầu tuyển dụng và bóc tách các từ khóa, kỹ năng quan trọng từ JD.
- **Google Custom Search API Request (`httpRequest`):** Điền API Key và Search Engine ID của Google Custom Search để hệ thống có quyền truy vấn tìm kiếm profile trên LinkedIn.
- **Run Apify Scraper & Get LinkedIn Data (`httpRequest`):** Cần cấu hình Apify API Token để workflow có thể gọi cácactor cào dữ liệu LinkedIn.
- **LLM Scoring (`openAi`) & Structured Output Parser (`outputParserStructured`):** Thiết lập prompt chuẩn để AI chấm điểm ứng viên theo thang điểm từ 1-10 và trả về định dạng JSON mạch lạc.
- **Save to Google Sheets (`googleSheets`):** Kết nối tài khoản Google của các sếp, chọn đúng file Google Sheets và các cột tương ứng (Họ tên, Link Profile, Điểm số, Đánh giá của AI...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một JD mẫu để kiểm tra luồng chạy qua các node `Filter LinkedIn Profiles`, `Prepare Apify Input`, và `Loop Over Items`.
- Sau khi kiểm tra dữ liệu đổ về Google Sheets chính xác, gạt công tắc sang **Active workflow** để chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ở cuối luồng để ngay khi AI quét và chấm điểm xong ứng viên top đầu, hệ thống sẽ bắn thông báo ngay lập tức vào nhóm chat của team HR.
- **Quản lý giới hạn (Rate Limits):** Khi cào dữ liệu qua Apify và Google Search, hãy chú ý cấu hình node `Wait for Scraping` và `Limit` cho phù hợp để tránh bị block IP hoặc vượt quá hạn mức API miễn phí.
- **Mở rộng kho dữ liệu:** Có thể lưu thêm lịch sử tuyển dụng theo từng phòng ban vào các sheet riêng biệt bằng cách phân loại từ kết quả bóc tách JD của Agent.

### 📌 Kết luận
Workflow **LinkedIn Talent Pipeline** là giải pháp tối tân giúp tự động hóa khâu tuyển dụng đầu vào bằng sức mạnh của AI. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất cho đội ngũ nhân sự của các sếp!