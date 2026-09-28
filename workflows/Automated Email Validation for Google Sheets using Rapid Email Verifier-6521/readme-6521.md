---
title: "🚀 Xác thực Email Tự động từ Google Sheets với Rapid Email Verifier"
description: "Giải pháp tự động xác thực email từ Google Sheets, cập nhật trạng thái ngay lập tức, giúp tối ưu danh sách liên hệ và chiến dịch marketing."
slug: "xac-thuc-email-tu-dong-tu-google-sheets"
tags: [n8n, automation, no-code, lead-generation, email-verification]
keywords: [n8n workflow, tự động hóa, xác thực email, Google Sheets, Rapid Email Verifier]
---

# 🚀 Xác thực Email Tự động từ Google Sheets với Rapid Email Verifier

Bạn đang phải làm thủ công kiểm tra hàng trăm email trong Google Sheets? Mỗi lần nhập dữ liệu mới, bạn phải tự tay gửi tới một công cụ xác thực, chờ phản hồi, rồi cập nhật lại bảng – tốn thời gian, dễ sai sót và không thể mở rộng.  
Workflow này sẽ **tự động**:

- Giám sát bảng Google Sheets mỗi giờ để phát hiện dòng mới.
- Lọc ra những email chưa được xác thực.
- Gửi từng email tới API Rapid Email Verifier (không cần key, miễn phí 1000 lần/ tháng).
- Cập nhật kết quả “valid/invalid” ngay trong bảng, giữ nguyên dữ liệu gốc và tạo lịch sử.

Bạn chỉ cần một lần cài đặt, workflow sẽ chạy 24/7, giảm tải công việc và nâng cao độ chính xác danh sách liên hệ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống vài phút tự động.  
- **Độ chính xác cao**: Tránh sai sót khi nhập liệu, giảm email spam.  
- **Tự động cập nhật**: Bảng luôn mới nhất, không cần thao tác thủ công.  
- **Chi phí thấp**: Sử dụng API miễn phí 1000 lần/ tháng, không tốn tiền.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo bảng với cột `SrNo | Name | Email | Email Verified`.  
- **Google Sheets OAuth2**: Đăng ký và lưu credential `googleSheetsOAuth2Api` trong n8n.  
- **Rapid Email Verifier**: Không cần key, chỉ cần URL `https://rapid-email-verifier.fly.dev`.  
- **VPS hoặc máy chủ n8n**: Để chạy workflow liên tục.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/6521>.  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** để đưa workflow vào danh sách workflow của bạn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên thực tế | Cấu hình cần chỉnh | Ghi chú |
|------|-------------|---------------------|---------|
| `Monitor New Email Entries` | `googleSheetsTrigger` | *Sheet ID*, *Range* (ví dụ: `Sheet1!A:D`) | Đảm bảo trigger chỉ lấy dòng mới. |
| `Filter Unverified Emails` | `filter` | *Condition*: `{{$json["Email Verified"]}} == ""` | Loại bỏ email đã được xác thực. |
| `Process Emails in Batches` | `splitInBatches` | *Batch size*: 1 (để tránh vượt giới hạn API) | Bạn có thể tăng lên 5 nếu API cho phép. |
| `Verify Email Address` | `httpRequest` | *Method*: GET<br>*URL*: `https://rapid-email-verifier.fly.dev?email={{$json["Email"]}}` | Trả về JSON: `{ "status": "valid" | "invalid" | "unknown" }`. |
| `Update Verification Results` | `googleSheets` | *Operation*: `appendOrUpdate`<br>*Sheet ID*<br>*Range*: `Sheet1!D:D` (cột Email Verified) | Dùng `{{$json["status"]}}` làm giá trị cập nhật. |

> **Lưu ý**: Đối với node `googleSheets`, chọn credential `googleSheetsOAuth2Api` đã tạo trước. Nếu chưa có, vào **Credentials** → **New Credential** → **Google Sheets OAuth2** và làm theo hướng dẫn.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một dòng mẫu trong Google Sheet, chạy workflow thủ công để kiểm tra.  
2. Kiểm tra bảng: Cột `Email Verified` sẽ được cập nhật thành `valid` hoặc `invalid`.  
3. Khi mọi thứ hoạt động, bật **Active** cho workflow. Workflow sẽ tự động chạy mỗi giờ.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notification**: Thêm node `Slack` hoặc `Telegram` sau node `Verify Email Address` để nhận thông báo khi có email mới được xác thực.  
- **Log lỗi**: Sử dụng node `Set` để ghi lại lỗi API vào cột `Error Log`.  
- **Báo cáo định kỳ**: Thêm node `Schedule` + `Google Sheets` để gửi báo cáo hàng ngày về số email đã xác thực.  
- **Webhook trigger**: Thay `googleSheetsTrigger` bằng `Webhook` để kích hoạt ngay khi có dữ liệu mới (đối với ứng dụng web).  

### 📌 Kết luận
Workflow này giúp các sếp **tối ưu danh sách liên hệ** mà không tốn thời gian hay công sức. Hãy thử ngay, cài đặt trên VPS, và trải nghiệm sự tự động hóa hoàn toàn. Nếu có bất kỳ câu hỏi hay muốn mở rộng thêm tính năng, hãy liên hệ với tác giả Gaurav hoặc cộng đồng n8n.  

Chúc các sếp thành công!