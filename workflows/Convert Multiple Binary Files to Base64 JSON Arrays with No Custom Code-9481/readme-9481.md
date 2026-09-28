---
title: "🚀 Chuyển Đổi Nhiều File Binary Thành Mảng JSON Base64 Không Cần Code"
description: "Tự động giải nén, mã hoá Base64 và tổng hợp các file binary thành JSON chỉ với 7 node trong n8n, không viết một dòng code."
slug: "chuyen-doi-nhiieu-file-binary-base64-json"
tags: [n8n, automation, no-code, file-processing, base64]
keywords: [n8n workflow, tự động hóa, chuyển đổi file base64, không code, xử lý binary]
---

# 🚀 Chuyển Đổi Nhiều File Binary Thành Mảng JSON Base64 Không Cần Code

Bạn đã bao giờ phải **giải nén một tập tin zip**, sau đó **mã hoá từng file thành Base64** và **đóng gói lại thành một JSON** để gửi cho API bên ngoài?  
Nếu có, bạn chắc đã tốn rất nhiều thời gian viết và bảo trì các đoạn JavaScript trong node **Code**.  

**Workflow này** giải quyết toàn bộ quy trình **100 % không code** chỉ với **7 node**:
- Giải nén (Compression)  
- Tải file zip (HTTP Request)  
- Tách từng file (Split Out)  
- Mã hoá Base64 (Extract From File)  
- Gắn lại đường dẫn (Set)  
- Tổng hợp thành mảng JSON (Aggregate)  

Kết quả: **Một payload JSON chuẩn** chứa `path` và `content` (Base64) của mọi file, sẵn sàng gửi API mà không lo lỗi cú pháp hay mất dữ liệu.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không cần viết một dòng JavaScript.  
- **Độ chính xác cao**: Mỗi file được mã hoá và gắn lại đường dẫn tự động.  
- **Mở rộng dễ dàng**: Thêm node gửi API, Slack, hoặc lưu log chỉ trong vài cú click.  
- **Hoạt động liên tục**: Workflow có thể chạy 24/7 trên VPS, không phụ thuộc vào máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **API key** (nếu bạn muốn tải zip từ một dịch vụ bảo mật).  
- **Quyền truy cập internet** để gọi HTTP Request tới file zip.  
- **Không cần bất kỳ credential nào khác** vì các node đều xử lý binary nội bộ.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/9481).  
2. Vào **n8n Editor → Import** → **Upload JSON** hoặc **Copy/Paste** nội dung JSON.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình quan trọng |
|------|---------|----------------------|
| **Start** (Manual Trigger) | Bắt đầu workflow | Không cần thay đổi. |
| **Download Demo Website** (HTTP Request) | Tải file zip từ URL | - **Method**: `GET` <br> - **URL**: nhập link zip của bạn (ví dụ: `https://example.com/demo.zip`). <br> - **Response Format**: `File` để nhận dạng binary. |
| **Unzip Demo Website** (Compression) | Giải nén file zip | - **Operation**: `Decompress` <br> - **Binary Property**: `data` (mặc định). |
| **Split Out Files** (Split Out) | Tách từng file thành một item | - **Binary Property**: `data` (kết quả từ node Compression). |
| **Encode Files to Base64** (Extract From File) | Chuyển binary → Base64 | - **Operation**: `Binary To Property` <br> - **Binary Property**: `{{ $binary.keys()[0] }}` (đảm bảo luôn lấy file hiện tại). <br> - **Property Name**: `content` (kết quả Base64). |
| **Add Path to Files** (Set) | Gắn lại đường dẫn đầy đủ | - **Values to Set**: <br>   - **Key**: `path` <br>   - **Value**: `{{ $binary.keys()[0] }}` (đường dẫn gốc trong zip). |
| **Aggregate Output** (Aggregate) | Tổng hợp thành một JSON duy nhất | - **Mode**: `Keep Key Values` <br> - **Field to Aggregate**: `path,content` <br> - **Output Property**: `files` (sẽ tạo mảng `files`). |

> **Lưu ý:** Đảm bảo **Binary Property** trong các node `Extract From File` và `Split Out` luôn trỏ tới key binary thực tế (thường là `data`). Nếu bạn đổi tên binary ở node trước, hãy cập nhật tương ứng.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** trên node **Start** để chạy thử với một file zip mẫu.  
2. Kiểm tra output cuối cùng ở node **Aggregate Output** – bạn sẽ thấy một item dạng:  

```json
{
  "files": [
    { "path": "folder/file1.txt", "content": "SGVsbG8gd29ybGQ=" },
    { "path": "folder/sub/file2.jpg", "content": "/9j/4AAQSkZJRgABAQAAAQ..." }
  ]
}
```

3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi màu xanh) để workflow tự động chạy mỗi khi bạn kích hoạt trigger (Manual, Cron, Webhook, …).

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi API ngay sau Aggregate**: Thêm node **HTTP Request** để POST payload `{{ $json["files"] }}` tới API của bạn.  
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi tin “Upload thành công X file” kèm link log.  
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** để ghi lại `path`, `size`, `timestamp`.  
- **Xử lý file lớn**: Kết hợp node **Split In Batches** để chia payload thành các batch nhỏ, tránh giới hạn payload của API.  

### 📌 Kết luận
Với **7 node** và **không một dòng code nào**, các sếp đã có thể biến một file zip thành **JSON array Base64** chuẩn, sẵn sàng tích hợp vào bất kỳ API nào. Hãy **import ngay**, **điều chỉnh URL zip**, và **bật Active** – công việc tẻ nhạt sẽ biến thành một cú click!  

Chúc các sếp thành công và luôn “no‑code, no‑pain”! 🚀