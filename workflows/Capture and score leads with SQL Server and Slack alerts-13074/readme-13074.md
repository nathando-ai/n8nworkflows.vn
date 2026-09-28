---
title: "🚀 Thu thập và xếp hạng khách hàng tiềm năng với SQL Server & Slack Alerts"
description: "Workflow tự động thu thập leads, tính điểm, và gửi cảnh báo Slack cho leads nóng, giảm thời gian xử lý thủ công."
slug: "thu-thap-va-xep-hang-khach-hang"
tags: [n8n, automation, no-code, lead-generation, ai-summarization]
keywords: [n8n workflow, tự động hóa, lead generation, scoring, Slack alerts, SQL Server]
---

# 🚀 Thu thập và xếp hạng khách hàng tiềm năng với SQL Server & Slack Alerts

Bạn đang phải xử lý hàng trăm, hàng nghìn leads mỗi ngày? Việc nhập dữ liệu thủ công, kiểm tra email, tính điểm và gửi cảnh báo tới đội ngũ bán hàng không chỉ tốn thời gian mà còn dễ gây sai sót.  
Workflow này giúp bạn **thu thập leads 100% tự động**, **tính điểm** dựa trên tiêu chí đã định, và **gửi cảnh báo Slack** ngay lập tức cho những leads nóng. Kết quả: giảm 80% công việc thủ công, tăng tốc độ phản hồi và nâng cao chất lượng chuyển đổi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý leads, giảm 80% công việc nhập liệu.  
- **Chính xác hơn**: Kiểm tra email và tính điểm theo logic đã định, giảm lỗi con người.  
- **Cá nhân hóa**: Gửi cảnh báo Slack tùy theo mức độ nóng của lead.  
- **Hoạt động liên tục**: Workflow 24/7, không phụ thuộc vào giờ làm việc.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Tài khoản / Dịch vụ | Mô tả | Cách lấy |
|----------------------|-------|----------|
| **Slack** | Token Bot (xem Slack API) | `xoxb-xxxxxxxxxx` |
| **API Upsert Contact** | URL endpoint & API key | Định dạng: `https://api.example.com/contacts/upsert` |
| **API Update Score** | URL endpoint & API key | Định dạng: `https://api.example.com/contacts/update-score` |
| **SQL Server** | Kết nối (host, db, user, pass) | Sử dụng trong node `Code` (đã được cấu hình sẵn) |
| **Webhook URL** | Địa chỉ nhận dữ liệu leads | Tự tạo khi import workflow |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc:  
   <https://n8n.io/workflows/13074> → `Download JSON`.
2. Mở n8n Editor → `File` → `Import` → chọn file JSON vừa tải.  
   Hoặc copy toàn bộ JSON → `File` → `Import` → `Paste JSON`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Webhook - Lead Capture** | Nhận dữ liệu từ form hoặc API bên ngoài | `Path` (ví dụ: `/lead-capture`) |
| **Normalize Lead Data** | Chuyển đổi dữ liệu thành định dạng chuẩn | Không cần chỉnh |
| **IF - Valid Email** | Kiểm tra email hợp lệ | Không cần chỉnh |
| **Format Error Response** | Định dạng lỗi | Không cần chỉnh |
| **Respond - Validation Error** | Trả về lỗi validation | Không cần chỉnh |
| **Prepare API Body** | Tạo body cho API Upsert | Không cần chỉnh |
| **API - Upsert Contact** | Gọi API upsert | `URL`, `Method`, `Headers` (API key) |
| **Calculate Lead Score** | Tính điểm lead | Không cần chỉnh |
| **Score Router** | Chuyển hướng theo điểm | Định nghĩa ngưỡng: Hot ≥ 80, Warm 50–79, Cold < 50 |
| **Format Slack Alert** | Định dạng tin nhắn Slack | Không cần chỉnh |
| **Slack - Hot Lead Alert** | Gửi cảnh báo cho leads nóng | `Channel`, `Token` |
| **API - Update Score (Hot)** | Cập nhật điểm cho leads nóng | `URL`, `Headers` |
| **API - Update Score (Warm)** | Cập nhật điểm cho leads ấm | `URL`, `Headers` |
| **Log Cold Lead** | Ghi log leads lạnh | Không cần chỉnh |
| **Format Success Response** | Định dạng phản hồi thành công | Không cần chỉnh |
| **Respond - Success** | Trả về thành công | Không cần chỉnh |
| **Error Trigger** | Xử lý lỗi | Không cần chỉnh |
| **Format Error** | Định dạng lỗi | Không cần chỉnh |
| **Slack - Error Alert** | Gửi cảnh báo lỗi tới Slack | `Channel`, `Token` |

> **Lưu ý**: Mỗi node `HTTP Request` cần có **Credential** (API key) đã được tạo trong phần `Credentials` của n8n. Nếu chưa có, vào `Credentials` → `Add New` → chọn `HTTP Basic Auth` hoặc `API Key` tùy API.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút `Execute Workflow` với dữ liệu mẫu (có thể copy JSON từ `Webhook - Lead Capture`).  
2. Kiểm tra log: Đảm bảo không có lỗi, leads được upsert và score được cập nhật.  
3. **Bật Active**: Bật công tắc `Active` ở góc trên bên phải.  
4. **Kiểm tra Slack**: Đảm bảo tin nhắn cảnh báo được gửi tới kênh đã cấu hình.

## ✍️ Mẹo & gợi ý nâng cao

- **Thêm Slack/Telegram**: Sử dụng node `Telegram` để gửi cảnh báo tới nhóm bán hàng.  
- **Lưu log chi tiết**: Thêm node `HTTP Request` gửi log tới một endpoint logging (ví dụ: Loggly, Papertrail).  
- **Báo cáo định kỳ**: Thêm node `Cron` + `HTTP Request` để gửi báo cáo tổng hợp leads hàng ngày tới email hoặc Slack.  
- **Tự động cập nhật ngưỡng**: Sử dụng node `Code` để lấy ngưỡng từ database hoặc biến môi trường, giúp dễ dàng điều chỉnh mà không cần chỉnh workflow.  
- **Bảo mật**: Sử dụng `n8n` secrets manager để lưu trữ API key, token Slack, và credentials SQL Server.

## 📌 Kết luận

Workflow “Capture and score leads with SQL Server and Slack alerts” là giải pháp tối ưu cho các doanh nghiệp muốn **tự động hoá toàn bộ quy trình** từ thu thập leads, tính điểm, tới cảnh báo ngay lập tức.  
Hãy **cài đặt ngay** trên VPS riêng, cấu hình các credentials, và bật workflow. Bạn sẽ thấy thời gian xử lý giảm đáng kể, đội ngũ bán hàng phản hồi nhanh hơn, và doanh thu tăng lên.  

**Bắt đầu ngay hôm nay** – vì mỗi lead nóng đang chờ đợi phản hồi của bạn!