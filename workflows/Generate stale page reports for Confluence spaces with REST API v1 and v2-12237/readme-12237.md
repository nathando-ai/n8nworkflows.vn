---
title: "🚀 Tự động tạo báo cáo tài liệu cũ (Stale Page) trên Confluence bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động quét và lọc các trang tài liệu Confluence cũ, không cập nhật theo thời gian thực sử dụng Confluence REST API v1 và v2."
slug: "tao-bao-cao-tai-lieu-cu-confluence-n8n"
tags: [n8n, automation, confluence, atlassian, document-management, rest-api]
keywords: [n8n workflow, confluence stale pages, tự động hóa confluence, api v1 v2 confluence, báo cáo tài liệu cũ]
---

# 🚀 Tự động tạo báo cáo tài liệu cũ (Stale Page) trên Confluence bằng n8n

Các sếp có đang đau đầu vì kho tài liệu trên Confluence ngày càng phình to, chứa đầy những bài viết lỗi thời từ nhiều năm trước mà không ai dọn dẹp? Việc kiểm tra thủ công từng không gian (space) vừa tốn thời gian vừa kém hiệu quả. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do tác giả **Alexander Schnabl** xây dựng. Workflow này sẽ tự động quét, lọc và tổng hợp danh sách các trang tài liệu chưa được cập nhật dựa trên mốc thời gian tùy chỉnh (ví dụ: quá 90 ngày) sử dụng cả Confluence REST API v1 và v2.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và không lo gián đoạn kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần tốn nhân lực đi rà soát từng không gian làm việc trên Confluence.
- **Linh hoạt chọn API:** Hỗ trợ cả Confluence REST API v2 (khuyên dùng, hiện đại) và v1 (tương thích hệ thống cũ thông qua CQL).
- **Dữ liệu chuẩn hóa:** Gom toàn bộ kết quả vào một mảng `stalePages` gọn gàng, sẵn sàng tích hợp gửi báo cáo qua Email, Slack, Microsoft Teams hoặc xuất file Excel/CSV.
- **Kiểm soát chất lượng tài liệu:** Giúp đội ngũ chủ động cập nhật hoặc xóa bỏ các tài liệu lỗi thời, nâng cao trải nghiệm tìm kiếm thông tin nội bộ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Atlassian / Confluence Cloud:** 
  - Quyền truy cập vào các space cần quét.
  - **Atlassian API Token** (được tạo từ tài khoản cá nhân).
- **Thông tin cấu hình:** 
  - Tên miền Atlassian (Domain).
  - Danh sách mã Space Key (ví dụ: `DOCS, ENG`).
  - Ngưỡng thời gian cũ (tính bằng số ngày, ví dụ: `90`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn gốc hoặc copy mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow sử dụng tổng cộng 13 nodes, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Set Variables`:** 
  Mở node này và cấu hình các biến đầu vào cốt lõi:
  - `atlassianDomain`: Đường dẫn cơ sở của Confluence (ví dụ: `https://your-domain.atlassian.net`).
  - `spaceKeys`: Các mã space cách nhau bằng dấu phẩy (ví dụ: `DOCS,ENG`).
  - `cutoffDateDays`: Ngưỡng số ngày được xem là cũ (ví dụ: `90`).
  - `apiV2`: Điền `true` để sử dụng API v2 (khuyên dùng) hoặc `false` nếu muốn dùng CQL cũ (API v1).

- **Thiết lập Credentials (`HTTP Basic Auth`):**
  - Toàn bộ các node `Confluence - Get Spaces`, `Confluence - Get Outdated Spaces via CQL`, `Confluence - Get Pages` đều sử dụng chung một loại xác thực **HTTP Basic Auth**.
  - **User:** Email tài khoản Atlassian của các sếp.
  - **Password:** Atlassian API Token (được tạo tại trang quản lý tài khoản Atlassian của bạn).

- **Luồng xử lý (`Switch API Version` & `Filter Version by cutoffDate`):**
  - Workflow sẽ tự rẽ nhánh dựa vào biến `apiV2` mà các sếp đã chọn ở bước đầu. 
  - Nếu chọn v2, hệ thống sẽ lấy danh sách space, lấy toàn bộ trang và lọc theo ngày chỉnh sửa cuối cùng (`cutoffDate`). Nếu chọn v1, hệ thống sẽ tận dụng sức mạnh tìm kiếm của CQL.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** (chạy thủ công) lần đầu tiên để kiểm tra dữ liệu trả về ở node `Aggregate`.
- Kiểm tra mảng `stalePages` xem đã đúng định dạng tiêu đề, đường dẫn URL, tác giả và ngày cập nhật cuối hay chưa.
- Sau khi test thành công, bật **Active** để hoàn tất quá trình tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** sau node `Aggregate` để bắn danh sách trang cũ trực tiếp vào kênh thông báo của nhóm quản lý nội dung hàng tuần.
- **Gửi Email tự động:** Kết hợp với node **Gmail** hoặc **SendGrid** để gửi báo cáo trực tiếp đến từng Owner của các space Confluence.
- **Lưu trữ lịch sử:** Đẩy toàn bộ mảng `stalePages` vào **Google Sheets** hoặc **Airtable** để theo dõi biểu đồ giảm thiểu tài liệu rác theo thời gian.

### 📌 Kết luận
Việc dọn dẹp kho tài liệu chưa bao giờ dễ dàng đến thế với workflow tự động hóa Confluence này. Hãy import ngay vào n8n của các sếp để tối ưu hóa không gian làm việc số và giữ cho kiến thức doanh nghiệp luôn tươi mới, chính xác!