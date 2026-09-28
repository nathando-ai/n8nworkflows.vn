---
title: "🚀 Chuyển Ảnh 2D Sang Mô Hình 3D Tự Động Với Fal.ai Trellis & Lưu Trên Google Drive"
description: "Workflow tự động hóa chuyển đổi ảnh 2D thành mô hình 3D 3D (.glb) bằng AI, lưu kết quả vào Google Drive và cập nhật tự động vào Google Sheets. Giúp các sếp tiết kiệm thời gian thiết kế và tối ưu hóa quy trình sản xuất 3D."
slug: "chuyen-doi-anh-2d-sang-3d-voi-fal-ai"
tags: [n8n, automation, ai, design, google-drive, google-sheets, fal-ai]
keywords: [n8n workflow 3D, tự động hóa thiết kế 3D, chuyển ảnh thành mô hình 3D, fal.ai api, lưu file 3D trên Google Drive]
---

# 🚀 **Chuyển Ảnh 2D Sang Mô Hình 3D Tự Động Với Fal.ai Trellis & Lưu Trên Google Drive**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm thời gian thiết kế 3D** từ 80% (so với làm thủ công).
- **Tự động hóa quy trình** từ ảnh 2D → mô hình 3D → lưu trữ.
- **Cập nhật kết quả** tự động vào Google Sheets và Google Drive.
- **Hoạt động 24/7** với lịch trình tự động (Schedule Trigger).

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thiết kế 3D từ đầu, chỉ cần cung cấp ảnh tham khảo.
- **Chính xác cao**: AI Fal.ai Trellis tự động hóa quá trình chuyển đổi với độ chính xác cao.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi thiết lập.
- **Lưu trữ an toàn**: Kết quả 3D (.glb) được lưu trên Google Drive, dễ dàng chia sẻ và truy cập.
- **Dễ dàng mở rộng**: Kết hợp với Slack/Email để thông báo kết quả hoặc lưu log cho quản lý.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Fal.ai** ([Đăng ký tại đây](https://fal.ai/)) để lấy **API Key**.
2. **Google Sheets** (mẫu đã được cung cấp [ở đây](https://docs.google.com/spreadsheets/d/1C0Et6X3Zwr_6CxeNjhLpDwjAfIGeUvLGFawckKb0utY/edit?usp=sharing)).
   - Cột **"IMAGE MODEL"** chứa ảnh tham khảo (các sếp điền URL ảnh hoặc file ảnh).
   - Cột **"3D RESULT"** sẽ tự động cập nhật link/download mô hình 3D sau khi xử lý.
3. **Google Drive** để lưu trữ file 3D (.glb) kết quả.
4. **n8n Self-hosted** (khuyến nghị để workflow hoạt động 24/7).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải workflow JSON** từ [đây](https://n8n.io/workflows/3894).
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô **"Import JSON"**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình API Key Fal.ai**
- **Node**: **"Create 3D Image"** và **"Get Url 3D image"**
  - Đi đến **Credentials** → Thêm **"httpHeaderAuth"**.
  - Điền:
    - **Name**: `Authorization`
    - **Value**: `Key YOURAPIKEY` (thay `YOURAPIKEY` bằng API Key từ Fal.ai).

#### **B. Cấu hình Google Sheets**
- **Node**: **"Get new image"** và **"Update result"**
  - Đi đến **Credentials** → Thêm **"googleSheetsOAuth2Api"**.
  - Cấu hình OAuth2 với tài khoản Google Sheets đã tạo (mẫu [đây](https://docs.google.com/spreadsheets/d/1C0Et6X3Zwr_6CxeNjhLpDwjAfIGeUvLGFawckKb0utY/edit?usp=sharing)).
  - **Key Parameters**:
    - **Operation**: `update` (để cập nhật kết quả vào cột **"3D RESULT"**).

#### **C. Cấu hình Google Drive**
- **Node**: **"Upload 3D Image"**
  - Đi đến **Credentials** → Thêm **"googleDriveOAuth2Api"**.
  - Cấu hình OAuth2 với tài khoản Google Drive.
  - **Folder**: Chọn thư mục muốn lưu file 3D (.glb).

#### **D. Thiết lập Schedule Trigger (Lịch trình tự động)**
- **Node**: **"Schedule Trigger"**
  - Thiết lập lịch trình chạy (ví dụ: **5 phút/lần**) để workflow tự động xử lý tất cả ảnh trong Google Sheets.

#### **E. Test Run & Kích hoạt**
- **Bước 1**: Nhấn **"Test workflow"** để chạy thử với 1 dòng dữ liệu mẫu.
- **Bước 2**: Kiểm tra:
  - Google Sheets có cập nhật link/download mô hình 3D không?
  - Google Drive có lưu file .glb không?
- **Bước 3**: Nếu thành công, chuyển **Active workflow** sang **"ON"**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[MỞ RỘNG THÊM FUNCS]
1. **Thông báo kết quả qua Slack/Email**:
   - Thêm node **"Slack"** hoặc **"Email"** sau **"Update result"** để gửi thông báo khi mô hình 3D hoàn tất.
2. **Lưu log hoạt động**:
   - Thêm node **"Set"** trước **"Update result"** để lưu thông tin trạng thái (thành công/thất bại) vào Google Sheets.
3. **Tự động xóa ảnh đã xử lý**:
   - Thêm node **"Google Drive"** để xóa ảnh tham khảo sau khi tạo xong mô hình 3D.
4. **Kết hợp với Figma/Blender**:
   - Sau khi lưu file .glb vào Google Drive, các sếp có thể import vào **Figma** hoặc **Blender** để chỉnh sửa tiếp.
:::

---
## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quy trình chuyển đổi ảnh 2D → mô hình 3D** chỉ với 3 bước đơn giản:
1. **Điền ảnh tham khảo** vào Google Sheets.
2. **Chạy workflow** (thủ công hoặc tự động theo lịch).
3. **Nhận mô hình 3D** tự động lưu trên Google Drive và cập nhật kết quả.

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất thiết kế 3D!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::