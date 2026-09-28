---
title: "🚀 Tự động theo dõi thay đổi website đối thủ cạnh tranh với OpenAI và Firecrawl"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động quét, phân tích và báo cáo mọi thay đổi trên website đối thủ cạnh tranh bằng AI và Firecrawl."
slug: "tu-dong-theo-doi-website-doi-thu-voi-openai-va-firecrawl"
tags: [n8n, automation, no-code, openai, firecrawl, marketing, ai-agent]
keywords: [n8n workflow, theo dõi đối thủ cạnh tranh, competitor monitoring, openai gpt-4o, firecrawl, tự động hóa marketing]
---

# 🚀 Tự động theo dõi thay đổi website đối thủ cạnh tranh với OpenAI và Firecrawl

Việc theo dõi sát sao các bước đi, cập nhật sản phẩm hay thay đổi giá cả của đối thủ cạnh tranh là yếu tố sống còn trong kinh doanh. Tuy nhiên, việc phải thủ công "lướt" qua từng website mỗi ngày vừa tốn thời gian, lại rất dễ bỏ lỡ thông tin quan trọng.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp xây dựng một hệ thống "gián谍" (espionage) tự động 100%. Hệ thống sẽ tự động quét website đối thủ, sử dụng sức mạnh của **OpenAI (GPT-4o)** để phân tích sự thay đổi và tự động gửi email báo cáo chi tiết qua **Gmail**. Tất cả hoàn toàn tự động, không cần tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối**: Không cần thủ công kiểm tra website đối thủ mỗi ngày.
- **Phát hiện thay đổi chớp nhoả**: AI sẽ đọc hiểu và tóm tắt chính xác những gì đã thay đổi trên trang (tính năng mới, đổi giá, nội dung marketing...).
- **Báo cáo tự động qua Gmail**: Nhận thông tin phân tích trực tiếp vào hộp thư đến một cách nhanh chóng.
- **Hoạt động bền bỉ**: Lên lịch định kỳ (ví dụ: quét mỗi ngày hoặc mỗi tuần) để không bỏ lỡ bất kỳ tin tức nào từ thị trường.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **OpenAI API Key** (Sử dụng model GPT-4o mạnh mẽ).
- **Firecrawl Account / API Key** (Dùng để scrape dữ liệu trang web dạng Markdown sạch sẽ).
- **Gmail Account** (Kết nối qua OAuth2 để gửi email báo cáo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp chú ý cấu hình kỹ các node sau:
- **New espionage assignment (`formTrigger`)**: Nơi các sếp nhập URL website đối thủ và các hướng dẫn/câu hỏi cần AI tập trung theo dõi.
- **convert message to website url & instruction (`httpRequest`)** & **OpenAI Chat Model**: Đảm bảo đã kết nối **OpenAI API** chuẩn chỉnh, cấu hình model `gpt-4o` để đảm bảo chất lượng phân tích tốt nhất.
- **scrape page - 1 & scrape page - 2 (`httpRequest`)**: Tích hợp dịch vụ **Firecrawl** (hoặc công cụ scrape tương đương) bằng thông tin xác thực (`httpHeaderAuth` / `httpBasicAuth`) để cào dữ liệu trang web mục tiêu.
- **send e-mail? (`agent`) & Gmail**: Cấu hình kết nối **Gmail OAuth2** và tuỳ chỉnh lại prompt bên trong Agent để AI định dạng nội dung email báo cáo theo đúng ý muốn của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách điền form yêu cầu mẫu để kiểm tra xem quá trình scrape website và gọi OpenAI có trả về kết quả như ý không.
- Sau khi test thành công, bật công tắc **Active** để workflow chính thức hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Ngoài Gmail, các sếp có thể gắn thêm node **Slack** hoặc **Telegram** để nhận cảnh báo ngay lập tức trên điện thoại khi đối thủ có biến động lớn.
- **Lưu trữ lịch sử**: Thêm node **Google Sheets** hoặc **Notion** để lưu lại lịch sử các lần quét và phân tích, giúp tạo cơ sở dữ liệu theo dõi dài hạn.
- **Điều chỉnh thời gian chờ**: Tinh chỉnh node **wait 1 day** thành chu kỳ ngắn hơn hoặc dài hơn tùy thuộc vào mức độ quan trọng và tần suất cập nhật của đối thủ.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho các marketer, product manager và chủ doanh nghiệp muốn nắm bắt thông tin thị trường một cách tự động và thông minh. Hãy cài đặt ngay hôm nay để luôn đi trước đối thủ một bước!