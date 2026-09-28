---
title: "🚀 Tự động lập dự toán chi phí xây dựng từ hình ảnh với GPT-4 Vision và n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động bóc tách khối lượng và tính dự toán xây dựng từ ảnh chụp công trình sử dụng AI và Vector Database Qdrant."
slug: "tu-dong-du-toan-xay-dung-gpt4-vision-n8n"
tags: [n8n, automation, ai, gpt-4-vision, qdrant, construction, no-code]
keywords: [n8n workflow, dự toán xây dựng, ai construction estimate, gpt-4 vision, qdrant vector search]
---

# 🚀 Tự động lập dự toán chi phí xây dựng từ hình ảnh với GPT-4 Vision & DDC CWICR

Các sếp làm trong ngành xây dựng, thiết kế nội thất hay cải tạo nhà cửa chắc hẳn đều hiểu cảm giác "đau đầu" khi phải ngồi nhìn bản vẽ hoặc hình ảnh hiện trạng để bóc tách khối lượng và làm dự toán (BOQ - Bill of Quantities). Công việc thủ công này không chỉ ngốn hàng giờ đồng hồ, dễ bỏ sót hạng mục mà còn phụ thuộc rất nhiều vào kinh nghiệm của kỹ sư định giá.

Đừng lo, workflow n8n cực kỳ xịn sò được phát triển bởi chuyên gia Artem Boiko (DataDrivenConstruction.io) sẽ giúp các sếp tự động hóa **100% quy trình này**. Hệ thống sẽ nhận ảnh chụp công trình, dùng **GPT-4 Vision** để phân tích không gian, bóc tách cấu kiện, phân rã thành các công tác thi công, kết hợp với cơ sở dữ liệu định mức **DDC CWICR** (qua Vector Database Qdrant) để tra cứu đơn giá, validate dữ liệu và cuối cùng xuất ra một bản báo cáo HTML chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng nhọc, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Biến bức ảnh chụp phòng tắm, nhà bếp hoặc hiện trạng công trình thành bảng dự toán chi tiết chỉ trong vài phút.
- **Độ chính xác cao nhờ AI & RAG:** Ứng dụng GPT-4 Vision phân tích hình ảnh kết hợp tìm kiếm vector trên cơ sở dữ liệu định mức khủng (700,000+ đơn giá).
- **Kiểm soát chất lượng tự động (Validation):** Tự động kiểm tra số lượng công tác, tỷ lệ tìm thấy đơn giá, và cấu trúc hạng mục (Chuẩn bị, Thi công chính, Hoàn thiện, MEP).
- **Báo cáo chuyên nghiệp:** Xuất file HTML trực quan với biểu đồ cơ cấu chi phí, tiến độ và liên kết tra cứu. Hỗ trợ đa ngôn ngữ/khu vực (Berlin, Toronto, Paris, Dubai...).
:::

### 📦 Tổng quan Pipeline (25 Nodes)
| Stage | Mô tả hoạt động |
|-------|-----------------|
| **Block 1** | Nhận ảnh từ Web Form (`Photo Upload Form`), trích xuất cấu hình ngôn ngữ/vùng, kiểm tra ảnh (`Has Photo?`). |
| **Stage 1** | GPT-4 Vision (`STAGE 1 Analyze Photo`) phân tích không gian, nhận diện vật liệu và cấu kiện từ ảnh. |
| **Stage 4** | Phân rã cấu kiện thành các công tác thi công chi tiết (`STAGE 4 Decompose LLM`). |
| **Stage 5** | Vòng lặp (`Loop Works`) qua từng công tác, thực hiện tìm kiếm vector (`Vector Search`) trên Qdrant với embedding `text-embedding-3-large`. |
| **Stage 5.2** | Phân tích và chấm điểm kết quả tìm kiếm đơn giá (`STAGE 5.2 Parse & Score`). |
| **Stage 7.5** | Kiểm tra và xác thực các hạng mục (Tối thiểu 3 công tác, tỷ lệ tìm thấy > 50%,...). |
| **Stage 9** | Tổng hợp dữ liệu và xuất báo cáo HTML (`STAGE 9 HTML Report`). |

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted trên VPS).
- **OpenAI API Key:** Cần thiết cho GPT-4 Vision, GPT-4 (Decompose) và OpenAI Embeddings (`text-embedding-3-large`).
- **Qdrant Vector Database:** Đã cài đặt Qdrant (local hoặc cloud) chứa bộ dữ liệu định mức xây dựng **DDC CWICR** (tải miễn phí từ [GitHub DataDrivenConstruction](https://github.com/datadrivenconstruction)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã nguồn JSON của workflow hoặc tải file JSON từ nguồn cấp.
- Mở n8n Editor, chọn **Workflows** -> **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các Credentials và thông số sau trong workflow:
- **GPT-4 Vision (`GPT-4 Vision` node) & GPT-4 Decompose (`GPT-4 Decompose` node):** Chọn credential OpenAI API đã chuẩn bị. Model mặc định đang dùng `chatgpt-4o-latest` (hoặc có thể thay thế bằng Claude 3.5, Gemini Pro nếu muốn).
- **Embeddings (`Embeddings` node):** Cấu hình OpenAI Embeddings với model `text-embedding-3-large`.
- **Vector Search (`Vector Search` node - Qdrant):** Thêm Qdrant API credentials, trỏ tới collection tương ứng với vùng/ngôn ngữ đã tải dataset DDC CWICR lên.
- **Form Trigger (`Photo Upload Form` node):** Nơi người dùng tải ảnh lên (hỗ trợ JPG, PNG, WebP). Các sếp có thể tuỳ chỉnh giao diện form thu thập thông tin nếu cần.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách tải lên một bức ảnh chụp không gian nội thất (nhà bếp, phòng tắm,...).
- Kiểm tra kết quả trả về ở node `Final HTML Output`.
- Sau khi test ngon lành, bật **Active workflow** để đưa hệ thống vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để ngay khi khách hàng/nhân viên submit ảnh và hoàn tất tính toán, bot sẽ gửi thẳng link báo cáo HTML về group chat.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các lần báo giá kèm link ảnh và tổng chi phí phục vụ việc chăm sóc khách hàng sau này.
- **Mở rộng đa ngôn ngữ:** Tận dụng 9 vùng địa lý có sẵn trong dataset DDC CWICR để mở rộng dịch vụ báo giá xây dựng quốc tế.

### 📌 Kết luận
Workflow tích hợp AI Vision và Vector Database này là một "vũ khí tối tân" giúp tối ưu hóa quy trình định giá xây dựng, tiết kiệm 90% thời gian bóc tách khối lượng thủ công. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tạo lợi thế cạnh tranh vượt trội trong kỷ nguyên số hóa!