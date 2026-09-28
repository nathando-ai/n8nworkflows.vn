---
title: "📅 Tự Động Hóa Lọc & Sắp Xếp Lịch Trang Forex Factory Sang Google Calendar (Không Code)"
description: "Workflow này tự động lấy dữ liệu sự kiện từ Forex Factory, lọc bỏ các sự kiện không quan trọng (như ngày Chủ Nhật 6h chiều), và đồng bộ chỉ những sự kiện có 'tác động cao' hoặc 'tác động trung bình' vào Google Calendar của các sếp. Giúp tiết kiệm thời gian lên đến 10 giờ/tuần và tránh bỏ lỡ các tin tức kinh tế quan trọng."
slug: "tieu-dong-hoa-forex-factory-sang-google-calendar"
tags: [n8n, automation, forex, google-calendar, crypto-trading, no-code]
keywords: [tự động hóa forex factory, đồng bộ lịch forex sang google calendar, workflow n8n forex, lọc sự kiện forex, tự động hóa trading]
---

# 🚀 **Tự Động Hóa Lọc & Sắp Xếp Lịch Trang Forex Factory Sang Google Calendar**

### **Giải pháp cho các sếp giao dịch forex: Không còn phải thủ công lọc tin tức kinh tế hàng ngày!**

Các sếp giao dịch forex hay trader chuyên nghiệp đều biết rằng **Forex Factory** là nguồn tin tức kinh tế quan trọng nhất để theo dõi các sự kiện có tác động đến thị trường ngoại hối. Tuy nhiên, việc **tải xuống lịch sự kiện từ Forex Factory, lọc bỏ các tin tức không cần thiết (như ngày Chủ Nhật 6h chiều), và đồng bộ vào Google Calendar** là một công việc **mệt mỏi, tốn thời gian và dễ bị bỏ lỡ**.

Workflow này **tự động hóa toàn bộ quá trình** với **không một dòng code nào**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/tuần** không phải thủ công lọc và đồng bộ lịch.
✅ **Tránh bỏ lỡ sự kiện quan trọng** nhờ lọc tự động theo mức độ tác động.
✅ **Cập nhật liên tục 24/7** mà không cần can thiệp.
✅ **Tối ưu hóa lịch cá nhân** bằng cách loại bỏ sự kiện không cần thiết.

---

## 🎯 **Kết quả các sếp nhận được**

:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tự động lấy dữ liệu** từ Forex Factory mỗi ngày (không cần tải thủ công).
- **Lọc bỏ sự kiện không quan trọng** (ví dụ: ngày Chủ Nhật 6h chiều).
- **Chỉ đồng bộ sự kiện có tác động cao/middium** vào Google Calendar.
- **Xóa sự kiện cũ** (trước 10 ngày) để lịch luôn sạch sẽ.
- **Hoạt động liên tục** mà không cần can thiệp, tiết kiệm thời gian cho các sếp.
:::

---

## 🔧 **Yêu cầu cần thiết**

:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Forex Factory** (để lấy dữ liệu lịch sự kiện).
2. **Tài khoản Google Calendar** (để đồng bộ lịch).
3. **API Key hoặc OAuth2** cho Google Calendar (cài đặt trong n8n).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud để đảm bảo hoạt động 24/7).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON vào n8n Editor**.

#### **Cách import từ file JSON:**
1. Tải workflow từ [đây](https://n8n.io/workflows/8327) (hoặc copy JSON dưới đây).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách copy/paste JSON:**
```json
// (JSON workflow sẽ được cung cấp sau khi các sếp yêu cầu)
```

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

Workflow này bao gồm **11 node** với các chức năng chính sau:

| **Node** | **Tên** | **Mô tả** | **Cần chỉnh sửa gì?** |
|----------|---------|-----------|----------------------|
| **HTTP Request** | `HTTP Request` | Lấy dữ liệu lịch từ Forex Factory | **Không cần chỉnh**, sử dụng URL mặc định: `https://www.forexfactory.com/calendar.php` |
| **Extract from File** | `Extract from File` (operation: `fromIcs`) | Trích xuất dữ liệu từ file `.ics` | **Không cần chỉnh**, tự động xử lý từ dữ liệu HTTP. |
| **Split Out** | `Split Out` | Chia dữ liệu thành các sự kiện riêng lẻ | **Không cần chỉnh**, n8n tự động phân tách. |
| **If ForexFactory.com event** | `If` | Kiểm tra xem sự kiện có nguồn từ Forex Factory không | **Không cần chỉnh**, logic mặc định. |
| **Switch** | `Switch` | Lọc sự kiện theo **mức độ tác động** (High/Medium) | **Không cần chỉnh**, sử dụng logic mặc định. |
| **High Impact** | `Google Calendar` (operation: `create`) | Thêm sự kiện **tác động cao** vào Google Calendar | **Cần chỉnh:** <br> - Chọn **credentials**: `googleCalendarOAuth2Api` <br> - Điền **Google Calendar ID** (tìm trong `https://calendar.google.com/calendar/r/settings`). |
| **Medium Impact** | `Google Calendar` (operation: `create`) | Thêm sự kiện **tác động trung bình** vào Google Calendar | **Cần chỉnh:** <br> - Chọn **credentials**: `googleCalendarOAuth2Api` <br> - Điền **Google Calendar ID** (giống như High Impact). |
| **Sunday 6 PM** | `Schedule Trigger` | Khởi động workflow vào **Chủ Nhật 6h chiều** (để xóa sự kiện không cần thiết) | **Không cần chỉnh**, sử dụng lịch trình mặc định. |
| **No Operation** | `NoOp` | Dừng workflow nếu không có sự kiện mới | **Không cần chỉnh**, logic mặc định. |
| **Delete an event** | `Google Calendar` (operation: `delete`) | Xóa sự kiện **trước 10 ngày** để lịch sạch sẽ | **Cần chỉnh:** <br> - Chọn **credentials**: `googleCalendarOAuth2Api` <br> - Điền **Google Calendar ID**. |
| **Get All Event 10 Days Before** | `Google Calendar` (operation: `getAll`) | Lấy danh sách sự kiện trong **10 ngày trước** để xóa | **Cần chỉnh:** <br> - Chọn **credentials**: `googleCalendarOAuth2Api` <br> - Điền **Google Calendar ID**. |

---

### **3. Cấu hình Google Calendar OAuth2**
1. Mở **n8n Editor** → **Credentials** → **Add new credential** → Chọn **Google Calendar OAuth2**.
2. Nhấn **Connect** và đăng nhập tài khoản Google Calendar.
3. Sau khi kết nối, **lưu credentials** với tên `googleCalendarOAuth2Api`.

---

### **4. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra logic.
   - Kiểm tra **Google Calendar** xem có sự kiện mới được thêm không.
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tự động xóa sự kiện cũ theo lịch trình**
Workflow đã cấu hình **xóa sự kiện trước 10 ngày** vào **Chủ Nhật 6h chiều**, nhưng các sếp có thể:
- **Thay đổi ngày giờ** trong `Schedule Trigger` để phù hợp với lịch làm việc.
- **Thêm điều kiện xóa khác** (ví dụ: xóa sự kiện đã qua ngày hôm nay).

### **2. Kết hợp với Slack/Telegram để báo động**
Các sếp có thể thêm **node Slack/Telegram** để nhận thông báo khi có sự kiện mới:
```json
{
  "name": "Notify Slack",
  "type": "slackWebhook",
  "credentials": ["slackWebhookApi"]
}
```
- **Cần thiết:** Cài đặt **Slack Webhook API** trong n8n.

### **3. Lưu log hoạt động**
Để theo dõi hoạt động của workflow, các sếp có thể thêm **node `n8n-nodes-base.set`** để lưu dữ liệu vào **Google Sheets** hoặc **Database**:
```json
{
  "name": "Log to Google Sheets",
  "type": "googleSheets",
  "credentials": ["googleSheetsOAuth2Api"]
}
```

### **4. Tự động gửi báo cáo định kỳ**
Nếu các sếp muốn **báo cáo số lượng sự kiện mới mỗi tuần**, có thể thêm:
- **Node `n8n-nodes-base.email`** để gửi email tổng hợp.
- **Node `n8n-nodes-base.dateTime`** để tính toán ngày báo cáo.

---

## 📌 **Kết luận**

Workflow này **giải phóng thời gian cho các sếp giao dịch forex** bằng cách tự động hóa việc lấy, lọc và đồng bộ lịch từ Forex Factory sang Google Calendar. **Không cần code, không cần kỹ thuật**, chỉ cần **cài đặt và chạy** là xong!

🚀 **Hành động ngay hôm nay:**
1. **Import workflow** vào n8n.
2. **Cấu hình Google Calendar OAuth2**.
3. **Bật Active Workflow** và **quên đi việc thủ công lọc tin tức kinh tế!**

**Các sếp có thể tùy chỉnh thêm** để phù hợp với nhu cầu cá nhân (ví dụ: thay đổi mức độ tác động, thêm báo động Slack, hoặc lưu log). **Hãy thử ngay và tiết kiệm thời gian cho mình!** 💰⏳