---
title: "🚀 Tự Động Hóa Mở Rộng Trang LinkedIn Công Ty Bằng Browserflow & Google Sheets (N8N)"
description: "Workflow tự động hóa 100% không code giúp các sếp tự động lấy leads từ bình luận bài viết LinkedIn, gửi yêu cầu kết nối, theo dõi kết quả và mời theo dõi trang công ty. Giúp tăng trưởng cộng đồng LinkedIn liên tục 24/7."
slug: "tu-dong-hoa-mo-ro-trang-linkedin-cong-ty"
tags: [n8n, automation, social-media, linkedin, browserflow, google-sheets, no-code]
keywords: [tự động hóa linkedin, browserflow n8n, lấy leads từ linkedin, tăng trưởng trang công ty linkedin, tự động gửi kết nối linkedin]
---

# 🚀 **Tự Động Hóa Mở Rộng Trang LinkedIn Công Ty Bằng Browserflow & Google Sheets**

### **Giải pháp cho các sếp muốn tăng trưởng cộng đồng LinkedIn mà không cần code**
Hãy tưởng tượng: Một workflow tự động hóa **lấy leads từ bình luận bài viết**, **gửi yêu cầu kết nối**, **theo dõi kết quả** và **mời theo dõi trang công ty** chỉ trong vài phút mỗi ngày. **Không cần viết code, không cần chuyên gia IT**, chỉ cần **n8n + Browserflow + Google Sheets** là xong!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần thủ công lấy leads từ hàng trăm bình luận mỗi ngày.
✅ **Tăng trưởng tự động**: Mỗi ngày workflow tự động gửi yêu cầu kết nối và mời theo dõi trang công ty.
✅ **Theo dõi chính xác**: Google Sheets làm "cơ sở dữ liệu" để quản lý trạng thái (đã kết nối, đang chờ, đã mời).
✅ **Hoạt động 24/7**: Không cần can thiệp, workflow chạy tự động theo lịch trình.
✅ **Tăng độ tin cậy**: Các leads được lọc trùng lặp và cập nhật liên tục.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản Browserflow** (đăng ký [tại đây](https://browserflow.io)) và **API Key**.
📌 **Tài khoản Google Sheets** và **OAuth 2.0 credentials** (cài đặt trong n8n).
📌 **Trang LinkedIn Công Ty** (các sếp cần quyền admin để mời người dùng theo dõi).
📌 **Danh sách URL bài viết LinkedIn** (được lưu trong Google Sheets để workflow lấy leads).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/11850](https://n8n.io/workflows/11850) hoặc copy JSON từ [đây](https://github.com/n8n-io/workflows/blob/master/workflows/11850.json).
- **Bước 2**: Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3**: Chọn **"Active"** để kích hoạt workflow.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **4 giai đoạn chính**, các sếp cần cấu hình kỹ các node sau:

#### **🔹 Giai đoạn 1: Lấy leads từ bình luận bài viết (Scrape Comments)**
- **Node "Fetch Posts to Scrape"**:
  - Điền **Google Sheets URL** (sử dụng template [đây](https://docs.google.com/spreadsheets/d/1-zak-RUGU4ubw3aZ_9lF9LF1dxEo9ME_-mtzRGtIDFg/edit)).
  - Cột `Post URL` chứa danh sách bài viết LinkedIn cần lấy leads.
- **Node "Scrape comments from Post"**:
  - Điền **Browserflow API Key** (từ tài khoản Browserflow).
  - Chọn **operation = "scrapeProfilesFromPostComments"**.

#### **🔹 Giai đoạn 2: Kiểm tra & gửi yêu cầu kết nối**
- **Node "Check if already collected"**:
  - Kiểm tra leads đã tồn tại trong Google Sheets để tránh trùng lặp.
- **Node "Send a LinkedIn connection invite"**:
  - Chọn **operation = "sendConnectionInvite"**.
  - **Lưu ý**: Browserflow chỉ hỗ trợ gửi yêu cầu kết nối cho **100 người/ngày** (miễn phí).

#### **🔹 Giai đoạn 3: Theo dõi kết quả (Acceptance Tracking)**
- **Node "List your LinkedIn connections"**:
  - Chạy định kỳ (ví dụ: hàng ngày) để cập nhật trạng thái kết nối.
- **Node "Update connection status"**:
  - Cập nhật trạng thái (Đã kết nối, Đang chờ) trong Google Sheets.

#### **🔹 Giai đoạn 4: Mời theo dõi trang công ty**
- **Node "Invite connections to follow page"**:
  - Điền **URL trang LinkedIn Công Ty** (ví dụ: `https://www.linkedin.com/company/tencongty/`).
  - Chọn **operation = "inviteToFollowPage"**.

#### **🔹 Cấu hình lịch trình (Schedule Trigger)**
- Các sếp có thể điều chỉnh thời gian chạy (ví dụ: **lấy leads hàng ngày**, **gửi kết nối hàng tuần**).
- **Lưu ý**: Browserflow có giới hạn API, nên không nên chạy quá thường xuyên.

### **3. Kích hoạt ⚡️**
- **Test run**: Chạy thử với **1-2 bài viết mẫu** để kiểm tra workflow.
- **Bật Active**: Sau khi kiểm tra xong, nhấn **"Active"** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
💡 **Kết hợp với Slack/Telegram**:
- Thêm node **Slack/Telegram** để nhận báo cáo hàng ngày về số leads mới, kết nối thành công, và trạng thái mời theo dõi.

💡 **Lưu log hoạt động**:
- Sử dụng node **Google Sheets** để ghi lại lịch sử hoạt động (ví dụ: ngày gửi kết nối, ngày kết nối thành công).

💡 **Tối ưu hóa danh sách bài viết**:
- Chọn bài viết có **số bình luận cao** để tăng hiệu quả lấy leads.

💡 **Dùng n8n AI để tự động hóa cấu hình**:
- Sử dụng **n8n AI** để tự động thay đổi URL Google Sheets khi copy template mới.

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa toàn bộ quy trình mở rộng trang LinkedIn Công Ty** chỉ với **n8n + Browserflow + Google Sheets**. **Không cần code, không cần chuyên gia**, chỉ cần **cấu hình đúng và chạy tự động** là xong!

🚀 **Hành động ngay**:
1. **Import workflow** từ [n8n.io/workflows/11850](https://n8n.io/workflows/11850).
2. **Cấu hình Google Sheets + Browserflow API**.
3. **Bật Active** và để workflow làm việc cho bạn!

**Chúc các sếp thành công trong việc mở rộng cộng đồng LinkedIn!** 💼🚀