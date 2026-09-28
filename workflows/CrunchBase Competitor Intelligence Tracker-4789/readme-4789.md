---
title: "🚀 Tự động theo dõi đối thủ cạnh tranh từ Crunchbase và tạo Task trên ClickUp bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động trích xuất dữ liệu tài chính, thông tin gọi vốn của đối thủ từ Crunchbase và tạo task review trên ClickUp."
slug: "tu-dong-theo-doi-doi-thu-crunchbase-clickup-n8n"
tags: [n8n, automation, no-code, marketing, finance, clickup, crunchbase]
keywords: [n8n workflow, tự động hóa marketing, theo dõi đối thủ crunchbase, n8n clickup integration, api crunchbase]
---

# 🚀 Tự động theo dõi đối thủ cạnh tranh từ Crunchbase và tạo Task trên ClickUp

Việc theo dõi các đối thủ cạnh tranh trên thị trường (như vòng gọi vốn, sản phẩm mới, cập nhật thông tin) thường ngốn rất nhiều thời gian của đội ngũ Marketing và Sales nếu phải làm thủ công. Các sếp có bao giờ quên kiểm tra thông tin quan trọng của đối thủ vì quá bận rộn?

Workflow này sẽ giúp các sếp giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: Lấy thông tin từ **Crunchbase**, xử lý dữ liệu và tự động tạo task giao việc trên **ClickUp** cho đội ngũ nghiên cứu thị trường mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần tra cứu thủ công trên Crunchbase cho từng đối thủ.
- **Cập nhật liên tục:** Nắm bắt ngay lập tức các thay đổi về nguồn vốn, mô tả hoặc thông tin quan trọng của đối thủ.
- **Phân công tự động:** Tự động tạo task review trên ClickUp kèm đầy đủ thông tin chi tiết để đội ngũ hành động ngay.
- **Vận hành trơn tru:** Quy trình No-code hoàn toàn, dễ dàng tùy chỉnh và mở rộng cho danh sách hàng chục đối thủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- Một tài khoản n8n (Cloud hoặc Self-hosted).
- **Crunchbase API Key** để gọi dữ liệu từ API v4 của họ.
- **Tài khoản ClickUp** và kết nối credentials với n8n để tự động tạo task trong Space/List mong muốn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó dán trực tiếp vào giao diện n8n Editor (hoặc chọn Import từ file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp chú ý cấu hình các điểm sau:
- **Set Competitor Name**: Node này dùng để nhập tên công ty đối thủ cần kiểm tra (ví dụ: `"Stripe, Inc."`). Khi chạy tự động, các sếp có thể thay thế node này bằng Google Sheets hoặc Database chứa danh sách hàng loạt đối thủ.
- **Generate Crunchbase Slug**: Node Code JavaScript có sẵn giúp chuyển đổi tên công ty dạng thô thành dạng URL-friendly (slug), ví dụ `"Stripe, Inc."` thành `"stripe-inc"`.
- **Fetch Crunchbase Data (HTTP Request)**: Điền API Key của Crunchbase vào tham số yêu cầu (User Key) theo định dạng URL API v4: `https://api.crunchbase.com/api/v4/entities/organizations/{{ $json.slug }}`.
- **Create Review Task in ClickUp**: Chọn đúng Workspace, Space và List trong ClickUp của các sếp, sau đó map các trường dữ liệu lấy từ Crunchbase (tên, mô tả, tổng số vốn, website) vào phần Tiêu đề và Mô tả của Task.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử nghiệm thủ công với dữ liệu mẫu qua nút *Manual Trigger* để kiểm tra xem task đã được đẩy lên ClickUp thành công chưa.
- Sau khi test ngon lành, gạt công tắc **Active** để sẵn sàng đưa vào vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn trigger**: Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Schedule Trigger` để chạy định kỳ hàng tuần, hoặc kết hợp với Google Sheets để quét danh sách hàng loạt đối thủ tự động.
- **Thông báo đa kênh**: Kết hợp thêm node Slack hoặc Telegram để bắn thông báo ngay vào nhóm chat của công ty mỗi khi có thông tin gọi vốn mới từ đối thủ.
- **Lưu trữ lịch sử**: Thêm node Google Sheets ở cuối luồng để lưu lại lịch sử các lần quét dữ liệu làm báo cáo kho tri thức (Market Intelligence Database).

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản cùng 5 nodes n8n, các sếp đã xây dựng thành công một hệ thống tình báo cạnh tranh (Competitive Intelligence) tự động hóa hoàn toàn. Áp dụng ngay để tối ưu hóa năng suất cho đội ngũ marketing và phát triển kinh doanh thôi nào!