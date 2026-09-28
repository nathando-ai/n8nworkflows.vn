---
title: "🚀 Tự Động Hóa DMARC Report: Nhận, Giải Nén, Lưu Trữ & Thông Báo Lỗi DKIM/SPF Miễn Code"
description: "Workflow này tự động lấy DMARC report từ email, giải nén XML, lưu dữ liệu vào cơ sở dữ liệu MySQL và thông báo ngay khi phát hiện lỗi DKIM/SPF. Giúp các sếp quản lý email security 24/7 mà không cần viết code."
slug: "tieu-dong-hoa-dmarc-report"
tags: [n8n, automation, email-security, dmarc, mysql, it-ops, no-code]
keywords: [tự động hóa dmarc report, lưu trữ dmarc report mysql, thông báo lỗi dkim spf, n8n workflow email, tự động hóa email security]
---

# 🚀 **Tự Động Hóa DMARC Report: Nhận, Giải Nén, Lưu Trữ & Thông Báo Lỗi DKIM/SPF**

## **🔍 Nỗi Đau Của Các Sếp**
Hiện nay, việc **quản lý DMARC report** vẫn là công việc thủ công, tốn thời gian và dễ mắc lỗi:
- **Nhận email DMARC** từ Postmaster và phải giải nén thủ công.
- **Phân tích XML** để tìm lỗi DKIM/SPF, mất nhiều thời gian.
- **Lưu trữ dữ liệu** vào cơ sở dữ liệu không được tự động hóa.
- **Không được thông báo kịp thời** khi có lỗi ảnh hưởng đến reputation email.

Workflow này **giải quyết tất cả** bằng cách tự động hóa **tất cả các bước** từ nhận email đến lưu trữ và cảnh báo lỗi.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần phân tích DMARC report thủ công.
✅ **Lưu trữ tự động** – Dữ liệu được lưu vào MySQL/MariaDB một cách chính xác.
✅ **Cảnh báo lỗi ngay lập tức** – Khi phát hiện DKIM/SPF lỗi, hệ thống tự động gửi thông báo qua Slack và email.
✅ **Hoạt động 24/7** – Không cần can thiệp người dùng, workflow chạy tự động.
✅ **Dữ liệu sạch và chuẩn** – XML được chuyển đổi thành JSON và định dạng cho cơ sở dữ liệu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản email Postmaster** (để nhận DMARC report).
- **Thư mục IMAP** (để n8n đọc email).
- **Thông tin kết nối MySQL/MariaDB** (host, username, password, database name).
- **Credentials Slack** (để gửi thông báo lỗi).
- **Credentials email** (để gửi email cảnh báo lỗi).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2369](https://n8n.io/workflows/2369).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON → **Import**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **📧 Email Trigger (IMAP)**
- **Chọn credentials IMAP** (đã cấu hình trước).
- **Chỉnh Host, Port, Username, Password** theo cấu hình email Postmaster.
- **Lọc email** theo tiêu đề chứa `"DMARC"` hoặc `"report"`.

#### **🔍 Unzip File & Extract XML Data**
- **Node `compression`** (Unzip File):
  - Chọn file đính kèm trong email (tệp `.zip`).
  - N8n sẽ tự động giải nén.
- **Node `extractFromFile`** (Extract XML data):
  - Chọn file XML đã giải nén.
  - **Operation:** `xml` (để chuyển XML thành JSON).

#### **🗃️ Input vào Database (MySQL)**
- **Node `mySql`**:
  - **Credentials:** Chọn MySQL đã cấu hình.
  - **Query:** Cần chỉnh sửa để phù hợp với schema bảng của bạn.
  - **Dữ liệu đầu vào:** Đảm bảo các trường `domain`, `policy`, `dkim`, `spf` được định dạng đúng.

#### **⚠️ If Issue with DKIM or SPF**
- **Node `if`** (kiểm tra lỗi DKIM/SPF):
  - **Condition:** Kiểm tra trường `dkim` hoặc `spf` có giá trị `fail` hay không.
  - Nếu có lỗi → **Gửi thông báo** (Slack + Email).

#### **📊 Rename Keys & Format Date**
- **Node `renameKeys`**:
  - Đảm bảo tên trường trong JSON phù hợp với bảng MySQL.
- **Node `dateTime`** (Begin/End date format):
  - Chỉnh định dạng ngày tháng theo yêu cầu của MySQL (ví dụ: `YYYY-MM-DD`).

#### **📢 Slack & Email Notification**
- **Node `slack`**:
  - Chọn **credentials Slack OAuth2**.
  - Chỉnh **channel** và **message template** để thông báo lỗi.
- **Node `emailSend`**:
  - Chọn **credentials email** (SMTP).
  - **Người nhận:** Địa chỉ email của team IT.
  - **Tiêu đề:** `"Lỗi DMARC: DKIM/SPF Failed"`.
  - **Nội dung:** Trích dẫn lỗi từ DMARC report.

---

### **⚡️ Kích Hoạt Workflow**
1. **Test Run** với một email mẫu DMARC.
2. **Kiểm tra Slack & Email** để đảm bảo thông báo lỗi hoạt động.
3. **Bật Active** workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
- **Lưu log lỗi** vào một bảng MySQL riêng để theo dõi lịch sử.
- **Kết hợp với Google Sheets** thay vì MySQL nếu cần dễ dàng phân tích.
- **Tự động gửi báo cáo tuần/month** về tình trạng DMARC qua email.
- **Kết nối với PagerDuty/Opsgenie** để cảnh báo cấp cao khi có lỗi nghiêm trọng.

---

## 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa toàn bộ quy trình quản lý DMARC**, từ nhận email đến cảnh báo lỗi, **miễn phí và không cần viết code**. **Hãy áp dụng ngay** để bảo mật email của doanh nghiệp được tối ưu!

👉 **Bắt đầu tự động hóa DMARC ngay hôm nay!** 🚀