---
title: "🚀 Tự động trích xuất và tóm tắt thông tin công ty trên Indeed với Bright Data & Google Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu từ Indeed bằng Bright Data, xử lý bằng AI Agent và tóm tắt thông tin chuyên sâu với Google Gemini."
slug: "tu-dong-trich-xuat-va-tom-tat-thong-tin-cong-ty-indeed-voi-bright-data-va-google-gemini"
tags: [n8n, automation, ai-agent, bright-data, google-gemini, web-scraping]
keywords: [n8n workflow, cào dữ liệu indeed, bright data web unlocker, google gemini n8n, tự động hóa hr marketing]
---

# 🚀 Tự động trích xuất và tóm tắt thông tin công ty trên Indeed với Bright Data & Google Gemini

Các sếp làm trong ngành Tuyển dụng (HR), Marketing hay Nghiên cứu thị trường chắc chắn hiểu rõ sự vất vả khi phải tìm kiếm, tổng hợp thông tin và đánh giá các công ty trên Indeed. Việc copy-paste thủ công hàng chục, hàng trăm trang web vừa tốn thời gian, vừa dễ bỏ sót thông tin quan trọng.

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n hoàn toàn tự động: sử dụng **Bright Data** để cào dữ liệu mượt mà, kết hợp sức mạnh siêu việt của **Google Gemini** và **AI Agent** để phân tích, trích xuất và tóm tắt toàn bộ thông tin công ty một cách chuyên nghiệp. Không cần viết code phức tạp, các sếp chỉ cần cấu hình và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn quy trình tìm kiếm, cào dữ liệu và tổng hợp báo cáo.
- **Dữ liệu chính xác, sạch sẽ:** AI Agent và Google Gemini giúp lọc bỏ nhiễu, trích xuất đúng thông tin cốt lõi của doanh nghiệp.
- **Đa năng ứng dụng:** Phục vụ đắc lực cho việc nghiên cứu đối thủ cạnh tranh, tìm kiếm khách hàng tiềm năng (B2B) hoặc đánh giá thị trường tuyển dụng.
- **Tích hợp linh hoạt:** Dễ dàng đẩy kết quả qua Webhook đến Slack, Telegram hoặc hệ thống CRM của công ty.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ AI Nodes).
- **Bright Data Account:** Cần dịch vụ Web Unlocker để vượt qua lớp bảo mật và cào dữ liệu Indeed (cần lấy API/Auth Credentials).
- **Google Gemini API Key:** Tài khoản Google AI Studio để kết nối với các node Google Gemini Chat Model.
- **Webhook Endpoint (Tùy chọn):** URL nhận thông báo (ví dụ: webhook từ Make, Slack, Telegram hoặc CRM nội bộ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ chính thức của n8n (Template ID: `3702`), sau đó vào n8n Editor chọn **Import from File** hoặc copy/paste trực tiếp đoạn JSON vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes thông minh phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Set Indeed Search Query`**: 
  - Đây là nơi các sếp thiết lập từ khóa tìm kiếm công ty hoặc vị trí công việc trên Indeed (ví dụ: tên công ty, vị trí tuyển dụng, địa điểm). Hãy thay đổi giá trị này thành từ khóa mong muốn của sếp.
- **Node `Perform Indeed Web Request` (HTTP Request)**: 
  - Cần cấu hình thông tin xác thực (`httpHeaderAuth`) kết nối với dịch vụ **Bright Data Web Unlocker** để gửi yêu cầu lấy dữ liệu web thành công mà không bị chặn.
- **Các Node Google Gemini (`Google Gemini Chat Model`, `Google Gemini Chat Model For Summarization`, `Google Gemini Chat Model for AI Agent`)**:
  - Cần điền **Google Palm/Gemini API Key** (`googlePalmApi`) để cấp quyền cho các chuỗi AI (`Markdown to Textual Data Extractor`, `Indeed Summarization`, và `Indeed Expert AI Agent`) hoạt động. Sử dụng model *Google Gemini Flash* để đạt tốc độ xử lý tối ưu.
- **Node `Initiate a Webhook Notification for Summarization` & `Initiate a Webhook Notification for Markdown to HTML Response`**:
  - Cập nhật lại đường dẫn Webhook URL của các sếp (ví dụ: endpoint của Slack, Telegram, hoặc hệ thống nội bộ) để nhận kết quả báo cáo sau khi AI xử lý xong.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** tại node `When clicking ‘Test workflow’` để kiểm tra luồng chạy thử.
- Theo dõi log ở từng node để đảm bảo dữ liệu trả về từ Bright Data và Google Gemini khớp với kỳ vọng.
- Sau khi test mượt mà, gạt công tắc sang **Active** để đưa workflow vào trạng thái tự động sẵn sàng.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Webhook HTTP Request thuần túy, các sếp có thể gắn thêm node Telegram hoặc Slack để bắn tin nhắn báo cáo trực tiếp vào group chat công ty ngay khi có kết quả.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable vào cuối chuỗi để lưu lại lịch sử cào thông tin các công ty, tiện cho việc theo dõi lâu dài.
- **Tùy biến Prompt AI:** Tinh chỉnh system prompt trong `Indeed Expert AI Agent` để yêu cầu AI trích xuất thêm các thông tin cụ thể như: quy mô công ty, mức lương trung bình, công nghệ sử dụng... tùy theo nhu cầu thực chiến của sếp.

### 📌 Kết luận
Workflow tự động hóa kết hợp giữa **Bright Data** và **Google Gemini** chính là "vũ khí bí mật" giúp các sếp tối ưu hóa thời gian nghiên cứu và tổng hợp thông tin doanh nghiệp trên Indeed. Hãy bắt tay vào cài đặt ngay hôm nay để biến những giờ làm việc thủ công thành tích tắc!