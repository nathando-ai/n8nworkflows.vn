---
title: "🚀 Trích xuất thông tin nhân sự và phân tích dữ liệu tuyển dụng thông minh từ LinkedIn với Decodo & GPT-4o-mini"
description: "Tự động hóa toàn diện quy trình phân tích hồ sơ LinkedIn và đánh giá mức độ phù hợp công việc sử dụng AI, giúp HR tối ưu hóa thời gian sàng lọc ứng viên."
slug: "trich-xuat-thong-tin-nhan-su-linkedin-gpt-4o-mini"
tags: [n8n, automation, hr-tech, ai, openai, google-sheets]
keywords: [n8n workflow, tuyển dụng thông minh, trích xuất dữ liệu linkedin, gpt-4o-mini, decodo, hr automation]
---

# 🚀 Trích xuất thông tin nhân sự và phân tích dữ liệu tuyển dụng thông minh từ LinkedIn với Decodo & GPT-4o-mini

Các sếp trong ngành nhân sự (HR) hay talent acquisition chắc chắn hiểu rõ nỗi đau khi phải sàng lọc hàng trăm hồ sơ LinkedIn thủ công mỗi ngày. Việc đọc hiểu từng profile, đối chiếu với mô tả công việc (Job Description), tổng hợp kỹ năng và đánh giá sự phù hợp tốn rất nhiều thời gian và dễ bỏ sót nhân tài.

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó! Nó tự động kết nối với **Decodo** để cào dữ liệu profile LinkedIn, sau đó sử dụng sức mạnh của **GPT-4o-mini** để phân tích sâu, trích xuất cấu trúc dữ liệu, đánh giá mức độ phù hợp với công việc và lưu trữ trực quan lên Google Sheets. Tất cả diễn ra tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình:** Thay vì mất 15-30 phút đọc mỗi profile, AI xử lý và phân tích toàn diện chỉ trong vài giây.
- **Phân tích sâu (Data Mining):** Đánh giá kỹ năng, kinh nghiệm, mức độ phù hợp văn hóa (cultural fit), quỹ đạo sự nghiệp và điểm mạnh cạnh tranh của ứng viên so với Job Description.
- **Dữ liệu cấu trúc sạch:** Tự động chuẩn hóa dữ liệu đầu ra dạng JSON và đồng bộ trực tiếp vào Google Sheets phục vụ tuyển dụng.
- **Hoạt động liên tục 24/7:** Sẵn sàng tích hợp với các hệ thống ATS, CRM hoặc nền tảng phân tích nhân sự của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru workflow này, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Decodo API Key**: Dùng cho node `Decodo` để cào dữ liệu LinkedIn.
- **OpenAI API Key**: Cấp quyền cho các node `OpenAI Chat Model` (sử dụng model `gpt-4o-mini`).
- **Google Sheets API / OAuth2**: Tài khoản Google để kết nối và lưu trữ dữ liệu vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ JSON), sau đó paste trực tiếp vào giao diện n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trước khi chạy:
- **Node `Set the Input Fields`**: Cấu hình URL của profile LinkedIn cần phân tích và đoạn mô tả công việc (Job Description) tương ứng.
- **Node `Decodo`**: Kết nối `decodoApi` credentials của sếp để công cụ tiến hành thu thập dữ liệu profile LinkedIn.
- **Nodes `OpenAI Chat Model`** (bao gồm các node liên quan đến Structured Data Extract, Data Mining, và Summarizer): Thêm `openAiApi` credentials và đảm bảo model được chọn là **`gpt-4o-mini`**.
- **Node `Append or update row in sheet`**: Kết nối tài khoản Google Sheets, trỏ đến file Google Sheet quản lý tuyển dụng của doanh nghiệp và map các cột dữ liệu (tên ứng viên, kinh nghiệm, kỹ năng, đánh giá AI...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** trên node `When clicking ‘Execute workflow’` với một profile mẫu để kiểm tra kết quả trả về.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào cuối chuỗi để bot tự động bắn thông báo tóm tắt đánh giá ứng viên về group chat của bộ phận HR ngay khi phân tích xong.
- **Lưu trữ file PDF:** Kết hợp node `Read/Write Files from Disk` hoặc Google Drive để lưu lại bản báo cáo phân tích chi tiết dạng file PDF gửi cho Hiring Manager.
- **Mở rộng quy mô:** Thay thế `Manual Trigger` bằng Webhook hoặc Google Forms để các sếp có thể dán link LinkedIn vào form và hệ thống tự động xử lý hàng loạt (Batch processing).

### 📌 Kết luận
Workflow tích hợp Decodo và GPT-4o-mini chính là "vũ khí bí mật" giúp đội ngũ tuyển dụng tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần, đồng thời nâng cao chất lượng sàng lọc nhân sự dựa trên dữ liệu thông minh. Hãy thiết lập ngay hôm nay và tối ưu hóa quy trình HR của doanh nghiệp các sếp nhé!