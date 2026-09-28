---
title: "🚀 Xử lý hội thoại với Trợ lý AI Sehatsanjha từ Replicate"
description: "Giải pháp tự động hóa 100% không cần code để tạo nội dung đa phương tiện từ mô hình AI của Replicate. Nhận kết quả nhanh chóng, chính xác và có thể tùy chỉnh theo nhu cầu."
slug: "xuly-hoi-thoai-sehatsanjha-replicate"
tags: [n8n, automation, no-code, AI, Replicate, content-creation]
keywords: [n8n workflow, tự động hóa, AI, Replicate, Sehatsanjha, content creation]
---

# 🚀 Xử lý hội thoại với Trợ lý AI Sehatsanjha từ Replicate

Bạn đang phải trả lời hàng trăm tin nhắn, tạo nội dung phản hồi nhanh chóng và chính xác? Việc nhập liệu thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Workflow này sẽ **tự động** gửi nội dung hội thoại tới mô hình AI `aihilums/sehatsanjha` trên Replicate, chờ kết quả và xử lý ngay lập tức – hoàn toàn **không cần viết code**.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút lên giây, bạn chỉ cần nhấn nút “execute”.
- **Độ chính xác cao**: AI xử lý ngôn ngữ tự nhiên, giảm lỗi nhập liệu.
- **Tùy biến linh hoạt**: Thay đổi prompt, tham số mô hình mà không cần chỉnh sửa code.
- **Hoạt động liên tục**: Được chạy 24/7 trên VPS, không bị gián đoạn.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Replicate API Key**: Đăng ký tại <https://replicate.com> và lấy API key.
- **Thông tin mô hình**: `aihilums/sehatsanjha` – không cần tham số bắt buộc, nhưng bạn có thể truyền prompt tùy ý.
- **n8n**: Phiên bản 0.200+ (đảm bảo hỗ trợ node `wait` và `if`).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ <https://n8n.io/workflows/6892> hoặc sao chép nội dung JSON vào clipboard.
2. Mở n8n, vào **Workflows** → **Import** → **Import from clipboard** hoặc **Upload file**.
3. Chọn file JSON, nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|-------|---------------------|
| **On clicking 'execute'** | Trigger thủ công | Không cần chỉnh |
| **Set API Key** | Lưu trữ Replicate API key | Điền `REPLICATE_API_KEY` = <API key> |
| **Create Prediction** | Gửi yêu cầu POST tới Replicate | URL: `https://api.replicate.com/v1/predictions`<br>Headers: `Authorization: Token {{ $json["REPLICATE_API_KEY"] }}`<br>Body: JSON với `model: "aihilums/sehatsanjha"` và `input: { prompt: "..." }` |
| **Extract Prediction ID** | Lấy `id` từ phản hồi | Code: `return [{ predictionId: $json.id }];` |
| **Wait** | Chờ một khoảng thời gian | `Seconds: 30` (hoặc tùy chỉnh) |
| **Check Prediction Status** | GET trạng thái | URL: `https://api.replicate.com/v1/predictions/{{ $json.predictionId }}`<br>Headers: `Authorization: Token {{ $json["REPLICATE_API_KEY"] }}` |
| **Check If Complete** | Kiểm tra `status === "succeeded"` | Condition: `{{$json.status}} === "succeeded"` |
| **Process Result** | Xử lý output | Code: `return [{ result: $json.output }];` |

> **Lưu ý**: Nếu bạn muốn truyền prompt động, hãy thay `prompt` trong node **Create Prediction** bằng một biến từ node trước (ví dụ: `{{$node["On clicking 'execute'"].json["prompt"]}}`).

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute** trên node **On clicking 'execute'**. Kiểm tra log để đảm bảo mọi bước chạy đúng.
2. **Bật Active**: Sau khi test thành công, bật toggle **Active** ở góc trên bên phải của workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node `Slack` sau **Process Result** để gửi kết quả ngay vào kênh.
- **Lưu trữ vào Google Sheets**: Dùng node `Google Sheets` để ghi lại prompt và output, tạo lịch sử.
- **Lưu log vào File**: Thêm node `Write Binary File` để lưu output vào file CSV/JSON trên server.
- **Tự động gửi email**: Thêm node `Email` để gửi kết quả cho khách hàng hoặc đội ngũ nội dung.

## 📌 Kết luận
Workflow “Xử lý hội thoại với Trợ lý AI Sehatsanjha từ Replicate” giúp các sếp **đưa nội dung AI vào quy trình làm việc** một cách nhanh chóng, chính xác và dễ dàng mở rộng. Hãy thử ngay, tận dụng sức mạnh của AI mà không cần viết code!