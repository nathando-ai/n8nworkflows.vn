---
title: "🚀 Tự động liên kết bản ghi NocoDB qua API với n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n để tự động hóa việc liên kết các bản ghi Many-to-Many trong NocoDB thông qua REST API một cách nhanh chóng và chính xác."
slug: "lien-ket-ban-ghi-nocodb-qua-api-n8n"
tags: [n8n, automation, nocodb, api, no-code, database]
keywords: [n8n workflow, nocodb link records, tự động hóa nocodb, n8n nocodb api, quan hệ many to many nocodb]
---

# 🚀 Tự động liên kết bản ghi NocoDB qua API với n8n

Việc quản lý cơ sở dữ liệu quan hệ (relational database) như NocoDB đôi khi gặp khó khăn khi bạn cần lập trình hoặc thao tác thủ công để liên kết các bảng có mối quan hệ **Many-to-Many (Nhiều-nhiều)**. Việc click chuột thủ công qua giao diện UI rất tốn thời gian và dễ xảy ra sai sót khi dữ liệu lớn. 

Workflow n8n này sẽ giúp các sếp tự động hóa hoàn toàn quy trình liên kết bản ghi giữa Bảng nguồn (Source Table) và Bảng đích (Target Table) thông qua NocoDB API một cách mượt mà và chuẩn xác 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn thao tác thủ công khi phải kết nối các bản ghi quan hệ Many-to-Many trong NocoDB.
- **Chính xác tuyệt đối:** Sử dụng API chính thức của NocoDB để map đúng ID bản ghi và ID cột liên kết (Link Field ID).
- **Linh hoạt mở rộng:** Dễ dàng tích hợp vào các luồng tự động lớn hơn (như đồng bộ từ CRM, Form, hoặc hệ thống bên thứ ba vào NocoDB).
- **Tiết kiệm thời gian:** Xử lý hàng loạt các liên kết bản ghi chỉ trong tích tắc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance NocoDB đang hoạt động (Self-hosted hoặc NocoDB Cloud).
- **NocoDB API Token** để xác thực kết nối từ n8n.
- Đã có sẵn cấu trúc bảng gồm Bảng nguồn (Source Table) và Bảng đích (Target Table) với trường dạng Link thiết lập sẵn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ [n8n Workflow #4070](https://n8n.io/workflows/4070) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các phần sau:

- **Node `Set Variables`**: Nơi các sếp định nghĩa các biến quan trọng như URL của NocoDB, Table ID của bảng đích, bảng nguồn... Hãy thay đổi các giá trị này khớp với hệ thống NocoDB thực tế của các sếp.
- **Nodes NocoDB (`Grab Target Table Row`, `Get Source Table Row`)**: 
  - Chọn đúng **Credentials** (NocoDB API Token) đã chuẩn bị.
  - Trỏ đến đúng Base ID và Table ID tương ứng.
- **Nodes HTTP Request (`Get Target Table Meta Data`, `Link Record from Source to Target`)**:
  - Node Meta Data sẽ gọi NocoDB Meta API để lấy thông tin cấu trúc cột liên kết (`linkFieldId`).
  - Node Link Record sẽ thực hiện lệnh `POST` theo cấu trúc endpoint:
    `https://<YOUR NOCODB URL>/api/v2/tables/<TARGET TABLE ID>/links/<TARGET TABLE COLUMN ID>/records/<RECORD ID>`
  - Đảm bảo phần Body truyền lên khớp với định dạng JSON yêu cầu (truyền ID bản ghi nguồn vào mảng `[ { "Id": <SOURCE TABLE RECORD ID> } ]`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** ở node `When clicking ‘Test workflow’` để kiểm tra kết quả chạy thử xem bản ghi đã được liên kết thành công chưa.
- Sau khi test ngon lành, gạt công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Webhook:** Thay thế trigger thủ công bằng *Webhook Trigger* hoặc *NocoDB Trigger* để tự động chạy workflow ngay khi có bản ghi mới được tạo trên hệ thống.
- **Xử lý hàng loạt (Batch Processing):** Nếu cần liên kết nhiều bản ghi cùng lúc, các sếp có thể cấu hình Body ở dạng mảng nhiều phần tử (`[ { "Id": 1 }, { "Id": 2 } ]`).
- **Gửi thông báo lỗi:** Thêm một node *Error Trigger* kết hợp với Telegram/Slack để nhận cảnh báo ngay lập tức nếu API NocoDB trả về lỗi kết nối.

### 📌 Kết luận
Workflow *Linking NocoDB Records via API* là một công cụ cực kỳ mạnh mẽ giúp các sếp làm chủ hoàn toàn việc quản lý dữ liệu quan hệ phức tạp trong NocoDB thông qua n8n. Áp dụng ngay để tối ưu hóa hệ thống dữ liệu của doanh nghiệp nhé!