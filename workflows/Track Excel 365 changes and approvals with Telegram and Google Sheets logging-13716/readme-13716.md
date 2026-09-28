---
title: "🚀 Theo dõi thay đổi Excel 365 và phê duyệt tự động qua Telegram + Google Sheets"
description: "Giải pháp tự động ghi nhận mọi thay đổi trong bảng tính Excel 365, gửi thông báo phê duyệt qua Telegram và lưu lịch sử vào Google Sheets – hoàn toàn không cần code."
slug: "theo-doi-thay-doi-excel-telegram-google-sheets"
tags: [n8n, automation, no-code, excel, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa, theo dõi excel, phê duyệt telegram, google sheets logging]
---

# 🚀 Theo dõi thay đổi Excel 365 và phê duyệt tự động qua Telegram + Google Sheets

Bạn đang phải mất hàng giờ mỗi ngày để kiểm tra bảng tính Excel 365, gửi email phê duyệt, và ghi lại lịch sử thay đổi trong Google Sheets?  
Workflow này sẽ **đưa toàn bộ quy trình vào một luồng công việc tự động 100%**, giúp bạn:

- Nhận thông báo ngay khi có thay đổi trong Excel.
- Gửi yêu cầu phê duyệt tới Telegram (hoặc Slack, Email…).
- Ghi lại mọi thay đổi và trạng thái phê duyệt vào Google Sheets.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở Excel, gửi email, ghi log thủ công.  
- **Chính xác & nhất quán**: Mọi thay đổi được ghi lại tự động, giảm thiểu sai sót.  
- **Cá nhân hóa**: Thông báo phê duyệt có thể tùy chỉnh nội dung, kèm hình ảnh, liên kết.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào lịch làm việc của con người.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Tên Credential | Mô tả | Cách tạo |
|---------|----------------|-------|----------|
| **Microsoft Excel (Office 365)** | `Microsoft Excel` | Kết nối tới tài khoản Office 365, cho phép đọc bảng tính. | Truy cập **n8n Credentials → Microsoft Excel → New Credential**. |
| **Google Sheets** | `Google Sheets` | Kết nối tới tài khoản Google, cho phép ghi dữ liệu vào bảng tính. | Truy cập **n8n Credentials → Google Sheets → New Credential**. |
| **Telegram Bot** | `Telegram` | Bot để gửi tin nhắn phê duyệt. | Tạo bot qua BotFather → nhận token → nhập vào n8n. |
| **Webhook (tùy chọn)** | `Webhook` | Nếu muốn kích hoạt workflow từ nguồn bên ngoài (ví dụ: khi có file upload). | Truy cập **n8n Credentials → Webhook → New Credential**. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc:  
   <https://n8n.io/workflows/13716> → **Download JSON**.  
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Mô tả | Tham số cần cấu hình |
|------|----------|-------|----------------------|
| **Schedule Trigger** | `scheduleTrigger` | Chạy workflow định kỳ (ví dụ: 5 phút). | `Cron Expression` (ví dụ: `*/5 * * * *`). |
| **Microsoft Excel** | `microsoftExcel` | Lấy danh sách thay đổi trong bảng tính. | `File ID`, `Worksheet Name`, `Range`, `Filter` (để lấy những dòng chưa được phê duyệt). |
| **If** | `if` | Kiểm tra điều kiện phê duyệt (ví dụ: cột “Status” = “Pending”). | `Expression` (ví dụ: `{{$json["Status"]}} === "Pending"`). |
| **Code** | `code` | Định dạng dữ liệu trước khi gửi tới Telegram/Google Sheets. | `JavaScript` code (định dạng JSON). |
| **Switch** | `switch` | Chuyển hướng tới “Approve” hoặc “Reject”. | `Switch Conditions` (ví dụ: `Approved`, `Rejected`). |
| **Telegram** | `telegram` | Gửi tin nhắn phê duyệt tới kênh/nhóm. | `Chat ID`, `Message Text`, `Parse Mode`. |
| **Google Sheets** | `googleSheets` | Ghi lại lịch sử thay đổi. | `Spreadsheet ID`, `Worksheet Name`, `Row Data`. |
| **Sticky Note** | `stickyNote` | Ghi chú cho từng bước (không ảnh hưởng tới logic). | Nội dung ghi chú. |

> **Lưu ý**:  
> - Đảm bảo **Credentials** đã được tạo và gán cho từng node.  
> - Kiểm tra **File ID** và **Spreadsheet ID** bằng cách mở file trong Excel/Sheets và sao chép từ URL.  
> - Nếu workflow sử dụng **Webhook**, hãy copy URL và cấu hình nguồn gửi dữ liệu (ví dụ: Zapier, Integromat).

### 3. Kích hoạt ⚡️

1. **Test run**: Chọn một dòng mẫu trong Excel, chạy workflow thủ công (`Execute Workflow`). Kiểm tra log, tin nhắn Telegram, và dữ liệu ghi vào Google Sheets.  
2. Nếu mọi thứ ổn, **bật** workflow (`Active`).  
3. Kiểm tra định kỳ: Đảm bảo rằng workflow chạy đúng lịch và không có lỗi.

## ✍️ Mẹo & gợi ý nâng cao

- **Thêm Slack**: Thay thế hoặc bổ sung node `Slack` để nhận tin nhắn phê duyệt.  
- **Lưu log vào Google Drive**: Dùng node `Google Drive` để lưu file log JSON mỗi lần chạy.  
- **Gửi báo cáo định kỳ**: Thêm node `Schedule Trigger` khác để gửi báo cáo hàng ngày/tuần qua Email hoặc Telegram.  
- **Tự động gửi email**: Thêm node `Email` (SMTP) để gửi email phê duyệt khi có thay đổi.  
- **Sử dụng AI Summarization**: Thêm node `OpenAI` hoặc `ChatGPT` để tóm tắt nội dung thay đổi trước khi gửi tới Telegram.

## 📌 Kết luận

Workflow “Track Excel 365 changes and approvals with Telegram and Google Sheets logging” là giải pháp tối ưu cho các doanh nghiệp muốn **đưa quy trình phê duyệt và ghi nhận thay đổi** vào một luồng tự động, giảm thiểu công việc thủ công và tăng tính chính xác.  
Hãy **cài đặt ngay** trên VPS của mình, cấu hình credentials, và bắt đầu trải nghiệm sự tiện lợi mà n8n mang lại!  

Chúc các sếp thành công và tiết kiệm thời gian!