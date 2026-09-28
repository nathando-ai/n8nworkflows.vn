---
title: "🚀 Tự động sao chép bảng NocoDB và dữ liệu sang base mới"
description: "Workflow n8n sao chép toàn bộ cấu trúc và dữ liệu của các bảng NocoDB từ một base nguồn sang base đích chỉ trong vài cú click, không cần viết code."
slug: "tu-dong-sao-chep-bang-nocodb-va-du-lieu"
tags: [n8n, automation, no-code, nocodb, file-management, api]
keywords: [n8n workflow, tự động hóa, NocoDB, sao chép bảng, API]
---

# 🚀 Tự động sao chép bảng NocoDB và dữ liệu sang base mới

Khi doanh nghiệp muốn mở rộng, di chuyển dự án hoặc sao lưu dữ liệu, **việc tạo lại từng bảng NocoDB và nhập dữ liệu thủ công** thường tốn hàng giờ, dễ gây lỗi và không đồng nhất. Các sếp thường phải:

* Đăng nhập vào giao diện NocoDB, tạo bảng, định nghĩa trường, thiết lập quan hệ…  
* Sao chép dữ liệu bằng CSV, rồi import lại – mất thời gian và dễ sai định dạng.  
* Kiểm tra lại từng bảng để chắc chắn mọi thứ đã được chuyển đúng.

**Workflow “Clone NocoDB tables and data to another base”** giải quyết 100 % vấn đề trên bằng cách **tự động lấy metadata, tạo bảng mới và chép dữ liệu** chỉ với một cú click, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: từ vài giờ giảm còn vài phút.  
- **Độ chính xác 100 %**: không còn lỗi nhập sai trường hay dữ liệu mất.  
- **Khả năng mở rộng**: sao chép hàng chục bảng cùng lúc, hỗ trợ batch.  
- **Hoạt động liên tục**: có thể lên lịch tự động, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản NocoDB** với quyền **API Token** (credential `nocoDbApiToken`).  
- **Base URL** của NocoDB (mặc định `https://app.nocodb.com`).  
- **ID của Source Base** và **Destination Base** (có thể lấy từ URL khi mở base trong giao diện).  
- **Danh sách tên bảng** muốn sao chép (cách nhau bằng dấu phẩy).  
- **Cờ “Copy Rows”**: `true` nếu muốn sao chép dữ liệu, `false` chỉ sao chép cấu trúc.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. **Tải file JSON** của workflow từ trang gốc: <https://n8n.io/workflows/15373>.  
2. Mở n8n → **Workflow → Import** → Chọn file JSON hoặc **Copy/Paste** nội dung JSON vào ô nhập.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
#### Node quan trọng & cách cấu hình

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **When clicking ‘Execute workflow’** | `manualTrigger` | Để mặc định, dùng để khởi chạy thủ công hoặc qua webhook. |
| **Config** | `set` | Điền 5 trường sau (đánh dấu “Add Field” → “String”): <br>• `baseUrl` – URL NocoDB (vd: `https://app.nocodb.com`). <br>• `sourceBaseId` – ID của base nguồn. <br>• `destBaseId` – ID của base đích. <br>• `sourceTables` – Tên các bảng muốn sao chép, ngăn cách bằng dấu phẩy. <br>• `copyRows` – `true` hoặc `false`. |
| **Create NocoDB Table** | `httpRequest` | **Credentials**: chọn `nocoDbApiToken`. <br>**Method**: `POST` <br>**URL**: `{{ $json["baseUrl"] }}/api/v3/meta/bases/{{ $json["destBaseId"] }}/tables` <br>**Body**: dùng dữ liệu từ node “Prepare fields data for Insert”. |
| **Create Tables** | `splitInBatches` | Chia danh sách bảng (`sourceTables`) thành từng batch (mặc định 10). Không cần thay đổi. |
| **Prepare fields data for Insert** | `set` | Tạo payload JSON chứa `table_name`, `columns` (được lấy từ metadata của bảng nguồn). |
| **Copy rows to new tables** | `splitInBatches` | Nếu `copyRows` = `true`, sẽ chia dữ liệu bản ghi thành batch để chèn nhanh. |
| **Fetch tables records** | `httpRequest` | **Credentials**: `nocoDbApiToken`. <br>**Method**: `GET` <br>**URL**: `{{ $json["baseUrl"] }}/api/v3/db/data/{{ $json["sourceBaseId"] }}/{{ $json["tableName"] }}` |
| **Get Source Table Metadata** | `httpRequest` | **Credentials**: `nocoDbApiToken`. <br>**Method**: `GET` <br>**URL**: `{{ $json["baseUrl"] }}/api/v3/meta/bases/{{ $json["sourceBaseId"] }}/tables/{{ $json["tableName"] }}` |
| **Split tables** | `splitOut` | Tách danh sách bảng thành các luồng riêng để xử lý song song. |
| **Fetch tables records1** | `httpRequest` | Tương tự “Fetch tables records”, dùng cho batch thứ hai khi có nhiều bảng. |
| **Copy data over?** | `switch` | Kiểm tra giá trị `copyRows`. Nếu `true` → đi tới “Copy rows to new tables”, nếu `false` → bỏ qua bước chép dữ liệu. |

> **Lưu ý quan trọng:** Workflow **không sao chép các trường quan hệ** (`Links`, `Lookup`, `LinkToAnotherRecord`, `ForeignKey`, `ID`). Nếu các bảng có quan hệ phức tạp, các sếp cần thực hiện bước thiết lập quan hệ thủ công sau khi sao chép.

### 3. Kích hoạt ⚡️
1. **Test chạy**: Nhấn nút **Execute Workflow** → Kiểm tra log từng node, đặc biệt là `Create NocoDB Table` và `Fetch tables records`.  
2. Đảm bảo không có lỗi **401 Unauthorized** (kiểm tra token) hoặc **404 Not Found** (ID base sai).  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow sẵn sàng chạy bất cứ lúc nào hoặc được lên lịch.

## ✍️ Mẹo & gợi ý nâng cao
- **Lên lịch tự động**: Dùng node **Cron** để sao chép hàng ngày/tuần, giữ bản sao đồng bộ giữa các môi trường dev‑prod.  
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node “Copy data over?” để báo cáo số bản ghi đã sao chép thành công hoặc lỗi.  
- **Ghi log vào Google Sheets**: Dùng node **Google Sheets** để lưu lịch sử chạy (thời gian, số bảng, số bản ghi).  
- **Xử lý lỗi nâng cao**: Bọc các node HTTP bằng **Error Trigger** → gửi email hoặc webhook tới hệ thống giám sát.  
- **Tối ưu batch size**: Nếu bảng có hàng nghìn bản ghi, tăng `Batch Size` trong node `splitInBatches` lên 100‑200 để giảm số lần gọi API.

## 📌 Kết luận
Với workflow này, các sếp có thể **tự động sao chép toàn bộ cấu trúc và dữ liệu NocoDB** chỉ trong vài phút, loại bỏ công việc lặp đi lặp lại, giảm rủi ro và tăng tốc độ triển khai dự án. Hãy import ngay, cấu hình các credentials và chạy thử – bạn sẽ thấy hiệu quả ngay lập tức!

---

Need help? Contact us at [developers@sailingbyte.com](mailto:developers@sailingbyte.com) or visit [sailingbyte.com](https://sailingbyte.com)!

Happy hacking!