---
title: "🚀 Tự động đồng bộ Baserow Campaign tới Shopify với Upload Hình & Template Động"
description: "Giải pháp 100% không code giúp chuyển dữ liệu chiến dịch từ Baserow sang Shopify, tải ảnh lên và cập nhật template Liquid ngay tức thì."
slug: "baserow-to-shopify-automation"
tags: [n8n, automation, no-code, Shopify, Baserow, GraphQL]
keywords: [n8n workflow, tự động hóa, Shopify API, Baserow, GraphQL]
---

# 🚀 Tự động đồng bộ Baserow Campaign tới Shopify với Upload Hình & Template Động

Bạn đang phải nhập dữ liệu chiến dịch từ Baserow vào Shopify bằng tay? Mỗi lần cập nhật mới, bạn phải tải ảnh lên, chỉnh sửa file Liquid, và kiểm tra lại thủ công. Điều này tốn thời gian, dễ sai sót và làm giảm năng suất. Workflow n8n dưới đây sẽ giúp bạn tự động hoá toàn bộ quy trình: nhận webhook từ Baserow, tải ảnh lên Shopify, cập nhật template Liquid và cuối cùng lưu dữ liệu vào Shopify – tất cả chỉ với vài cú click, không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn thao tác thủ công, toàn bộ quy trình diễn ra trong vài giây.
- **Chính xác hơn**: Dữ liệu được chuyển trực tiếp, giảm thiểu lỗi nhập liệu.
- **Cá nhân hóa**: Dễ dàng thay đổi template Liquid, hình ảnh, hoặc cấu hình theo từng chiến dịch.
- **Hoạt động liên tục**: Workflow tự động chạy 24/7, không phụ thuộc vào lịch làm việc.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Baserow**: Đảm bảo webhook đã được bật và có URL nhận POST.
- **Shopify Admin API**: Tạo Private App hoặc Custom App, lấy `API Key`, `Password` và `Store Domain`.
- **Credentials n8n**:
  - `httpHeaderAuth` – dùng cho GraphQL và HTTP Request tới Shopify.
  - `shopifyAccessTokenApi` – dùng cho HTTP Request tới Shopify (đối với cập nhật Liquid).
- **Node “Set values here!”**: Cập nhật các biến như `shopifyDomain`, `shopifyApiKey`, `shopifyPassword`, `themeId`, `imageUrl`, v.v.
- **Webhook Path**: `3041fdd6-4cb5-4286-9034-1337dddc3f45` (được đặt trong node “Call from Baserow”).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/2186) hoặc sao chép nội dung JSON.
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.
3. Nhấn **Import** để hoàn tất.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cài đặt cần chỉnh |
|------|-------|-------------------|
| **Call from Baserow** | Webhook nhận dữ liệu từ Baserow | Đảm bảo `path` và `httpMethod` đúng; URL webhook sẽ được cung cấp khi workflow được publish. |
| **Check** | Node If để kiểm tra điều kiện (ví dụ: `campaign_status == "active"`) | Đặt điều kiện đúng với dữ liệu nhận được từ Baserow. |
| **Set values here!** | Đặt các biến cấu hình | Thêm các trường: `shopifyDomain`, `shopifyApiKey`, `shopifyPassword`, `themeId`, `imageUrl`, `campaignName`, v.v. |
| **Upload Image** | GraphQL mutation tải ảnh lên Shopify | Sử dụng `httpHeaderAuth` với `Authorization: Bearer <access_token>`. Đặt query/mutation đúng theo tài liệu GraphQL. |
| **Save campaign.liquid** | HTTP Request cập nhật file Liquid | - `Method`: `PUT` <br> - `URL`: `https://<shopifyDomain>/admin/api/2023-10/themes/<themeId>/assets.json` <br> - `Headers`: `Content-Type: application/json` <br> - `Body`: JSON chứa `asset: { key: "templates/campaign.liquid", value: "<liquid code>" }`. |
| **No Operation, do nothing** | Node placeholder | Không cần chỉnh sửa. |
| **Sticky Note** | Ghi chú trong workflow | Dùng để ghi chú cho người quản trị. |
| **httpHeaderAuth** | Credentials cho GraphQL & HTTP Request | Cấu hình `Authorization` header với token Shopify. |
| **shopifyAccessTokenApi** | Credentials cho HTTP Request | Cấu hình `X-Shopify-Access-Token` hoặc `Authorization`. |

### 3. Kích hoạt ⚡️
1. **Test run**: Gửi dữ liệu mẫu từ Baserow (hoặc sử dụng Postman) tới URL webhook. Kiểm tra log trong n8n để xác nhận mọi node chạy đúng.
2. **Bật Active**: Trong giao diện n8n, chuyển trạng thái workflow từ **Inactive** sang **Active**.
3. **Monitoring**: Kiểm tra “Execution” logs thường xuyên để phát hiện lỗi.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram Notification**: Thêm node Slack hoặc Telegram sau node “Check” để gửi thông báo khi campaign được cập nhật thành công.
- **Lưu Log vào Google Sheets**: Sử dụng node Google Sheets để ghi lại lịch sử cập nhật, giúp theo dõi và phân tích.
- **Cập nhật định kỳ**: Sử dụng node “Cron” để tự động trigger workflow hàng ngày/tuần, thay vì chỉ khi có webhook.
- **Error Handling**: Thêm node “Error Trigger” để gửi email khi workflow gặp lỗi.
- **Version Control**: Lưu file JSON workflow vào GitHub để quản lý phiên bản và rollback nhanh.

## 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian, giảm lỗi và tăng tính linh hoạt khi quản lý chiến dịch marketing trên Shopify. Hãy thử triển khai ngay hôm nay, tận dụng sức mạnh của n8n và Shopify Admin API để tự động hoá quy trình làm việc của bạn!

---