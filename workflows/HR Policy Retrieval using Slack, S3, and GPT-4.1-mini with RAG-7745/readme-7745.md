---
title: "🤖 Xây dựng Trợ lý AI Tra cứu Chính sách Nhân sự trên Slack với RAG, AWS S3 và GPT-4o-mini"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình trả lời câu hỏi chính sách nhân sự (HR Policy) trên Slack sử dụng công nghệ RAG, kết hợp AWS S3 và OpenAI."
slug: "tro-ly-ai-tra-cuu-chinh-sach-nhan-su-slack-rag-s3"
tags: [n8n, automation, no-code, AI RAG, Slack, OpenAI, AWS S3]
keywords: [n8n workflow, trợ lý AI nhân sự, RAG n8n, Slackbot AI, OpenAI GPT-4o-mini, AWS S3 n8n]
---

# 🤖 Xây dựng Trợ lý AI Tra cứu Chính sách Nhân sự trên Slack với RAG, AWS S3 và GPT-4o-mini

Các sếp có bao giờ đau đầu khi nhân viên liên tục hỏi đi hỏi lại những câu hỏi quen thuộc: *"Quy chế nghỉ phép năm nay thế nào?"*, *"Thủ tục thanh toán công tác phí ra sao?"* hay *"Bảo hiểm công ty chi trả những gì?"*? Việc HR phải túc trực trả lời thủ công không chỉ tốn thời gian mà còn làm gián đoạn công việc chuyên môn.

Giải pháp ở đây là gì? Hãy để **Trợ lý AI Tra cứu Chính sách Nhân sự (HR Policy Retrieval)** làm thay các sếp! Workflow n8n này sẽ tự động hóa 100% việc đọc hiểu tài liệu chính sách lưu trên **AWS S3**, tích hợp công nghệ **RAG (Retrieval-Augmented Generation)** và trực tiếp giải đáp mọi thắc mắc của nhân viên ngay trên **Slack** một cách chính xác, nhanh chóng và bảo mật.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giải phóng 80% thời gian cho bộ phận HR**: Không còn mất thời gian trả lời lặp lại các câu hỏi chung chung.
- **Tốc độ phản hồi tức thì**: Nhân viên nhận được câu trả lời chính xác dựa trên đúng văn bản quy định của công ty ngay trong kênh Slack 24/7.
- **Độ chính xác cao nhờ RAG**: AI không "bịa" thông tin mà tra cứu trực tiếp từ các tài liệu chính sách được lưu trữ trên AWS S3.
- **Trải nghiệm mượt mà**: Tích hợp sẵn bộ nhớ đệm hội thoại (Memory), giúp AI hiểu được ngữ cảnh các câu hỏi trước đó.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI** (để lấy API Key sử dụng cho các model GPT và Embeddings).
- **Tài khoản AWS** (với quyền truy cập S3 để lưu trữ và tải tài liệu chính sách).
- **Workspace Slack** (có quyền cài đặt Bot/App để lắng nghe tin nhắn và gửi phản hồi).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ n8n template (ID: 7745), sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Slack Trigger & Send a message**: Kết nối tài khoản Slack của công ty. Node này làm nhiệm vụ lắng nghe câu hỏi từ nhân viên và gửi câu trả lời trả về kênh Slack tương ứng.
- **S3 Document Downloader & Document Loader**: Cấu hình thông tin kết nối AWS S3 Credentials để hệ thống có thể truy cập vào kho chứa tài liệu chính sách nhân sự (PDF, Word, TXT...).
- **Knowledge Base Embeddings & Knowledge Base Embeddings Generator**: Nhập OpenAI API Key để tạo vector embeddings cho tài liệu, giúp AI hiểu và tìm kiếm văn bản thông minh.
- **Conversation Model & Knowledge Base Response Chat Model**: Cấu hình model OpenAI (khuyên dùng `gpt-4o-mini` để tối ưu chi phí và tốc độ) cho cả chatbot tương tác và phần sinh câu trả lời RAG.
- **Simple Memory (Memory Buffer Window)**: Giúp chatbot ghi nhớ ngữ cảnh trò chuyện ngắn hạn của người dùng trong Slack.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài câu hỏi mẫu để kiểm tra kết quả trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa trợ lý AI vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh chat**: Ngoài Slack, các sếp có thể thay thế bằng node Telegram Trigger hoặc Microsoft Teams để phù hợp với văn hóa giao tiếp của công ty.
- **Lưu log câu hỏi**: Thêm một node Google Sheets hoặc Airtable để ghi lại lịch sử câu hỏi của nhân viên, giúp ban quản lý nắm bắt những vấn đề nào nhân viên hay thắc mắc nhất để cải thiện chính sách.
- **Báo cáo định kỳ**: Thiết lập một nhánh workflow phụ gửi thống kê số lượng câu hỏi hàng tuần về một kênh Slack riêng cho đội ngũ HR.

### 📌 Kết luận
Việc tự động hóa tra cứu chính sách nhân sự chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và AI RAG. Hãy triển khai ngay hôm nay để tiết kiệm thời gian, tối ưu hóa vận hành và mang lại trải nghiệm hiện đại cho nhân viên của các sếp!