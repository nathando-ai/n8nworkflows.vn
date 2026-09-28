---
title: "🚀 Tự động tạo hình ảnh cá nhân hoá từ Google Sheets với Layerre"
description: "Tự động lấy dữ liệu từ Google Sheets, tạo hình ảnh AI cá nhân hoá bằng Layerre và xuất ra ngay, giảm 90% thời gian so với thao tác thủ công."
slug: "tu-dong-tao-hinh-anh-ca-nhan-hoa-tu-google-sheets-layerre"
tags: [n8n, automation, no-code, content-creation, multimodal-ai, layerre]
keywords: [n8n workflow, tự động hóa, tạo hình ảnh cá nhân hoá, Google Sheets, Layerre]
---

# 🚀 Tự động tạo hình ảnh cá nhân hoá từ Google Sheets với Layerre

Trong môi trường marketing hiện đại, việc tạo ra những hình ảnh cá nhân hoá (ví dụ: banner chào mừng tên khách, thiệp sinh nhật, voucher có tên) thường phải thực hiện thủ công: **copy‑paste** dữ liệu từ bảng tính, mở công cụ thiết kế, nhập nội dung, lưu lại và gửi.  
Quá trình này tốn **nhiều giờ** mỗi tuần, dễ gây lỗi sai và không thể mở rộng khi số lượng khách hàng tăng lên.

**Workflow n8n** này sẽ giải quyết hoàn toàn vấn đề:  
- Lấy dữ liệu khách hàng từ **Google Sheets**.  
- Gửi dữ liệu tới **Layerre** – dịch vụ AI tạo hình ảnh đa phương tiện.  
- Nhận lại hình ảnh đã được cá nhân hoá và lưu (hoặc gửi) ngay lập tức.  
Tất cả chỉ cần **1 click** và chạy 24/7 mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: giảm tới 90% thời gian tạo hình ảnh so với thủ công.  
- **Độ chính xác cao**: không còn lỗi sai do nhập liệu tay.  
- **Cá nhân hoá mạnh mẽ**: mỗi hình ảnh được tạo dựa trên dữ liệu thực tế (tên, ngày sinh, mã khuyến mãi…).  
- **Hoạt động liên tục**: workflow chạy tự động 24/7, luôn sẵn sàng khi có dữ liệu mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền truy cập **Google Sheets API** (OAuth2 credentials).  
- **API Key của Layerre** (đăng ký tại https://layerre.com).  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
- **Google Sheet** chứa các cột dữ liệu cần thiết (ví dụ: `Name`, `Email`, `PromoCode`).  
- (Tùy chọn) Thư mục lưu ảnh trên Google Drive hoặc Dropbox nếu muốn lưu trữ lâu dài.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Click **Import** → **From File** và chọn file JSON của workflow (được tải từ trang gốc).  
   *Hoặc* sao chép toàn bộ JSON và dán vào **Import → Paste JSON**.  
3. Nhấn **Import**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Manual Trigger** | Bắt đầu workflow thủ công (hoặc có thể chuyển thành Cron). | Không cần thay đổi, chỉ dùng để test. |
| **Google Sheets** | Đọc dữ liệu từ bảng tính. | - Chọn **Credentials**: Google OAuth2.<br>- **Spreadsheet ID**: ID của Google Sheet.<br>- **Range**: ví dụ `Sheet1!A2:C` (tùy theo cấu trúc). |
| **Layerre** | Gửi yêu cầu tạo hình ảnh AI. | - **Credentials**: Layerre API Key.<br>- **Prompt**: sử dụng các biến từ Google Sheets, ví dụ `Create a birthday banner for {{ $json["Name"] }} with the promo code {{ $json["PromoCode"] }}`.<br>- **Output Format**: `png` hoặc `jpeg` tùy nhu cầu. |
| **Sticky Note** | Ghi chú mô tả workflow (không ảnh hưởng tới chạy). | Không cần chỉnh, chỉ dùng để lưu ý nội bộ. |
| **(Optional) Google Drive / Dropbox** | Lưu hình ảnh đã tạo. | Cấu hình **Credentials** và **Folder Path** nếu muốn lưu. |

> **Lưu ý:** Đảm bảo các **Credentials** đã được tạo trong n8n → **Credentials** trước khi gán vào node. Nếu chưa có, tạo mới và nhập API Key hoặc OAuth token tương ứng.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** trên **Manual Trigger** để chạy thử với **dữ liệu mẫu**.  
2. Kiểm tra **Output** của node Layerre: hình ảnh có được trả về không, và nếu có, xem URL hoặc binary data.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy khi được kích hoạt (hoặc lên lịch Cron).  

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động gửi email**: Thêm node **Send Email** (SMTP hoặc Gmail) để gửi hình ảnh trực tiếp tới khách hàng.  
- **Thông báo Slack/Telegram**: Khi hình ảnh được tạo xong, gửi link hoặc preview tới kênh Slack/Telegram để đội ngũ marketing nhanh chóng kiểm tra.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** hoặc **Google Drive** để lưu toàn bộ hình ảnh và log vào một thư mục chung, hỗ trợ audit.  
- **Lên lịch chạy định kỳ**: Thay **Manual Trigger** bằng **Cron** (ví dụ mỗi ngày 00:00) để tự động xử lý dữ liệu mới mỗi ngày.  
- **Kết hợp OpenAI**: Trước khi gửi prompt tới Layerre, dùng node **OpenAI** để tạo tagline hoặc mô tả ngắn gọn, tăng tính sáng tạo cho hình ảnh.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình tạo hình ảnh cá nhân hoá** chỉ trong vài phút, giảm chi phí nhân lực và tăng độ chính xác. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc cho bạn! 🚀