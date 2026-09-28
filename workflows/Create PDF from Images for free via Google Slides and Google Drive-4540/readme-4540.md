---
title: "📄 Tự Động Tạo PDF Từ Hình Ảnh Trên Google Drive MIỄN PHÍ (Không Cần Code)"
description: "Workflow tự động hóa chuyển đổi tất cả hình ảnh từ một thư mục Google Drive thành PDF duy nhất bằng Google Slides, tiết kiệm thời gian và đảm bảo tính nhất quán cho các dự án thiết kế, marketing hoặc nội dung. Phù hợp với các sếp cần giải pháp tự động hóa thiết kế không cần kỹ thuật."
slug: "tay-dong-tao-pdf-tu-hinh-anh-google-drive"
tags: [n8n, automation, google-drive, google-slides, design-automation, no-code]
keywords: [tự động hóa tạo pdf, google drive pdf, google slides automation, tự động hóa thiết kế, workflow n8n google drive]
---

# 🚀 **Tự Động Tạo PDF Từ Hình Ảnh Trên Google Drive (Không Cần Code)**

### **Giải pháp hoàn hảo cho các sếp thiết kế, marketing hoặc nội dung**
Bạn có bao giờ phải mất nhiều giờ để sắp xếp hàng loạt hình ảnh từ Google Drive, sau đó chuyển chúng thành một tài liệu PDF duy nhất để chia sẻ? Hay phải lo lắng về kích thước, định dạng hoặc mất mát chất lượng khi làm thủ công? **Workflow này sẽ giải quyết tất cả những vấn đề đó chỉ với một cú nhấp chuột!**

Dùng **n8n** kết hợp với **Google Drive và Google Slides**, workflow này sẽ:
✅ **Tự động lấy tất cả hình ảnh** từ một thư mục Google Drive.
✅ **Sắp xếp theo ngày tạo** để đảm bảo trật tự logic.
✅ **Chuyển đổi thành PDF** với định dạng chính xác (A4, Letter, hoặc tùy chỉnh) bằng một bản mẫu Google Slides.
✅ **Xóa trang trắng đầu tiên** để PDF sạch sẽ, chuyên nghiệp.
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải copy-paste từng hình ảnh vào PowerPoint/Canva.
- **Định dạng chuyên nghiệp**: PDF ra mắt với kích thước và trang số chính xác, không bị giật dãn.
- **Tự động hóa hoàn toàn**: Chỉ cần kích hoạt workflow, hệ thống sẽ làm tất cả.
- **Không giới hạn số lượng hình ảnh**: Hoạt động hiệu quả với từ 5 đến 200+ hình ảnh (tuỳ thuộc vào dung lượng Google Drive).
- **Miễn phí**: Sử dụng API Google miễn phí (đủ cho nhu cầu thông thường).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive và Google Slides** (đã kết nối với n8n).
2. **Một thư mục Google Drive** chứa hình ảnh cần chuyển đổi (chủ yếu là `.png` hoặc `.jpg`).
3. **Một bản mẫu Google Slides** với kích thước trang mong muốn (A4, Letter, hoặc tùy chỉnh).
4. **API Key của Google Drive và Google Slides** (đã cấu hình trong n8n).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/4540) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/4540) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **16 node** quan trọng, các sếp cần chú ý đến các bước sau:

##### **A. Cấu hình tên PDF cuối cùng**
- **Node**: *"Set Pdf File Name"*
  - Điền giá trị `presentation_title` với tên muốn đặt cho PDF (ví dụ: `"Báo cáo tháng 12 2024"`).

##### **B. Kết nối Google Drive & Google Slides**
- **Tất cả các node sử dụng Google Drive/Slides** (ví dụ: *"Get All Files From the Folder"*, *"CopyPdfTemplate"*) **cần OAuth2 API Key**.
  - Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/) và tạo **API Key** cho:
    - **Google Drive API**
    - **Google Slides API**
  - Thêm credentials vào n8n trong **Credentials Manager**.

##### **C. Chọn bản mẫu Google Slides**
- **Node**: *"CopyPdfTemplate"*
  - Chọn **File** từ danh sách là bản mẫu Slides đã tạo (đã cấu hình kích thước trang mong muốn).
  - Chọn **Parent Folder** là thư mục chứa hình ảnh nguồn (PDF cuối cùng sẽ được tạo ở đây).

##### **D. Lọc hình ảnh theo định dạng**
- **Node**: *"Filter: Only Images"*
  - Mặc định workflow chỉ lấy `.png`. Nếu sử dụng `.jpg` hoặc `.gif`, cần thay đổi điều kiện lọc:
    - Thay `image/png` thành `image/jpeg` (cho JPG) hoặc `image/gif` (cho GIF).

##### **E. Xóa trang trắng đầu tiên (nếu có)**
- **Node**: *"Delete First Empty Slide"*
  - Workflow tự động xóa slide trắng đầu tiên (nếu có) sau khi chuyển đổi xong.

##### **F. Cấu hình kích thước hình ảnh**
- **Node**: *"Add Image To The Slide"*
  - Google Slides có giới hạn kích thước hình ảnh. Nếu hình ảnh quá lớn, có thể:
    - Nén hình ảnh trước khi upload vào Google Drive.
    - Sử dụng công cụ như **Canva** hoặc **Photoshop** để điều chỉnh kích thước.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Kích hoạt **Manual Trigger** (*"When clicking ‘Test workflow’"*).
   - Chọn **Run Once** và kiểm tra kết quả.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng tuần/monthly (ví dụ: tự động tạo PDF báo cáo định kỳ).

2. **Gửi PDF qua Email/Slack**:
   - Kết nối với **Gmail** hoặc **Slack** để tự động gửi PDF cho team sau khi tạo xong.

3. **Lưu log hoạt động**:
   - Thêm **Google Sheets** vào workflow để ghi lại lịch sử tạo PDF (ngày tạo, tên file, số lượng hình ảnh).

4. **Tùy chỉnh trang bìa**:
   - Thêm một slide giới thiệu vào bản mẫu Google Slides để PDF có trang bìa chuyên nghiệp.

5. **Sử dụng nhiều thư mục**:
   - Nếu cần lấy hình ảnh từ nhiều thư mục, thêm **node Google Drive** để lấy danh sách thư mục và xử lý từng thư mục riêng biệt.

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa quá trình tạo PDF từ hình ảnh trên Google Drive. **Không cần kỹ thuật, không cần code**, chỉ cần một vài bước cấu hình là có thể tiết kiệm hàng giờ làm việc mỗi tuần.

**Hãy thử ngay và chia sẻ kết quả với team của bạn!** 🚀
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với **n8n Community** để được hỗ trợ.

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/4540)** | **📌 [Cài đặt n8n Self-hosted](https://n8n.io/docs/)**