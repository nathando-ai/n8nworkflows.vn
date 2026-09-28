---
title: "🚀 CallForge - 08: Xử lý Dữ liệu Sản phẩm AI 100% Tự động"
description: "Giải pháp tự động thu thập, xử lý và cập nhật dữ liệu sản phẩm cùng AI từ cuộc gọi bán hàng, giúp doanh nghiệp tiết kiệm thời gian và giảm sai sót."
slug: "callforge-08-xu-ly-du-lieu-san-pham-ai"
tags: [n8n, automation, no-code, notion, ai, sales]
keywords: [n8n workflow, tự động hóa, Notion, AI, sales call]
---

# 🚀 CallForge - 08: Xử lý Dữ liệu Sản phẩm AI 100% Tự động

Bạn đang phải trích xuất dữ liệu sản phẩm và thông tin AI từ các cuộc gọi bán hàng qua Gong, sau đó nhập vào Notion? Việc làm thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. **CallForge - 08** là workflow n8n được thiết kế để tự động hoá toàn bộ quy trình: nhận dữ liệu AI, phân tích, gộp, và cập nhật ngay vào Notion mà không cần viết một dòng code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống chỉ còn vài phút.
- **Độ chính xác cao**: Trích xuất dữ liệu tự động, giảm lỗi nhập liệu.
- **Tích hợp linh hoạt**: Dữ liệu được lưu trữ ngay trong Notion, dễ dàng chia sẻ và phân tích.
- **Tự động cập nhật**: Khi có dữ liệu mới, Notion được cập nhật ngay lập tức.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Notion** với quyền truy cập vào database cần lưu trữ dữ liệu sản phẩm và AI.
- **API Key Notion** (được tạo trong phần Integrations của Notion).
- **Database ID** của Notion cho:
  - Cơ sở dữ liệu sản phẩm.
  - Cơ sở dữ liệu phản hồi sản phẩm.
  - Cơ sở dữ liệu cuộc gọi (để cập nhật tóm tắt AI).
- **Workflow Trigger**: Workflow này được kích hoạt bởi workflow khác (ví dụ: “CallForge - 07 - AI Data Generator”) qua node **Execute Workflow Trigger**.

:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/3039) hoặc sao chép nội dung JSON.
2. Trong n8n Editor, chọn **Import** → **Import from Clipboard** hoặc **Import from File**.
3. Nhập tên workflow: `CallForge - 08 - Product AI Data Processor`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Execute Workflow Trigger** | Nhận dữ liệu từ workflow trước. | Không cần cấu hình thêm. |
| **Check if Product Data Found** | Kiểm tra có dữ liệu sản phẩm không. | `{{ $json["productData"] ? true : false }}` |
| **Create Product Data Object1** | Tạo trang trong Notion cho dữ liệu sản phẩm. | <ul><li>**Database ID**: ID của DB sản phẩm.</li><li>**Properties**: Mapping các trường từ `productData` (ví dụ: tên, mô tả, giá).</li></ul> |
| **Create Product Feedback Data Object** | Tạo trang trong Notion cho phản hồi sản phẩm. | <ul><li>**Database ID**: ID của DB phản hồi.</li><li>**Properties**: Mapping từ `feedbackData`.</li></ul> |
| **Check if AI Use Case Data Found** | Kiểm tra có dữ liệu AI use case không. | `{{ $json["aiUseCaseData"] ? true : false }}` |
| **Check if AI Mentioned On Call** | Kiểm tra AI có được đề cập trong cuộc gọi không. | `{{ $json["aiMentioned"] ? true : false }}` |
| **Wait for rate limiting - AI Use Case** | Đợi để tránh vượt giới hạn API. | `{{ $json["aiRateLimitMs"] || 1000 }}` |
| **Wait for rate limiting - Product Data** | Đợi để tránh vượt giới hạn API. | `{{ $json["productRateLimitMs"] || 1000 }}` |
| **Split Out Product Data** | Phân tách từng mục dữ liệu sản phẩm. | `{{ $json["productData"] }}` |
| **Bundle AI Use Case Data to 1 object** | Gộp dữ liệu AI use case thành một object. | `{{ $json["aiUseCaseData"] }}` |
| **Bundle Product Feedback Data to 1 object** | Gộp dữ liệu phản hồi thành một object. | `{{ $json["feedbackData"] }}` |
| **Merge AI Use Case Thread** | Tạo chuỗi tóm tắt AI use case. | `{{ $json["aiUseCaseSummary"] }}` |
| **Merge Product Feedback Thread** | Tạo chuỗi tóm tắt phản hồi sản phẩm. | `{{ $json["feedbackSummary"] }}` |
| **Update Call with AI Data Summary** | Cập nhật trang cuộc gọi trong Notion với tóm tắt AI. | <ul><li>**Database ID**: ID của DB cuộc gọi.</li><li>**Properties**: Thêm trường `AI Summary` với giá trị `{{ $json["aiSummary"] }}`.</li></ul> |

> **Lưu ý**: Mỗi node **Notion** cần được cấu hình credentials `notionApi`. Mở node, chọn **Credentials** → **Add New** → nhập API Key.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (có thể copy JSON từ workflow trước) để kiểm tra xem các node có thực thi đúng không.
2. **Bật Active**: Khi mọi thứ chạy ổn, chuyển workflow sang trạng thái **Active** để tự động kích hoạt khi có dữ liệu mới.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram Notification**: Thêm node **Slack** hoặc **Telegram** vào cuối workflow để gửi thông báo khi dữ liệu được cập nhật thành công.
- **Logging**: Sử dụng node **Set** để ghi log vào một database Notion riêng, giúp theo dõi lịch sử cập nhật.
- **Scheduled Reports**: Kết hợp với node **Cron** để gửi báo cáo tóm tắt AI hàng ngày/tuần tới nhóm bán hàng.
- **Error Handling**: Thêm node **If** để kiểm tra lỗi và gửi email cảnh báo khi có lỗi trong quá trình cập nhật Notion.

## 📌 Kết luận
Workflow **CallForge - 08** giúp các sếp chuyển đổi hoàn toàn quy trình xử lý dữ liệu sản phẩm và AI từ cuộc gọi sang tự động, giảm thiểu sai sót và tăng năng suất. Hãy thử ngay, tích hợp vào hệ thống hiện tại và cảm nhận sự khác biệt!

---