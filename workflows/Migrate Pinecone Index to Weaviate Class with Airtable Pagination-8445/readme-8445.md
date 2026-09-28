---
title: "🚀 Tự động chuyển đổi dữ liệu Vector từ Pinecone sang Weaviate với Airtable Pagination trong n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để tự động migration hàng loạt vector database từ Pinecone sang Weaviate sử dụng phân trang lưu qua Airtable."
slug: "chuyen-doi-vector-pinecone-sang-weaviate-n8n"
tags: [n8n, automation, pinecone, weaviate, airtable, vector-database, ai]
keywords: [n8n workflow, migrate pinecone to weaviate, airtable pagination, vector database migration, n8n automation]
keywords: [n8n workflow, migrate pinecone to weaviate, airtable pagination, vector database migration, n8n automation]
---

# 🚀 Tự động chuyển đổi dữ liệu Vector từ Pinecone sang Weaviate với Airtable Pagination

Trong các dự án AI và LLM, việc chuyển đổi hạ tầng Vector Database (như từ Pinecone sang Weaviate) là một bài toán khó khăn khi lượng dữ liệu lớn và cần phân trang (pagination) liên tục để tránh quá tải API. Việc làm thủ công vừa tốn thời gian, dễ sót dữ liệu vừa khó kiểm soát trạng thái.

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quá trình trích xuất vector từ Pinecone, định dạng lại cấu trúc và đẩy lên Weaviate theo từng trang, kết hợp Airtable để lưu trữ `Pagination Token` giúp quá trình chạy ngắt quãng an toàn, không sợ mất trạng thái.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt khi xử lý lượng vector lớn), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần can thiệp thủ công vào từng trang vector.
- **Quản lý trạng thái thông minh:** Sử dụng Airtable để lưu token trang tiếp theo (`Next Page Token`), cho phép tạm dừng và tiếp tục migration bất cứ lúc nào.
- **Xử lý hàng loạt (Batching):** Giúp tối ưu hóa tài nguyên API của cả Pinecone và Weaviate, tránh lỗi Timeout hoặc Rate Limit.
- **Hoạt động bền bỉ:** Có cơ chế kiểm tra điều kiện kết thúc (`Is Next Pagination Token null?`) để tự động đóng quy trình khi hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Pinecone** cùng thông tin Index URL và Namespace.
- Tài khoản **Weaviate** cùng Cluster REST Endpoint và thông tin Collection mục tiêu.
- Tài khoản **Airtable** với bảng quản lý trạng thái (có 2 cột: `Name` và `Number`, khởi tạo sẵn bản ghi `INIT,0`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ hệ thống hoặc copy đoạn mã JSON được cung cấp, sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:
- **Parameters (`set`):** Điền các tham số cốt lõi bao gồm Endpoint của Pinecone, Namespace, giới hạn đọc mỗi request (Read limit - tối đa 100 với Pinecone), tên collection đích và Cluster Endpoint của Weaviate.
- **Get Next Page Token & Save Next Page Token (`airtable`):** Kết nối tài khoản Airtable và trỏ tới đúng Base/Table dùng để lưu trạng thái trang. Đảm bảo bảng đã có sẵn record khởi tạo `(INIT, 0)`.
- **Fetch Vectors (`httpRequest`):** Cấu hình API Key của Pinecone để gọi dữ liệu vector.
- **LoadWeAviate (`httpRequest`):** Cấu hình Header và API Key để đẩy dữ liệu đã được định dạng sang Weaviate Cluster.
- **Format2Weaviate & Prepare Fetch Body (`code`):** Kiểm tra cấu trúc dữ liệu JavaScript trong các node này nếu Schema vector của các sếp có sự thay đổi về metadata hoặc dimensions.

#### 3. Kích hoạt ⚡️
- Chạy thử công (Test run) thủ công qua nút **Execute Workflow** để kiểm tra trang dữ liệu đầu tiên từ Pinecone sang Weaviate.
- Kiểm tra Airtable xem `Next Page Token` đã được cập nhật chưa.
- Bật công tắc **Active** để workflow chạy tự động theo lịch trình (`Schedule Trigger`).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** vào nhánh `Migration completed` để nhận thông báo ngay khi quá trình chuyển đổi hàng triệu vector hoàn tất.
- **Ghi log lỗi:** Thêm nhánh Error Trigger để gửi cảnh báo về email hoặc chat nếu API Pinecone/Weaviate gặp sự cố gián đoạn mạng.
- **Tùy chỉnh lịch chạy:** Điều chỉnh `Schedule Trigger` chạy vào khung giờ thấp điểm (ban đêm) để tối ưu băng thông và tài nguyên hệ thống.

### 📌 Kết luận
Với workflow n8n này, bài toán chuyển đổi vector database phức tạp từ Pinecone sang Weaviate nay đã trở nên đơn giản, trực quan và an toàn tuyệt đối nhờ cơ chế phân trang thông minh. Hãy "lên đồ" ngay cho hệ thống AI của các sếp nào!