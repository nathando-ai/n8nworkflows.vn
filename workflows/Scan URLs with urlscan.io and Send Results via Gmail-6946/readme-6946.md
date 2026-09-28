---
title: "🚀 Quét URL với urlscan.io và gửi kết quả qua Gmail"
description: "Tự động quét URL, lấy screenshot và dữ liệu JSON, gửi qua Gmail 100% không cần code."
slug: "quet-url-urlscan-gmail"
tags: [n8n, automation, no-code, secops, urlscan, gmail]
keywords: [n8n workflow, tự động hóa, urlscan, gmail, secops]
---

# 🚀 Quét URL với urlscan.io và gửi kết quả qua Gmail

Bạn đang phải quét hàng trăm URL thủ công, chờ đợi screenshot và lấy dữ liệu JSON?  
Workflow này sẽ giúp bạn **tự động** thực hiện toàn bộ quy trình chỉ với một lần POST, **không cần viết code** và **đảm bảo độ chính xác**.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Quét và nhận kết quả trong vài giây thay vì hàng giờ.  
- **Độ chính xác cao**: Tránh sai sót do nhập liệu thủ công.  
- **Tự động hóa 100%**: Không cần can thiệp, chỉ cần gửi POST.  
- **Cập nhật liên tục**: Mỗi lần gửi URL mới, workflow tự động chạy và gửi email.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **urlScanIo API Key**: Đăng ký tại [urlscan.io](https://urlscan.io) → Settings → API Key.  
- **Gmail OAuth2**: Cấu hình trong n8n → Credentials → Gmail OAuth2.  
- **Địa chỉ email nhận**: Đặt trong node Gmail (To).  
- **Webhook URL**: Được tạo khi workflow được kích hoạt.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow (địa chỉ: https://n8n.io/workflows/6946).  
2. Mở n8n → **Workflows** → **Import** → **Upload File** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| Webhook | `Webhook` | `Path: urlscan` <br> `HTTP Method: POST` | Đảm bảo URL công khai (ví dụ: `https://your-domain.com/webhook/urlscan`). |
| urlScanIo | `Perform a scan` | **Credentials**: `urlScanIoApi` <br> **URL**: từ body (`{{ $json.url }}`) | Không hard-code API key. |
| Wait | `Wait` | **Wait Time**: 30s (tăng nếu screenshot chưa sẵn sàng). | Giúp urlscan.io tạo screenshot. |
| Gmail | `Send a message` | **Credentials**: `gmailOAuth2` <br> **To**: địa chỉ nhận <br> **Subject**: “Kết quả quét URL” <br> **Body**: Thêm link tới result page, screenshot, JSON. | Đặt `{{ $json.resultUrl }}` v.v. |

> **Sticky Note**: Được dùng để ghi chú nội dung trong workflow, không ảnh hưởng tới thực thi.

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn node đầu tiên (Webhook) → **Execute Node** với payload mẫu:  
   ```json
   { "url": "https://example.com" }
   ```  
2. Kiểm tra log: Xác nhận ID, result URL, screenshot URL, JSON URL.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận thông báo ngay khi email được gửi.  
- **Lưu log**: Dùng Google Sheets hoặc Airtable để ghi lại lịch sử quét.  
- **Báo cáo định kỳ**: Kết hợp với node “Cron” để gửi báo cáo hàng ngày/tuần.  
- **Đính kèm file**: Nếu muốn gửi screenshot/JSON dưới dạng attachment, cấu hình trường **Attachments** trong Gmail node.  
- **Tùy chỉnh email**: Sử dụng HTML trong body để tạo email đẹp mắt, bao gồm hình ảnh screenshot inline.

## 📌 Kết luận
Workflow “Scan URLs với urlscan.io và Send Results via Gmail” là giải pháp **đơn giản, nhanh chóng, không cần code** cho các bộ phận SecOps.  
Hãy **đăng ký API key**, **cấu hình Gmail OAuth2**, **import workflow** và **bật nó** ngay hôm nay để tự động quét URL và nhận kết quả qua email.  

Chúc các sếp **đánh bại công việc thủ công** và **tăng năng suất**!