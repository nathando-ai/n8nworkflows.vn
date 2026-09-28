---
title: "🚀 Tự động đồng bộ dữ liệu lớn từ Hugging Face sang MongoDB với n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để di chuyển các tập dữ liệu lớn từ Hugging Face API sang MongoDB theo từng batch thông qua subworkflow một cách tối ưu."
slug: "dong-bo-du-lieu-hugging-face-sang-mongodb-n8n"
tags: [n8n, automation, huggingface, mongodb, datamigration, no-code]
keywords: [n8n workflow, migrate huggingface to mongodb, tu dong hoa du lieu, hugging face api, mongodb insert]
---

# 🚀 Tự động đồng bộ dữ liệu lớn từ Hugging Face sang MongoDB với n8n

Việc di chuyển (migrate) các tập dữ liệu AI/ML khổng lồ từ Hugging Face vào cơ sở dữ liệu MongoDB thường gặp nhiều thách thức như tràn bộ nhớ (RAM), giới hạn timeout của API hoặc nghẽn cổ chai khi xử lý hàng triệu bản ghi cùng lúc. Thay vì viết script Python phức tạp, bài toán này có thể được giải quyết triệt để bằng một hệ thống tự động hóa 100% không cần code (No-code) với n8n.

Workflow này sử dụng cấu trúc **Looping Subworkflow** thông minh, cho phép tải dữ liệu theo từng batch (phân trang), chuyển đổi cấu trúc dữ liệu và đẩy vào MongoDB một cách an toàn, ổn định.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 đối với các tác vụ xử lý dữ liệu lớn (Big Data migration), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Xử lý dữ liệu lớn không sợ tràn RAM:** Nhờ cơ chế chia nhỏ thành các batch (phân trang theo offset/length), hệ thống có thể đồng bộ hàng triệu dòng từ Hugging Face mượt mà.
- **Tự động hóa hoàn toàn quy trình:** Từ việc gọi API, bóc tách dữ liệu, làm sạch (_id cũ) cho đến ghi dữ liệu vào MongoDB.
- **Linh hoạt cấu hình:** Dễ dàng thay đổi tên dataset, kích thước batch (mặc định 100 dòng/batch) ngay tại node cấu hình ban đầu.
- **Hoạt động liên tục & đáng tin cậy:** Cơ chế vòng lặp tự động gọi subworkflow cho đến khi toàn bộ dữ liệu được đồng bộ xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyến nghị phiên bản mới nhất).
- **MongoDB Database:** Đã có tài khoản MongoDB (Atlas hoặc Self-hosted) và thông tin kết nối (Connection String).
- **Hugging Face Dataset:** Tên dataset công khai hoặc API endpoint hợp lệ trên Hugging Face.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste toàn bộ mã nguồn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Node `Config_Start` (Set):** Nơi khai báo tên dataset, cấu hình split (ví dụ: `train`, `test`) và kích thước batch (`length`, mặc định là 100).
- **Node `HF_FetchRows` (HTTP Request):** Đảm bảo URL trỏ chính xác đến Hugging Face Dataset Server API để lấy dữ liệu đúng định dạng.
- **Node `Mongo_InsertOrUpsert` (MongoDB):** 
  - Chọn Credentials kết nối MongoDB của các sếp.
  - Chỉ định Database và Target Collection cụ thể.
- **Node `Transform_RemoveId_AddMeta` (Code):** Node này có nhiệm vụ loại bỏ trường `_id` mặc định do Hugging Face sinh ra (giúp MongoDB tự động tạo `ObjectId` mới tránh xung đột) và bổ sung thêm metadata nếu cần.
- **Node `InsertBatch` (Execute Workflow):** Cập nhật ID của subworkflow thực thi batch để vòng lặp (`ContinueLoop?`) hoạt động chính xác.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Trigger_Manual`) với một dataset nhỏ để kiểm tra dữ liệu đã vào MongoDB thành công chưa.
- Sau khi test OK, bật trạng thái **Active** để workflow sẵn sàng vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node thông báo ở cuối vòng lặp (khi `ContinueLoop?` trả về false) để nhận tin nhắn báo cáo khi quá trình migrate hàng triệu bản ghi hoàn tất.
- **Ghi log tiến trình:** Lưu lại số lượng bản ghi đã chạy vào một bảng Google Sheets hoặc một collection log riêng trên MongoDB để dễ dàng theo dõi tiến độ.
- **Xử lý lỗi (Error Handling):** Thêm nhánh `Error Trigger` để tự động ghi lại các batch bị lỗi do mất mạng hoặc lỗi API từ phía Hugging Face.

### 📌 Kết luận
Việc di chuyển tập dữ liệu lớn giờ đây đã trở nên đơn giản hơn bao giờ hết với kiến trúc looping subworkflow trên n8n. Hãy áp dụng ngay giải pháp này để tiết kiệm hàng giờ viết code thủ công và tối ưu hóa hệ thống dữ liệu AI của doanh nghiệp các sếp!