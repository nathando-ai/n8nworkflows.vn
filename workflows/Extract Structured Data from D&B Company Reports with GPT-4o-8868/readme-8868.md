---
title: "🚀 Trích xuất dữ liệu doanh nghiệp từ báo cáo D&B tự động bằng GPT-4o trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động gọi API lấy báo cáo Dun & Bradstreet (D&B), chuyển đổi PDF và trích xuất dữ liệu cấu trúc bằng OpenAI GPT-4o."
slug: "trich-xuat-du-lieu-doanh-nghiep-db-gpt-4o"
tags: [n8n, automation, no-code, openai, gpt-4o, ai-agent, dnb]
keywords: [n8n workflow, trích xuất dữ liệu d&b, gpt-4o structured output, tự động hóa n8n, dun & bradstreet api]
---

# 🚀 Trích xuất dữ liệu doanh nghiệp từ báo cáo D&B tự động bằng GPT-4o

Việc phân tích các báo cáo tài chính và thông tin doanh nghiệp từ **Dun & Bradstreet (D&B)** theo cách thủ công thường tốn rất nhiều thời gian của đội ngũ Sales, Phân tích tín dụng hoặc M&A. Các sếp thường phải tải file, đọc hàng chục trang dữ liệu và nhập tay vào CRM hoặc Google Sheets.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa toàn bộ quy trình: gọi API lấy dữ liệu từ D&B, chuyển đổi báo cáo, và sử dụng sức mạnh của **OpenAI GPT-4o** kết hợp với **AI Agent** để bóc tách thông tin thành các trường dữ liệu có cấu trúc chuẩn xác 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công từ việc lấy token xác thực, gọi API D&B đến phân tích báo cáo.
- **Trích xuất thông tin thông minh:** Sử dụng GPT-4o và Structured Output để lấy chính xác các chỉ số tài chính, lịch sử thanh toán và thông tin pháp lý từ báo cáo D&B.
- **Tối ưu thời gian:** Biến các báo cáo phức tạp thành dữ liệu JSON sạch chỉ trong vài giây, sẵn sàng đẩy vào CRM, Database hoặc Google Sheets.
- **Độ chính xác cao:** Tránh sai sót do nhập liệu thủ công nhờ AI hiểu ngữ cảnh ngữ pháp chuyên sâu.
:::

### 🔑 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain / AI Nodes).
- **OpenAI API Key:** Tài khoản OpenAI có quyền truy cập mô hình `gpt-4o`.
- **D&B Direct+ Account:** Tài khoản API của Dun & Bradstreet (gồm Username, Password và mã DUNS của doanh nghiệp cần tra cứu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n template (hoặc copy toàn bộ JSON) và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính được thiết kế để xử lý từ bước xác thực đến phân tích AI. Các sếp cần chú ý cấu hình các node sau:

- **Get Token (`Get Token` - HTTP Request):** 
  - Cấu hình Authentication dạng **Basic Auth** bằng D&B **username** và **password**.
  - Method: `POST`, URL: `https://plus.dnb.com/v3/token`.
  - Body Parameter: `grant_type = client_credentials`.
- **D&B Report (`D&B Report` - HTTP Request):**
  - Sử dụng token động từ node `Get Token` để truyền vào Header: `Authorization: Bearer {{$json["access_token"]}}`.
  - URL gọi dữ liệu Data Blocks: `https://plus.dnb.com/v1/data/duns/{{ $json.duns }}?blockIDs=paymentinsight_L4_v1&tradeUp=hq...`
- **Convert to PDF File (`Convert to PDF File` - convertToFile):** Chuyển đổi dữ liệu nhận được sang dạng file nhị phân (binary).
- **Extract Binary (`Extract Binary` - extractFromFile):** Trích xuất nội dung văn bản từ file PDF vừa tạo.
- **OpenAI Chat Model6 & OpenAI Chat Model7 (`lmChatOpenAi`):** 
  - Chọn model `gpt-4o`.
  - Nhập OpenAI API Credentials của các sếp.
- **Analyze PDF (`Analyze PDF` - agent) & Structured Output (`outputParserStructured`):**
  - Cấu hình AI Agent đọc nội dung văn bản PDF và ép buộc đầu ra tuân theo schema JSON được định nghĩa sẵn (ví dụ: tên công ty, điểm rủi ro, lịch sử thanh toán, thông tin CEO...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một mã DUNS cụ thể để kiểm tra luồng dữ liệu từ API D&B qua AI Agent.
- Kiểm tra kết quả trả về từ node `Structured Output`.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đẩy dữ liệu về CRM:** Thêm node HubSpot hoặc Salesforce ngay sau node `Structured Output` để tự động cập nhật hồ sơ khách hàng doanh nghiệp.
- **Lưu trữ file:** Thêm node Google Drive hoặc AWS S3 để lưu trữ file PDF báo cáo gốc phục vụ việc kiểm tra sau này.
- **Cảnh báo qua Slack/Telegram:** Thiết lập điều kiện nếu điểm rủi ro từ D&B cao hơn mức cho phép, tự động bắn thông báo khẩn cấp vào nhóm Telegram/Slack của bộ phận Quản trị rủi ro.

### 📌 Kết luận
Workflow tích hợp AI và API D&B này là vũ khí cực mạnh giúp các doanh nghiệp B2B, tài chính, bảo hiểm tối ưu hóa quy trình thẩm định đối tác và khách hàng. Hãy áp dụng ngay vào hệ thống của các sếp để tiết kiệm hàng ngàn giờ làm việc thủ công!