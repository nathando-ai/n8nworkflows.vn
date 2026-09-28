---
title: "🚀 Hệ thống sao lưu workflow tự động với Google Drive và lưu trữ"
description: "Sao lưu toàn bộ workflow n8n hàng ngày, phân loại và lưu trữ an toàn trên Google Drive, giúp doanh nghiệp tránh mất dữ liệu và dễ dàng khôi phục."
slug: "he-thong-sao-luu-workflow-tang-dong-gmail-drive"
tags: [n8n, automation, no-code, google-drive, backup]
keywords: [n8n workflow, tự động hóa, sao lưu workflow, backup n8n, lưu trữ Google Drive]
---

# 🚀 Hệ thống sao lưu workflow tự động với Google Drive và lưu trữ

Bạn đang phải lo lắng về việc mất dữ liệu workflow n8n do lỗi hệ thống, lỗi người dùng hay thậm chí là mất mát dữ liệu do không sao lưu đúng cách? Việc sao lưu thủ công không chỉ tốn thời gian, dễ gây sai sót mà còn làm gián đoạn quy trình làm việc.  
Workflow **Automated Workflow Backup System with Google Drive and Archiving** là giải pháp hoàn toàn tự động, không cần code, giúp bạn:

- **Sao lưu** mọi workflow n8n một cách định kỳ.
- **Phân loại** lưu trữ theo ngày và loại workflow (ARCHIVE vs. non-ARCHIVE).
- **Lưu trữ** an toàn trên Google Drive, dễ dàng truy cập và khôi phục.
- **Xóa** các bản sao lưu cũ (ARCHIVE) để tránh lãng phí dung lượng lưu trữ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thao tác thủ công, workflow tự động chạy theo lịch.
- **Độ chính xác cao**: Mọi workflow được sao lưu đúng cấu trúc JSON, tránh lỗi dữ liệu.
- **An toàn dữ liệu**: Lưu trữ trên Google Drive, có thể thiết lập quyền truy cập và sao lưu đa vùng.
- **Quản lý dễ dàng**: Các file được đặt tên theo ngày và loại, giúp tìm kiếm nhanh chóng.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Drive**: Tạo một tài khoản Google Drive và cấp quyền truy cập (OAuth 2.0) cho n8n.
- **n8n Credentials**: Cần API Key hoặc Token để gọi API n8n (để lấy danh sách workflow và xóa workflow).
- **Định kỳ chạy**: Thiết lập thời gian chạy (ví dụ: 02:00 mỗi ngày) trong node `Schedule Trigger`.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc: <https://n8n.io/workflows/3559>.
2. Mở n8n Editor → **Import** → **Import from file** → chọn file JSON vừa tải.
3. Hoặc copy toàn bộ nội dung JSON → **Import** → **Paste JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|-------|---------------------|
| **Schedule Trigger** | Định kỳ chạy workflow. | Thời gian chạy (ví dụ: 02:00), múi giờ. |
| **If** | Kiểm tra tên workflow có chứa “ARCHIVE” hay không. | Điều kiện: `{{$json["name"]}} contains "ARCHIVE"`. |
| **Create to date folder** (Google Drive) | Tạo thư mục theo ngày hiện tại. | `Folder name`: `{{now().format("YYYY-MM-DD")}}`. |
| **GET Workflows** (n8n) | Lấy danh sách tất cả workflow. | Chọn **Credentials**: n8n API Key. |
| **Convert to JSON** (ConvertToFile) | Chuyển dữ liệu workflow thành file JSON. | `File name`: `{{ $json["name"] }}.json`. |
| **Convert to JSON'** (ConvertToFile) | Chuyển dữ liệu workflow khác thành file JSON. | Tương tự như trên. |
| **Save 'ARCHIVE' Workflows** (Google Drive) | Upload file vào thư mục `ARCHIVE`. | `Folder ID`: ID thư mục `ARCHIVE` trong Google Drive. |
| **Save all other Workflows** (Google Drive) | Upload file vào thư mục chính. | `Folder ID`: ID thư mục gốc. |
| **Delete 'ARCHIVE' Workflows** (n8n) | Xóa workflow có tên chứa “ARCHIVE”. | Chọn **Credentials**: n8n API Key. |

> **Lưu ý**: Đảm bảo các **Folder ID** trong Google Drive đã tồn tại trước khi chạy workflow. Nếu chưa có, tạo thư mục “ARCHIVE” và thư mục gốc (ví dụ: “Workflow Backups”) trong Google Drive, sau đó copy ID vào các node tương ứng.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow một lần thủ công để kiểm tra xem các file JSON được tạo và upload đúng thư mục chưa.
2. **Bật Active**: Khi mọi thứ ổn, chuyển workflow sang trạng thái **Active** để nó tự động chạy theo lịch.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node Slack để gửi tin nhắn khi backup hoàn thành hoặc khi có lỗi.
- **Lưu log**: Sử dụng node `Write Binary File` để lưu log vào Google Drive, giúp theo dõi lịch sử backup.
- **Chính sách lưu trữ**: Kết hợp với node `Delete` để tự động xóa các file backup cũ hơn 30 ngày.
- **Sao lưu đa vùng**: Tạo một thư mục backup trên Google Drive và một thư mục backup trên Dropbox, đồng bộ dữ liệu qua n8n.

## 📌 Kết luận
Bạn đã có một hệ thống sao lưu workflow n8n hoàn toàn tự động, an toàn và dễ quản lý. Hãy áp dụng ngay workflow này để bảo vệ dữ liệu quan trọng của doanh nghiệp, giảm thiểu rủi ro và tập trung vào công việc cốt lõi. Nếu gặp bất kỳ vấn đề nào, hãy tham khảo tài liệu n8n hoặc liên hệ với cộng đồng để được hỗ trợ. Chúc các sếp thành công!