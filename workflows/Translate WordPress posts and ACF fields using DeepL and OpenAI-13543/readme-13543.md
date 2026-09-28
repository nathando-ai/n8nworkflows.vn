---
title: "🚀 Tự động hóa Dịch Bài WordPress + ACF bằng DeepL & OpenAI - Không cần code"
description: "Hướng dẫn chi tiết cách tự động dịch bài viết WordPress cùng các trường ACF bằng công nghệ AI DeepL và OpenAI, tiết kiệm thời gian và đảm bảo chất lượng bản dịch."
slug: "tu-dong-dich-bai-wordpress-acf-deepl-openai"
tags: [n8n, automation, no-code, wordpress, ai, deepl, openai]
keywords: [n8n workflow, tự động hóa, dịch bài viết, wordpress, acf, deepl, openai]
---

# 🚀 Tự động hóa Dịch Bài WordPress + ACF bằng DeepL & OpenAI - Không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải dịch thủ công hàng trăm bài viết WordPress cùng các trường ACF. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động dịch hàng trăm bài viết trong vài phút.
- Chất lượng bản dịch: Sử dụng công nghệ AI tiên tiến của DeepL và OpenAI.
- Bảo toàn cấu trúc: Giữ nguyên cấu trúc ACF khi dịch.
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- WordPress Application Password (để xác thực HTTP Basic Auth)
- OpenAI API Key (để phát hiện ngôn ngữ)
- DeepL API Key (để dịch nội dung)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13543](https://n8n.io/workflows/13543)
2. Nhấn nút "Import" và chọn "Import from URL"
3. Dán URL vào ô nhập liệu và nhấn "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Node**:
   - Đảm bảo đường dẫn "translate-post" là duy nhất và không bị trùng lặp.
   - Phương thức HTTP nên để là "POST".

2. **Get Post Data Node**:
   - Cập nhật URL của WordPress site của bạn.
   - Chọn credentials "httpBasicAuth" đã được cấu hình với Application Password của WordPress.

3. **OpenAI Language Detect Node**:
   - Chọn credentials "openAiApi" đã được cấu hình với API Key của OpenAI.
   - Model nên để là "gpt-4o-mini" để đảm bảo hiệu suất và chi phí.

4. **Smart Router & Targets Node**:
   - Mở node này và cập nhật mảng "allSupported" để khớp với các ngôn ngữ được hỗ trợ trên website của bạn.
   - Ví dụ: `["en", "fr", "es", "de"]` cho các ngôn ngữ Anh, Pháp, Tây Ban Nha và Đức.

5. **Extract Content Node**:
   - Mở node này và cập nhật mảng "textKeys" để khớp với các tên trường ACF thực tế trên WordPress site của bạn.
   - Ví dụ: `["title", "content", "excerpt", "custom_field_1", "custom_field_2"]`.

6. **DeepL Translate Node**:
   - Thêm API Key của DeepL vào Header Parameters.
   - Đảm bảo URL của DeepL API là chính xác và không bị thay đổi.

7. **Create Translated Post Node**:
   - Cập nhật URL của WordPress site của bạn.
   - Chọn credentials "httpBasicAuth" đã được cấu hình với Application Password của WordPress.

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra workflow với dữ liệu mẫu.
2. Kiểm tra kết quả dịch trên WordPress site của bạn.
3. Nếu mọi thứ hoạt động tốt, nhấn nút "Activate Workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi dịch xong bài viết.
- **Lưu log dịch**: Thêm node để lưu log các bài viết đã dịch vào Google Sheets.
- **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp các bài viết đã dịch hàng tuần.
- **Tích hợp với Google Translate**: Thay thế DeepL bằng Google Translate nếu muốn giảm chi phí.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể khi dịch bài viết WordPress cùng các trường ACF. Với công nghệ AI tiên tiến của DeepL và OpenAI, các sếp có thể đảm bảo chất lượng bản dịch cao nhất. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của mình!