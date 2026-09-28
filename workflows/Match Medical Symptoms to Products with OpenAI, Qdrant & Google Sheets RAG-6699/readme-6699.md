---
title: "🚀 Tự động hóa tư vấn y tế thông minh với RAG: OpenAI, Qdrant & Google Sheets trong n8n"
description: "Hướng dẫn xây dựng hệ thống AI RAG tư vấn triệu chứng bệnh và đề xuất sản phẩm y tế tự động bằng n8n, OpenAI, Qdrant Vector DB và Google Sheets."
slug: "tu-dong-hoa-tu-van-y-te-rag-openai-qdrant-google-sheets"
tags: [n8n, automation, ai-rag, openai, qdrant, google-sheets]
keywords: [n8n workflow, rag y te, openai n8n, qdrant vector store, google sheets automation]
use strict: true
---

# 🚀 Tự động hóa tư vấn y tế thông minh với RAG: OpenAI, Qdrant & Google Sheets

Trong ngành y tế và chăm sóc sức khỏe, việc tư vấn đúng sản phẩm, thuốc hoặc thực phẩm chức năng dựa trên triệu chứng của khách hàng đóng vai trò cốt lõi để chốt đơn và tạo lòng tin. Tuy nhiên, nếu làm thủ công, nhân viên phải tra cứu hàng trăm sản phẩm khác nhau, rất dễ dẫn đến sai sót hoặc chậm trễ phản hồi.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách ứng dụng mô hình **RAG (Retrieval-Augmented Generation)** kết hợp giữa **OpenAI**, **Qdrant Vector Database** và **Google Sheets**. Hệ thống sẽ tự động học dữ liệu sản phẩm từ Google Sheets, lưu trữ vào vector database và cho phép AI tư vấn chính xác 100% dựa trên ngữ cảnh thực tế.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tư vấn tự động 24/7:** AI trò chuyện trực tiếp với khách hàng, lắng nghe triệu chứng và đưa ra gợi ý sản phẩm cực kỳ chuẩn xác.
- **Dữ liệu luôn cập nhật:** Chỉ cần thêm sản phẩm mới vào Google Sheets, hệ thống tự động đồng bộ vào Qdrant Vector DB.
- **Cá nhân hóa cao:** Nhờ kết hợp `Store Chats` (Memory Buffer), AI nhớ được lịch sử trò chuyện để tư vấn xuyên suốt, không bị quên ngữ cảnh.
- **Tiết kiệm thời gian:** Giảm tải 90% khối lượng công việc tra cứu danh mục sản phẩm cho đội ngũ chăm sóc khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **OpenAI API Key:** Dành cho LLM (`OpenAI LLM`) và tạo Embedding (`Create Embedding`, `Create Embedding2`).
- **Qdrant Vector Database:** Tài khoản Qdrant Cloud hoặc Self-hosted instance để lưu trữ vector sản phẩm.
- **Google Sheets:** File Google Sheets chứa danh sách sản phẩm, công dụng và triệu chứng đi kèm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc copy toàn bộ JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Get all products (Google Sheets):** Kết nối tài khoản Google của các sếp, chọn đúng file Sheet chứa danh sách sản phẩm y tế và cấu hình lấy dữ liệu đầu vào.
- **Create Embedding & Create Embedding2:** Nhập OpenAI API Credentials để chuyển đổi văn bản sản phẩm thành dạng vector.
- **Qdrant Vector Database & Get data from Qdrant database:** Cấu hình URL và API Key của Qdrant Database để đồng bộ và truy vấn dữ liệu ngữ cảnh (Retrieval).
- **RAG Agent & OpenAI LLM:** Cấu hình mô hình OpenAI (khuyên dùng `gpt-4o` hoặc `gpt-4o-mini`) và kết nối bộ nhớ `Store Chats` (`Memory Buffer Window`) để duy trì ngữ cảnh trò chuyện.
- **When chat message received:** Điểm chạm đầu vào để nhận tin nhắn từ người dùng/khách hàng.

#### 3. Kích hoạt ⚡️
- Bấm nút **"When clicking ‘Execute workflow’"** để chạy thử tiến trình đồng bộ dữ liệu từ Google Sheets sang Qdrant Vector DB.
- Test thử tính năng chat thông qua `When chat message received`.
- Khi mọi thứ hoạt động trơn tru, bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat đa nền tảng:** Thay thế hoặc kết nối thêm node Telegram, Messenger hoặc Slack vào `When chat message received` để tư vấn khách hàng trực tiếp trên mạng xã hội.
- **Lưu lịch sử hội thoại:** Thêm node Google Sheets hoặc Database ở cuối luồng để lưu lại thông tin tư vấn và SĐT khách hàng làm Lead Nurturing.
- **Báo cáo định kỳ:** Tạo một nhánh phụ gửi email hoặc tin nhắn báo cáo tổng hợp các sản phẩm được khách hàng hỏi nhiều nhất trong tuần qua Slack.

### 📌 Kết luận
Workflow RAG kết hợp OpenAI, Qdrant và Google Sheets là giải pháp tối ưu giúp tự động hóa khâu tư vấn y tế và sản phẩm. Hãy triển khai ngay hôm nay để nâng cấp hệ thống CSKH của các sếp lên một tầm cao mới!