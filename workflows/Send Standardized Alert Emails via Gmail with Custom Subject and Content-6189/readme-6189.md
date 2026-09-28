---
title: "🚀 Gửi Email Cảnh Báo Chuẩn Hóa qua Gmail – Tự Động Hóa 100%"
description: "Workflow n8n giúp gửi email cảnh báo với tiêu đề và nội dung tùy chỉnh, dễ nhận diện và quản lý trong Gmail."
slug: "gửi-email-cảnh-báo-qua-gmail"
tags: [n8n, automation, no-code, gmail, alert]
keywords: [n8n workflow, tự động hóa, email cảnh báo, gmail, no-code]
---

# 🚀 Gửi Email Cảnh Báo Chuẩn Hóa qua Gmail – Tự Động Hóa 100%

Bạn đang phải gửi hàng trăm email cảnh báo thủ công, mỗi lần phải chỉnh sửa tiêu đề, nội dung, và lo lắng về việc email bị Gmail đánh dấu “Không quan trọng” hay bị lạc trong hộp thư?  
Workflow này là giải pháp “điểm tắt” giúp bạn:

- **Tự động gửi** email cảnh báo với tiêu đề và nội dung tùy chỉnh.
- **Dễ dàng nhận diện** trong Gmail nhờ tiền tố `❗ n8n Alert:`.
- **Không cần code** – chỉ cần cấu hình một vài tham số và bật workflow.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết script, chỉ cấu hình 1 lần.  
- **Chính xác**: Tiêu đề và nội dung được chuẩn hoá, tránh lỗi đánh máy.  
- **Cá nhân hóa**: Dễ dàng truyền tham số từ workflow khác (subject, lines).  
- **Hoạt động liên tục**: Được chạy 24/7, không phụ thuộc vào máy tính cá nhân.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** có bật **OAuth2** và **được cấp quyền gửi email**.  
- **API Key** của Gmail (được tạo trong Google Cloud Console).  
- **Email nhận cảnh báo** (điền vào node Gmail).  
- **Workflow trigger** (được gọi từ workflow khác).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/6189>  
2. Trong n8n Editor, chọn **Import** → **Upload file** → chọn file JSON vừa tải.  
3. Hoặc copy toàn bộ JSON và dán vào **Import JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên | Tham số cần cấu hình | Ghi chú |
|------|-----|----------------------|---------|
| `When Executed by Another Workflow` | **Trigger** | `Workflow ID` (được lấy từ workflow gọi) | Đảm bảo workflow gọi truyền đúng `subject` và `lines`. |
| `Send a message` | **Gmail** | `To` – email nhận cảnh báo <br>`Subject` – `❗ n8n Alert: {{ $json.subject }}` <br>`Body` – `{{ $json.lines.join('\n') }}` <br>`Credentials` – Gmail OAuth2 | **Quan trọng**: Tiền tố `❗ n8n Alert:` giúp Gmail dễ lọc. |
| **Credentials** | Gmail OAuth2 | Đăng nhập Google, cấp quyền `Send Email` | Nếu chưa có, tạo mới trong **Credentials**. |

> ⚠️ **Nếu bạn thay đổi tiêu đề** (subject), **hãy cập nhật bộ lọc Gmail** (filter) để vẫn nhận được email có tiền tố `❗ n8n Alert:`.  

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công, truyền `subject` và `lines` mẫu.  
2. Kiểm tra hộp thư Gmail – email phải có tiêu đề `❗ n8n Alert: ...` và nội dung đúng.  
3. Bật **Active** cho workflow.  

## ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack**: Thêm node Slack để gửi cảnh báo ngay trong kênh.  
- **Lưu log**: Dùng node Google Sheets hoặc Airtable để ghi lại mọi email đã gửi.  
- **Báo cáo định kỳ**: Kết hợp với node “Cron” để gửi báo cáo tổng hợp hàng ngày/tuần.  
- **Gửi đính kèm**: Thêm file PDF/CSV từ node “Read Binary File” vào Gmail.  

## 📌 Kết luận
Workflow “Send Standardized Alert Emails via Gmail” là công cụ “điểm tắt” giúp các sếp tiết kiệm thời gian, giảm lỗi và quản lý cảnh báo hiệu quả.  
Hãy **tích hợp ngay** vào quy trình làm việc của mình, tận dụng sức mạnh của n8n mà không cần viết dòng code.  

Chúc các sếp thành công!