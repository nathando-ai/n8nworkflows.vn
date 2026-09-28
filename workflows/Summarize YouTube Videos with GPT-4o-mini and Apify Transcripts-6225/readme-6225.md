---
title: "🎬 Tự động tóm tắt video YouTube bằng GPT-4o-mini và Apify"
description: "Hướng dẫn tự động hóa quy trình tóm tắt video YouTube bằng n8n, Apify và OpenAI. Tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-tom-tat-video-youtube-bang-gpt-4o-mini-va-apify"
tags: [n8n, automation, no-code, AI, content creation]
keywords: [n8n workflow, tự động hóa, tóm tắt video, Apify, OpenAI, GPT-4o-mini]
---

# 🎬 Tự động tóm tắt video YouTube bằng GPT-4o-mini và Apify

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xem hàng loạt video YouTube để tìm thông tin quan trọng? Với workflow này, các sếp có thể tự động hóa quy trình tóm tắt nội dung video chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình tóm tắt video YouTube.
- Tăng hiệu suất: Xử lý hàng loạt video một cách nhanh chóng và chính xác.
- Cá nhân hóa: Tóm tắt nội dung theo nhu cầu cụ thể của từng video.
- Hoạt động liên tục: Workflow hoạt động 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify (để lấy transcript từ video YouTube).
- Tài khoản OpenAI (để sử dụng mô hình GPT-4o-mini).
- URL của video YouTube cần tóm tắt.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/6225`
4. Nhấn "OK" để hoàn tất quá trình import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình form để nhận URL của video YouTube.
   - Đảm bảo form có trường nhập liệu cho URL.

2. **Node "Apify"**:
   - Chọn credentials là `apifyApi`.
   - Trong phần "Operation", chọn `Run actor`.
   - Điền thông tin actor ID (ví dụ: `apify/youtube-transcript`).

3. **Node "OpenAI Chat Model"**:
   - Chọn credentials là `openAiApi`.
   - Trong phần "Model", chọn `gpt-4o-mini`.
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng mô hình này.

4. **Node "Summarization Chain"**:
   - Không cần cấu hình thêm, node này sẽ tự động xử lý dữ liệu đầu vào.

5. **Node "Payload" và "Caption"**:
   - Không cần cấu hình thêm, hai node này sẽ xử lý dữ liệu đầu ra từ các node trước đó.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để test run với dữ liệu mẫu.
2. Kiểm tra kết quả đầu ra để đảm bảo workflow hoạt động đúng.
3. Sau khi test thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi tóm tắt hoàn thành.
- Lưu log các video đã tóm tắt để theo dõi lịch sử.
- Gửi báo cáo định kỳ về các video đã tóm tắt qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình tóm tắt video YouTube một cách nhanh chóng và chính xác. Với sự kết hợp của Apify và OpenAI, các sếp có thể tiết kiệm thời gian và nâng cao hiệu suất làm việc. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!