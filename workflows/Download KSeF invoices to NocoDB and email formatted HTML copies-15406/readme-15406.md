---
title: "🚀 Tự động hóa tải hóa đơn KSeF lên NocoDB và gửi email HTML bằng n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động kết nối hệ thống hóa đơn điện tử KSeF, đồng bộ vào NocoDB và gửi thông báo email định dạng HTML."
slug: "tu-dong-hoa-tai-hoa-don-ksef-nocodb-email-n8n"
tags: [n8n, automation, no-code, nocodb, ksef, invoice-processing]
keywords: [n8n workflow, ksef invoice automation, nocodb n8n, tự động hóa hóa đơn, n8n ksef integration]
---

# 🚀 Tự động hóa tải hóa đơn KSeF lên NocoDB và gửi email HTML

Các doanh nghiệp hoạt động tại Ba Lan thường đối mặt với khó khăn khi phải tải xuống, quản lý và kiểm tra thủ công các hóa đơn từ hệ thống **KSeF (Krajowy System e-Faktur)**. Việc này tốn rất nhiều thời gian, dễ bỏ sót hóa đơn đầu vào (cost invoices) hoặc đầu ra (issued invoices), dẫn đến sai lệch dữ liệu kế toán.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: xác thực bảo mật với KSeF (v2 API), lấy danh sách hóa đơn mới, đối chiếu với cơ sở dữ liệu **NocoDB** để tránh trùng lặp, chuyển đổi sang định dạng HTML dễ đọc, lưu trữ và gửi email thông báo kèm file trực quan.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Định kỳ hàng ngày kiểm tra và tải hóa đơn mới từ KSeF mà không cần can thiệp thủ công.
- **Không trùng lặp**: Tự động so sánh với dữ liệu sẵn có trên NocoDB, chỉ xử lý và lưu trữ các hóa đơn mới phát sinh.
- **Quản lý trực quan**: Đồng bộ toàn bộ thông tin chi tiết vào NocoDB và chuyển hóa đơn thành định dạng HTML thân thiện với người dùng.
- **Thông báo tức thì**: Nhận email chi tiết hóa đơn ngay khi có dữ liệu mới, giúp kiểm soát tài chính doanh nghiệp chặt chẽ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Cloud hoặc Self-hosted).
- Tài khoản và Token xác thực KSeF (Auth Token, mã NIP 10 chữ số).
- Tài khoản NocoDB kèm API Token (`nocoDbApiToken`).
- Dịch vụ gửi email (SMTP hoặc các node email tích hợp sẵn trong n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số sau trong workflow:
- **Node `⚙️ Config`**: Điền thông tin cấu hình cá nhân bao gồm:
  - `nip`: Mã số thuế 10 chữ số của doanh nghiệp.
  - `authToken`: Token xác thực KSeF.
  - `startDate / endDate`: Khoảng thời gian lấy hóa đơn (định dạng ISO 8601).
  - `subjectType`: Chọn `Subject2` (hóa đơn mua vào - buyer) hoặc `Subject1` (hóa đơn bán ra - seller).
- **Node `NocoDB Config`**: Cài đặt thông tin kết nối tới bảng dữ liệu NocoDB của các sếp.
- **Credentials**: Thiết lập API Token cho node `Get existing invoices`, `Insert new invoice details`, `Create NocoDB KSeF Invoices Table` bằng cách chọn `nocoDbApiToken`.
- **Node `Send an Email`**: Cấu hình thông tin người nhận, tiêu đề và tài khoản gửi email phù hợp.

#### 3. Khởi tạo & Kích hoạt ⚡️
- **Bước chạy thiết lập (Setup)**: Chạy node `Create Tables` (`manualTrigger`) trước tiên để workflow tự động tạo bảng `KSeF Invoices` cần thiết trong NocoDB.
- **Test Run**: Thực hiện chạy thử công đoạn lấy dữ liệu để kiểm tra kết nối KSeF và NocoDB hoạt động trơn tru.
- **Active**: Bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm theo lịch trình từ node `Monitor Every Day for new invoices`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat**: Kết nối thêm node Telegram hoặc Slack sau bước xử lý hóa đơn để nhận thông báo tức thì trên điện thoại thay vì chỉ check email.
- **Lưu trữ file PDF/XML**: Bổ sung node lưu trữ tự động file gốc vào Google Drive hoặc OneDrive để phục vụ cho việc quyết toán thuế.
- **Báo cáo định kỳ**: Thiết lập thêm một nhánh phụ tổng hợp chi phí hóa đơn hàng tuần/tháng và gửi báo cáo tóm tắt cho kế toán trưởng.

### 📌 Kết luận
Tự động hóa quy trình tải hóa đơn KSeF và đồng bộ về NocoDB không chỉ giúp tiết kiệm hàng giờ thao tác tay mà còn loại bỏ hoàn toàn rủi ro sót hóa đơn. Hãy áp dụng ngay workflow này để nâng cấp hệ thống vận hành tài chính cho doanh nghiệp của các sếp!