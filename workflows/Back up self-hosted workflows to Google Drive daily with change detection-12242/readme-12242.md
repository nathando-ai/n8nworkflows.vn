---
title: "🚀 Sao lưu workflow n8n tự động lên Google Drive – phát hiện thay đổi 100%"
description: "Giải pháp tự động sao lưu hàng ngày các workflow n8n self‑hosted lên Google Drive, phát hiện thay đổi và chỉ lưu file mới, giúp doanh nghiệp tránh mất dữ liệu và tiết kiệm thời gian."
slug: "sao-luu-workflow-n8n-google-drive"
tags: [n8n, automation, no-code, devops, google-drive, backup]
keywords: [n8n workflow, tự động hóa, sao lưu, google drive, phát hiện thay đổi]
---

# 🚀 Sao lưu workflow n8n tự động lên Google Drive – phát hiện thay đổi 100%

Bạn đang tự quản lý một hệ thống n8n self‑hosted? Mỗi lần chỉnh sửa workflow, bạn lo lắng về việc mất dữ liệu do lỗi hệ thống, mất kết nối internet, hoặc quên sao lưu?  
Workflow “Back up self‑hosted workflows to Google Drive daily with change detection” của Chandan Singh đã giúp các sếp giải quyết vấn đề này một cách **100% tự động, không cần code**. Hãy để n8n làm việc cho bạn: chạy hàng ngày, kiểm tra thay đổi, và chỉ lưu file mới lên Google Drive – bảo vệ dữ liệu, giảm rủi ro và tiết kiệm thời gian.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thao tác thủ công, workflow tự động chạy hàng ngày.  
- **Chính xác & tin cậy**: Phát hiện thay đổi dựa trên hash, tránh lưu trữ file trùng lặp.  
- **Cá nhân hóa**: Định dạng file, thư mục lưu trữ linh hoạt theo nhu cầu.  
- **Hoạt động liên tục**: Được lưu trữ ngay trên Google Drive, có thể truy cập bất cứ lúc nào, bất cứ nơi đâu.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive**: Tạo một “Service Account” và tải file JSON credentials.  
- **API Key / Token của n8n**: Để truy cập danh sách workflow qua HTTP request.  
- **VPS hoặc máy chủ n8n**: Đảm bảo n8n đang chạy và có thể thực thi workflow.  
- (Tùy chọn) **Slack / Telegram**: Nếu muốn nhận thông báo khi backup thành công.  
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/12242).  
2. Mở n8n Editor → **Import** → **Upload JSON** → chọn file vừa tải.  
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Mô tả | Tham số cần cấu hình |
|------|----------|-------|----------------------|
| **Schedule Trigger** | `scheduleTrigger` | Đặt lịch chạy hàng ngày (ví dụ 02:00 AM). | `Cron Expression` hoặc `Time` |
| **HTTP Request** | `httpRequest` | Lấy danh sách workflow từ API n8n (`GET /workflows`). | `URL`, `Authentication` (API Token) |
| **Split In Batches** | `splitInBatches` | Xử lý từng nhóm workflow (để tránh giới hạn API). | `Batch Size` (đặt 10-20) |
| **Code** | `code` (tính hash) | Tính SHA‑256 của nội dung workflow. | `Code` (JavaScript) |
| **If** | `if` (so sánh hash) | Kiểm tra xem hash đã lưu trước đó có khác không. | `Expression` (`{{$json["hash"]}} !== {{$node["StoreHash"].json["hash"]}}`) |
| **Set** | `set` (định dạng file) | Chuẩn bị dữ liệu file JSON để upload. | `File Name`, `File Content` |
| **Google Drive** | `googleDrive` | Upload file lên thư mục đã chọn. | `Folder ID`, `File Name`, `File Content` |
| **StoreHash** | `dataTable` (hoặc `code` lưu hash) | Lưu hash cuối cùng để so sánh lần sau. | `Key`, `Value` |
| **Slack / Telegram** | `slack` / `telegram` (tùy chọn) | Gửi thông báo khi backup thành công. | `Channel`, `Message` |

> **Lưu ý**:  
> - Đảm bảo **Google Drive Credential** đã được cấu hình trong n8n (Credentials → Google Drive).  
> - Đặt **API Token** của n8n trong node HTTP Request (Credentials → HTTP Basic Auth hoặc Bearer Token).  
> - Nếu workflow được lưu trữ trong một thư mục cụ thể, hãy nhập **Folder ID** của thư mục đó trong node Google Drive.  
> - Node `StoreHash` có thể là một `dataTable` lưu trữ hash trong một bảng, hoặc một `code` node ghi hash vào một file JSON trên server.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công với dữ liệu mẫu để kiểm tra tính đúng đắn.  
2. Kiểm tra log: Đảm bảo không có lỗi “Authentication failed” hoặc “File already exists”.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Kiểm tra Google Drive: File mới nhất sẽ xuất hiện trong thư mục đã chọn.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo định kỳ**: Thêm node `email` để gửi bản sao lưu cuối cùng mỗi tuần.  
- **Lưu trữ lịch sử**: Sử dụng node `dataTable` để ghi lại thời gian, hash, và trạng thái backup.  
- **Bảo mật**: Mã hóa nội dung file trước khi upload (sử dụng node `crypto`).  
- **Tích hợp Slack/Telegram**: Nhận thông báo ngay khi backup thành công hoặc khi có lỗi.  
- **Tối ưu thời gian chạy**: Đặt lịch chạy vào ban đêm hoặc thời điểm ít traffic để tránh ảnh hưởng đến hệ thống chính.

## 📌 Kết luận
Workflow “Back up self‑hosted workflows to Google Drive daily with change detection” là giải pháp hoàn hảo cho các sếp muốn bảo vệ dữ liệu workflow n8n của mình một cách **đơn giản, nhanh chóng và an toàn**.  
Hãy thử ngay, bật lịch tự động, và để n8n lo liệu mọi thứ cho bạn – bạn chỉ cần tập trung vào việc phát triển nghiệp vụ.

Nếu cần hỗ trợ tùy chỉnh workflow, tích hợp thêm tính năng, hoặc có bất kỳ câu hỏi nào, hãy liên hệ với Chandan Singh qua email: **coolchandan62@gmail.com**. Happy automating!