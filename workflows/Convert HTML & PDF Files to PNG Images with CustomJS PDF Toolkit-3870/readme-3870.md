---
title: "🚀 Chuyển đổi HTML & PDF sang PNG hoàn toàn tự động với CustomJS PDF Toolkit"
description: "Giải pháp tự động chuyển đổi HTML hoặc PDF thành hình ảnh PNG chất lượng cao, giúp tiết kiệm thời gian và công sức xử lý tài liệu."
slug: "convert-html-pdf-to-png-customjs"
tags: [n8n, automation, no-code, pdf, image, design, ai]
keywords: [n8n workflow, tự động hóa, chuyển đổi PDF, chuyển đổi PNG, PDF Toolkit, CustomJS]
---

# 🚀 Chuyển đổi HTML & PDF sang PNG hoàn toàn tự động với CustomJS PDF Toolkit

Bạn đang phải xử lý hàng trăm file HTML hoặc PDF mỗi ngày, chỉ để lấy ra hình ảnh PNG để chèn vào báo cáo, slide hay website? Việc chuyển đổi thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Workflow này sẽ giúp bạn **tự động hóa 100%** quy trình này mà không cần viết một dòng code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi hàng nghìn file chỉ trong vài giây.
- **Chính xác 100%**: Không còn lỗi chuyển đổi do thao tác thủ công.
- **Tự động hóa liên tục**: Workflow chạy 24/7, chỉ cần kích hoạt một lần.
- **Dễ dàng mở rộng**: Thêm Slack, Email, hoặc lưu trữ lên Google Drive chỉ vài bước.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc n8n.cloud).
- **CustomJS API Key**: Đăng ký tại [CustomJS](https://customjs.io) và tạo credential `customJsApi` trong n8n.
- **URL của file PDF** (nếu muốn chuyển PDF từ mạng) hoặc **HTML nội dung** (được nhập vào node `Set PDF URL`).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link:  
   `https://n8n.io/workflows/3870` (hoặc copy toàn bộ JSON).
2. Mở n8n Editor → **Import** → **Upload JSON** → chọn file vừa tải.
3. Workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Tham số cần cấu hình | Credential |
|------|-------|----------------------|------------|
| **When clicking ‘Test workflow’** | Trigger thủ công | Không cần tham số | - |
| **Set PDF URL** | Nhận URL PDF hoặc HTML | `pdfUrl` (URL) hoặc `htmlContent` (HTML) | - |
| **HTML to PDF** | Chuyển HTML sang PDF | `html` (được lấy từ node trước) | `customJsApi` |
| **Convert PDF into PNG1** | Chuyển PDF (từ URL) sang PNG | `resource: url` (URL PDF) | `customJsApi` |
| **Convert PDF into PNG** | Chuyển PDF (từ file đã tạo) sang PNG | `resource: file` (đường dẫn PDF nội bộ) | `customJsApi` |

#### Cấu hình chi tiết từng node

1. **Set PDF URL**  
   - Chọn `Set` node, thêm trường `pdfUrl` (URL PDF) hoặc `htmlContent` (HTML).  
   - Ví dụ: `pdfUrl = https://example.com/file.pdf` hoặc `htmlContent = <html>...</html>`.

2. **HTML to PDF**  
   - Chọn `customJsApi` trong Credentials.  
   - Truyền `html` từ node trước (`{{ $json["htmlContent"] }}`).

3. **Convert PDF into PNG1**  
   - Chọn `customJsApi`.  
   - Trong `resource` chọn `url` và truyền `{{ $json["pdfUrl"] }}`.

4. **Convert PDF into PNG**  
   - Chọn `customJsApi`.  
   - Trong `resource` chọn `file` và truyền đường dẫn PDF đã được tạo ở node `HTML to PDF` (`{{ $json["pdfFile"] }}`).

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** để chạy thử với dữ liệu mẫu. Kiểm tra tab **Execution** xem output của từng node.
2. **Bật Active**: Sau khi xác nhận mọi thứ hoạt động, bật toggle **Active** để workflow tự động chạy khi trigger được kích hoạt.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi kết quả lên Slack**: Thêm node `Slack` sau node `Convert PDF into PNG` để thông báo kèm file PNG.
- **Lưu trữ lên Google Drive**: Sử dụng node `Google Drive` để upload PNG vào thư mục cụ thể.
- **Lưu log vào Google Sheets**: Ghi lại thời gian, URL nguồn, và đường dẫn file PNG để theo dõi.
- **Chạy theo lịch**: Thay vì `manualTrigger`, dùng node `Cron` để tự động chạy hàng ngày/giờ.

## 📌 Kết luận

Workflow này giúp các sếp **đưa công việc chuyển đổi tài liệu** từ thủ công sang tự động, giảm thiểu sai sót và tăng năng suất. Hãy thử ngay, tùy chỉnh cho phù hợp với quy trình của mình, và chia sẻ phản hồi để cộng đồng n8n ngày càng mạnh mẽ hơn!