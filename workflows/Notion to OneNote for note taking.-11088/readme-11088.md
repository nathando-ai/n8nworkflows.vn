---
title: "🚀 Tự Động Đồng Bộ Ghi Chú Notion Sang OneNote/Nextcloud Không Cần Code"
description: "Workflow n8n giúp tự động chuyển đổi và lưu trữ ghi chú từ Notion sang hệ thống lưu trữ đám mây (OneNote/Nextcloud) ngay lập tức, tối ưu hóa quy trình làm việc cá nhân và doanh nghiệp."
slug: "tu-dong-dong-bo-notion-sang-onenote-nextcloud"
tags: [n8n, automation, no-code, notion, nextcloud, productivity]
keywords: [n8n workflow, tự động hóa ghi chú, notion to onenote, nextcloud sync, productivity automation]
---

# 🚀 Tự Động Đồng Bộ Ghi Chú Notion Sang OneNote/Nextcloud Không Cần Code

Bạn có đang cảm thấy mệt mỏi khi phải sao chép thủ công các ghi chú quan trọng từ Notion sang OneNote hoặc Nextcloud để lưu trữ dài hạn hoặc chia sẻ? Việc này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót, bỏ sót thông tin hoặc định dạng bị lỗi. Với workflow n8n này, các sếp có thể tự động hóa hoàn toàn quy trình: mỗi khi có ghi chú mới hoặc cập nhật trong Notion, hệ thống sẽ tự động xử lý, chuyển đổi định dạng và đẩy dữ liệu lên nền tảng lưu trữ đám mây của bạn trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian sao chép:** Không cần mở 2 tab trình duyệt, mọi thao tác diễn ra tự động trong nền.
- **Đảm bảo tính nhất quán dữ liệu:** Ghi chú trong Notion luôn được đồng bộ chính xác sang hệ thống lưu trữ, tránh thất lạc thông tin.
- **Tích hợp linh hoạt:** Hỗ trợ cả Nextcloud (thông qua API) và có thể điều chỉnh để tương thích với các dịch vụ lưu trữ khác.
- **Quản lý trạng thái thông minh:** Sử dụng Redis để theo dõi các bản ghi đã xử lý, tránh việc gửi trùng lặp dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản n8n:** Đã cài đặt và chạy instance n8n (Self-hosted hoặc Cloud).
2. **Tài khoản Notion:** Tạo API Key (Internal Integration) và chia sẻ Database chứa ghi chú cho integration này.
3. **Tài khoản Nextcloud:** Tạo App Password hoặc API Key để kết nối với Nextcloud (Workflow gốc sử dụng Nextcloud, nhưng logic có thể áp dụng cho OneNote qua các service khác).
4. **Redis Server:** Một instance Redis (có thể chạy local hoặc cloud) để lưu trữ trạng thái (state) của các bản ghi đã xử lý.
5. **Webhook URL:** Địa chỉ webhook của n8n để nhận sự kiện từ Notion.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow bằng cách tải file JSON từ link gốc [n8n.io/workflows/11088](https://n8n.io/workflows/11088) hoặc copy toàn bộ code JSON và dán vào n8n Editor. Sau đó, lưu workflow với tên dễ nhớ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần kiểm tra và cấu hình các node sau:

- **Node `Webhook`**:
  - Đảm bảo `Path` (ví dụ: `09aff775-83ef-404f-9b05-1bc806f4dbcd`) là duy nhất.
  - Trong Notion, các sếp cần thêm Webhook Integration vào Database, chỉ định URL webhook của n8n (địa chỉ public của instance n8n + path).
  - Chọn sự kiện kích hoạt: `page.created`, `page.updated`, hoặc `database_page.created`.

- **Node `Redis` (Operation: get) & `Store` (Operation: set)**:
  - Chọn credentials Redis đã tạo trong n8n.
  - Node `Redis` (get) sẽ kiểm tra xem ID của bản ghi Notion đã được xử lý chưa. Nếu có, nó sẽ bị lọc bỏ.
  - Node `Store` (set) sẽ lưu ID của bản ghi sau khi xử lý thành công để lần sau không gửi lại.

- **Node `Get Notion page`**:
  - Chọn credentials `notionApi`.
  - `Database ID`: Điền ID của Database Notion chứa ghi chú.
  - `Page ID`: Thường lấy từ payload của webhook.

- **Node `Mapping` (Code Node)**:
  - Đây là node xử lý logic chuyển đổi dữ liệu. Các sếp cần kiểm tra code để đảm bảo nó trích xuất đúng nội dung (title, body, tags) từ Notion và định dạng lại cho phù hợp với API của Nextcloud/OneNote.
  - Nếu dùng OneNote, các sếp có thể cần sửa code này để gọi API Microsoft Graph thay vì Nextcloud.

- **Node `HTTP Request` & `HTTP Request1` (Nextcloud API)**:
  - Chọn credentials `nextCloudApi`.
  - `URL`: Địa chỉ Nextcloud của các sếp (ví dụ: `https://cloud.example.com/api/v1/...`).
  - `Method`: POST hoặc PUT.
  - `Body`: Cấu hình payload chứa nội dung ghi chú đã được mapping.
  - *Lưu ý:* Nếu các sếp muốn dùng OneNote, cần thay thế các node này bằng các node gọi API Microsoft Graph (Create Page in Notebook).

- **Node `Update task in Notion` & `Update task in Notion1`**:
  - Chọn credentials `notionApi`.
  - Mục đích: Cập nhật trạng thái trong Notion (ví dụ: thêm tag "Synced" hoặc cập nhật thời gian đồng bộ) để người dùng biết ghi chú đã được xử lý.
  - `Page ID`: Lấy từ dữ liệu đầu vào.
  - `Properties`: Định nghĩa trường cần cập nhật (ví dụ: `Status` = `Done`).

- **Node `If` & `Filter`**:
  - Các node này dùng để kiểm tra điều kiện (ví dụ: chỉ đồng bộ khi có thay đổi thực sự, hoặc bỏ qua các bản ghi bị khóa).
  - Kiểm tra logic trong node `If` để đảm bảo nó phù hợp với nhu cầu của các sếp (ví dụ: chỉ đồng bộ khi trường `Sync Status` là `Pending`).

#### 3. Kích hoạt ⚡️
1. **Test Run**: Tạo một ghi chú mới trong Notion. Kiểm tra xem workflow có chạy không, dữ liệu có xuất hiện trong Nextcloud/OneNote không, và trạng thái trong Notion có được cập nhật không.
2. **Bật Active**: Sau khi test thành công, bật nút `Active` để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Slack/Telegram**: Sau khi đồng bộ thành công, thêm node `Slack` hoặc `Telegram` để gửi thông báo "Ghi chú [Tên] đã được đồng bộ thành công" cho các sếp.
- **Lọc theo Tag**: Sửa node `Filter` để chỉ đồng bộ các ghi chú có tag cụ thể (ví dụ: `#important`), tránh việc đồng bộ toàn bộ database.
- **Lưu log lỗi**: Thêm node `Error Trigger` và gửi thông báo khi có lỗi xảy ra (ví dụ: lỗi API Nextcloud) để các sếp kịp thời xử lý.
- **Hỗ trợ OneNote trực tiếp**: Thay vì Nextcloud, các sếp có thể tìm kiếm các n8n nodes có sẵn cho Microsoft OneNote hoặc sử dụng `HTTP Request` để gọi API Microsoft Graph, tạo page mới trong notebook OneNote.

### 📌 Kết luận
Workflow "Notion to OneNote/Nextcloud" là một công cụ mạnh mẽ giúp các sếp tự động hóa quy trình quản lý ghi chú, tiết kiệm thời gian và đảm bảo dữ liệu luôn được lưu trữ an toàn, đồng bộ. Với khả năng tùy biến cao, các sếp có thể dễ dàng điều chỉnh workflow để phù hợp với hệ thống lưu trữ đám mây của mình. Hãy thử ngay và trải nghiệm sự khác biệt!