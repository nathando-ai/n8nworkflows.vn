---
title: "🚀 Tự động hóa cuộc họp Zoom với AI: Tạo tóm tắt email, nhiệm vụ ClickUp và cuộc gọi theo dõi"
description: "Tự động hóa toàn bộ quy trình sau cuộc họp Zoom: Tạo tóm tắt email, nhiệm vụ ClickUp và đặt lịch cuộc gọi theo dõi bằng AI - tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tu-dong-hoa-cuoc-hop-zoom-voi-ai-tao-tom-tat-email-nhiem-vu-clickup-cuoc-goi-theo-doi"
tags: [n8n, automation, no-code, zoom, clickup, ai, microsoft-outlook]
keywords: [n8n workflow, tự động hóa cuộc họp, AI meeting assistant, ClickUp tasks, Outlook calendar]
---

# 🚀 Tự động hóa cuộc họp Zoom với AI: Tạo tóm tắt email, nhiệm vụ ClickUp và cuộc gọi theo dõi

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết không? Sau mỗi cuộc họp Zoom, bạn phải:
- Tóm tắt nội dung cuộc họp và gửi email cho tất cả thành viên
- Tạo các nhiệm vụ trong ClickUp cho những việc cần làm sau cuộc họp
- Đặt lịch cuộc gọi theo dõi cho những điểm quan trọng

Việc này tốn rất nhiều thời gian và dễ bị lỗi. Hãy để n8n và AI làm việc này cho bạn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho các công việc thủ công
- Tóm tắt cuộc họp chính xác và đầy đủ thông tin
- Tạo nhiệm vụ ClickUp tự động từ nội dung cuộc họp
- Đặt lịch cuộc gọi theo dõi một cách hiệu quả
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zoom với quyền truy cập API
- Tài khoản Microsoft Outlook với quyền tạo sự kiện
- Tài khoản ClickUp với quyền tạo nhiệm vụ
- API key từ nhà cung cấp AI (OpenAI, Anthropic, Google hoặc Ollama)
- Thông tin SMTP để gửi email
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/2800)
2. Nhấp vào nút "Download" để tải file JSON
3. Trong n8n Editor, nhấp vào menu "Workflow" > "Import from File" và chọn file đã tải
4. Hoặc copy toàn bộ nội dung JSON và dán vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Zoom: Get data of last meeting"**:
   - Chọn credentials "zoomOAuth2Api" đã được cấu hình
   - Đảm bảo tài khoản Zoom có quyền truy cập vào các cuộc họp cần xử lý

2. **Node "Zoom: Get transcript file"**:
   - Chọn credentials "zoomOAuth2Api" đã được cấu hình
   - Đảm bảo cuộc họp đã được ghi lại và có bản ghi âm/transcript

3. **Node "Send meeting summary"**:
   - Chọn credentials "smtp" đã được cấu hình
   - Cập nhật địa chỉ email người nhận trong node này

4. **Node "Create follow-up call"**:
   - Chọn credentials "microsoftOutlookOAuth2Api" đã được cấu hình
   - Đảm bảo tài khoản Outlook có quyền tạo sự kiện

5. **Node "ClickUp"**:
   - Chọn credentials "clickUpOAuth2Api" đã được cấu hình
   - Cập nhật ID của Space và List trong ClickUp mà bạn muốn tạo nhiệm vụ

6. **Node "Anthropic Chat Model"**:
   - Chọn credentials "anthropicApi" đã được cấu hình
   - Đảm bảo bạn có đủ credit trong tài khoản AI

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Test workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấp vào nút "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy mỗi khi có cuộc họp mới trong Zoom

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi tần suất chạy workflow từ "khi nhấp Test workflow" thành "lên lịch" để chạy định kỳ
- Kết hợp với Slack hoặc Teams để thông báo khi workflow hoàn thành
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tạo báo cáo tổng hợp hàng tuần từ các cuộc họp đã xử lý
- Kết nối với các công cụ khác như Airtable, Google Calendar, hoặc Gmail thay vì ClickUp và Outlook

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình sau cuộc họp Zoom, từ tóm tắt nội dung đến tạo nhiệm vụ và đặt lịch cuộc gọi theo dõi. Với AI xử lý nội dung và n8n kết nối các công cụ, bạn có thể tiết kiệm thời gian quý giá và tập trung vào những việc quan trọng hơn.

Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của đội ngũ!