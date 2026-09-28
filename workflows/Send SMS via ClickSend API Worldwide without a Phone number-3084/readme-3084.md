---
title: "🚀 Gửi SMS toàn cầu qua ClickSend API – Không cần số điện thoại"
description: "Tự động gửi tin nhắn SMS tới bất kỳ quốc gia nào chỉ với vài cú click, không cần thiết lập số điện thoại gửi. Workflow n8n hoàn toàn không cần code."
slug: "gui-sms-toan-goc-qua-clicksend-api"
tags: [n8n, automation, no-code, clicksend, sms, api]
keywords: [n8n workflow, tự động hóa, SMS, ClickSend, API]
---

# 🚀 Gửi SMS toàn cầu qua ClickSend API – Không cần số điện thoại

Bạn đang gặp khó khăn khi muốn gửi SMS tới khách hàng quốc tế mà không muốn quản lý số điện thoại gửi? Workflow này sẽ giúp bạn **tự động gửi tin nhắn SMS** tới bất kỳ quốc gia nào chỉ với vài cú click, hoàn toàn không cần viết code. Bạn chỉ cần một tài khoản ClickSend, một vài thông tin cấu hình và workflow sẽ làm việc 24/7 cho bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Gửi hàng trăm tin nhắn chỉ trong vài giây.  
- **Độ chính xác cao**: Không cần lo lắng về định dạng số điện thoại.  
- **Tự động 24/7**: Workflow chạy liên tục, không cần can thiệp thủ công.  
- **Chi phí thấp**: Bắt đầu với 2 € credit miễn phí, chỉ trả khi sử dụng.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản ClickSend**: Đăng ký tại [ClickSend](https://clicksend.com/?u=586989) và lấy API Key.  
- **Creds n8n**: Tạo credential `Basic Auth` trong n8n với tên đăng nhập và API Key làm mật khẩu.  
- **Thông tin SMS**: Nhiệm vụ của node `Set SMS data` là nhập nội dung tin nhắn và số điện thoại người nhận (bao gồm tiền tố quốc gia, ví dụ: `+39` + số điện thoại).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc hoặc sao chép JSON vào editor n8n.  
2. Trong n8n, chọn **Import Workflow** → **Upload JSON** → chọn file.  
3. Workflow sẽ xuất hiện với 3 node: `When clicking ‘Test workflow’`, `Send SMS`, `Set SMS data`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | `When clicking ‘Test workflow’` | Không cần cấu hình thêm | Node này dùng để trigger thủ công khi muốn thử. |
| 2 | `Set SMS data` | - `Text` (nội dung tin nhắn) <br> - `To` (số điện thoại người nhận, bao gồm +xx) | Đảm bảo không có khoảng trắng trong số điện thoại. |
| 3 | `Send SMS` | - **Credentials**: Chọn `Basic Auth` đã tạo. <br> - **HTTP Method**: POST <br> - **URL**: `https://rest.clicksend.com/v3/sms/send` <br> - **Body**: JSON với `messages` array chứa `to`, `body` | Node này thực hiện gọi API. |

> **Tip**: Nếu bạn muốn gửi nhiều tin nhắn cùng lúc, hãy cấu hình `Set SMS data` để trả về một mảng `messages` và dùng `SplitInBatches` trước `Send SMS`.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** trong n8n để kiểm tra dữ liệu mẫu.  
2. Kiểm tra log của node `Send SMS` xem có lỗi không.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Bây giờ bạn có thể trigger thủ công hoặc tích hợp với webhook/trigger khác.

## ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack**: Thêm node `Slack` để nhận thông báo khi SMS gửi thành công hoặc thất bại.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại lịch sử gửi tin.  
- **Gửi báo cáo định kỳ**: Kết hợp với `Cron` node để gửi báo cáo tổng hợp số tin đã gửi mỗi ngày.  
- **Quản lý số điện thoại**: Nếu muốn gửi từ nhiều số, tạo một danh sách số trong Google Sheets và dùng `Set` + `SplitInBatches` để lặp qua từng số.  

## 📌 Kết luận
Workflow này giúp các sếp **đơn giản hóa quy trình gửi SMS** tới khách hàng toàn cầu mà không cần quản lý số điện thoại gửi. Với ClickSend API và n8n, bạn có thể **tự động, nhanh chóng và chi phí thấp**. Hãy thử ngay hôm nay và trải nghiệm sự tiện lợi của tự động hóa 100% không code!