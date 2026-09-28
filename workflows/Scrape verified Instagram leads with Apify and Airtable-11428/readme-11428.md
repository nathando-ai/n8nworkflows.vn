---
title: "🚀 Scrape verified Instagram leads với Apify & Airtable – Tự động thu thập leads Instagram chất lượng"
description: "Workflow n8n giúp tự động scrape dữ liệu Instagram, lọc leads hợp lệ và lưu vào Airtable, chuẩn bị cho chiến dịch cold outreach."
slug: "scrape-verified-instagram-leads-apify-airtable"
tags: [n8n, automation, no-code, lead-generation, instagram, airtable, apify]
keywords: [n8n workflow, tự động hóa, lead generation, Instagram scraping, Airtable integration, Apify]
---

# 🚀 Scrape verified Instagram leads với Apify & Airtable

Bạn đang phải mất hàng giờ để tìm kiếm, lọc và xác thực leads Instagram?  
Workflow này sẽ **tự động 100%**: từ việc nhập query → scrape dữ liệu Instagram qua Apify → lọc email hợp lệ → lưu vào Airtable, sẵn sàng cho chiến dịch cold outreach mà không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** – giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ → vài phút.  
- **Chính xác**: Chỉ lưu leads có email hợp lệ (được xác thực qua API).  
- **Tự động liên tục**: Khi có query mới, workflow chạy ngay mà không cần can thiệp.  
- **Dễ dàng mở rộng**: Thêm Slack/Telegram thông báo, gửi báo cáo định kỳ, v.v.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Tài khoản / Dịch vụ | Mô tả | Cách lấy |
|---------------------|-------|----------|
| **Apify** | Actor “Google Search Scraper” (hoặc bất kỳ scraper nào lấy dữ liệu Instagram). | Đăng ký tại [Apify](https://apify.com) → tạo Actor → lấy API token. |
| **Airtable** | Base + Table có các trường: `Username`, `Contact Details`, `URL`, `Followers`, `Email Verifier`. | Đăng ký tại [Airtable](https://airtable.com) → tạo Personal Access Token. |
| **Email Verification API** | API để xác thực email (ví dụ: [EmailVerify](https://emailverify.com)). | Đăng ký API key. |
| **n8n** | Self‑hosted hoặc n8n.cloud. | Cài đặt n8n, tạo workflow. |
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/11428).  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** để tải workflow vào workspace.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Tham số cần cấu hình | Ghi chú |
|------|-------|----------------------|---------|
| **Form Trigger** | Nhận query từ người dùng (ví dụ: “keyword: fashion”). | `query` field | Đặt tên trường `query` trong form. |
| **Apify Scraping Data** | Gửi request tới Apify để lấy dữ liệu Instagram. | `URL`: `https://api.apify.com/v2/actor-tasks/<taskId>/run-syncs?token=<YOUR_TOKEN>` <br> `Body`: `{ "input": { "searchQuery": "{{$json.query}}" } }` | Thay `<taskId>` và `<YOUR_TOKEN>` bằng token của bạn. |
| **Wait** | Chờ Apify trả về dữ liệu. | `Wait for`: `Apify Scraping Data` | Đặt thời gian chờ (ví dụ: 30s). |
| **Split Out** | Tách mảng dữ liệu thành từng lead. | `Split by`: `items` | Đảm bảo dữ liệu trả về là mảng. |
| **If1** | Lọc những lead có email Gmail. | `Condition`: `{{$json.email}}` contains `gmail.com` | Nếu không, bỏ qua. |
| **Email Verifier** | Gọi API xác thực email. | `URL`: `https://api.emailverify.com/v1/verify?email={{$json.email}}&api_key=<YOUR_KEY>` | Thay `<YOUR_KEY>` bằng API key của bạn. |
| **Passing Emails** | Kiểm tra kết quả xác thực. | `Condition`: `{{$json.result.status}}` equals `valid` | Nếu hợp lệ, lưu vào Airtable. |
| **Airtable DB** | Upsert lead vào bảng Airtable. | `Operation`: `upsert` <br> `Base ID`, `Table Name` | Đảm bảo trường `Username`, `Contact Details`, `URL`, `Followers`, `Email Verifier` khớp với bảng. |
| **Sticky Note** | Ghi chú cho người dùng. | - | Không cần cấu hình. |

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Workflow** với dữ liệu mẫu (đặt query “fashion”).  
2. Kiểm tra logs: Đảm bảo dữ liệu đã được lấy, email đã được xác thực và lưu vào Airtable.  
3. Khi mọi thứ ổn, bật **Active** để workflow chạy tự động khi có form trigger mới.

## ✍️ Mẹo & gợi ý nâng cao

- **Thông báo Slack**: Thêm node `Slack` sau `Airtable DB` để gửi tin nhắn khi lead mới được lưu.  
- **Lưu log**: Dùng node `Write Binary File` để ghi log vào Google Drive hoặc S3.  
- **Báo cáo định kỳ**: Thêm node `Cron` + `Airtable` để xuất dữ liệu hàng ngày và gửi email.  
- **Tùy chỉnh Scraper**: Thay đổi Actor của Apify để lấy thêm trường `Bio`, `Website`, v.v.  

## 📌 Kết luận

Workflow “Scrape verified Instagram leads với Apify & Airtable” là công cụ **no-code** mạnh mẽ giúp các sếp nhanh chóng thu thập, xác thực và lưu trữ leads Instagram chất lượng.  
Hãy **đăng ký Apify, Airtable, Email Verify API** ngay, **import workflow** và **bật chạy** – bạn sẽ thấy thời gian tìm kiếm leads giảm gấp 10 lần, chất lượng tăng 100%!

Nếu có bất kỳ câu hỏi hoặc cần hỗ trợ, hãy liên hệ với tác giả:  
📧 [@msiddhant](#)