---
title: "🚀 Tự Động Tạo Bài Toàn Trello Từ Google Form - Giảm Thời Gian Chăm Sóc Khách Hàng Gấp 10 Lần"
description: "Workflow này tự động chuyển đổi tất cả các lead từ Google Form thành bài toàn Trello, giúp các sếp tiết kiệm thời gian và đảm bảo không bỏ lỡ bất kỳ cơ hội nào. Hỗ trợ cập nhật thông tin chi tiết như kích thước công ty, nguồn lead và ngành nghề."
slug: "tu-dong-tao-bai-toan-trello-tu-google-form"
tags: [n8n, automation, sales, trello, google-forms, no-code]
keywords: [tự động hóa trello, google form automation, n8n workflow sales, tự động tạo bài toàn trello, giảm thời gian chăm sóc khách hàng]
---

# 🚀 **Tự Động Tạo Bài Toàn Trello Từ Google Form - Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp Trong Quá Trình Chăm Sóc Khách Hàng**
Hàng ngày, các sếp phải:
- **Nhập thủ công** dữ liệu từ Google Form vào Trello, tốn thời gian và dễ xảy ra lỗi.
- **Bỏ lỡ lead** vì không cập nhật kịp thời khi có phản hồi mới từ khách hàng.
- **Không theo dõi được chi tiết** như nguồn lead, kích thước công ty hay ngành nghề, khiến quá trình bán hàng trở nên khó quản lý.

**Workflow này giải quyết tất cả!** Nó tự động chuyển đổi **tất cả lead từ Google Form thành bài toàn Trello**, đồng thời **cập nhật thông tin chi tiết** như:
✅ **Kích thước công ty** (Solo, Small, Medium, Large, Enterprise)
✅ **Nguồn lead** (Youtube, Facebook, Google, Friend/Family)
✅ **Ngành nghề** (tùy chỉnh theo yêu cầu của doanh nghiệp)

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập thủ công, tự động hóa 100% quá trình.
- **Chính xác 100%**: Không sai sót khi chuyển dữ liệu từ Google Form sang Trello.
- **Cá nhân hóa lead**: Trello tự động phân loại và cập nhật thông tin chi tiết.
- **Hoạt động 24/7**: Workflow chạy liên tục, không bỏ lỡ bất kỳ lead nào.
- **Dễ dàng theo dõi**: Tất cả thông tin lead được lưu trữ sẵn trong Trello.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu trữ phản hồi từ Google Form).
✔ **Tài khoản Trello** (để tạo bài toàn tự động).
✔ **API Key của Trello** (để kết nối với Trello).
✔ **Google Sheets Trigger OAuth2** (để n8n đọc dữ liệu từ Google Form).
✔ **Thiết lập Google Form** (đảm bảo form gửi phản hồi về Google Sheets).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [đây](https://n8n.io/workflows/4946).
2. **Nhấp vào "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn "Import".

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 chế độ hoạt động**:
- **Chế độ không sử dụng Custom Fields** (tất cả thông tin lưu trong mô tả bài toàn).
- **Chế độ sử dụng Custom Fields** (tự động cập nhật thông tin chi tiết).

##### **🔹 Cấu Hình Google Sheets Trigger**
- **Chọn Google Sheets** chứa dữ liệu từ Google Form.
- **Chọn Sheet** và **Range** (ví dụ: `Sheet1!A1:Z1000`).
- **Kích hoạt "Trigger"** để n8n theo dõi phản hồi mới.

##### **🔹 Cấu Hình Trello**
- **Thêm Credentials Trello API**:
  - Đăng nhập vào Trello và tạo **API Key** tại [Trello Developer](https://trello.com/app-key).
  - Trong n8n, thêm **Trello API** với `Key` và `Token`.
- **Chọn Board & List** để tạo bài toàn:
  - Trong node **"Create Lead"**, chọn **Board ID** và **List ID** (thường là "Potential Leads").
  - Trong node **"Create Card"**, chọn **Board ID** và **List ID** tương ứng.

##### **🔹 Cấu Hình Set Fields & Set IDs**
- **Node "Set Fields"**: Đặt tên cho bài toàn (ví dụ: `{{$node["New Form Submission"].json["Name"]}}`).
- **Node "Set IDs"**: Lưu **Board ID** và **List ID** để tạo bài toàn chính xác.

##### **🔹 Cấu Hình Switch & Code (Phân Loại Lead)**
Workflow sử dụng **Switch** để phân loại:
- **Kích thước công ty** (Solo, Small, Medium, Large, Enterprise).
- **Nguồn lead** (Youtube, Facebook, Google, Friend/Family).
- **Ngành nghề** (tùy chỉnh trong node **"Options for Company Industry"**).

**Lưu ý quan trọng**:
- **Node "Options for Company Industry"** sử dụng **Code** để định nghĩa các ngành nghề.
  ```javascript
  // Ví dụ: Cập nhật ngành nghề từ Google Form
  return {
    industry: {{$node["New Form Submission"].json["Industry"]}}
  };
  ```
- **Node "Trello | Update Custom Fields"** sẽ cập nhật thông tin này vào bài toàn Trello.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu từ Google Form.
2. **Bật Active** workflow để nó hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi thông báo Slack/Telegram** khi có lead mới:
  - Thêm node **Slack/Telegram Webhook** sau node **"Create Card"** để thông báo tức thời.
- **Lưu log hoạt động** vào Google Sheets:
  - Thêm node **Google Sheets (Write)** để ghi lại lịch sử lead.
- **Gửi báo cáo định kỳ** về số lượng lead mới:
  - Sử dụng **n8n Cron Trigger** để gửi báo cáo hàng tuần.
- **Tự động chuyển lead** từ List "Potential Leads" sang List "Follow Up" sau 3 ngày:
  - Thêm node **Trello (Update Card)** với điều kiện thời gian.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập liệu thủ công, đồng thời **tăng cường hiệu quả chăm sóc khách hàng** bằng cách tự động hóa toàn bộ quy trình từ Google Form đến Trello.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa doanh nghiệp của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔍 Cần hỗ trợ thêm?** Hãy để lại bình luận dưới đây! 👇