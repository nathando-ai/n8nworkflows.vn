---
title: "🚀 Xác minh số WhatsApp hàng loạt từ Google Sheets bằng n8n & WasenderAPI"
description: "Hướng dẫn tự động hóa xác minh số WhatsApp hàng loạt từ Google Sheets bằng n8n và WasenderAPI, tiết kiệm thời gian và tăng hiệu quả marketing"
slug: "xac-minh-so-whatsapp-hang-loat-tu-google-sheets-bang-n8n"
tags: [n8n, automation, no-code, whatsapp, google-sheets]
keywords: [n8n workflow, tự động hóa, xác minh số whatsapp, wasenderapi, google sheets]
---

# 🚀 Xác minh số WhatsApp hàng loạt từ Google Sheets bằng n8n & WasenderAPI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong quá trình xác minh số WhatsApp hàng loạt
- Tăng độ chính xác trong quá trình marketing trên WhatsApp
- Tự động hóa hoàn toàn quá trình xác minh mà không cần can thiệp thủ công
- Giảm thiểu rủi ro sai sót trong quá trình xử lý dữ liệu
- Tích hợp liền mạch với các công cụ khác trong hệ sinh thái n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp cá nhân hoặc doanh nghiệp hoạt động
- Đã cấu hình Google Sheets API trong n8n
- File Google Sheets đã được cấu trúc theo định dạng yêu cầu
- Tài khoản WasenderAPI.com với API key hoạt động
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/6183`
4. Nhấn "Import" để hoàn tất quá trình

Hoặc bạn cũng có thể:
1. Truy cập vào trang workflow gốc: [n8n.io/workflows/6183](https://n8n.io/workflows/6183)
2. Nhấn vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, nhấn vào nút "Import from Clipboard"
4. Dán JSON đã sao chép và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Trigger Every 5 Minute** (scheduleTrigger):
   - Cấu hình thời gian chạy workflow theo nhu cầu của bạn (mặc định là mỗi 5 phút)

2. **Fetch All Pending Contacts for Verifing** (googleSheets):
   - Cấu hình kết nối Google Sheets OAuth2
   - Chọn file Google Sheets chứa danh sách số điện thoại cần xác minh
   - Đảm bảo cột "Status" ban đầu là trống cho các hàng chưa được xác minh

3. **Verify WhatsApp Number Using HTTP Request** (httpRequest):
   - Cấu hình credentials với API key từ WasenderAPI.com
   - Đảm bảo URL và cấu trúc JSON body phù hợp với API của WasenderAPI

4. **Set Status** và **Set Status1** (code):
   - Kiểm tra và điều chỉnh logic xử lý trạng thái xác minh nếu cần

5. **Change State of Rows in Checked** (googleSheets):
   - Cấu hình kết nối Google Sheets OAuth2
   - Đảm bảo cập nhật đúng cột "Status" trong file Google Sheets

#### 3. Kích hoạt ⚡️
- Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
- Sau khi kiểm tra thành công, nhấn "Active" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tự động gửi báo cáo định kỳ về kết quả xác minh số WhatsApp
- Tích hợp với các công cụ CRM khác để cập nhật trạng thái khách hàng
- Sử dụng workflow này như một phần của chuỗi tự động hóa marketing toàn diện

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc xác minh số WhatsApp hàng loạt từ Google Sheets, giúp các sếp tiết kiệm thời gian và tăng hiệu quả trong chiến dịch marketing trên WhatsApp. Với khả năng tự động hóa hoàn toàn và tích hợp liền mạch với các công cụ khác, workflow này là công cụ không thể thiếu cho bất kỳ doanh nghiệp nào muốn tối ưu hóa quá trình marketing trên WhatsApp.