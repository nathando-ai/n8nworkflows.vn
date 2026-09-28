---
title: "🎙️ Tự động hóa tổng kết podcast Apple với ElevenLabs và GPT-5-MINI"
description: "Giải pháp tự động hóa 100% không cần code giúp các sếp tổng kết nhanh chóng các tập podcast Apple bằng công nghệ chuyển văn bản và AI tổng hợp thông tin."
slug: "tu-dong-hoa-tong-ket-podcast-apple-voi-elevenlabs-gpt5-mini"
tags: [n8n, automation, no-code, podcast, ai]
keywords: [n8n workflow, tự động hóa podcast, tổng kết podcast, ElevenLabs, GPT-5-MINI]
---

# 🎙️ Tự động hóa tổng kết podcast Apple với ElevenLabs và GPT-5-MINI

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải nghe lại toàn bộ tập podcast để tóm tắt nội dung? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ tìm kiếm tập podcast đến gửi email tổng kết chỉ trong vài phút, mà không cần phải viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nghe lại toàn bộ tập podcast để tóm tắt nội dung.
- **Chính xác cao**: Sử dụng công nghệ chuyển văn bản tiên tiến của ElevenLabs và AI tổng hợp thông tin của GPT-5-MINI.
- **Cá nhân hóa**: Nhận được tổng kết theo định dạng và nội dung mà các sếp mong muốn.
- **Hoạt động liên tục**: Workflow hoạt động 24/7, giúp các sếp không bỏ lỡ bất kỳ tập podcast quan trọng nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ElevenLabs với API key.
- Tài khoản OpenAI với API key.
- Tài khoản Gmail với quyền truy cập OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/14170](https://n8n.io/workflows/14170).
2. Nhấn vào nút "Import" để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấn vào nút "Import" và chọn file JSON vừa tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Transcribe Episode with ElevenLabs"**:
   - Thêm credentials "httpHeaderAuth" với API key của ElevenLabs.
   - Cập nhật URL của tập podcast trong node này.

2. **Node "Generate Episode Summary"**:
   - Thêm credentials "openAiApi" với API key của OpenAI.
   - Điều chỉnh prompt trong node này để phù hợp với nhu cầu tổng kết của các sếp.

3. **Node "Send Summary Email"**:
   - Thêm credentials "gmailOAuth2" với thông tin tài khoản Gmail.
   - Cập nhật địa chỉ email nhận tổng kết trong node này.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Test" để kiểm tra workflow với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Active" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm node để gửi tổng kết qua Slack hoặc Telegram thay vì email.
- **Lưu log**: Thêm node để lưu log các tập podcast đã tổng kết để theo dõi lịch sử.
- **Gửi báo cáo định kỳ**: Thiết lập workflow để gửi báo cáo tổng kết định kỳ (hàng tuần, hàng tháng) đến các sếp.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình tổng kết podcast Apple chỉ trong vài phút. Hãy áp dụng ngay để tiết kiệm thời gian và tập trung vào những việc quan trọng hơn!