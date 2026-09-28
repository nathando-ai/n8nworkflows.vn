---
title: "🚀 Tự động trích xuất thông tin liên hệ doanh nghiệp từ Google Maps vào Google Sheets bằng Regex trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu doanh nghiệp từ Google Maps, lọc URL và quét email bằng Regex để lưu vào Google Sheets hoàn toàn miễn phí không cần API."
slug: "trich-xuat-thong-tin-google-maps-vao-google-sheets-n8n"
tags: [n8n, automation, no-code, google-maps, lead-generation, regex]
keywords: [n8n workflow, cào dữ liệu google maps, trích xuất email, google sheets automation, lead generation tự động]
---

# 🚀 Tự động trích xuất thông tin liên hệ doanh nghiệp từ Google Maps vào Google Sheets

Các sếp có đang đau đầu vì việc tìm kiếm khách hàng tiềm năng (Lead Generation) cứ phải làm thủ công hàng ngày? Ngồi lướt Google Maps, copy từng tên doanh nghiệp, click vào website tìm email rồi paste vào file Excel vừa mất thời gian, vừa dễ nhầm lẫn mà lại cực kỳ nhàm chán? 

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do chuyên gia *Yar Malik* thiết kế. Workflow này sẽ tự động hóa toàn bộ quy trình: tìm kiếm trên Google Maps, lọc website, dùng Regex thông minh để bóc tách email và tự động đẩy toàn bộ dữ liệu sạch sẽ vào Google Sheets. Tất cả diễn ra tự động 100% và **không cần dùng đến bất kỳ dịch vụ API trả phí nào**!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công từ bản đồ sang file quản lý.
- **Dữ liệu chất lượng cao:** Tự động lọc sạch các URL rác của Google và tìm chính xác địa chỉ email doanh nghiệp.
- **Sẵn sàng cho chiến dịch Cold Email:** Dữ liệu sau khi quét được đổ thẳng vào Google Sheets, sẵn sàng cho các chiến dịch tiếp thị tự động tiếp theo.
- **Tiết kiệm chi phí:** Không tốn tiền mua các tool cào dữ liệu đắt đỏ hay đăng ký API Key phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Google Account** để kết nối với Google Sheets.
- Một Google Sheet chuẩn bị sẵn các cột để lưu thông tin (Tên doanh nghiệp, Website, Email, Địa chỉ...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow (hoặc copy toàn bộ mã nguồn JSON từ n8n.io/workflows/7943), sau đó mở n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình các điểm sau để chạy mượt mà:

- **Node `When clicking ‘Test workflow’` (`manualTrigger`):** Node khởi chạy thủ công để test. Sau khi chạy ổn định, các sếp có thể thay thế bằng Schedule Trigger để chạy tự động định kỳ hàng ngày/tuần.
- **Node `Set Form Fields` (`set`):** Đây là nơi các sếp định nghĩa từ khóa tìm kiếm và khu vực (Ví dụ: *"Calgary dentists"* hoặc *"Nha khoa tại Hà Nội"*). **Hãy nhớ thay đổi từ khóa này thành dịch vụ và địa điểm mục tiêu của các sếp.**
- **Node `Build Search URL` (`code`):** Node JavaScript giúp chuyển đổi từ khóa của các sếp thành URL truy vấn chuẩn xác của Google Maps.
- **Node `Scrape Google Maps1` (`httpRequest`):** Thực hiện gửi HTTP Request để cào dữ liệu HTML thô từ Google Maps mà không cần API.
- **Node `Extract Business Info` (`code`):** Trái tim của workflow. Sử dụng biểu thức chính quy (Regex) để bóc tách URL website doanh nghiệp, lọc bỏ các domain không liên quan (`google.com`, `gstatic`,...) và quét sâu vào HTML của website để tìm các địa chỉ email liên hệ.
- **Node `Save to Google Sheets` (`googleSheets`):** 
  - Chọn **Credentials** là tài khoản Google Sheets OAuth2 của các sếp.
  - Chọn thao tác (Operation) là `Append`.
  - Map các trường dữ liệu (Tên, Website, Email) từ node trước vào đúng các cột tương ứng trong Google Sheet của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test Run) và kiểm tra kết quả trong Google Sheets.
- Sau khi thấy dữ liệu đổ về ngon lành, hãy bật nút **Active** ở góc trên bên phải để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay lập tức mỗi khi quét xong một danh sách khách hàng mới.
- **Lọc trùng lặp:** Thêm một bước kiểm tra email trong Google Sheets trước khi ghi dữ liệu để tránh việc lưu trùng lặp một doanh nghiệp nhiều lần.
- **Tự động hóa toàn diện:** Kết hợp với một Trigger định kỳ hàng tuần để tự động tìm kiếm khách hàng mới ở các khu vực khác nhau mà không cần chạm tay vào.

### 📌 Kết luận
Việc tự động hóa tìm kiếm khách hàng tiềm năng chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Regex. Hãy áp dụng ngay workflow này để tối ưu hóa đội ngũ sales và marketing của các sếp ngay hôm nay! Chúc các sếp thao tác thành công!