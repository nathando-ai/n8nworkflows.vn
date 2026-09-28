---
title: "🚀 Clone Workflow giữa các Instance n8n – Tự động hoá 100%"
description: "Giải pháp chuyển toàn bộ workflows từ một instance n8n sang instance khác chỉ với vài cú click, tiết kiệm thời gian và tránh lỗi thủ công."
slug: "clone-workflow-n8n"
tags: [n8n, automation, no-code, workflow, API]
keywords: [n8n workflow, tự động hóa, clone workflow, n8n API, no-code automation]
---

# 🚀 Clone Workflow giữa các Instance n8n – Tự động hoá 100%

Bạn đang quản lý nhiều instance n8n cho các dự án khác nhau? Thủ công sao chép workflow từ một instance sang instance khác không chỉ tốn thời gian mà còn dễ gây lỗi khi copy‑paste cấu hình. Workflow “Clone n8n Workflows between Instances using n8n API” của Alex Kim (n8n Ambassador & Verified Partner) giúp bạn **đơn giản hóa quy trình** này thành một chuỗi tự động 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ cần 1 workflow chạy, không cần thao tác thủ công.  
- **Độ chính xác cao**: Tự động lấy dữ liệu từ API, tránh sai sót khi copy.  
- **Tích hợp linh hoạt**: Có thể clone cả workflow, project, và các tham số liên quan.  
- **Tự động hoá liên tục**: Đặt lên cron hoặc trigger tự động để đồng bộ định kỳ.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Hai credentials n8nApi**:  
  - *Source* – credential của instance nguồn (để lấy danh sách workflow).  
  - *Destination* – credential của instance đích (để tạo workflow).  
- **Project ID (tùy chọn)**: Nếu muốn clone vào một project cụ thể, cần biết `projectId` của destination.  
- **API URL**: Đảm bảo endpoint `https://<your-instance>/rest` đã được bật.  
- **Quyền truy cập**: Credential phải có quyền `read` và `write` trên cả hai instance.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ <https://n8n.io/workflows/3048> hoặc copy nội dung JSON.  
2. Mở **n8n Editor**, chọn **Import** → **JSON** → dán nội dung.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **When clicking ‘Test workflow’** | Trigger thủ công | Không cần thay đổi |
| **GET - Workflows** | Lấy danh sách workflow nguồn | `credentials`: *Source n8nApi* |
| **CREATE - Workflow** | Tạo workflow mới trên đích | `credentials`: *Destination n8nApi*; `operation`: `create` |
| **n8n - GET - Projects** | Lấy danh sách project đích | `credentials`: *Destination n8nApi* |
| **SET Project ID** | Đặt `projectId` cho workflow mới | `projectId`: ID project đích (nếu cần) |
| **PUT - Workflow in Project** | Gắn workflow vào project | `credentials`: *Destination n8nApi* |
| **Loop Over Items** | Lặp qua từng workflow nguồn | Không cần thay đổi |
| **GET - Destination Workflows** | Kiểm tra workflow đã tồn tại | `credentials`: *Destination n8nApi* |
| **Code** | Kiểm tra và chuẩn bị dữ liệu | Không cần thay đổi |
| **Split Out Workflows / Split Out Workflows1** | Phân tách dữ liệu workflow | Không cần thay đổi |
| **Merge Workflows** | Gộp dữ liệu thành một mảng | Không cần thay đổi |
| **Split Out Projects** | Phân tách project | Không cần thay đổi |
| **Filter Project** | Lọc project cần clone | `projectName`: tên project đích (nếu muốn) |

> **Chú ý**:  
> - Đảm bảo **đặt đúng credential** cho từng node `n8n` và `httpRequest`.  
> - Nếu muốn clone vào một project cụ thể, chỉnh `projectId` trong node **SET Project ID**.  
> - Nếu muốn clone toàn bộ project, bỏ qua node **Filter Project**.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow bằng nút **Execute Workflow** để kiểm tra dữ liệu mẫu.  
2. Kiểm tra console logs, đảm bảo không có lỗi `401/403`.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Đặt trigger tự động (cron, webhook) nếu muốn đồng bộ định kỳ.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo qua Slack**: Thêm node Slack `Send Message` sau khi clone xong để thông báo thành công.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets `Append Row` để ghi lại tên workflow, thời gian clone.  
- **Thêm xác thực 2FA**: Sử dụng node `HTTP Request` với header `Authorization: Bearer <token>` để bảo mật hơn.  
- **Clone nhiều project**: Sử dụng `SplitInBatches` để lặp qua danh sách project nguồn và đích.

## 📌 Kết luận
Workflow “Clone n8n Workflows between Instances using n8n API” là công cụ **đắc lực** giúp các sếp tiết kiệm thời gian, giảm lỗi và duy trì đồng nhất giữa các instance n8n. Hãy thử ngay, tùy chỉnh theo nhu cầu và chia sẻ trải nghiệm của mình!