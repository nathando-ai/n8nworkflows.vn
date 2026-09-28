---
title: "🧹 Xóa Bulk Liên Lạc HubSpot Tự Động Từ File Excel/CSV - Tiết Kiệm 100% Thời Gian Xử Lý"
description: "Workflow tự động hóa xóa hàng loạt liên lạc HubSpot từ file Excel/CSV tải lên, giảm thiểu sai sót và tối ưu hóa quản lý danh sách khách hàng. Hoàn toàn không cần code!"
slug: "xoa-bulk-lien-lac-hubspot-tu-excel-csv"
tags: [n8n, automation, hubspot, sales, marketing, excel-csv]
keywords: [xóa bulk hubspot, tự động hóa hubspot, xóa liên lạc hubspot từ excel, workflow n8n hubspot, tự động hóa bán hàng marketing]
---

# 🚀 **Xóa Bulk Liên Lạc HubSpot Tự Động Từ File Excel/CSV**

### **Giải pháp cho các sếp bán hàng/marketing:**
Bạn có bao giờ phải xóa hàng loạt liên lạc không cần thiết trên HubSpot bằng tay? Thời gian mất để kiểm tra từng email, ID, hoặc thông tin liên lạc trong file Excel/CSV là vô cùng tốn kém và dễ gây sai sót. **Workflow này tự động hóa toàn bộ quá trình**, cho phép bạn tải lên file danh sách và xóa tất cả liên lạc không mong muốn chỉ với một cú nhấp chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Xóa hàng loạt liên lạc chỉ trong vài giây thay vì mất giờ làm thủ công.
- **Tránh sai sót:** Không còn lo lắng xóa nhầm liên lạc quan trọng do kiểm tra sai.
- **Hoạt động liên tục:** Workflow chạy tự động 24/7, không phụ thuộc vào giờ làm việc.
- **Tối ưu hóa danh sách:** Dọn sạch danh sách khách hàng không hoạt động, tăng hiệu quả marketing.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** và **API Key** (App Token) của HubSpot.
   - **Cách lấy API Key HubSpot:**
     - Đăng nhập vào [HubSpot Developer](https://developers.hubspot.com/docs/api/private-apps).
     - Tạo một **Private App** và sao lưu **App Token**.
2. **File Excel/CSV** chứa danh sách liên lạc cần xóa.
   - **Cấu trúc file:** Cột `emails` (hoặc tên cột khác nếu thay đổi) chứa địa chỉ email của liên lạc muốn xóa.
   - **Dạng file:** `.xlsx` (Excel) hoặc `.csv` (CSV).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/4100](https://n8n.io/workflows/4100) (chọn **Download JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Workflow sẽ tự động xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. Sao chép nội dung JSON từ [n8n.io/workflows/4100](https://n8n.io/workflows/4100).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. Workflow sẽ được tạo từ mã JSON.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **a. Cấu hình Webhook (Node đầu tiên)**
- **Không cần thay đổi gì** nếu chỉ muốn sử dụng workflow này.
- **Nếu muốn tích hợp với ứng dụng khác:**
  - Copy **URL Webhook** từ node `Webhook` (dạng: `https://[your-n8n-domain]/webhook/[path]`).
  - Dùng URL này trong Postman, Zapier, hoặc ứng dụng khác để gửi file Excel/CSV.

#### **b. Thay đổi tên cột trong file (Node "Parse Data")**
- Mặc định, workflow giả định cột chứa email là `emails`.
- **Nếu file của bạn có tên cột khác (ví dụ: `email`, `user_email`):**
  1. Tìm node **"Parse Data"** (type: `set`).
  2. Chỉnh sửa **tham số `emails`** trong `jsonpath` để phù hợp với tên cột thực tế.
     - Ví dụ: Nếu cột là `user_email`, thay đổi thành:
     ```json
     "emails": "$[*]['user_email']"
     ```

#### **c. Thay đổi định dạng file (Node "Extract File Data")**
- Mặc định, workflow hỗ trợ file **Excel (.xlsx)**.
- **Nếu bạn dùng file CSV:**
  1. Tìm node **"Extract File Data"** (type: `extractFromFile`).
  2. Thay đổi `operation` từ `"xlsx"` thành `"csv"`.

#### **d. Kiểm tra và cấu hình HubSpot**
- **Node "Search Contact" và "Delete Contact":**
  - Đảm bảo đã chọn **credentials** là `hubspotAppToken` (API Key HubSpot).
  - Kiểm tra lại **App Token** có đúng không (nếu sai, workflow sẽ báo lỗi).

---

### **3. Kích hoạt ⚡️**
1. **Test Run với file mẫu:**
   - Tải file Excel/CSV mẫu lên (chứa ít nhất 1 email).
   - Chạy workflow để kiểm tra xem có xóa thành công không.
2. **Bật Active workflow:**
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi nhận file.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram để báo cáo:**
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `Delete Contact` để thông báo kết quả xóa (thành công/thất bại).
   - Ví dụ: `"Xóa thành công [X] liên lạc!"`.

2. **Lưu log hoạt động:**
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử xóa (ngày giờ, số lượng liên lạc xóa).

3. **Chạy định kỳ với Zapier:**
   - Nếu muốn tự động xóa liên lạc định kỳ (ví dụ: hàng tháng), sử dụng **Zapier** để kích hoạt workflow khi file mới được tải lên Google Drive/Dropbox.

4. **Tối ưu hóa danh sách trước khi xóa:**
   - Thêm node **Google Sheets** để kiểm tra lại danh sách trước khi xóa (tránh xóa nhầm).

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp bán hàng/marketing **xóa bulk liên lạc HubSpot một cách nhanh chóng và chính xác**, không cần viết code. **Tiết kiệm thời gian, giảm sai sót, và tối ưu hóa danh sách khách hàng** chỉ với một cú nhấp chuột!

**Hãy thử ngay và tự động hóa công việc của mình!** 🚀
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/discord).