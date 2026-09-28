---
title: "🚀 Tăng tốc 9 lần khi gửi dữ liệu tới Airtable với n8n – Batching tự động"
description: "Workflow n8n giúp gửi dữ liệu tới Airtable nhanh hơn 9 lần bằng cách chia batch, giảm tải API và tăng hiệu suất."
slug: "batch-airtable-requests-9x-fast"
tags: [n8n, automation, no-code, Airtable, batch-processing, API]
keywords: [n8n workflow, tự động hóa, Airtable, batch processing, API, no-code]
---

# 🚀 Tăng tốc 9 lần khi gửi dữ liệu tới Airtable với n8n – Batching tự động

Bạn đang phải gửi hàng nghìn bản ghi tới Airtable mỗi ngày? Việc gửi từng bản ghi một không chỉ tốn thời gian mà còn dễ bị giới hạn tốc độ của API. Workflow này sẽ giúp bạn **gửi dữ liệu tới Airtable 9 lần nhanh hơn** bằng cách tự động chia dữ liệu thành các batch, giảm số lần gọi API và tối ưu hiệu suất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Gửi dữ liệu 9 lần nhanh hơn, giảm thời gian chờ API.  
- **Độ chính xác cao**: Batching giảm lỗi do giới hạn tốc độ, dữ liệu được xử lý đồng bộ.  
- **Tự động hóa 100%**: Không cần code, chỉ cần cấu hình credentials và kích hoạt workflow.  
- **Khả năng mở rộng**: Dễ dàng điều chỉnh batch size, thêm các bước xử lý dữ liệu khác.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Tài khoản / Dịch vụ | Mô tả | Lưu ý |
|----------------------|-------|-------|
| **Airtable** | API Key, Base ID, Table Name | Lưu trữ trong n8n Credentials (HTTP Basic Auth hoặc API Key). |
| **n8n** | Self‑hosted hoặc n8n Cloud | Cài đặt phiên bản mới nhất để hỗ trợ node `executeWorkflow`. |
| **Sub‑workflow** | `Airtable_Batch_Processor` | Đảm bảo sub‑workflow đã được import và có tên chính xác. |
| **Webhook (tùy chọn)** | Nếu muốn trigger từ bên ngoài | Cấu hình URL trong node `Batch_Airtable`. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/2831> hoặc copy nội dung JSON.  
2. Mở n8n Editor → **Workflows** → **Import** → **Upload JSON**.  
3. Chọn file hoặc dán JSON, rồi nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên thực tế | Mô tả | Cấu hình cần chỉnh |
|------|-------------|-------|---------------------|
| **Batch_Airtable** | `executeWorkflowTrigger` | Trigger workflow (manual hoặc webhook). | Đặt URL webhook nếu dùng trigger từ bên ngoài. |
| **mode** | `switch` | Chọn chế độ `upsert` hoặc `insert`. | Đặt giá trị mặc định hoặc truyền từ trigger. |
| **upsert_airtable** | `httpRequest` | Gửi request upsert tới Airtable. | - URL: `https://api.airtable.com/v0/{BaseID}/{TableName}`<br>- Method: PATCH<br>- Header: `Authorization: Bearer {API_KEY}`<br>- Body: JSON theo Airtable API. |
| **insert_airtable** | `httpRequest` | Gửi request insert tới Airtable. | - URL: `https://api.airtable.com/v0/{BaseID}/{TableName}`<br>- Method: POST<br>- Header: `Authorization: Bearer {API_KEY}`<br>- Body: JSON. |
| **set_Batching_vars** | `set` | Định nghĩa kích thước batch (ví dụ 10). | Đặt `batchSize: 10`. |
| **compile_records** / **compile_records1** | `summarize` | Tập hợp dữ liệu thành mảng để split. | Đặt `mode: "array"` và `value: $json`. |
| **Each_10_items** / **Each_10_items1** | `splitInBatches` | Chia dữ liệu thành các batch 10. | Đặt `batchSize: 10`. |
| **Airtable_Batch_Processor** | `executeWorkflow` | Gọi sub‑workflow để xử lý batch. | Đặt `workflowId` tới sub‑workflow `Airtable_Batch_Processor`. |
| **upsert_airtable / insert_airtable** | `httpRequest` | Gọi API Airtable trong sub‑workflow. | Sử dụng credentials đã cấu hình. |

> **Tip**: Kiểm tra **Credentials** trong n8n → **Credentials** → **HTTP Basic Auth** hoặc **API Key**. Đảm bảo tên credential trùng với node.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút **Execute Workflow** → nhập dữ liệu mẫu (mảng bản ghi).  
2. Kiểm tra log: Đảm bảo các node `Each_10_items` và `Airtable_Batch_Processor` thực thi thành công.  
3. Khi mọi thứ ổn, bật **Active** (đánh dấu xanh) để workflow tự động chạy khi trigger.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram Notification**: Thêm node `Slack` hoặc `Telegram` sau `Airtable_Batch_Processor` để nhận thông báo khi batch hoàn thành.  
- **Lưu Log**: Sử dụng node `Write Binary File` để ghi log vào file hoặc `Google Sheets` để lưu lịch sử.  
- **Thời gian chạy định kỳ**: Thêm node `Cron` để trigger workflow hàng giờ, ngày.  
- **Tối ưu batch size**: Thử nghiệm với `batchSize: 20` hoặc `30` tùy thuộc vào giới hạn API của Airtable.  

## 📌 Kết luận

Workflow **Batch Airtable requests to send data 9x faster** là công cụ mạnh mẽ giúp các sếp tiết kiệm thời gian, giảm tải API và tự động hóa quy trình gửi dữ liệu tới Airtable. Hãy thử ngay, điều chỉnh batch size phù hợp và mở rộng thêm các bước xử lý tùy ý. Chúc các sếp thành công!