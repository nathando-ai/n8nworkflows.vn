---
title: "🚀 Chuyển Nhiều File sang Base64 Bằng Node Code – Tự Động Hóa N8N"
description: "Hướng dẫn chi tiết cách tự động tải, giải nén và mã hóa nhiều file thành Base64 trong n8n, giúp tích hợp API yêu cầu định dạng này mà không cần viết code phức tạp."
slug: "chuyen-nhiem-file-sang-base64-n8n"
tags: [n8n, automation, no-code, file-management, base64, code-node]
keywords: [n8n workflow, tự động hóa, chuyển file sang base64, n8n code node, file management, API integration]
---

# 🚀 Chuyển Nhiều File sang Base64 Bằng Node Code – Tự Động Hóa N8N

Bạn đang phải tải xuống, giải nén và chuyển đổi hàng loạt file thành chuỗi Base64 để gửi lên API? Việc này thường tốn thời gian và dễ gây lỗi khi làm thủ công. Workflow **Convert Multiple Files to Base64 with JavaScript Code** của Viktor Klepikovskyi đã giải quyết mọi vấn đề này trong 4 node đơn giản, 100% không cần code ngoài node Code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tải, giải nén và mã hóa file trong vài giây.
- **Độ chính xác cao**: Tránh sai sót khi chuyển đổi thủ công.
- **Tích hợp linh hoạt**: Dữ liệu Base64 có thể gửi tới bất kỳ API nào yêu cầu định dạng này.
- **Quản lý dễ dàng**: Tất cả các file được xử lý trong một workflow duy nhất, dễ bảo trì.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **n8n instance** (Self-hosted hoặc Cloud) đã cài đặt.
- **Kết nối Internet** để tải file ZIP mẫu.
- Không cần bất kỳ credential nào ngoài node HTTP Request (URL công khai).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Truy cập **https://n8n.io/workflows/6885** và nhấn nút **Download** để lấy file JSON.
2. Trong n8n, vào **Workflows → Import** và tải lên file JSON vừa tải.
3. Hoặc copy toàn bộ nội dung JSON và dán vào **Editor → Import from Clipboard**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | `When clicking ‘Execute workflow’` | Không cần chỉnh | Node `manualTrigger` để khởi chạy workflow. |
| 2 | `Download n8n demo website zip` | `URL` → `https://github.com/n8n-io/n8n-demo-website/archive/refs/heads/main.zip` (hoặc URL file ZIP của bạn) <br> `Method` → `GET` | Đảm bảo URL có thể truy cập công khai. |
| 3 | `Unzip` | Không cần chỉnh | Node `compression` tự động giải nén file binary nhận được. |
| 4 | `Encode to base64` | **Code** → Dưới đây là đoạn JavaScript mẫu (đã được bao gồm trong workflow). <br> **Output** → Định dạng `{{ $json }}` để truyền tới node tiếp theo. | Node `code` sẽ lặp qua `items[0].binary` và chuyển từng file thành Base64. |

#### Mã JavaScript mẫu (đã được chèn sẵn trong node `Encode to base64`)

```javascript
// Lấy danh sách file trong binary
const binaryData = items[0].binary;

// Tạo mảng kết quả
const result = Object.keys(binaryData).map((fileName) => {
  const file = binaryData[fileName];
  // Mã hóa Base64
  const base64 = Buffer.from(file.data, 'base64').toString('base64');
  return { fileName, base64 };
});

return result.map((item) => ({ json: item }));
```

> **Lưu ý**: Nếu bạn muốn giữ nguyên tên file, hãy sử dụng `fileName` trong output.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút **Execute Workflow** và kiểm tra tab **Execution**. Bạn sẽ thấy 3 file (`index.html`, `style.css`, `script.js`) đã được mã hóa thành Base64.
2. **Bật Active**: Khi mọi thứ ổn, chuyển workflow sang trạng thái **Active** để tự động chạy khi có trigger.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi kết quả tới Slack**: Thêm node `Slack` sau `Encode to base64` để thông báo khi hoàn thành.
- **Lưu file Base64 vào Google Drive**: Dùng node `Google Drive` để lưu từng file dưới dạng văn bản Base64.
- **Tự động gửi tới API**: Thêm node `HTTP Request` với method `POST` và body `{{ $json }}` để gửi dữ liệu lên endpoint yêu cầu Base64.
- **Lịch trình định kỳ**: Thay `manualTrigger` bằng `Cron` để chạy workflow hàng ngày/giờ.

## 📌 Kết luận

Workflow **Convert Multiple Files to Base64 with JavaScript Code** là công cụ tuyệt vời giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi khi làm việc với nhiều file. Hãy thử ngay, tùy chỉnh URL tải file và mở rộng sang các node khác để phù hợp với quy trình kinh doanh của bạn. 🚀

> **Link gốc**: <https://n8n.io/workflows/6885>  
> **Blog hướng dẫn chi tiết**: <https://n8n-tips.blogspot.com/2025/08/from-binary-to-base64-guide-to-file.html>