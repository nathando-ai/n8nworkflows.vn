---
title: "🚀 Tự động hóa tạo và gửi phiếu lương PDF từ Google Sheets qua Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tính lương, kết xuất phiếu lương PDF chuyên nghiệp và gửi email cho nhân viên."
slug: "tu-dong-hoa-tao-va-gui-phieu-luong-pdf-google-sheets-gmail"
tags: [n8n, automation, hr, google-sheets, gmail, puppeteer]
keywords: [n8n workflow, tự động hóa tính lương, gửi phiếu lương tự động, google sheets gmail n8n, tạo pdf từ html n8n]
---

# 🚀 Tự động hóa tạo và gửi phiếu lương PDF từ Google Sheets qua Gmail

Mỗi kỳ phát lương đến là bộ phận Nhân sự (HR) và Kế toán lại "đầu bù tóc rối" với hàng tá công việc thủ công: tính toán, thiết kế phiếu lương cho từng người, xuất file PDF, mở email và gửi đi từng cái một. Quá trình này không chỉ tốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót nhầm lẫn thông tin nhạy cảm.

Giải pháp là gì? Workflow n8n này sẽ thay thế hoàn toàn sức người, tự động hóa từ A-Z quy trình đọc dữ liệu bảng lương từ Google Sheets, thiết kế phiếu lương chuẩn chỉnh, chuyển đổi thành file PDF bảo mật và tự động gửi email cho từng nhân sự một cách nhanh chóng, chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Xử lý hàng trăm bảng lương chỉ bằng một cú click chuột hoặc lịch trình tự động.
- **Chính xác tuyệt đối:** Loại bỏ hoàn toàn rủi ro gửi nhầm phiếu lương hoặc sai sót dữ liệu tính toán thủ công.
- **Chuyên nghiệp hóa:** Phiếu lương định dạng PDF được thiết kế chuẩn đẹp, gửi trực tiếp qua Gmail cá nhân của từng nhân viên.
- **Kiểm soát trạng thái:** Tự động ghi nhận lại trạng thái "Đã gửi" lên Google Sheets để tránh việc gửi trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted đã cài đặt node Puppeteer).
- **Google Sheets:** File Google Sheets chứa bảng lương nhân viên (họ tên, email, lương cơ bản, các khoản thưởng, khấu trừ...).
- **Gmail Credentials:** Tài khoản Gmail cá nhân hoặc Google Workspace để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn chính thức của n8n (Tác giả: Khairul Muhtadin) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Company Configuration (`set`):** Điền các thông tin chung của công ty như Tên công ty, địa chỉ, mã số thuế hoặc logo để hiển thị lên phiếu lương.
- **Fetch Payroll Data (`googleSheets`):** Kết nối với tài khoản Google Drive/Sheets của sếp, chọn đúng file bảng lương và sheet chứa dữ liệu nhân sự.
- **Iterate Payslip Rows & Prepare Payslip Data (`splitInBatches` & `code`):** Các node này giúp bóc tách từng dòng dữ liệu nhân viên, xử lý logic tính toán tổng thu nhập, khấu trừ, thực lĩnh trước khi tạo file.
- **Check Email Not Sent (`filter`):** Đảm bảo hệ thống chỉ gửi email cho những nhân viên có trạng thái email chưa được đánh dấu là "Sent".
- **Generate Payslip HTML & Generate Payslip PDF (`html` & `n8n-nodes-puppeteer.puppeteer`):** Node HTML dùng để dựng template phiếu lương, sau đó Puppeteer sẽ chụp/kết xuất template đó thành file PDF nét căng.
- **Create PDF File (`convertToFile`):** Chuyển đổi định dạng dữ liệu nhị phân thành file PDF đính kèm hợp lệ.
- **Send Payslip Email (`gmail`):** Cấu hình tài khoản Gmail gửi đi, thiết lập tiêu đề, nội dung email kèm file PDF phiếu lương vừa tạo.
- **Mark Email Sent in Sheet (`googleSheets`):** Node cập nhật ngược lại file Google Sheets, đổi cột trạng thái thành "Đã gửi" cho dòng của nhân viên đó.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với dữ liệu của 1-2 nhân viên để kiểm tra email gửi đi có chuẩn xác không.
- Sau khi test thành công, bật công tắc **Active** để workflow sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node *Manual Trigger* bằng *Schedule Trigger* để hệ thống tự động phát lương vào ngày cố định hàng tháng (ví dụ: ngày 5 hàng tháng).
- **Cảnh báo lỗi qua Slack/Telegram:** Thêm nhánh xử lý lỗi (Error Trigger) để nếu có lỗi phát sinh trong quá trình tạo PDF hay gửi mail, hệ thống sẽ bắn tin nhắn thông báo ngay lập tức cho bộ phận IT hoặc HR.
- **Bảo mật file PDF:** Có thể cấu hình thêm các bước đặt mật khẩu cho file PDF phiếu lương nếu công ty yêu cầu tính bảo mật thông tin nhân sự cao.

### 📌 Kết luận
Quy trình tính lương và gửi payslip chưa bao giờ nhẹ nhàng đến thế. Thay vì tốn hàng giờ đồng hồ với các thao tác chân tay, giờ đây các sếp chỉ cần bấm nút và để n8n lo toàn bộ phần việc nặng nhọc. Áp dụng ngay hôm nay để tối ưu hóa hiệu suất vận hành cho doanh nghiệp của mình nhé!