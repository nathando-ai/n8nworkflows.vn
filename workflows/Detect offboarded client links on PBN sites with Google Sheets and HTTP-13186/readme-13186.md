---
title: "🚀 Tự động quét và phát hiện liên kết khách hàng cũ trên hệ thống PBN với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra mã nguồn HTML của các trang PBN, phát hiện backlink của khách hàng đã ngưng hợp tác và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-phat-hien-link-khach-hang-cu-tren-pbn"
tags: [n8n, automation, no-code, google-sheets, seo, pbn-management]
keywords: [n8n workflow, tự động hóa pbn, kiểm tra backlink, google sheets, seo automation, phát hiện link chết]
---

# 🚀 Tự động quét và phát hiện liên kết khách hàng cũ trên hệ thống PBN

Việc quản lý một hệ thống PBN (Private Blog Network) lớn đòi hỏi sự tỉ mỉ rất cao. Khi một khách hàng ngừng hợp tác (offboard), việc rà soát thủ công hàng trăm website để gỡ bỏ backlink hoặc anchor text cũ là một "cực hình" mất rất nhiều thời gian và dễ bỏ sót. Nếu để quên backlink của khách cũ trên PBN, bạn có thể vô tình làm rò rỉ cấu trúc mạng lưới hoặc vi phạm các thỏa thuận dịch vụ.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó. Nó tự động hóa 100% quy trình: đọc danh sách PBN, tải mã nguồn HTML trực tiếp, đối chiếu với danh sách dự án đã dừng, và ghi nhận kết quả ngay lập tức vào Google Sheets mà không cần một dòng code thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Desky VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mở hàng loạt trang web để check Ctrl+F, workflow tự động duyệt qua toàn bộ danh sách PBN trong vài phút.
- **Không bỏ sót lỗi:** Tự động lọc ra các dòng chưa xử lý và chỉ quét những PBN mới hoặc chưa kiểm tra.
- **Đồng bộ dữ liệu minh bạch:** Tự động ghi tên miền của khách hàng cũ còn sót lại vào đúng cột "Offboarded Links" trong Google Sheets.
- **An toàn cho hệ thống:** Tích hợp tính năng chờ (Wait/Pause) giữa các lần gọi request để tránh làm quá tải (rate-limit) các trang PBN của bạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Google Sheets:** 
  - Sheet 1: Chứa danh sách các trang PBN cần kiểm tra.
  - Sheet 2: Chứa danh sách tên miền của các dự án/khách hàng đã offboard (đặt ở Cột A).
- **Google Sheets Credentials:** Cấp quyền kết nối tài khoản Google trong n8n để đọc và ghi dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và dán trực tiếp vào giao diện n8n Editor của các sếp, hoặc import file JSON thông qua menu tuỳ chọn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:
- **Read PBN Sites from Sheet & Read Offboarded Project Domains:** Kết nối tài khoản Google Sheets OAuth2, sau đó chọn đúng File ID, Sheet Name chứa danh sách PBN và danh sách tên miền khách hàng cũ.
- **Filter Unprocessed PBN Rows (Code Node):** Node này dùng để lọc các dòng chưa xử lý (dựa vào việc cột "Offboarded Links" đang trống) nhằm tối ưu số lượng request.
- **Fetch PBN Site HTML (HTTP Request Node):** Thực hiện gọi lệnh GET tới từng URL của PBN để lấy mã nguồn HTML sống.
- **Match Domains in HTML (Code Node):** Chạy thuật toán so khớp xem tên miền nào từ danh sách offboard xuất hiện trong đoạn HTML vừa tải về.
- **Write Matched Domain to PBNs Sheet (Google Sheets Node):** Cấu hình `Operation` là **Update**, map đúng ID dòng để cập nhật tên miền tìm được vào cột kết quả.
- **Pause Before Next Iteration (Wait Node):** Giúp tạo độ trễ nhỏ giữa các lần lặp, bảo vệ server PBN khỏi bị chặn IP do gửi request quá nhanh.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node `Run Workflow Manually` để chạy thử nghiệm với một vài dòng dữ liệu mẫu và kiểm tra kết quả trả về trên Google Sheets.
- Sau khi test thành công, lưu lại và bật trạng thái **Active** nếu muốn chuyển sang chế độ tự động định kỳ.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo:** Thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay lập tức vào điện thoại mỗi khi phát hiện một PBN còn sót link khách cũ.
- **Lập lịch chạy tự động:** Thay thế node `Run Workflow Manually` bằng `Schedule Trigger` để hệ thống tự động quét danh sách PBN hàng tuần hoặc hàng tháng.
- **Mở rộng dữ liệu:** Có thể lưu thêm thời gian quét (Timestamp) vào Google Sheets để dễ dàng theo dõi lịch sử kiểm tra của từng site PBN.

### 📌 Kết luận
Việc kiểm soát liên kết trên hệ thống PBN chưa bao giờ dễ dàng đến thế với tự động hóa. Áp dụng ngay workflow này để tiết kiệm hàng giờ thao tác thủ công và giữ cho mạng lưới SEO của các sếp luôn sạch sẽ, chuyên nghiệp!