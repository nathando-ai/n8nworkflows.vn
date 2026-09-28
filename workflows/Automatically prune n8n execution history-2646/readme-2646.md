---
title: "🚀 Xóa lịch sử thực thi n8n tự động – Giải pháp tối ưu cho workflow"
description: "Workflow này tự động xoá lịch sử thực thi cũ của n8n, giúp giảm tải và duy trì hiệu suất 24/7."
slug: "xoa-lich-su-thuc-hanh-n8n"
tags: [n8n, automation, no-code, pruning, execution-history]
keywords: [n8n workflow, tự động hóa, xóa lịch sử, n8n execution, prune history]
---

# 🚀 Xóa lịch sử thực thi n8n tự động – Giải pháp tối ưu cho workflow

Bạn đang phải lo lắng vì **lịch sử thực thi** của n8n ngày càng đầy rẫy, làm chậm hệ thống và chiếm dung lượng lưu trữ?  
Workflow này sẽ **xoá bỏ các thực thi cũ** một cách tự động, giúp bạn duy trì hệ thống sạch sẽ, nhanh chóng và không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm dung lượng**: Xóa tự động các thực thi cũ, tránh tràn disk.
- **Tăng tốc độ**: Giảm tải cho cơ sở dữ liệu, giúp workflow phản hồi nhanh hơn.
- **Dễ dàng quản lý**: Không cần thao tác thủ công, giảm rủi ro lỗi con người.
- **Chạy liên tục 24/7**: Đảm bảo hệ thống luôn sẵn sàng và ổn định.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản n8n** đã được cài đặt và chạy (Self-hosted hoặc n8n Cloud).
- **Credentials**: `n8nApi` – API key của n8n (có thể tạo trong Settings → Credentials → n8n API).
- **Quyền**: API key phải có quyền `Read` và `Delete` trên resource `execution`.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/2646) hoặc copy nội dung JSON.
2. Mở **n8n Editor**, chọn **Import** → **Import from Clipboard** hoặc **Import from File**.
3. Dán JSON và nhấn **Import**. Workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **When clicking ‘Test workflow’** (manualTrigger) | Để kiểm tra nhanh workflow. | Không cần cấu hình. |
| **n8n1** (n8n, resource: execution) | Lấy danh sách thực thi hiện tại. | - |
| **n8n list execution** (n8n, resource: execution) | Lấy danh sách thực thi (để so sánh). | - |
| **If** | Kiểm tra số lượng thực thi > giới hạn (ví dụ 1000). | `Conditions` → `{{ $json["executions"].length }}` > 1000. |
| **Schedule Trigger** | Đặt lịch chạy tự động (ví dụ: hàng ngày lúc 02:00). | `Cron` hoặc `Interval`. |
| **delete execution** (n8n, operation: delete, resource: execution) | Xóa thực thi cũ. | `Execution ID` lấy từ node trước. |
| **No Operation, do nothing** | Kết thúc khi không cần xoá. | Không cần cấu hình. |

**Lưu ý**:  
- Node **delete execution** cần được kết nối với **If** node khi điều kiện đúng.  
- Đảm bảo **n8nApi** credentials được chọn cho tất cả các node `n8n`.  
- Nếu muốn xoá nhiều thực thi cùng lúc, bạn có thể lặp qua danh sách bằng `SplitInBatches` hoặc `Function` node, nhưng workflow gốc chỉ xoá một thực thi tại một lần chạy.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy thủ công bằng cách nhấn nút **Execute Workflow**. Kiểm tra log xem có thực thi xoá hay không.
2. **Bật Active**: Sau khi xác nhận, chuyển workflow sang trạng thái **Active**. Nếu bạn đã cấu hình **Schedule Trigger**, workflow sẽ chạy tự động theo lịch.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi báo cáo qua Slack**: Thêm node `Slack` sau `delete execution` để thông báo số thực thi đã xoá.
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại thời gian và số lượng thực thi xoá.
- **Tăng cường bảo mật**: Sử dụng `Webhook` với token bảo mật để kích hoạt workflow từ bên ngoài.
- **Tùy chỉnh giới hạn**: Thay đổi điều kiện trong node `If` để xoá khi số thực thi vượt 500, 2000, tùy nhu cầu.

## 📌 Kết luận

Workflow **Automatically prune n8n execution history** là công cụ tuyệt vời giúp các sếp duy trì hệ thống n8n sạch sẽ và hiệu quả mà không cần tốn công sức.  
Hãy **đưa nó vào thực tiễn ngay hôm nay** – bạn sẽ cảm nhận được sự khác biệt trong tốc độ và độ tin cậy của workflow!