---
title: "🚀 Sao lưu workflow n8n tự động lên Google Drive & Slack"
description: "Giải pháp tự động sao lưu toàn bộ workflow n8n lên Google Drive, đồng thời gửi thông báo thành công hoặc lỗi qua Slack, giúp doanh nghiệp giảm thiểu rủi ro mất dữ liệu và tăng tính minh bạch."
slug: "sao-luu-workflow-n8n-tro-voi-google-drive-va-slack"
tags: [n8n, automation, no-code, devops, backup]
keywords: [n8n workflow, tự động hóa, sao lưu workflow, google drive backup, slack notification]
---

# 🚀 Sao lưu workflow n8n tự động lên Google Drive & Slack

Bạn đang phải sao lưu thủ công từng workflow n8n, mất thời gian, dễ sai sót và có thể quên mất một vài workflow quan trọng?  
Workflow này sẽ **tự động** tạo thư mục mới trên Google Drive, lưu toàn bộ cấu trúc workflow dưới dạng file JSON, nén file và gửi thông báo tới kênh Slack khi hoàn thành hoặc khi có lỗi. Bạn chỉ cần kích hoạt một lần và workflow sẽ chạy 24/7 mà không cần can thiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thao tác thủ công, workflow tự động thực hiện mọi bước.
- **Đảm bảo chính xác**: Mỗi lần chạy đều tạo file JSON đầy đủ, tránh sai sót khi sao chép thủ công.
- **Cá nhân hóa**: Tùy chỉnh tên thư mục, kênh Slack, tần suất chạy theo nhu cầu.
- **Hoạt động liên tục**: Chạy theo lịch (ví dụ: hàng ngày, hàng tuần) hoặc khi cần (manual trigger).
- **Bảo mật**: Dữ liệu lưu trữ trên Google Drive, có thể thiết lập quyền truy cập riêng.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Drive OAuth2**: Tạo credential `googleDriveOAuth2Api` trong n8n.
- **Slack API**: Tạo credential `slackApi` và lấy `Channel ID` cần gửi thông báo.
- **n8n API**: Tạo credential `n8nApi` để gọi API nội bộ lấy danh sách workflow.
- **VPS hoặc máy chủ Self-hosted**: Để chạy workflow 24/7.
- (Tùy chọn) **M