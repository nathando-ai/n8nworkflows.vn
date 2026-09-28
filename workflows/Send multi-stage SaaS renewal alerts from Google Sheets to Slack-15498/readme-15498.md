---
title: "🚀 Tự động hóa cảnh báo gia hạn SaaS từ Google Sheets đến Slack - Giải pháp 4 giai đoạn hoàn hảo"
description: "Hướng dẫn chi tiết cách tự động hóa cảnh báo gia hạn SaaS 4 giai đoạn từ Google Sheets đến Slack, tiết kiệm 90% thời gian quản lý hợp đồng và giảm rủi ro ngừng hoạt động dịch vụ"
slug: "tu-dong-hoa-canh-bao-gia-han-saas-tu-google-sheets-den-slack"
tags: [n8n, automation, no-code, SaaS, contract management]
keywords: [n8n workflow, tự động hóa hợp đồng, cảnh báo gia hạn, quản lý SaaS, Slack integration]
---

# 🚀 Tự động hóa cảnh báo gia hạn SaaS từ Google Sheets đến Slack - Giải pháp 4 giai đoạn hoàn hảo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý hàng trăm hợp đồng SaaS thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code, giảm thiểu rủi ro ngừng hoạt động dịch vụ.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **90% thời gian** quản lý hợp đồng thủ công
- Giảm rủi ro **ngừng hoạt động dịch vụ** do quên gia hạn
- Cảnh báo **4 giai đoạn** (45, 30, 14, 7 ngày) với mức độ ưu tiên khác nhau
- Đồng bộ trạng thái hợp đồng **tự động** với Google Sheets
- Nhận báo cáo **hằng ngày** về tiến độ gia hạn
- Hệ thống **bảo trì tự động** khi có lỗi xảy ra
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace với quyền truy cập Google Sheets
- Tài khoản Slack với quyền tạo channel và thêm bot
- Dữ liệu hợp đồng đã chuẩn bị trong Google Sheets theo định dạng sau:
  - Cột A: Tên hợp đồng (text)
  - Cột B: Tên nhà cung cấp (text)
  - Cột C: Ngày gia hạn (YYYY-MM-DD)
  - Cột D: Chi phí hàng năm (số, không có ký tự €)
  - Cột E: Liên kết giá nhà cung cấp (URL)
  - Cột F: Trạng thái (Active, Renewed, Cancelled)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15498)
2. Chọn "Copy JSON" và lưu file JSON vào máy tính
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã lưu

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets: Load Contracts**
   - Thay thế `YOUR_SPREADSHEET_ID` bằng ID của Google Sheet chứa dữ liệu hợp đồng
   - Đảm bảo đã thiết lập OAuth2 credentials trong n8n
   - Chia sẻ Google Sheet với tài khoản dịch vụ của n8n

2. **Google Sheets: Update Status**
   - Đảm bảo các tham số cột (A-F) được cấu hình chính xác
   - Kiểm tra lại tên sheet nếu sử dụng nhiều sheet trong cùng một file

3. **Slack: Send Alert**
   - Tạo channel `#contract-renewals` trong Slack
   - Thêm bot vào channel này
   - Cấu hình credentials Slack với các scopes: `chat:write`, `chat:write.public`

4. **Slack: Daily Summary**
   - Đảm bảo channel được cấu hình chính xác
   - Kiểm tra định dạng tin nhắn mẫu

5. **Slack: Error Alert**
   - Thiết lập channel nhận thông báo lỗi (có thể cùng với channel chính)
   - Đảm bảo bot có quyền gửi tin nhắn trong channel này

6. **Schedule: Daily 9AM**
   - Kiểm tra múi giờ hệ thống của n8n
   - Điều chỉnh thời gian nếu cần thiết

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra logic cảnh báo
2. Kích hoạt workflow bằng cách nhấn "Activate" trên thanh công cụ
3. Kiểm tra channel Slack để xác nhận nhận được cảnh báo thử nghiệm

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node **Google Calendar** để tạo sự kiện nhắc nhở gia hạn
- Kết hợp với **Zapier** để gửi email cảnh báo bổ sung
- Thêm node **Google Drive** để lưu trữ bản sao dữ liệu hợp đồng
- Tích hợp với **Notion** để quản lý hợp đồng trong cơ sở dữ liệu
- Thiết lập báo cáo tuần/tháng tổng hợp tiến độ gia hạn

### 📌 Kết luận
Workflow này không chỉ tự động hóa quy trình cảnh báo gia hạn SaaS mà còn cung cấp hệ thống giám sát toàn diện, giúp các sếp quản lý hợp đồng một cách hiệu quả và chủ động. Với khả năng cảnh báo 4 giai đoạn và đồng bộ trạng thái tự động, giải pháp này giúp giảm thiểu rủi ro ngừng hoạt động dịch vụ và tối ưu hóa chi phí vận hành. Hãy triển khai ngay để nâng cao hiệu suất quản lý hợp đồng của doanh nghiệp!