---
title: "🚀 Tự động gửi email marketing dựa trên hành vi với GPT‑4o và SendGrid"
description: "Giải pháp tự động hóa 100% gửi email cá nhân hóa dựa trên hành vi người dùng, giảm thời gian và tăng tỷ lệ chuyển đổi."
slug: "tuy-chinh-email-gpt-4o-sendgrid"
tags: [n8n, automation, no-code, marketing, AI]
keywords: [n8n workflow, tự động hóa, email marketing, GPT‑4o, SendGrid]
---

# 🚀 Tự động gửi email marketing dựa trên hành vi với GPT‑4o và SendGrid

Bạn đang mất hàng giờ để viết email cá nhân hóa cho từng khách hàng? Bạn muốn gửi email vào thời điểm tối ưu, dựa trên hành vi thực tế của người dùng? Workflow này sẽ giúp bạn:

- Thu thập dữ liệu hành vi từ website và email trong thời gian thực.
- Phân đoạn người dùng theo hành vi (intent cao, giỏ hàng bỏ rơi, cần tái tương tác…).
- Tạo nội dung email tự động, cá nhân hóa bằng GPT‑4o‑mini.
- Gửi email qua SendGrid với timing thông minh và ghi log vào Google Sheet.
- Hoàn toàn không cần viết code, chỉ cần cấu hình credentials.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo nội dung và gửi email, giảm công việc thủ công tới 90%.
- **Chính xác hơn**: Gửi email vào thời điểm người dùng có khả năng mở cao nhất.
- **Cá nhân hóa sâu**: GPT‑4o‑mini tạo nội dung dựa trên dữ liệu hành vi thực tế.
- **Tăng tỷ lệ chuyển đổi**: Email được gửi tới đúng đối tượng, đúng lúc, tăng ROI.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Mô tả | Credential cần thiết |
|---------|-------|-----------------------|
| **Webhook** | Nhận sự kiện website/email | URL webhook (được n8n tạo) |
| **SendGrid** | Gửi email | API Key SendGrid |
| **OpenAI** | Tạo nội dung email | API Key OpenAI |
| **Google Sheets** (hoặc Airtable) | Ghi log campaign | Credentials Google Sheets |
| **Website Tracking** | Gửi sự kiện hành vi | GA4, Segment, pixel tùy chọn |
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥
1. Tải file JSON từ <https://n8n.io/workflows/15615> hoặc copy nội dung JSON.  
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON → **Import**.  
3. Workflow sẽ xuất hiện với tên “Send behavior‑based marketing emails with OpenAI GPT‑4o and SendGrid”.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên thực tế | Mục đích | Tham số cần cấu hình |
|------|-------------|----------|----------------------|
| **Webhook – Website & Email Events** | `Webhook - Website & Email Events` | Nhận dữ liệu sự kiện | Path: `behavior-event-webhook`, Method: `POST` |
| **Schedule Trigger – Daily Behavior Digest** | `Daily Behavior Digest` | Gửi digest hàng ngày | Thời gian (ví dụ 00:00 UTC) |
| **Set – Prepare Event Context** | `Prepare Event Context` | Chuẩn bị dữ liệu context | Định dạng JSON, fields |
| **Code – Python – Segment Behavior** | `Python - Segment Behavior` | Phân đoạn hành vi (intent, cart, re‑engagement) | Script Python, input fields |
| **Filter – High Intent / Abandoned Cart / Re‑engagement** | `Filter High Intent`, `Filter Abandoned Cart`, `Filter Re‑engagement` | Lọc các nhóm mục tiêu | Conditions (e.g., intent > 0.7) |
| **Wait – Rate Limit** | `Wait - Rate Limit` | Giới hạn tốc độ gửi | Duration (ms) |
| **Agent – Generate Personalized Email** | `AI - Generate Personalized Email` | Gọi GPT‑4o‑mini để tạo nội dung | Prompt template, input data |
| **Code – JS – Format Campaign** | `JS - Format Campaign` | Định dạng email (subject, body) | Script JS |
| **Wait – Send Buffer** | `Wait - Send Buffer` | Đợi buffer trước khi gửi | Duration (ms) |
| **HTTP Request – Send Personalized Email** | `Send Personalized Email` | Gửi email qua SendGrid | URL: `https://api.sendgrid.com/v3/mail/send`, Method: `POST`, Headers: `Authorization: Bearer <API_KEY>` |
| **HTTP Request – Log Campaign to Sheet** | `Log Campaign to Sheet` | Ghi log vào Google Sheet | URL Sheets API, Method: `POST` |
| **OpenAI Chat Model** | `OpenAI Chat Model` | Định nghĩa model GPT‑4o‑mini | Credentials: `openAiApi`, Model: `gpt-4o-mini` |
| **Wait For Result** | `Wait For Result` | Đợi kết quả AI | Duration (ms) |

> **Tip**: Kiểm tra từng node, đảm bảo **Credentials** đã được tạo trong n8n → **Credentials** → **Add New**.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đăng ký webhook, gửi payload JSON).  
2. Kiểm tra log, email đã gửi, sheet đã ghi.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack/Telegram để thông báo khi email gửi thành công.  
- **Logging**: Sử dụng node `Set` để ghi log vào một bảng `Logs` trong Google Sheet.  
- **Scheduled Reports**: Thêm node `Schedule Trigger` để gửi báo cáo hàng tuần tới quản trị viên.  
- **Dynamic Segmentation**: Thêm điều kiện `Filter` mới (ví dụ: “New Visitor”, “High Value Customer”) để mở rộng mục tiêu.  
- **Rate Limiting**: Tùy chỉnh node `Wait - Rate Limit` theo giới hạn API của SendGrid.

## 📌 Kết luận
Workflow “Send behavior‑based marketing emails with OpenAI GPT‑4o and SendGrid” là công cụ mạnh mẽ giúp các sếp tự động hóa chiến dịch email dựa trên hành vi thực tế, giảm công sức, tăng hiệu quả và tối ưu hoá ROI. Hãy triển khai ngay hôm nay, thử nghiệm và điều chỉnh cho phù hợp với doanh nghiệp của bạn!