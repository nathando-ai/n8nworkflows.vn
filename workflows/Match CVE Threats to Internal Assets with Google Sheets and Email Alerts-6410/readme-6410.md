---
title: "🚀 Tự động quét và khớp lỗi CVE với tài sản nội bộ qua Google Sheets và Email"
description: "Hướng dẫn xây dựng hệ thống SecOps tự động bằng n8n giúp rà soát lỗ hổng CVE mới nhất, đối chiếu với danh mục tài sản nội bộ và gửi cảnh báo qua Email ngay lập tức."
slug: "tu-dong-khop-cve-threats-voi-tai-san-noi-bo-google-sheets"
tags: [n8n, automation, no-code, secops, cve, cybersecurity, google-sheets]
keywords: [n8n workflow, tự động hóa bảo mật, quản lý lỗ hổng CVE, SecOps automation, n8n google sheets email]
---

# 🚀 Tự động quét và khớp lỗi CVE với tài sản nội bộ qua Google Sheets và Email

Các đội ngũ bảo mật (SecOps) và quản trị viên hệ thống thường xuyên đối mặt với cơn ác mộng: hàng trăm lỗ hổng CVE mới được công bố mỗi tuần. Việc phải thủ công rà soát xem các CVE này có đang ảnh hưởng đến hệ thống hay không vừa tốn thời gian, lại dễ bỏ sót các lỗ hổng chí mạng.

Workflow n8n này ra đời như một giải pháp tự động hóa 100% giúp các sếp giải quyết bài toán SecOps: Tự động tải danh sách mối đe dọa, đối chiếu thông minh với cơ sở dữ liệu tài sản nội bộ lưu trên Google Sheets, cập nhật trạng thái và bắn cảnh báo qua email ngay khi phát hiện nguy cơ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy ngầm định kỳ hàng ngày mà không cần con người can thiệp.
- **Đối chiếu chính xác:** Tự động so sánh mã CVE mới với danh sách phần mềm/hệ thống đang sử dụng trong nội bộ doanh nghiệp.
- **Cảnh báo tức thì:** Gửi báo cáo tóm tắt qua email giúp đội ngũ IT/Security xử lý vá lỗi kịp thời.
- **Quản lý dữ liệu tập trung:** Tự động đồng bộ, ghi nhận mối đe dọa mới và lưu trữ (archive) dữ liệu gọn gàng trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Account:** Tài khoản Google Sheets chứa bảng dữ liệu Asset DB (Tài sản nội bộ) và bảng Threat Intel (Mối đe dọa).
- **SMTP Server / Email Credential:** Tài khoản email (Gmail, SendGrid, SMTP cá nhân) để gửi cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc sử dụng tính năng Copy/Paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node cốt lõi sau để hệ thống chạy mượt mà:
- **`🔁 Daily Trigger` (Cron):** Thiết lập lịch chạy tự động (ví dụ: mỗi ngày 1 lần vào 8h sáng).
- **`📊Load Asset DB` & `📊Threats Sheets` (Google Sheets):** Kết nối tài khoản Google Drive/Sheets của sếp, trỏ đúng đến file Google Sheets quản lý tài sản nội bộ và danh sách CVE.
- **`🧠Match Threats to Assets` (Function):** Node chứa đoạn code JavaScript tùy chỉnh để thực hiện logic so khớp thông minh giữa các trường thông tin CVE và Asset. Các sếp có thể tinh chỉnh logic match tại đây nếu cần thiết.
- **`📊 Apend New Threat` & `📊 Delete Row` & `🗃️ Archived_Threats` (Google Sheets):** Cấu hình các thao tác ghi dữ liệu mới, xóa dòng cũ hoặc chuyển dữ liệu sang bảng lưu trữ bảo mật.
- **`📬Send Summary Email` (Email):** Điền thông tin cấu hình SMTP hoặc tích hợp dịch vụ gửi mail để nhận báo cáo tổng hợp.

#### 3. Kích hoạt ⚡️
- Bấm **"Execute Workflow"** chạy thử nghiệm lần đầu (Test run) với một vài dòng dữ liệu mẫu để kiểm tra kết quả trả về.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, gạt công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp ChatOps:** Kết nối thêm node Telegram hoặc Slack để bắn tin nhắn cảnh báo ngay vào group chat của đội ngũ kỹ thuật thay vì chỉ nhận qua email.
- **Ghi log chi tiết:** Lưu lịch sử quét vào một bảng Google Sheets riêng để làm báo cáo kiểm toán (Audit Log) hàng tháng.
- **Nâng cấp nguồn CVE:** Thay vì nhập tay vào Sheets, có thể kết nối thêm các API nguồn threat intel miễn phí như NVD (National Vulnerability Database) để workflow tự động cập nhật CVE mới nhất.

### 📌 Kết luận
Tự động hóa quy trình SecOps chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để bảo vệ hệ thống doanh nghiệp của các sếp trước các mối đe dọa mạng ngày càng tinh vi!