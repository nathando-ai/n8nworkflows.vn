---
title: "🚀 Sao lưu Workflows n8n lên Google Drive tự động"
description: "Tự động sao lưu toàn bộ workflow n8n mỗi ngày vào Google Drive, bảo vệ dữ liệu và giảm rủi ro mất mát."
slug: "sao-luu-workflows-n8n-google-drive"
tags: [n8n, automation, no-code, backup, google-drive]
keywords: [n8n workflow, sao lưu n8n, tự động hóa, Google Drive, backup workflow]
---

# 🚀 Sao lưu Workflows n8n lên Google Drive tự động

Bạn có bao giờ lo lắng khi một workflow quan trọng bị xóa nhầm, server gặp sự cố hoặc muốn chuyển sang môi trường mới?  
Việc **export thủ công** từng workflow, lưu vào máy tính rồi sao chép lên đám mây không chỉ tốn thời gian mà còn dễ gây lỗi.  

**Workflow này** sẽ giải quyết mọi nỗi lo: mỗi ngày vào 02:30 am, toàn bộ danh sách workflow của n8n sẽ được **đóng gói thành file JSON** và **đẩy tự động lên Google Drive** của bạn. Ngoài ra, bạn vẫn có thể **kích hoạt thủ công** bất kỳ lúc nào bằng nút “Execute”. Hoàn toàn **không cần viết code** – chỉ cần cấu hình một lần và để n8n làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ dữ liệu**: Mỗi workflow luôn có bản sao lưu mới nhất trên Google Drive.  
- **Tiết kiệm thời gian**: Không còn việc export thủ công, chỉ một cú click hoặc để tự động chạy.  
- **Độ chính xác 100 %**: Dữ liệu được lấy trực tiếp qua API, không bị lỗi copy‑paste.  
- **Hoạt động liên tục**: Lịch chạy hàng ngày, luôn sẵn sàng phục hồi khi cần.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (phiên bản mới nhất) đang chạy và có **API endpoint** (thường là `https://your-n8n-instance.com`).  
- **Tài khoản Google** với quyền **Google Drive API** được bật, tạo **OAuth 2.0 Client ID** và lưu **Credentials** (`googleApi`).  
- **HTTP Basic Auth** cho n8n API (username & password) – sẽ dùng trong các node `httpRequest`.  
- Thư mục Google Drive nơi lưu backup (cần **Folder ID**).  
- (Tùy chọn) Địa chỉ email nhận thông báo lỗi (nếu muốn thêm node Email).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON của workflow (hoặc copy toàn bộ JSON và dán vào ô “Paste JSON”).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node quan trọng** và cách cấu hình chi tiết:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **On clicking 'execute'** | `manualTrigger` | Không cần thay đổi, dùng để chạy thủ công. |
| **Run Daily at 2:30am** | `cron` | Đặt **Minute** = `30`, **Hour** = `2`, **Timezone** = `Asia/Ho_Chi_Minh` (hoặc múi giờ phù hợp). |
| **Get Workflow List** | `httpRequest` | - **Method**: `GET` <br> - **URL**: `{{ $json["baseUrl"] }}/workflow` <br> - **Authentication**: chọn **HTTP Basic Auth** → nhập username & password của n8n. |
| **Get Workflow** | `httpRequest` | - **Method**: `GET` <br> - **URL**: `{{ $json["baseUrl"] }}/workflow/{{ $json["id"] }}` <br> - **Authentication**: **HTTP Basic Auth** (giống trên). |
| **FunctionItem** | `functionItem` | Mã JavaScript (được cung cấp trong workflow) chuyển **workflow JSON** thành **binary data** (`item.binary = { data: { data: Buffer.from(JSON.stringify(item.json), 'utf8'), mimeType: 'application/json', fileName: `${item.json.name}.json` } }`). |
| **Map** | `function` (được đặt tên “Map”) | Định dạng lại danh sách workflow, tạo mảng các **ID** để truyền cho node `Get Workflow`. |
| **Merge** | `merge` | Đặt **Mode** = `Pass Through` → `Wait for All` để chờ toàn bộ request trả về. |
| **Move Binary Data** | `moveBinaryData` | Di chuyển binary từ node `FunctionItem` sang node `Google Drive`. Đặt **Source Property** = `data`, **Destination Property** = `binary`. |
| **Google Drive** | `googleDrive` | - **Operation**: `Upload` <br> - **File Name**: `{{$binary["data"].fileName}}` <br> - **Folder ID**: nhập **Folder ID** của thư mục backup trên Drive. <br> - **Credentials**: chọn **Google API** đã tạo. |

> **Lưu ý:** Các node `httpRequest` cần biến môi trường `baseUrl` (URL n8n) được khai báo trong **Set** hoặc **Environment Variable** của n8n để dễ bảo trì.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → Kiểm tra log, đảm bảo file JSON xuất hiện trong Google Drive.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải).  
3. Kiểm tra lịch chạy: Vào **Executions** → Xem lịch `Run Daily at 2:30am` đã được kích hoạt.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram ngay sau node Google Drive để gửi tin nhắn “Backup thành công” kèm link file.  
- **Lưu log chi tiết**: Dùng node **Google Sheets** hoặc **Airtable** để ghi lại thời gian, số lượng workflow, và trạng thái backup.  
- **Nén file**: Trước khi upload, dùng node **Code** (Node.js) để zip toàn bộ file JSON thành một archive `.zip` → giảm dung lượng lưu trữ.  
- **Phiên bản lưu trữ**: Đặt tên file theo ngày (`backup-{{ $now.format("YYYY-MM-DD") }}-{{ $json["name"] }}.json`) để dễ quản lý lịch sử.  

## 📌 Kết luận
Với workflow **“Backup n8n Workflows to Google Drive”**, các sếp sẽ không còn lo lắng về việc mất mát các quy trình tự động quan trọng. Chỉ cần một lần cấu hình, n8n sẽ tự động **đóng gói & lưu trữ** mọi workflow vào Google Drive mỗi ngày, đồng thời cho phép **run thủ công** bất kỳ lúc nào. Hãy triển khai ngay hôm nay để bảo vệ tài sản kỹ thuật số của doanh nghiệp! 🚀