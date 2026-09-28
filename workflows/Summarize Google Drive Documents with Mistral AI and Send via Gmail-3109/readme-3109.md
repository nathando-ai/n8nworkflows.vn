---
title: "🚀 Tóm tắt tài liệu Google Drive bằng Mistral AI và gửi qua Gmail - Workflow n8n"
description: "Tự động hóa tóm tắt tài liệu Google Drive bằng AI và gửi kết quả qua email - tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tom-tat-tai-lieu-google-drive-bang-mistral-ai-va-gui-qua-gmail"
tags: [n8n, automation, no-code, google-drive, gmail, ai]
keywords: [n8n workflow, tự động hóa, tóm tắt tài liệu, Mistral AI, Google Drive, Gmail]
---

# 🚀 Tóm tắt tài liệu Google Drive bằng Mistral AI và gửi qua Gmail - Workflow n8n

[Các sếp đang làm việc với lượng tài liệu khổng lồ trên Google Drive? Bạn mệt mỏi với việc phải đọc và tóm tắt từng tài liệu một? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đọc tài liệu: Tự động tóm tắt nội dung chính của tài liệu dài
- Nâng cao hiệu suất làm việc: Nhận được bản tóm tắt chất lượng ngay lập tức
- Tăng tính chuyên nghiệp: Gửi bản tóm tắt qua email thay vì gửi tài liệu nguyên bản
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với các tài liệu cần tóm tắt
- Tài khoản Gmail để nhận bản tóm tắt
- API Key của Mistral AI (đăng ký tại [Mistral AI](https://mistral.ai/))
- Quyền truy cập đầy đủ vào các tài liệu Google Drive cần xử lý
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [Workflow gốc trên n8n.io](https://n8n.io/workflows/3109)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Download uploaded File from Google Drive"**:
   - Chọn credentials "googleDriveOAuth2Api"
   - Điền ID của tài liệu Google Drive cần tóm tắt vào trường "File ID"

2. **Node "Mistral Cloud Chat Model"**:
   - Chọn credentials "mistralCloudApi"
   - Đảm bảo đã nhập đúng API Key của Mistral AI

3. **Node "Send Summarized text to Gmail"**:
   - Chọn credentials "gmailOAuth2"
   - Điền địa chỉ email nhận bản tóm tắt vào trường "To"
   - Tùy chỉnh tiêu đề email nếu cần

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra email để xác nhận đã nhận được bản tóm tắt
3. Sau khi kiểm tra thành công, click vào nút "Activate workflow" để kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Google Drive Trigger" để tự động tóm tắt khi có tài liệu mới được tải lên
- Kết hợp với Slack để thông báo khi tóm tắt hoàn thành
- Lưu bản tóm tắt vào Google Sheets để theo dõi lịch sử tóm tắt
- Tùy chỉnh prompt tóm tắt để phù hợp với nhu cầu cụ thể của từng loại tài liệu

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày với việc đọc và tóm tắt tài liệu. Bằng cách tích hợp Google Drive, Mistral AI và Gmail, workflow tự động hóa hoàn toàn quy trình này, mang lại kết quả chính xác và chuyên nghiệp. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!