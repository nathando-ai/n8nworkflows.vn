---
title: "🚀 Tự động Nhận và Xử Lý Lead Web Form cho Odoo CRM"
description: "Workflow n8n giúp nhận dữ liệu từ form web, chuyển đổi thành cơ hội bán hàng trong Odoo CRM – hoàn toàn không cần code."
slug: "tac-dong-nhan-va-xu-ly-lead-web-form-cho-odoo-crm"
tags: [n8n, automation, no-code, odoo, crm]
keywords: [n8n workflow, tự động hóa, Odoo CRM, capture leads, web form]
---

# 🚀 Tự động Nhận và Xử Lý Lead Web Form cho Odoo CRM

Bạn đang phải nhập thủ công dữ liệu từ các form web vào Odoo CRM? Mỗi lần một lead mới xuất hiện, bạn phải copy‑paste, kiểm tra, và tạo cơ hội bán hàng – tốn thời gian, dễ lỗi và không hiệu quả.  
Workflow này sẽ **tự động** nhận dữ liệu từ webhook, xử lý, và tạo **Opportunity** trong Odoo CRM, giúp bạn tiết kiệm thời gian, giảm sai sót và tăng tốc độ chuyển đổi khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập dữ liệu thủ công, giảm 80% công việc lặp đi lặp lại.
- **Chính xác hơn**: Dữ liệu được chuyển trực tiếp, giảm sai sót do người dùng nhập.
- **Tự động hóa liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc.
- **Tăng tốc độ chuyển đổi**: Lead mới ngay lập tức được tạo thành Opportunity, giúp đội bán hàng hành động nhanh hơn.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Odoo** (v15‑v18) với quyền **Create** trên mô hình `crm.lead` hoặc `crm.opportunity`.
- **Odoo API Key** hoặc **OAuth2 credentials** (được cấu hình trong n8n Credentials).
- **URL webhook** sẽ được tạo bởi node `Webhook` trong workflow.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/5477) hoặc sao chép nội dung JSON.
2. Mở **n8n Editor**, chọn **Import** → **Import from JSON** → dán nội dung JSON → **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| Webhook | `Webhook` | *HTTP Method*: `POST` <br>*Path*: `/odoo-lead` (hoặc tùy chọn) | Đảm bảo URL sẽ được expose qua ngrok hoặc VPS. |
| Code | `Code` | *Code*: xử lý dữ liệu nhận được (ví dụ: chuyển đổi JSON, chuẩn hóa trường). | Không cần credentials. |
| Create Opportunity | `Create Opportunity` | *Credentials*: Odoo <br>*Model*: `crm.lead` hoặc `crm.opportunity` <br>*Fields*: map dữ liệu từ node Code vào các trường Odoo (e.g., `name`, `email_from`, `phone`, `partner_name`). | Kiểm tra tên trường chính xác với Odoo. |
| Respond to Webhook | `Respond to Webhook` | *Response*: `200 OK` + message (ví dụ: `{"status":"success"}`) | Gửi phản hồi tới form web để xác nhận. |

> **Tip**: Nếu form web yêu cầu xác nhận JSON, hãy cấu hình `Respond to Webhook` với `Content-Type: application/json`.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Node** trên `Webhook` với dữ liệu mẫu (có thể dùng Postman).
2. Kiểm tra trong Odoo xem Opportunity đã được tạo chưa.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram Notification**: Thêm node `Slack` hoặc `Telegram` sau `Create Opportunity` để gửi thông báo khi lead mới được tạo.
- **Lưu Log**: Sử dụng node `Write Binary File` hoặc `Google Sheets` để ghi lại dữ liệu nhận được, hỗ trợ audit trail.
- **Scheduled Cleanup**: Thêm node `Cron` để chạy hàm `Code` định kỳ, xóa dữ liệu tạm thời hoặc gửi báo cáo hàng ngày.
- **Validation**: Thêm node `Function` để kiểm tra tính hợp lệ của email/phone trước khi gửi tới Odoo.

## 📌 Kết luận
Workflow này giúp các sếp **đưa dữ liệu từ form web ngay vào Odoo CRM** mà không cần viết một dòng code. Bạn chỉ cần cấu hình một vài credentials và chạy. Hãy thử ngay, và nếu muốn mở rộng, thêm Slack, email hay log để workflow của bạn trở nên hoàn chỉnh hơn. 🚀

---

**Tác giả**: Evozard (🚀 AI & Automation Expert | n8n Creator)  
**Link gốc**: <https://n8n.io/workflows/5477>