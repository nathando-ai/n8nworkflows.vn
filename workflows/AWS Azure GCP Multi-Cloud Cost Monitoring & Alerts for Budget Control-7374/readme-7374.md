---
title: "🚀 Giám sát chi phí đa đám mây AWS, Azure, GCP & gửi cảnh báo tự động"
description: "Workflow n8n tự động thu thập, phân tích và cảnh báo chi phí trên ba nền tảng đám mây, giúp doanh nghiệp kiểm soát ngân sách 100% không cần code."
slug: "gia-mot-chi-phi-da-dam-may-aws-azure-gcp"
tags: [n8n, automation, no-code, devops, cloud-cost-management]
keywords: [n8n workflow, tự động hóa, chi phí đám mây, giám sát chi phí, cảnh báo chi phí]
---

# 🚀 Giám sát chi phí đa đám mây AWS, Azure, GCP & gửi cảnh báo tự động

Bạn đang phải lắp ghép nhiều bảng tính, dashboard và script để theo dõi chi phí trên AWS, Azure và GCP? Mỗi lần cập nhật dữ liệu, bạn phải làm thủ công, dễ sai sót và mất thời gian. Workflow n8n này sẽ giải quyết ngay vấn đề đó: **thu thập dữ liệu chi phí 24/7, phân tích tự động, phát hiện lộ trình chi tiêu bất thường và gửi cảnh báo tới Email, WhatsApp, Slack – hoàn toàn không cần viết code.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động chạy mỗi giờ, không cần thao tác thủ công.
- **Chính xác 100%**: Dữ liệu được lấy trực tiếp từ API chính thức của AWS, Azure, GCP.
- **Cá nhân hóa**: Gửi cảnh báo tới từng nhóm/owner dựa trên quy tắc tự động.
- **Hoạt động liên tục**: Được triển khai 24/7 trên VPS, không bị gián đoạn.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **AWS**: Tạo API Key và Secret Key, bật AWS Cost Explorer API. Cấu hình `httpBasicAuth` trong node **AWS Billing Fetch**.
- **Azure**: Đăng ký Azure Cost Management API, lấy `Client ID`, `Client Secret`, `Tenant ID`. Cấu hình `oAuth1Api` trong node **Azure Billing Fetch**.
- **GCP**: Tạo Service Account, tải file JSON key, bật Cloud Billing API. Cấu hình `oAuth1Api` trong node **GCP Billing Fetch**.
- **Email**: Cấu hình SMTP (địa chỉ máy chủ, port, username, password) trong node **Alert Sender On Email**.
- **WhatsApp**: Đăng ký Twilio/WhatsApp API, lấy `Account SID`, `Auth Token`, `WhatsApp number`. Cấu hình `whatsAppApi` trong node **Alert Sender On WhatsApp**.
- **Slack**: Tạo Slack App, lấy `Bot Token`. Cấu hình `slackApi` trong node **Alert Sender On Slack**.
- **Node.js**: Đảm bảo môi trường n8n có thể chạy các node `code` (JavaScript).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
- Tải file JSON từ link gốc: <https://n8n.io/workflows/7374>.
- Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc copy toàn bộ JSON vào ô nhập liệu.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên trong workflow | Cấu hình cần chỉnh | Ghi chú |
|------|--------------------|---------------------|---------|
| Cron Trigger | Cron Trigger | `Interval: 1 hour` | Đặt thời gian chạy hàng giờ. |
| AWS Billing Fetch | AWS Billing Fetch | `httpBasicAuth` → API Key/Secret | URL: `https://costexplorer.amazonaws.com` |
| Azure Billing Fetch | Azure Billing Fetch | `oAuth1Api` → Client ID/Secret/Tenant | URL: `https://management.azure.com/providers/Microsoft.CostManagement/query` |
| GCP Billing Fetch | GCP Billing Fetch | `oAuth1Api` → Service Account | URL: `https://cloudbilling.googleapis.com/v1/projects/{projectId}/billingInfo` |
| Data Parser | Data Parser | **Code** (JS) – hợp nhất dữ liệu | Đảm bảo output là mảng các mục chi phí. |
| Cost Spike Detector | Cost Spike Detector | **Code** (JS) – so sánh với ngân sách | Trả về `true` nếu vượt ngưỡng. |
| Owner Identifier | Owner Identifier | `if` condition → `owner` field | Định tuyến theo owner. |
| Auto-Tag Resource | Auto-Tag Resource | **Code** (JS) – gọi API tag | Đặt tag “cost-alert” cho resource. |
| Alert Sender On Email | Alert Sender On Email | `smtp` credentials, `to`, `subject`, `body` | Body có thể lấy từ `Cost Spike Detector` output. |
| Alert Sender On WhatsApp | Alert Sender On WhatsApp | `whatsAppApi` credentials, `to`, `message` | Gửi tin nhắn ngắn gọn. |
| Alert Sender On Slack | Alert Sender On Slack | `slackApi` credentials, `channel`, `text` | Đưa thông tin chi tiết. |

> **Lưu ý**: Các node `code` cần copy code mẫu từ tài liệu gốc hoặc viết lại tùy theo cấu trúc dữ liệu trả về. Đảm bảo `return` đúng định dạng JSON.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute Workflow”).
2. Kiểm tra logs, đảm bảo không có lỗi.
3. Khi mọi thứ ổn, bật **Active** (đánh dấu nút “Active”).
4. Đảm bảo cron trigger đang chạy (bạn sẽ thấy “Last run” trong lịch sử).

## ✍️ Mẹo & gợi ý nâng cao
- **Lưu log vào database**: Thêm node `MySQL` hoặc `PostgreSQL` để ghi lại lịch sử chi phí.
- **Cảnh báo theo mức độ**: Sử dụng Slack attachments để hiển thị màu đỏ/đỏ cho mức chi phí cao.
- **Báo cáo định kỳ**: Thêm node `Cron` khác để gửi báo cáo hàng ngày/tuần qua Email.
- **Tích hợp với Teams**: Thêm node `Microsoft Teams` để nhận cảnh báo trong kênh doanh nghiệp.
- **Tự động điều chỉnh ngân sách**: Khi phát hiện vượt ngưỡng, gọi API của từng cloud để tắt dịch vụ tạm thời.

## 📌 Kết luận
Workflow n8n “AWS Azure GCP Multi-Cloud Cost Monitoring & Alerts for Budget Control” giúp các sếp **đánh giá chi phí, phát hiện lộ trình chi tiêu bất thường và hành động kịp thời** mà không cần viết dòng code. Hãy triển khai ngay trên VPS của mình, cấu hình các credential và bật workflow – bạn sẽ thấy chi phí được kiểm soát chặt chẽ, giảm rủi ro và tăng tính minh bạch cho toàn bộ tổ chức. 🚀