---
title: "🚀 Tự động tạo Thư mời làm việc cho nhân viên mới với Google Docs, HR Approval & Gmail"
description: "Giải pháp không code giúp HR nhanh chóng tạo thư mời làm việc cá nhân hoá, chuyển sang PDF và gửi duyệt/đăng ký cho ứng viên chỉ trong vài phút."
slug: "tu-dong-tao-thu-moi-lam-viec-nhan-vien-moi-google-docs-hr-approval-gmail"
tags: [n8n, automation, no-code, HR, Google-Docs, Gmail]
keywords: [n8n workflow, tự động hóa, thư mời làm việc, HR approval, Google Docs, Gmail]
---

# 🚀 Tự động tạo Thư mời làm việc cho nhân viên mới với Google Docs, HR Approval & Gmail

Khi tuyển dụng, HR thường phải **điền tay** vào mẫu thư mời, chuyển sang PDF, lưu trữ và gửi duyệt cho người quản lý.  
Quá trình này tốn thời gian, dễ sai sót và không đồng nhất.  
Workflow này sẽ **tự động**:

1. Nhận dữ liệu từ form đăng ký của ứng viên.  
2. Tạo bản sao cá nhân hoá của mẫu thư mời trên Google Docs.  
3. Chuyển sang PDF và lưu trên Google Drive.  
4. Gửi email cho HR duyệt (Approve/Reject).  
5. Nếu được duyệt, tự động gửi PDF cho ứng viên.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ 10‑15 phút giảm còn < 1 phút cho mỗi thư.  
- **Độ chính xác 100 %**: Dữ liệu được chèn tự động, không còn lỗi đánh máy.  
- **Quy trình duyệt nhanh**: HR chỉ cần trả lời “Approve” hoặc “Reject” trong email.  
- **Lưu trữ tự động**: PDF luôn có bản sao trên Google Drive, dễ truy xuất.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** (Google Drive, Google Docs, Gmail) với quyền **OAuth2** được cấp cho n8n.  
- **Mẫu thư mời** (Google Docs) đã có các placeholder như `{{candidateName}}`, `{{position}}`, `{{startDate}}`, `{{salary}}`.  
- **Form** (n8n Form Trigger) với các trường:  
  - `candidateName`  
  - `position`  
  - `startDate`  
  - `salary`  
  - `hrEmail` (email của người duyệt)  
  - `candidateEmail` (email của ứng viên)  
- **Thư mục Google Drive** để lưu bản sao và PDF (cần ID thư mục).  
- **API credentials** trong n8n:  
  - `googleDriveOAuth2Api`  
  - `googleDocsOAuth2Api`  
  - `gmailOAuth2`  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ link gốc hoặc đính kèm).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
3. Hoặc copy toàn bộ JSON, vào **New Workflow**, nhấn **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần thay đổi | Hướng dẫn chi tiết |
|------|----------------------|--------------------|
| **On form submission** (Form Trigger) | Thêm các trường form như trên | Vào **Fields** → **Add Field** → Đặt `Name` = `candidateName`, `Type` = **String**, … |
| **Create a candidate copy of the appointment letter template** (Google Drive – Copy) | **File ID** của mẫu Google Docs & **Folder ID** đích | Trong **File ID** dán ID của mẫu (URL: `https://docs.google.com/document/d/<FILE_ID>/edit`). <br> **Destination Folder**: dán ID thư mục lưu bản sao. |
| **Update the candidate appointment letter with offer details** (Google Docs – Update) | **Document ID** (được truyền từ node copy) & **Placeholders** | Trong **Update Fields**: <br> - `{{candidateName}}` → `{{$json["candidateName"]}}` <br> - `{{position}}` → `{{$json["position"]}}` <br> - `{{startDate}}` → `{{$json["startDate"]}}` <br> - `{{$json["salary"]}}` → `{{salary}}` |
| **Download the appointment letter as a PDF** (Google Drive – Download) | **File ID** (output của node Update) | Đặt **File ID** = `{{$node["Update the candidate appointment letter with offer details"].json["id"]}}` và **Export Format** = `pdf`. |
| **Upload the PDF to Google Drive** (Google Drive – Upload) | **Folder ID** để lưu PDF | Đặt **Folder ID** = ID thư mục lưu PDF. **File Name** có thể dùng `{{$json["candidateName"]}}_Appointment.pdf`. |
| **Send message and wait for response** (Gmail – Send & Wait) | **To** = `{{$json["hrEmail"]}}` <br> **Subject** & **Body** (chứa link PDF) | Trong **Attachments**: chọn **Binary Data** từ node “Upload the PDF”. <br> **Wait for Reply**: bật **Wait for Reply** và đặt **Filter**: Subject chứa “Approve” hoặc “Reject”. |
| **If** (Condition) | Kiểm tra nội dung trả lời | **Expression**: `{{$json["body"]?.toLowerCase().includes("approve")}}` → **True** (được duyệt). |
| **Download file** (Google Drive – Download) | Lấy lại PDF nếu cần (đối với nhánh **True**) | **File ID** = `{{$node["Upload the PDF to Google Drive"].json["id"]}}`. |
| **Send a message** (Gmail – Send) | **To** = `{{$json["candidateEmail"]}}` <br> **Subject** = “Thư mời làm việc – {{candidateName}}” <br> **Attachment** = PDF từ node trên | Đảm bảo **From** là tài khoản Gmail đã kết nối. |

> **Lưu ý:** Các node “Download file” và “Send a message” chỉ chạy khi HR **Approve**. Nếu HR **Reject**, workflow sẽ dừng (hoặc bạn có thể thêm node “Send rejection email” tùy chỉnh).

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** → Kiểm tra dữ liệu mẫu (điền form thử).  
2. Xác nhận PDF được tạo, email HR nhận được và phản hồi “Approve”.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo tuần**: Thêm node Google Sheets để ghi lại danh sách các thư đã gửi, ngày gửi, trạng thái duyệt.  
- **Thông báo Slack/Telegram**: Khi HR duyệt, gửi tin nhắn nhanh tới kênh nội bộ để mọi người biết.  
- **Kiểm tra trùng lặp**: Trước khi tạo bản sao, dùng node “Google Drive – Search” để kiểm tra nếu đã tồn tại thư cho cùng một ứng viên.  
- **Chữ ký điện tử**: Kết hợp DocuSign hoặc HelloSign để HR ký trực tiếp trên PDF trước khi gửi cho ứng viên.

### 📌 Kết luận
Với workflow **Automated New Hire Appointment Letters**, các sếp có thể **loại bỏ hoàn toàn công đoạn thủ công**, giảm lỗi nhập liệu, rút ngắn thời gian duyệt và luôn có bản sao lưu trên Drive.  
Hãy **import ngay**, cấu hình các credential và bắt đầu tự động hoá quy trình tuyển dụng của mình ngay hôm nay! 🚀