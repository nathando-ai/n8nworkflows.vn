---
title: "🚀 Tự Động Hóa Báo Giá Thông Minh Với OpenAI, Qdrant AI và CraftMyPDF trên n8n"
description: "Xây dựng hệ thống tự động tạo và gửi báo giá cá nhân hóa cho khách hàng sử dụng AI RAG (OpenAI, Qdrant Vector Store) kết hợp sinh file PDF chuyên nghiệp."
slug: "tu-dong-hoa-bao-gia-ai-qdrant-craftmypdf-n8n"
tags: [n8n, automation, ai-rag, openai, qdrant, craftmypdf]
keywords: [n8n workflow, tao bao gia tu dong, ai rag, qdrant vector store, craftmypdf, openai automation]
---

# 🚀 Tự Động Hóa Báo Giá Thông Minh Với OpenAI, Qdrant AI và CraftMyPDF

Trong quy trình bán hàng B2B hoặc dịch vụ phức tạp, việc soạn thảo các bản báo giá (Sales Quote) chi tiết, chính xác dựa trên danh mục sản phẩm khổng lồ thường ngốn rất nhiều thời gian của đội ngũ sales. Nếu làm thủ công, khách hàng có thể phải chờ đợi lâu, làm giảm tỷ lệ chốt đơn. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách ứng dụng **AI RAG (Retrieval-Augmented Generation)**. Hệ thống sẽ tự động tiếp nhận yêu cầu từ Form, truy vấn kho sản phẩm thông minh qua **Qdrant**, sử dụng **OpenAI** để phân tích và tổng hợp nội dung báo giá, sau đó thiết kế file PDF chuyên nghiệp bằng **CraftMyPDF** và gửi thẳng tới email khách hàng trong vòng chưa đầy 1 phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ phản hồi thần tốc**: Khách hàng nhận được báo giá chi tiết ngay sau khi vừa bấm gửi form yêu cầu.
- **Cá nhân hóa đỉnh cao**: AI tự động chọn lọc sản phẩm, tính toán cấu hình phù hợp nhất với nhu cầu riêng biệt của từng khách hàng từ cơ sở dữ liệu Qdrant.
- **Chuyên nghiệp hóa thương hiệu**: File báo giá xuất ra định dạng PDF đẹp mắt, chuẩn chỉnh thông qua CraftMyPDF mà không cần can thiệp thủ công.
- **Vận hành 24/7 tự động 100%**: Giải phóng đội ngũ sales khỏi các tác vụ hành chính lặp đi lặp lại để tập trung vào việc chốt deal.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **OpenAI API Key** (Dành cho LLM Chat Model và Embeddings).
- **Google Gemini API Key** (Dành cho model dự phòng hoặc bổ trợ).
- **Qdrant Vector Database** (Đã lưu sẵn thông tin sản phẩm/dịch vụ của doanh nghiệp).
- **CraftMyPDF API Key** (Tài khoản tạo template PDF).
- **SMTP Server / Email Credential** (Để gửi email tự động chứa file PDF báo giá).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc tải file JSON gốc từ nguồn, sau đó mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào bảng làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình lại các node cốt lõi sau đây để hệ thống nhận diện đúng tài nguyên:
- **Form: Request a Quote (`formTrigger`)**: Thiết lập các trường thông tin đầu vào mà khách hàng cần điền (Họ tên, Công ty, Yêu cầu chi tiết, Ngân sách...).
- **Qdrant Vector Store (Products) (`vectorStoreQdrant`) & Embeddings OpenAI (`embeddingsOpenAi`)**: Điền thông tin kết nối tới cụm Qdrant Vector Database của doanh nghiệp để AI có thể tra cứu thông tin sản phẩm chính xác.
- **OpenAI Chat Model (Agent) & Google Gemini Chat Model**: Chọn đúng Credential API đã đăng ký của OpenAI và Google.
- **Sales Quote Agent (`agent`)**: Kiểm tra lại System Prompt của Agent, đảm bảo AI hiểu rõ ngữ cảnh, cách thức tư vấn và giới hạn sản phẩm.
- **Create a PDF (`n8n-nodes-craftmypdf.craftMyPdf`)**: Liên kết với tài khoản CraftMyPDF và chọn Template ID báo giá được thiết kế sẵn trên hệ thống này.
- **Email: Send Quote (`emailSend`)**: Cấu hình thông tin người gửi (SMTP), tiêu đề và nội dung email kèm file PDF được tải về từ node **Get PDF file**.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách submit thử một form mẫu để kiểm tra toàn bộ luồng từ AI trả kết quả, tạo PDF cho đến gửi email.
- Sau khi kiểm tra mọi thứ hoạt động hoàn hảo, hãy gạt công tắc sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc phụ**: Thêm node **Telegram** hoặc **Slack** ngay sau khi có form gửi đến để bắn thông báo "Có khách hàng mới yêu cầu báo giá!" cho sếp và đội ngũ sales.
- **Lưu trữ dữ liệu khách hàng**: Thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử yêu cầu báo giá của khách hàng phục vụ cho việc chăm sóc sau bán hàng (Lead Nurturing).
- **Cải tiến Template PDF**: Tùy biến template trên CraftMyPDF có thêm mã QR code hoặc điều khoản hợp đồng tự động để nâng cao tỷ lệ chốt đơn.

### 📌 Kết luận
Workflow tích hợp AI RAG và CraftMyPDF là một vũ khí cực kỳ mạnh mẽ giúp tự động hóa khâu tiền kỳ trong bán hàng. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất doanh nghiệp và mang lại trải nghiệm chuyên nghiệp tuyệt đối cho khách hàng của các sếp!