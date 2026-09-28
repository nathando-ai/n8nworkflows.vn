---
title: "📧 Tự động hóa Gmail: Tóm tắt email bằng AI Gemini và gửi báo cáo HTML"
description: "Hướng dẫn tự động hóa hoàn toàn không cần code để tóm tắt email Gmail bằng AI Gemini và gửi báo cáo HTML định kỳ. Tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-gmail-tom-tat-email-ai-gemini"
tags: [n8n, automation, no-code, gmail, ai, productivity]
keywords: [n8n workflow, tự động hóa email, tóm tắt email, ai gemini, báo cáo html]
---

# 📧 Tự động hóa Gmail: Tóm tắt email bằng AI Gemini và gửi báo cáo HTML

[Các sếp] có bao giờ cảm thấy bị ngập lụt bởi lượng email hàng ngày không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình tóm tắt email Gmail bằng AI Gemini và nhận báo cáo HTML định kỳ. Không cần phải mở từng email một, các sếp sẽ nhận được bản tóm tắt rõ ràng, ưu tiên và hành động cần thực hiện.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng trăm email mỗi ngày mà không cần can thiệp.
- **Tăng hiệu suất**: Nhận bản tóm tắt rõ ràng về nội dung quan trọng nhất.
- **Tăng cường quản lý**: Xác định ưu tiên và hành động cần thực hiện cho từng email.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail và các thông tin xác thực OAuth2 cho n8n.
- API key của Google Gemini.
- Địa chỉ email nhận báo cáo (có thể cấu hình trong node "Config (edit me)").
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13126](https://n8n.io/workflows/13126) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy toàn bộ nội dung JSON từ trang web và dán vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Google Gemini Chat Model"**:
   - Chọn credentials của Google Gemini.
   - Đảm bảo sử dụng model **Gemini 2.5 Flash** hoặc model tương đương có sẵn trong tài khoản của bạn.

2. **Node "Fetch Gmail emails (receivedAfter)"**:
   - Thêm credentials Gmail OAuth2 với quyền truy cập "Fetch Emails".

3. **Node "Send HTML digest email" và "Send “no new emails” email"**:
   - Thêm credentials Gmail OAuth2 với quyền truy cập "Send Emails".
   - Cập nhật địa chỉ email nhận báo cáo trong trường "To".

4. **Node "Config (edit me)"**:
   - Cập nhật tham số `recipientEmail` với địa chỉ email nhận báo cáo.
   - Có thể điều chỉnh tham số `hours: 12` để thay đổi khoảng thời gian lấy email (ví dụ: 24 giờ cho báo cáo hàng ngày).

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Test workflow" để kiểm tra với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Active workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh khoảng thời gian**: Thay đổi tham số `hours` trong node "Compute receivedAfter (now - 12h)" để điều chỉnh khoảng thời gian lấy email (ví dụ: 24 giờ cho báo cáo hàng ngày).
- **Tùy chỉnh mẫu báo cáo**: Chỉnh sửa nội dung HTML trong node "Send HTML digest email" để phù hợp với phong cách báo cáo của bạn.
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo đến Slack hoặc Telegram sau khi gửi báo cáo email.
- **Lưu log hoạt động**: Thêm node lưu log hoạt động vào cơ sở dữ liệu để theo dõi lịch sử xử lý email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình tóm tắt email Gmail bằng AI Gemini và gửi báo cáo HTML định kỳ. Với việc tự động hóa hoàn toàn, các sếp có thể tiết kiệm thời gian và tập trung vào những nhiệm vụ quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!