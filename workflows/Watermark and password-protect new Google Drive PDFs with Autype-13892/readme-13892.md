---
title: "🔒 Tự động chèn watermark và bảo mật PDF mới trong Google Drive với Autype"
description: "Hướng dẫn tự động hóa quy trình bảo mật PDF mới trong Google Drive bằng cách chèn watermark và mã hóa mật khẩu chỉ với 7 nodes trong n8n"
slug: "tu-dong-bao-mat-pdf-google-drive-voi-autype"
tags: [n8n, automation, no-code, google-drive, pdf]
keywords: [n8n workflow, tự động hóa, bảo mật PDF, watermark, Autype]
---

# 🔒 Tự động chèn watermark và bảo mật PDF mới trong Google Drive với Autype

[Các sếp] có bao giờ phải tự tay chèn watermark và mã hóa mật khẩu cho hàng trăm file PDF mới trong Google Drive không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ với 7 nodes đơn giản trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý ngay khi có file PDF mới trong Google Drive
- **Bảo mật tăng cường**: Tự động chèn watermark "CONFIDENTIAL" và mã hóa mật khẩu
- **Chuẩn hóa quy trình**: Đảm bảo tất cả file PDF đều được xử lý theo cùng tiêu chuẩn
- **Hoạt động liên tục**: Không cần can thiệp thủ công, chạy 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Autype ([Đăng ký tại đây](https://app.autype.com))
- Tài khoản Google Drive đã kết nối với n8n
- Node cộng đồng Autype đã cài đặt trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/13892)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn **Import from Clipboard** và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "New PDF Uploaded to Drive"**:
   - Chọn credentials Google Drive OAuth2
   - Cấu hình folder cần theo dõi trong tham số "folderId"

2. **Node "Upload PDF to Autype"**:
   - Chọn credentials Autype API
   - Đảm bảo tài khoản Autype đã kích hoạt Document Tools

3. **Node "Add Watermark"**:
   - Đặt nội dung watermark (mặc định là "CONFIDENTIAL")
   - Cấu hình vị trí và độ trong suốt watermark

4. **Node "Password-Protect PDF"**:
   - Đặt mật khẩu mở file (user password)
   - Đặt mật khẩu chỉnh sửa file (owner password)

5. **Node "Save Watermarked PDF to Drive" và "Save Protected PDF to Drive"**:
   - Chọn credentials Google Drive OAuth2
   - Cấu hình folder lưu kết quả (có thể cùng folder với file gốc)

#### 3. Kích hoạt ⚡️
1. Test run với file PDF mẫu
2. Kiểm tra kết quả trong Google Drive (file `-watermark.pdf` và `-protected.pdf`)
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo khi xử lý xong
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets
3. **Xử lý nhiều định dạng**: Mở rộng workflow để xử lý cả Word và Excel
4. **Lập lịch báo cáo**: Tự động gửi báo cáo hàng tuần về số lượng file đã xử lý

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình bảo mật PDF trong Google Drive, đảm bảo tính bảo mật và chuyên nghiệp cho toàn bộ tài liệu. Với chỉ 7 nodes đơn giản, các sếp có thể tiết kiệm hàng giờ mỗi ngày và đảm bảo tất cả file PDF đều được xử lý theo cùng tiêu chuẩn. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!