---
title: "🚀 Tự động thêm thành viên mới vào Mailchimp chỉ với 1 click"
description: "Giải pháp workflow n8n giúp doanh nghiệp thêm khách hàng vào danh sách Mailchimp một cách nhanh chóng, chính xác và không cần viết code."
slug: "create-new-member-mailchimp"
tags: [n8n, automation, no-code, mailchimp, marketing]
keywords: [n8n workflow, tự động hóa, Mailchimp, marketing automation, no-code]
---

# 🚀 Tự động thêm thành viên mới vào Mailchimp chỉ với 1 click

Bạn đang phải nhập tay từng email vào danh sách Mailchimp? Mỗi lần thêm một khách hàng mới là một công việc lặp đi lặp lại, dễ gây sai sót và mất thời gian. Workflow “Create a new member on Mailchimp” của n8n giúp bạn **đưa khách hàng vào danh sách Mailchimp 100% tự động, không cần code**. Chỉ cần một lần click “Execute” và workflow sẽ thực hiện việc thêm thành viên ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Bỏ qua thao tác nhập tay, chỉ cần 1 click.
- **Độ chính xác cao**: Tránh sai sót khi nhập dữ liệu thủ công.
- **Tích hợp dễ dàng**: Có thể kết nối với các công cụ khác như Slack, Google Sheets, hay webhook.
- **Tự động liên tục**: Khi workflow được kích hoạt, dữ liệu luôn được cập nhật ngay lập tức.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Mailchimp**: Đăng ký và lấy **API Key**.
- **Mailchimp List ID**: ID của danh sách mà bạn muốn thêm thành viên.
- **n8n**: Đã cài đặt và chạy (Self-hosted hoặc n8n.cloud).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/413) hoặc sao chép nội dung JSON.
2. Mở **n8n Editor**, chọn **Import** → **Import from Clipboard** hoặc **Import from File**.
3. Dán JSON và nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh |
|------|----------|---------------------|
| 1 | **On clicking 'execute'** | Không cần cấu hình thêm. Đây là trigger thủ công. |
| 2 | **Mailchimp** | - **Credentials**: Chọn `mailchimpApi` đã tạo.<br>- **Operation**: `Add a member to a list`.<br>- **List ID**: Điền ID danh sách Mailchimp.<br>- **Email address**: Chọn trường dữ liệu (ví dụ: `{{$json["email"]}}`).<br>- **Status**: `subscribed` (hoặc tùy chọn).<br>- **Merge Fields**: Nếu muốn thêm tên, số điện thoại, v.v., điền các trường tương ứng. |

> **Lưu ý**: Nếu bạn muốn workflow nhận dữ liệu từ nguồn khác (ví dụ: Google Sheets), hãy thay đổi trigger thành `Webhook` hoặc `Google Sheets` và điều chỉnh mapping dữ liệu cho phù hợp.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút **Execute Node** trên node `On clicking 'execute'` để kiểm tra xem dữ liệu có được gửi thành công tới Mailchimp không. Kiểm tra console logs và Mailchimp dashboard.
2. **Bật Active**: Khi mọi thứ hoạt động đúng, chuyển trạng thái workflow sang **Active** để tự động chạy khi trigger được kích hoạt.

## ✍️ Mẹo & gợi ý nâng cao

- **Tích hợp Slack**: Thêm node `Slack` để gửi thông báo khi thành viên mới được thêm.
- **Lưu log**: Dùng node `Write Binary File` hoặc `Google Sheets` để ghi lại lịch sử thêm thành viên.
- **Gửi báo cáo định kỳ**: Kết hợp với node `Cron` để gửi danh sách thành viên mới mỗi ngày/tuần.
- **Xử lý lỗi**: Thêm node `If` để kiểm tra `status` trả về từ Mailchimp và gửi email cảnh báo khi có lỗi.

## 📌 Kết luận

Workflow “Create a new member on Mailchimp” là công cụ **đơn giản nhưng mạnh mẽ** giúp doanh nghiệp tiết kiệm thời gian và giảm sai sót khi quản lý danh sách email. Hãy thử ngay, tích hợp vào quy trình marketing của bạn và cảm nhận sự khác biệt! Nếu cần hỗ trợ, hãy liên hệ với cộng đồng n8n hoặc đặt câu hỏi tại diễn đàn của chúng tôi. Happy automating!