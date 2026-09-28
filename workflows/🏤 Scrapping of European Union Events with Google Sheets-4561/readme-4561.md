---
title: "🏤 Tự động hóa Scraping Sự kiện Liên minh Châu Âu với Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc thu thập thông tin sự kiện từ trang web EU và lưu trữ vào Google Sheets bằng n8n. Tiết kiệm thời gian và tránh trùng lặp dữ liệu."
slug: "tu-dong-hoa-scraping-su-kien-eu-voi-google-sheets"
tags: [n8n, automation, no-code, google-sheets, web-scraping]
keywords: [n8n workflow, tự động hóa, scraping dữ liệu, google sheets, sự kiện EU]
---

# 🏤 Tự động hóa Scraping Sự kiện Liên minh Châu Âu với Google Sheets

[Các sếp] có bao giờ phải đối mặt với tình trạng thu thập thông tin sự kiện từ trang web EU thủ công? Với hàng trăm sự kiện hàng ngày, việc này không chỉ tốn thời gian mà còn dễ gây trùng lặp dữ liệu. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình từ scraping đến lưu trữ dữ liệu vào Google Sheets một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình thu thập dữ liệu hàng ngày.
- **Tránh trùng lặp**: So sánh dữ liệu mới với dữ liệu đã có trong Google Sheets.
- **Dữ liệu chính xác**: Lấy thông tin chi tiết về sự kiện bao gồm tên, liên kết, ngày, tháng, năm, loại sự kiện và địa điểm.
- **Hoạt động liên tục**: Chạy tự động mỗi ngày lúc 8:30 sáng theo giờ địa phương.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Credentials Google Sheets OAuth 2.0 đã được thiết lập trong n8n.
- Quyền truy cập vào trang web EU để scraping dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/4561](https://n8n.io/workflows/4561) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy toàn bộ nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Chọn thời gian chạy tự động (mặc định là 8:30 sáng mỗi ngày).
   - Đảm bảo múi giờ được thiết lập chính xác.

2. **Query EU Website**:
   - Không cần cấu hình gì thêm, node này sẽ truy cập trang web EU để lấy dữ liệu HTML.

3. **Extract Blocks** và **Parse Information**:
   - Hai node này sẽ tự động trích xuất và phân tích dữ liệu từ HTML.
   - Không cần cấu hình thêm.

4. **Load Old Records**:
   - Cấu hình credentials Google Sheets OAuth 2.0.
   - Chọn file và sheet chứa dữ liệu sự kiện cũ.
   - Mapping các trường dữ liệu: `event_name`, `event_link`, `day`, `month`, `year`, `event_type`, `event_location`.

5. **Store New Records**:
   - Cấu hình credentials Google Sheets OAuth 2.0.
   - Chọn file và sheet để lưu dữ liệu sự kiện mới.
   - Mapping các trường dữ liệu: `Reference Number`, `Committee`, `Rapporteur`, `Title/Description`, `PDF Link`.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để test với dữ liệu mẫu.
2. Kiểm tra kết quả trong Google Sheets để đảm bảo dữ liệu được lưu trữ đúng cách.
3. Bật chế độ "Active" để workflow chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có sự kiện mới.
- **Lưu log hoạt động**: Thêm node ghi log để theo dõi quá trình chạy workflow.
- **Gửi báo cáo định kỳ**: Tạo workflow phụ để tổng hợp và gửi báo cáo hàng tuần.
- **Xử lý lỗi tự động**: Thêm node xử lý lỗi và gửi thông báo khi workflow gặp sự cố.

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn đảm bảo dữ liệu được thu thập một cách chính xác và không bị trùng lặp. Hãy áp dụng ngay để tối ưu hóa quá trình quản lý thông tin sự kiện của doanh nghiệp!