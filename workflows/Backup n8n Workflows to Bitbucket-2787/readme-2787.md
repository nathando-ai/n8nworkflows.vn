---
title: "🚀 Sao lưu Workflows n8n lên Bitbucket tự động, không lo mất dữ liệu"
description: "Tự động sao lưu toàn bộ workflows n8n mỗi ngày vào repository Bitbucket, giúp các sếp bảo vệ dữ liệu, quản lý phiên bản và giảm rủi ro mất mát."
slug: "sao-luu-workflows-n8n-bitbucket"
tags: [n8n, automation, no-code, backup, bitbucket, workflow]
keywords: [n8n workflow, tự động sao lưu, Bitbucket, backup workflow, no-code automation]
---

# 🚀 Sao lưu Workflows n8n lên Bitbucket tự động, không lo mất dữ liệu

Khi các sếp quản lý một hệ thống n8n với hàng chục, thậm chí hàng trăm workflow, việc sao lưu thủ công mỗi khi có thay đổi là cực kỳ mất thời gian và dễ gây sai sót. Thêm vào đó, nếu server gặp sự cố, các workflow quan trọng có thể biến mất trong chớp mắt.  
**Workflow “Backup n8n Workflows to Bitbucket”** giải quyết vấn đề này 100% tự động: mỗi ngày vào lúc 02:00 sáng, nó sẽ lấy danh sách tất cả workflow hiện có, so sánh với bản sao đã lưu trên Bitbucket và chỉ tải lên những workflow mới hoặc đã thay đổi. Không cần viết code, không cần thao tác thủ công – chỉ cần cấu hình một lần và để nó chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Bảo vệ dữ liệu:** Mọi workflow đều được lưu trữ an toàn trên Bitbucket, tránh mất mát khi server hỏng.  
- **Quản lý phiên bản:** Mỗi lần thay đổi sẽ tạo commit mới, giúp các sếp dễ dàng rollback hoặc xem lịch sử.  
- **Tiết kiệm thời gian:** Không còn phải sao lưu thủ công, chỉ cần một lần thiết lập.  
- **Giảm rủi ro rate‑limit:** Workflow tự động chờ giữa các request để không bị Bitbucket chặn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản n8n** (để lấy API key `n8nApi`).  
- **Tài khoản Bitbucket** với **Workspace** và **Repository** đã tạo sẵn.  
- **Credentials HTTP Basic Auth** cho Bitbucket (username + app password).  
- **Quyền truy cập**: API key n8n cần quyền `Read/Write` các workflow; Bitbucket app password cần quyền `Repository: Write`.  
- **n8n đang chạy** (self‑hosted hoặc cloud) và có thể truy cập internet để gọi API Bitbucket.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ link gốc hoặc đính kèm).  
2. Vào n8n → **Workflows** → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình chúng:

| Node | Loại | Mô tả ngắn | Cấu hình cần chỉnh |
|------|------|------------|--------------------|
| **Run Daily at 2 AM** | `scheduleTrigger` | Kích hoạt workflow mỗi ngày lúc 02:00. | Đảm bảo múi giờ (Timezone) phù hợp với môi trường của các sếp. |
| **Get All Workflows** | `n8n` | Lấy danh sách toàn bộ workflow hiện có từ n8n. | **Credentials:** chọn `n8nApi` → nhập API Key của n8n. |
| **Loop Workflows** | `splitInBatches` | Duyệt từng workflow một cách batch. | **Batch Size:** để mặc định (1) hoặc tùy chỉnh nếu workflow rất nhiều. |
| **Get Existing Workflow from Bitbucket** | `httpRequest` | Kiểm tra file workflow đã tồn tại trên Bitbucket. | **Credentials:** `httpBasicAuth` (username + app password). <br> **Method:** `GET` <br> **URL:** `https://api.bitbucket.org/2.0/repositories/{{ $json["workspace"] }}/{{ $json["repo"] }}/src/master/{{ $json["name"] }}.json` <br> **Response Format:** `JSON`. |
| **New or Changed?** | `if` | So sánh hash (hoặc nội dung) của workflow hiện tại với file trên Bitbucket. | **Condition:** `{{ $json["exists"] === false || $json["localHash"] !== $json["remoteHash"] }}` (có thể dùng `Set` node để tạo hash). |
| **Upload Workflow to Bitbucket** | `httpRequest` | Đẩy workflow mới/đã thay đổi lên Bitbucket. | **Credentials:** `httpBasicAuth`. <br> **Method:** `POST` <br> **URL:** `https://api.bitbucket.org/2.0/repositories/{{ $json["workspace"] }}/{{ $json["repo"] }}/src` <br> **Form Data:** <br> - `files/{{ $json["name"] }}.json` → `{{ $json["workflowData"] }}` <br> - `message` → `"Backup: {{ $json["name"] }} - {{ $now }}`". |
| **Wait to Avoid Rate Limiting** | `wait` | Dừng một khoảng thời gian ngắn để tránh hitting rate limit của Bitbucket. | **Time to Wait:** giá trị được tính bởi node **Calculate Wait Time** (thường 1‑2 giây). |
| **Set Bitbucket Workspace & Repository** | `set` | Đặt các biến tĩnh cho workspace và repo. | **Fields:** `workspace` (tên workspace), `repo` (tên repository). |
| **Calculate Wait Time** | `code` | Tính thời gian chờ ngẫu nhiên (ví dụ 1‑3 giây) để giảm khả năng bị rate‑limit. | Không cần thay đổi, chỉ cần chắc chắn output là `waitTime`. |

**Lưu ý quan trọng:**
- **Credentials**: Đảm bảo `httpBasicAuth` được tạo trong **Credentials** → **HTTP Basic Auth** và gán cho các node HTTP.  
- **Tên file**: Workflow sẽ được lưu dưới dạng `{{ workflowName }}.json`. Đảm bảo không có ký tự đặc biệt trong tên workflow.  
- **Permission**: Bitbucket app password phải có quyền `Repository: Write` để có thể tạo/ghi file.  

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow bằng nút **Execute Workflow** → kiểm tra log để chắc chắn các request tới Bitbucket thành công.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Kiểm tra repository Bitbucket vào ngày hôm sau để xác nhận các file `.json` đã được tạo/ cập nhật.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Upload Workflow to Bitbucket` để gửi tin nhắn báo cáo thành công hoặc lỗi.  
- **Lưu log chi tiết**: Dùng node `Write Binary File` để ghi log chạy vào một file trên server, giúp debug khi có lỗi.  
- **Backup định kỳ toàn bộ repository**: Kết hợp với node `Cron` khác để tạo snapshot toàn bộ repo (zip) và lưu vào S3 hoặc Google Drive.  
- **Kiểm tra thay đổi bằng hash**: Thay vì so sánh toàn bộ nội dung, dùng node `Code` để tạo SHA‑256 hash của workflow JSON, giảm tải so sánh.  

### 📌 Kết luận
Với workflow “Backup n8n Workflows to Bitbucket”, các sếp sẽ có một giải pháp sao lưu tự động, an toàn và có khả năng quản lý phiên bản mạnh mẽ mà không tốn công sức lập trình. Hãy triển khai ngay hôm nay, bảo vệ tài sản quan trọng của doanh nghiệp và tập trung vào việc phát triển các automation giá trị hơn! 🚀