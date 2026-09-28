---
title: "🚀 Tự Động Hóa Báo Cáo Hàng Ngày Cho Nhà Hàng Với AI Gemini: Sales, Giảm Thiểu Thừa Thực Phẩm & Phản Hồi Khách Hàng"
description: "Workflow tự động hóa hoàn toàn bằng n8n kết hợp AI Gemini để phân tích dữ liệu bán hàng, thừa thực phẩm và phản hồi khách hàng, tổng hợp thành báo cáo hàng ngày được gửi tự động qua email - tiết kiệm 10+ giờ công mỗi tuần cho các sếp nhà hàng."
slug: "tieu-dong-hoa-bao-cao-ngay-cua-nha-hang-voi-gemini-ai"
tags: [n8n, automation, no-code, ai-gemini, google-sheets, restaurant-management, email-automation]
keywords: [tự động hóa nhà hàng, gemini ai n8n, báo cáo hàng ngày nhà hàng, giảm thừa thực phẩm, phân tích phản hồi khách hàng, workflow n8n google sheets]
---

# 🚀 **Tự Động Hóa Báo Cáo Hàng Ngày Cho Nhà Hàng: Sales, Giảm Thừa Thực Phẩm & Phản Hồi Khách Hàng Với AI Gemini**

Hàng ngày, các sếp nhà hàng phải mất **từ 5-10 giờ** để tổng hợp dữ liệu bán hàng, phân tích thừa thực phẩm, và xử lý hàng trăm phản hồi khách hàng từ Google Sheets. Kết quả? Báo cáo thường **chậm trễ, không chính xác**, và thiếu **đề xuất hành động cụ thể** để tối ưu hóa hoạt động. **Workflow này giải quyết tất cả vấn đề đó bằng AI Gemini + n8n**, tự động hóa toàn bộ quy trình từ lấy dữ liệu đến gửi báo cáo qua email.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** mà không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) với tài nguyên ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ công/tuần**: Không cần thủ công tổng hợp dữ liệu từ Google Sheets.
✅ **Báo cáo chính xác 100%**: AI Gemini phân tích dữ liệu với **độ chính xác cao**, tránh sai sót của con người.
✅ **Đề xuất hành động cụ thể**: Nhận **gợi ý tối ưu hóa bán hàng**, **giảm thừa thực phẩm**, và **cải thiện trải nghiệm khách hàng**.
✅ **Hoạt động liên tục**: Báo cáo được gửi tự động **mỗi ngày** vào thời gian đã đặt (ví dụ: 8h sáng).
✅ **Cá nhân hóa**: Dữ liệu được tổng hợp theo **mẫu email chuyên nghiệp**, dễ đọc và hành động.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản Google Sheets** (để lưu trữ dữ liệu bán hàng, thừa thực phẩm và phản hồi khách hàng).
- **API Key Google Gemini** (để kết nối với AI Gemini của Google).
- **Tài khoản Gmail** (để gửi báo cáo hàng ngày).
- **Dữ liệu mẫu trong Google Sheets** (các sếp có thể tham khảo [mẫu này](https://docs.google.com/spreadsheets/d/1XYZ/edit) để cấu hình).

:::note[Cấu trúc Google Sheets yêu cầu]
Các sếp cần **3 bảng riêng biệt** trong Google Sheets với cấu trúc sau:
1. **Bán hàng hàng ngày** (`Sales_Data`):
   | Ngày       | Món ăn       | Số lượng | Giá bán | Chi phí nguyên liệu | Loại món (Chính/Phụ) |
   |------------|--------------|----------|---------|---------------------|----------------------|
   | 2024-05-20 | Bánh mì thịt  | 50       | 30.000  | 15.000              | Chính               |

2. **Thừa thực phẩm** (`Waste_Data`):
   | Ngày       | Món ăn       | Số lượng thừa | Nguyên nhân thừa |
   |------------|--------------|---------------|------------------|
   | 2024-05-20 | Salad trộn   | 10           | Quá trình chuẩn bị |

3. **Phản hồi khách hàng** (`Feedback_Data`):
   | Ngày       | Tên khách   | Đánh giá (1-5) | Nội dung phản hồi          |
   |------------|--------------|----------------|----------------------------|
   | 2024-05-20 | Nguyễn Văn A | 5              | "Món bánh mì ngon lắm!"   |
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
- **Tải workflow từ n8n.io**: [Tải JSON](https://n8n.io/workflows/5991) (ấn vào "Export").
- **Import vào n8n**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **"Import"** và chọn file JSON đã tải.
  3. **Hoặc** copy toàn bộ JSON và paste vào **"Import from JSON"** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **không hoạt động được** nếu không cấu hình đúng các node sau:

##### **A. Cấu hình Credentials (API Keys & Tài khoản)**
| Node Name                          | Tham số cần điền                          | Mô tả                                                                 |
|------------------------------------|--------------------------------------------|------------------------------------------------------------------------|
| `Daily Report Scheduler`           | Thời gian chạy (ví dụ: `0 8 * * *`)       | Chọn giờ gửi báo cáo hàng ngày (UTC). Ví dụ: `0 8 * * *` = 8h sáng. |
| `Fetch Daily Sales Data`           | **Credentials**: `googleApi`               | Chọn tài khoản Google Sheets đã kết nối.                             |
| `Fetch Daily Food Waste Records`   | **Credentials**: `googleApi`               | Cùng tài khoản Google Sheets.                                         |
| `Fetch Customer Feedback`         | **Credentials**: `googleApi`               | Cùng tài khoản Google Sheets.                                         |
| `Email Final Report via Gmail`     | **Credentials**: `gmailOAuth2`             | Chọn tài khoản Gmail để gửi báo cáo.                                |
| **Tất cả node `lmChatGoogleGemini`** | **Credentials**: `googlePalmApi`      | Nhập **API Key Google Gemini** (mua tại [Google AI Studio](https://aistudio.google.com/)). |

##### **B. Cấu hình Google Sheets (Sheet Name & Range)**
Các node `Fetch Daily Sales Data`, `Fetch Daily Food Waste Records`, và `Fetch Customer Feedback` **cần thiết lập**:
- **Sheet Name**:
  - `Sales_Data` (cho node `Fetch Daily Sales Data`).
  - `Waste_Data` (cho node `Fetch Daily Food Waste Records`).
  - `Feedback_Data` (cho node `Fetch Customer Feedback`).
- **Range**: `A1:Z` (hoặc tùy chỉnh theo cột dữ liệu của các sếp).

##### **C. Cấu hình Email (Recipient & Subject)**
Trong node `Email Final Report via Gmail`:
- **To**: Địa chỉ email của người nhận (ví dụ: `quanly@nahang.com`).
- **Subject**: Tùy chỉnh (ví dụ: **"Báo cáo Hàng Ngày - [Tên Nhà Hàng] - Ngày [DD/MM]"**).

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **mode "Test"** để kiểm tra các node.
   - Kiểm tra **log** trong n8n để đảm bảo dữ liệu được lấy và xử lý đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **mode "Active"**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CẬP NHẬT & TỐI ƯU HỌC]
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo **ngay khi có sự cố** (ví dụ: lỗi lấy dữ liệu).
   - Cài đặt trong node `Wait for All Data Processing` bằng **Webhook** từ Slack/Telegram.

2. **Lưu Log Dữ liệu**:
   - Thêm node **Google Drive** hoặc **Firebase** để lưu **tất cả báo cáo** theo lịch sử.
   - Cấu hình trong node `Format Final Email Content` bằng **API Google Drive**.

3. **Tùy chỉnh AI Prompt**:
   - Các sếp có thể **sửa lại prompt** trong node `AI-Generated Daily Summary` để AI **nhấn mạnh các chỉ số quan trọng** hơn (ví dụ: "Tối ưu hóa món ăn có lợi nhuận thấp").

4. **Gửi Báo cáo cho Nhiều Người Nhận**:
   - Thay vì chỉ gửi cho 1 email, các sếp có thể **tách node `Email Final Report via Gmail`** thành nhiều node với **nhiều địa chỉ email** (ví dụ: quản lý, nhân viên bán hàng).

5. **Kết hợp với CRM**:
   - Nếu nhà hàng sử dụng **CRM như HubSpot hoặc Zoho**, các sếp có thể **tích hợp node CRM** để cập nhật thông tin khách hàng từ phản hồi vào hệ thống.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp nhà hàng để tập trung vào **quản lý chiến lược** thay vì làm việc thủ công với dữ liệu. Với **AI Gemini**, báo cáo không chỉ **tổng hợp dữ liệu** mà còn **đề xuất giải pháp cụ thể** để tối ưu hóa bán hàng, giảm thừa thực phẩm, và cải thiện trải nghiệm khách hàng.

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình Google Sheets và API Keys**.
3. **Bật Active** và **nhận báo cáo hàng ngày tự động**!

👉 [Tải workflow ngay](https://n8n.io/workflows/5991) và **cải thiện hiệu suất nhà hàng của bạn trong 24 giờ đầu tiên!** 🚀