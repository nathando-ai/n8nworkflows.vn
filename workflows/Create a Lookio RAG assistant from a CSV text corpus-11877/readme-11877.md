---
title: "🚀 Xây Dựng Trợ Lý RAG Thông Minh Từ Dữ Liệu CSV Với Lookio"
description: "Hướng dẫn chi tiết cách tự động hóa việc nạp dữ liệu CSV vào Lookio để tạo trợ lý AI RAG, giúp doanh nghiệp khai thác tri thức nội bộ nhanh chóng và chính xác."
slug: "xay-dung-try-li-rag-lookio-tu-csv"
tags: [n8n, automation, no-code, RAG, Lookio, AI]
keywords: [n8n workflow, tự động hóa RAG, Lookio API, xử lý dữ liệu CSV, AI assistant]
---

# 🚀 Xây Dựng Trợ Lý RAG Thông Minh Từ Dữ Liệu CSV Với Lookio

Trong kỷ nguyên của AI, việc biến các tập dữ liệu thô (như bảng tính CSV, tài liệu nội bộ) thành một trợ lý AI có khả năng trả lời câu hỏi dựa trên chính dữ liệu của doanh nghiệp là xu hướng tất yếu. Tuy nhiên, quy trình thủ công thường gặp nhiều "nỗi đau":

1.  **Dữ liệu lớn:** File CSV có thể chứa hàng nghìn dòng, không thể copy-paste trực tiếp vào giao diện Lookio.
2.  **Định dạng phức tạp:** Lookio yêu cầu dữ liệu được cấu trúc và nạp qua API hoặc file upload chuẩn, trong khi CSV thường cần được xử lý, tách nhỏ (chunking) hoặc chuyển đổi định dạng.
3.  **Thiếu tính tự động:** Mỗi lần cập nhật dữ liệu mới, nhân viên phải làm lại từ đầu, tốn thời gian và dễ sai sót.

Workflow **Create a Lookio RAG assistant from a CSV text corpus** do chuyên gia Guillaume Duvernay phát triển chính là giải pháp "chìa khóa trao tay". Nó tự động hóa toàn bộ quy trình: Nhận file CSV -> Xử lý dữ liệu -> Nạp vào Lookio -> Tạo trợ lý RAG. Các sếp chỉ cần upload file, hệ thống sẽ lo phần còn lại.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý các file dữ liệu lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần code, chỉ cần upload file CSV là có ngay trợ lý AI dựa trên dữ liệu của mình.
- **Xử lý dữ liệu lớn:** Workflow sử dụng cơ chế `Split In Batches` để xử lý từng phần dữ liệu, tránh lỗi timeout hay vượt giới hạn kích thước API.
- **Chính xác & Cập nhật:** Dữ liệu được nạp trực tiếp vào Lookio, đảm bảo trợ lý AI luôn phản ánh đúng tri thức nội bộ mới nhất.
- **Tiết kiệm thời gian:** Rút ngắn thời gian triển khai trợ lý RAG từ vài giờ (làm thủ công) xuống còn vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản self-hosted hoặc cloud.
- **Tài khoản Lookio:** Các sếp cần có API Key của Lookio để workflow có thể gọi API nạp dữ liệu.
- **File dữ liệu CSV:** File chứa nội dung văn bản (text corpus) muốn dùng để huấn luyện trợ lý AI.
- **Hiểu biết cơ bản về RAG:** Nắm rõ khái niệm Retrieval-Augmented Generation để tối ưu câu hỏi cho trợ lý.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1.  Tải xuống file JSON của workflow từ link gốc: [n8n.io/workflows/11877](https://n8n.io/workflows/11877).
2.  Mở n8n Editor, chọn **Import from File** hoặc **Import from URL**.
3.  Chọn file JSON vừa tải về. Workflow sẽ xuất hiện trong canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dựa trên các nodes chính trong workflow (`Form Trigger`, `Set`, `Split In Batches`, `HTTP Request`, `ConvertToFile`, `ExtractFromFile`), các sếp cần cấu hình các điểm sau:

*   **Node: Form Trigger (n8n-nodes-base.formTrigger)**
    *   Đây là điểm bắt đầu. Workflow sẽ tạo một form web để các sếp upload file CSV.
    *   **Cấu hình:** Kiểm tra tên trường (field name) của file upload (ví dụ: `csvFile`) để đảm bảo khớp với các node xử lý dữ liệu phía sau.

*   **Node: Set (n8n-nodes-base.set)**
    *   Node này thường dùng để chuẩn bị biến môi trường hoặc cấu hình ban đầu.
    *   **Cấu hình:** Kiểm tra các biến như `Lookio_API_Key`, `Project_ID` hoặc `Collection_Name`. Các sếp cần điền đúng thông tin tài khoản Lookio của mình vào đây hoặc tham chiếu từ Environment Variables.

*   **Node: Split In Batches (n8n-nodes-base.splitInBatches)**
    *   **Vai trò quan trọng:** Tách dữ liệu CSV thành các batch nhỏ để xử lý tuần tự. Điều này giúp tránh lỗi khi file CSV quá lớn.
    *   **Cấu hình:** Điều chỉnh tham số `Batch Size` (số dòng xử lý mỗi lần). Nếu file nhỏ, có thể tăng lên; nếu file lớn, nên giảm xuống (ví dụ: 10-50 dòng/batch) để ổn định.

*   **Node: HTTP Request (n8n-nodes-base.httpRequest)**
    *   **Vai trò:** Gọi API của Lookio để nạp dữ liệu (upload documents/chunks).
    *   **Cấu hình:**
        *   **Method:** POST.
        *   **URL:** Endpoint API của Lookio (thường là `https://api.lookio.com/v1/...`).
        *   **Headers:** Thêm `Authorization: Bearer [YOUR_API_KEY]`.
        *   **Body:** Đảm bảo cấu trúc JSON body khớp với tài liệu API của Lookio (thường là mảng các object chứa `text` và `metadata`).

*   **Node: ConvertToFile & ExtractFromFile**
    *   Các node này hỗ trợ chuyển đổi dữ liệu từ dạng JSON/CSV sang file hoặc ngược lại nếu cần.
    *   **Lưu ý:** Đảm bảo encoding UTF-8 để tránh lỗi ký tự tiếng Việt trong dữ liệu CSV.

*   **Node: Aggregate (n8n-nodes-base.aggregate)**
    *   Tổng hợp kết quả từ các batch đã xử lý để báo cáo trạng thái thành công/thất bại.

#### 3. Kích hoạt ⚡️
1.  **Test Run:**
    *   Click vào nút **Test** ở Form Trigger.
    *   Upload một file CSV mẫu nhỏ (10-20 dòng) để kiểm tra luồng dữ liệu.
    *   Quan sát từng node: Dữ liệu có được tách batch đúng không? API Lookio có trả về mã 200 không?
2.  **Bật Active:**
    *   Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
    *   Copy link Form để chia sẻ cho team hoặc dùng nội bộ.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước xác thực:** Nếu chia sẻ link Form công khai, hãy thêm một node `If` hoặc `Code` để kiểm tra API Key hoặc email người dùng trước khi cho phép upload, tránh bị spam dữ liệu rác.
- **Gửi thông báo qua Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau node `Aggregate` để gửi thông báo "Dữ liệu đã nạp thành công" hoặc "Lỗi" cho quản trị viên.
- **Lịch trình tự động (Cron):** Thay vì dùng Form Trigger, các sếp có thể thay bằng `Cron Trigger` và `Google Drive` hoặc `S3` để tự động kiểm tra và nạp dữ liệu mới từ một thư mục cố định mỗi ngày.
- **Xử lý lỗi chi tiết:** Trong node `HTTP Request`, bật `On Error: Continue` và thêm logic để log lỗi cụ thể (ví dụ: dòng nào trong CSV bị lỗi định dạng) vào Google Sheets để dễ dàng debug.

### 📌 Kết luận
Việc xây dựng một trợ lý RAG từ dữ liệu CSV không còn là việc phức tạp dành riêng cho các kỹ sư AI. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình, biến dữ liệu thô thành tri thức có giá trị, hỗ trợ ra quyết định nhanh chóng và chính xác. Hãy thử ngay để trải nghiệm sức mạnh của AI RAG kết hợp với n8n!