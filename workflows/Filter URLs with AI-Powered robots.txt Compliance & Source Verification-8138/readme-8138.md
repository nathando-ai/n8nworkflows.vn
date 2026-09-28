---
title: "🚀 Lọc URL tự động thông minh với AI và kiểm tra Robots.txt chuẩn xác trên n8n"
description: "Hướng dẫn sử dụng workflow n8n tích hợp AI (Groq, Gemini, Mistral) và PostgreSQL để tự động kiểm tra, tuân thủ robots.txt và xác thực nguồn URL một cách thông minh."
slug: "loc-url-tu-dong-ai-robots-txt-n8n"
tags: [n8n, automation, no-code, ai-agents, postgresql, web-scraping]
keywords: [n8n workflow, loc url ai, robots.txt compliance, ai summarization, postgresql n8n]
---

# 🚀 Lọc URL tự động thông minh với AI và kiểm tra Robots.txt chuẩn xác trên n8n

Việc thu thập dữ liệu (Web Scraping) hoặc xử lý hàng loạt danh sách URL thường gặp phải rào cản lớn: vi phạm quy tắc `robots.txt` của website đích, dẫn đến việc bị chặn IP hoặc xử lý nhầm các đường dẫn không hợp lệ. Làm thủ công thì cực kỳ mất thời gian, còn viết code riêng thì tốn kém tài nguyên. 

Được phát triển bởi **Hybroht**, workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), kết hợp sức mạnh của AI Agents (Groq, Google Gemini, Mistral Cloud) và cơ sở dữ liệu PostgreSQL để kiểm tra tuân thủ `robots.txt` và xác thực nguồn URL một cách thông minh, tự động hoàn toàn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tuân thủ pháp lý & kỹ thuật:** Tự động phân tích và tuân thủ tuyệt đối file `robots.txt` của từng website trước khi cào dữ liệu.
- **AI thông minh:** Sử dụng linh hoạt các mô hình ngôn ngữ lớn (LLMs) như Groq, Google Gemini, Mistral Cloud qua các node *Information Extractor* và *Model Selector* để xử lý logic phức tạp.
- **Lưu trữ tối ưu:** Tích hợp sâu với cơ sở dữ liệu PostgreSQL để lưu trữ, cache trạng thái `robots.txt` và danh sách URL bị cấm (*forbidden urls*), giúp tăng tốc độ xử lý cho các lần chạy sau.
- **Vận hành tự động:** Lên lịch chạy định kỳ với *Schedule Trigger* hoặc kích hoạt linh hoạt qua *Execute Workflow Trigger*.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **n8n Instance:** Đã cài đặt n8n (bản self-hosted hoặc cloud).
- **PostgreSQL Database:** Một cơ sở dữ liệu PostgreSQL để workflow tự động tạo bảng và lưu trữ trạng thái.
- **AI API Credentials:** Ít nhất một trong các API Keys sau:
  - Groq API Key (cho *Groq Chat Model*)
  - Google Gemini API Key (cho *Google Gemini Chat Model*)
  - Mistral Cloud API Key (cho *Mistral Cloud Chat Model*)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ trang chủ n8n (ID: `8138`).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình workflow).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow có tới 37 nodes bao gồm nhiều thao tác với Database và AI, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **PostgreSQL Nodes** (ví dụ: *Create robots.txt Table*, *Create forbidden urls table*, *Upsert robots.txt Table*...): Cần trỏ đúng **PostgreSQL Credentials** của hệ thống database mà các sếp đang sử dụng. Workflow sẽ tự động thực hiện các câu lệnh tạo bảng và quản lý dữ liệu.
- **AI Model Nodes** (*Groq Chat Model*, *Google Gemini Chat Model*, *Mistral Cloud Chat Model*): Thêm các API Credentials tương ứng cho nhà cung cấp AI mà các sếp muốn ưu tiên sử dụng.
- **Model Selector & Information Extractor**: Kiểm tra lại cấu hình mô hình AI mặc định trong các node này để đảm bảo chúng liên kết chính xác với các Chat Model node vừa cấu hình bên trên.
- **Schedule Trigger**: Điều chỉnh lại lịch chạy (thời gian, chu kỳ) cho phù hợp với nhu cầu thực tế của dự án.

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công bằng nút **Test step** hoặc **Execute Workflow** với một vài URL mẫu để kiểm tra luồng dữ liệu qua các nhánh `If Link Allowed` và kết xuất kết quả tại node `Output`.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo lỗi:** Thêm node Telegram hoặc Slack ở nhánh xử lý URL bị cấm (*Prepare Output for Link Disallowed*) để nhận thông báo ngay lập tức khi hệ thống phát hiện URL vi phạm.
- **Mở rộng nguồn dữ liệu:** Thay vì dùng *Schedule Trigger* đơn thuần, các sếp có thể kết nối thêm Webhook hoặc Google Sheets để nhận danh sách URL đầu vào theo thời gian thực từ người dùng.
- **Tối ưu chi phí AI:** Tận dụng Groq hoặc các mô hình open-source nhẹ nhàng thông qua các node tích hợp để tiết kiệm chi phí gọi API khi phải xử lý số lượng lớn URL hàng ngày.

### 📌 Kết luận
Workflow **Filter URLs with AI-Powered robots.txt Compliance** là một cỗ máy tự động hóa cực kỳ mạnh mẽ, giúp tiết kiệm hàng đống thời gian và bảo vệ hệ thống của các sếp khỏi việc truy cập trái phép vào các trang web hạn chế. Hãy cài đặt ngay lên VPS của mình và tận hưởng sức mạnh tự động hóa do AI mang lại nhé các sếp!