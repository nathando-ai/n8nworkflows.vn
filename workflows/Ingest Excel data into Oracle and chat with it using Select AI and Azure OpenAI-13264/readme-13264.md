---
title: "🚀 Tự động đưa dữ liệu Excel lên Oracle Database và chat thông minh với Select AI & Azure OpenAI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình upload file Excel, tạo bảng động trên Oracle Database và tích hợp Azure OpenAI Select AI để trò chuyện trực tiếp với dữ liệu bằng ngôn ngữ tự nhiên."
slug: "tu-dong-hoa-excel-oracle-select-ai-azure-openai-n8n"
tags: [n8n, automation, oracle-database, azure-openai, ai-rag, select-ai]
keywords: [n8n workflow, oracle database, excel to oracle, azure openai, select ai, tu dong hoa du lieu]
---

# 🚀 Tự động Ingest Excel lên Oracle Database & Chat với dữ liệu qua Azure OpenAI Select AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải xử lý thủ công các file Excel cồng kềnh, loay hoay viết script tạo bảng trên cơ sở dữ liệu doanh nghiệp, rồi lại mất hàng giờ viết câu lệnh SQL để truy vấn báo cáo? Quá tốn thời gian và dễ xảy ra sai sót!

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do **Saumil Diwaker** xây dựng. Workflow này sẽ giải quyết trọn gói bài toán: Tự động nhận file Excel qua Webhook, phân tích cấu trúc schema, tự động tạo bảng trên Oracle Database, nạp dữ liệu theo từng batch, tích hợp **Oracle Select AI** và **Azure OpenAI** để các sếp có thể "chat" trực tiếp bằng tiếng Việt/ngôn ngữ tự nhiên với đống dữ liệu vừa nạp mà không cần biết viết câu lệnh SQL phức tạp nào cả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file dữ liệu lớn mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình ETL**: Biến file Excel thô thành bảng cơ sở dữ liệu Oracle chuẩn hóa chỉ trong vài giây.
- **AI RAG & Text-to-SQL thông minh**: Sử dụng Azure OpenAI thông qua Oracle Select AI (`DBMS_CLOUD_AI`) để tự động dịch câu hỏi thông thường thành câu lệnh SQL và trả về kết quả chính xác.
- **Tiết kiệm nhân lực kỹ thuật**: Đội ngũ kinh doanh hay vận hành có thể tự hỏi đáp dữ liệu từ Oracle Database bằng ngôn ngữ tự nhiên mà không cần nhờ đến Data Analyst.
- **Hoạt động ổn định, phân đoạn thông minh**: Chia nhỏ dữ liệu thành các batch (50 dòng/lần) để đảm bảo không bị nghẽn mạng hay tràn bộ nhớ database.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Oracle Database**: Có quyền tạo bảng và cấu hình Select AI (hỗ trợ `DBMS_CLOUD_AI`).
- **Azure OpenAI API**: Tài khoản Azure OpenAI đã deploy model LLM để tích hợp với Select AI.
- **Credentials trong n8n**:
  - `oracleDBApi`: Thông tin kết nối Oracle Database (Host, Database/Service Name, User, Password, Port).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 16 nodes được chia làm 2 luồng chính: Workflow A (Ingest Excel & Đăng ký Select AI) và Workflow B (Chat trực tiếp với dữ liệu).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Cấu hình thông tin Oracle Database**:
  Click vào các node liên quan đến database như `Create Oracle Table`, `Insert Rows into Oracle`, và `Register with Select AI`, chọn `oracleDBApi` credential và điền đầy đủ:
  - **Host**: Địa chỉ máy chủ Oracle DB của sếp.
  - **Database**: Service name hoặc SID.
  - **User / Password**: Thông tin tài khoản truy cập.
  - **Port**: `1521` (mặc định).

- **Node `Insert Rows into Oracle`**:
  - Nhớ thay thế chuỗi `YOUR_SCHEMA_NAME` thành schema thực tế trên cơ sở dữ liệu Oracle của sếp (ví dụ: `ADMIN`, `SCOTT`, v.v.).

- **Node `Configure Select AI Settings` & `Configure Select AI Profile`**:
  - Cập nhật đối tượng cấu hình `selectAIConfig` tích hợp thông tin kết nối Azure OpenAI và profile AI phù hợp với hạ tầng Oracle của sếp.

- **Node `Split into Batches`**:
  - Mặc định chia 50 dòng cho mỗi batch nạp dữ liệu. Các sếp có thể điều chỉnh con số này tùy thuộc vào dung lượng file Excel và hiệu năng của Oracle Database.

#### 3. Kích hoạt ⚡️
- Gửi một request mẫu qua Webhook endpoint (`/upload-excel`) bằng Postman hoặc cURL kèm theo file Excel để test luồng nạp dữ liệu (Workflow A).
- Sử dụng `Chat Input` (`chatTrigger`) để thử nghiệm tính năng hỏi đáp với dữ liệu vừa nạp (Workflow B).
- Sau khi test thành công, bấm nút **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh Chat nội bộ**: Thay thế `Chat Input` mặc định bằng node **Telegram Trigger** hoặc **Slack** để nhân viên có thể chat trực tiếp với dữ liệu Excel ngay trên ứng dụng chat của công ty.
- **Lưu lịch sử chat (Logging)**: Thêm một node Google Sheets hoặc một bảng phụ trên Oracle để lưu lại các câu hỏi của người dùng và câu trả lời từ AI phục vụ cho việc kiểm tra chất lượng (Audit).
- **Cảnh báo lỗi tự động**: Nối thêm nhánh Error Trigger để nếu file Excel có định dạng sai hoặc lỗi kết nối Oracle, hệ thống sẽ tự động bắn tin nhắn cảnh báo về kênh Telegram của bộ phận IT.

### 📌 Kết luận
Với workflow n8n này, việc đưa dữ liệu từ Excel lên hệ thống enterprise như Oracle Database và khai thác chúng bằng AI đã trở nên dễ dàng hơn bao giờ hết. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tối ưu hóa năng suất xử lý dữ liệu ngay hôm nay!